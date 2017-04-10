---
title: "Integration Services(SSIS) 규모 확장에서 패키지 실행 | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4c2f4cd7-9c47-416d-bb1e-40acc3e05342
caps.latest.revision: 5
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 5
---
# Integration Services(SSIS) 규모 확장에서 패키지 실행
패키지를 Integration Services 서버에 배포한 후 규모 확장에서 실행할 수 있습니다.

## <a name="run-packages-with-execute-package-in-scale-out-dialog"></a>**규모 확장 시 패키지 실행** 대화 상자를 사용하여 패키지 실행 

1. ### <a name="open-the-execute-package-in-scale-out-dialog-box"></a>규모 확장 시 패키지 실행 대화 상자 열기 ###
    [!INCLUDE[ssManStudioFull_md](../includes/ssmanstudiofull-md.md)]에서 Integration Services 서버에 연결합니다. 개체 탐색기에서 트리를 확장하여 **Integration Services 카탈로그** 아래의 노드를 표시합니다. **SSISDB** 노드 또는 실행하려는 프로젝트나 패키지를 마우스 오른쪽 단추로 클릭한 다음 **Execute in Scale Out(규모 확장 시 실행)**을 클릭합니다.
2. ### <a name="select-packages-and-set-the-options"></a>패키지를 선택하고 옵션 설정 ###
    **패키지 선택** 페이지에서 실행하려는 여러 패키지를 선택하고 각 패키지에 대해 환경, 매개 변수, 연결 관리자 및 고급 옵션을 설정합니다. 이러한 옵션을 설정할 패키지를 클릭합니다.
    
    **고급** 탭에서 **다시 시도 횟수**라는 규모 확장 옵션을 설정합니다. 이 옵션을 패키지 실행이 실패할 경우 다시 시도하는 횟수를 설정합니다.
3. ### <a name="select-machines"></a>컴퓨터 선택 ###
    **컴퓨터 선택** 페이지에서 패키지를 실행할 규모 확장 작업자 컴퓨터를 선택합니다. 기본적으로 모든 컴퓨터에서 패키지를 실행할 수 있습니다. 

   > [!NOTE]
> 패키지는 **컴퓨터 선택** 페이지에 표시되는 규모 확장 작업자 서비스의 사용자 계정 자격 증명을 사용하여 실행됩니다. 기본적으로 이 계정은 NT Service\SSISScaleOutWorker140입니다. 고유한 랩 계정으로 변경할 수 있습니다.

4. ### <a name="run-the-packages-and-view-reports"></a>패키지를 실행하고 보고서 보기 
    **확인**을 클릭하여 패키지 실행을 시작합니다. 패키지에 대한 실행 보고서를 보려면 개체 탐색기에서 패키지를 마우스 오른쪽 단추로 클릭하고 **보고서**, **모든 실행**을 차례로 클릭한 다음 실행을 찾습니다.
    
    
## <a name="run-packages-with-stored-procedures"></a>저장 프로시저를 사용하여 패키지 실행

1. ### <a name="create-executions"></a>실행 만들기 ###
    각 패키지에 대해 [catalog].[create_execution]을 호출합니다. **@runincluster** 매개 변수를 True로 설정합니다. 일부 규모 확장 작업자 컴퓨터에서 패키지를 실행할 수 없는 경우 **@useanyworker** 매개 변수를 False로 설정합니다.   
2. ### <a name="set-execution-parameters"></a>실행 매개 변수 설정 ###
    각 실행에 대해 [catalog].[set_execution_parameter_value]를 호출합니다.
3. ### <a name="set-scale-out-workers"></a>규모 확장 작업자 설정 ###
    [catalog].[add_execution_worker]를 호출합니다. 모든 컴퓨터에서 패키지를 실행할 수 있는 경우 이 저장 프로시저를 호출할 필요가 없습니다. 
4. ### <a name="start-executions"></a>실행 시작 ###
    [catalog].[start_execution]을 호출합니다. **@retry_count** 매개 변수를 설정하여 패키지 실행이 실패할 경우 다시 시도하는 횟수를 설정합니다.
    
    ### <a name="example"></a>예제  ###  
    다음 예제에서는 규모 확장 시 하나의 규모 확장 작업자에서 package1.dtsx와 package2.dtsx라는 두 개의 패키지를 실행합니다.  
    ```
    Declare @execution_id bigint
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package1.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder1', @project_name=N'project1', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runincluster=True
    Select @execution_id
    DECLARE @var0 smallint = 1
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
    EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
    EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
    GO

    Declare @execution_id bigint
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package2.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder2', @project_name=N'project2', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runincluster=True
    Select @execution_id
    DECLARE @var0 smallint = 1
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
    EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
    EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
    GO
    ```


## <a name="permissions"></a>Permissions
규모 확장 시 패키지를 실행하려면 다음 권한 중 하나가 필요합니다.

-   **ssis_admin** 데이터베이스 역할의 멤버 자격  

-   **ssis_cluster_executor** 데이터베이스 역할의 멤버 자격  
  
-   **sysadmin** 서버 역할의 멤버 자격  
    