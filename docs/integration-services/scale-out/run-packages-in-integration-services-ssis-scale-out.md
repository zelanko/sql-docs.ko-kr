---
title: "SQL Server Integration services (SSIS) 패키지를 실행할된 확장할 | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
f1_keywords:
- sql13.ssis.ssms.ispackageexecuteinscaleout.f1
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2c158ae6a711ecb5f5065561c0c8c303e9a09980
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---

# <a name="run-packages-in-integration-services-ssis-scale-out"></a>Integration Services (SSIS) 스케일 아웃에 패키지를 실행 합니다.
패키지를 Integration Services 서버에 배포한 후 규모 확장에서 실행할 수 있습니다.

## <a name="run-packages-with-execute-package-in-scale-out-dialog"></a>실행 패키지의 스케일 아웃 대화 상자와 패키지를 실행 합니다. 

1. 규모 확장 시 패키지 실행 대화 상자 열기

    [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)]에서 Integration Services 서버에 연결합니다. 개체 탐색기에서 트리를 확장하여 **Integration Services 카탈로그**아래의 노드를 표시합니다. **SSISDB** 노드 또는 실행하려는 프로젝트나 패키지를 마우스 오른쪽 단추로 클릭한 다음 **Execute in Scale Out(규모 확장 시 실행)**을 클릭합니다.

2. 패키지를 선택하고 옵션 설정

    **패키지 선택** 페이지에서 실행하려는 여러 패키지를 선택하고 각 패키지에 대해 환경, 매개 변수, 연결 관리자 및 고급 옵션을 설정합니다. 이러한 옵션을 설정할 패키지를 클릭합니다.
    
    **고급** 탭에서 **다시 시도 횟수**라는 규모 확장 옵션을 설정합니다. 이 옵션을 패키지 실행이 실패할 경우 다시 시도하는 횟수를 설정합니다.

    > [!Note]
    > **오류 덤프** 스케일 아웃 Worker 서비스를 실행 하는 계정 관리자가 로컬 컴퓨터의 경우만 옵션 적용 됩니다.

3. 컴퓨터 선택

    **컴퓨터 선택** 페이지에서 패키지를 실행할 규모 확장 작업자 컴퓨터를 선택합니다. 기본적으로 모든 컴퓨터에서 패키지를 실행할 수 있습니다. 

   > [!Note] 
   > 패키지는 **컴퓨터 선택** 페이지에 표시되는 규모 확장 작업자 서비스의 사용자 계정 자격 증명을 사용하여 실행됩니다. 기본적으로 이 계정은 NT Service\SSISScaleOutWorker140입니다. 고유한 랩 계정으로 변경할 수 있습니다.

   >[!WARNING]
   >패키지 실행 시 서로 다른 사용자는 동일한 작업자에 의해 트리거되는 동일한 계정으로 실행 됩니다. 그중에서 없는 보안 경계가 있습니다. 

4. 패키지를 실행하고 보고서 보기 

    **확인** 을 클릭하여 패키지 실행을 시작합니다. 패키지에 대한 실행 보고서를 보려면 개체 탐색기에서 패키지를 마우스 오른쪽 단추로 클릭하고 **보고서**, **모든 실행**을 차례로 클릭한 다음 실행을 찾습니다.
    
## <a name="run-packages-with-stored-procedures"></a>저장 프로시저를 사용하여 패키지 실행

1. 실행 만들기

    각 패키지에 대해 [catalog].[create_execution]을 호출합니다. **@runinscaleout** 매개 변수를 True로 설정합니다. 일부 규모 확장 작업자 컴퓨터에서 패키지를 실행할 수 없는 경우 **@useanyworker** 매개 변수를 False로 설정합니다.   

2. 실행 매개 변수 설정

    각 실행에 대해 [catalog].[set_execution_parameter_value]를 호출합니다.

3. 규모 확장 작업자 설정

    [catalog].[add_execution_worker]를 호출합니다. 모든 컴퓨터에서 패키지를 실행할 수 있는 경우 이 저장 프로시저를 호출할 필요가 없습니다. 

4. 실행 시작

    [catalog].[start_execution]을 호출합니다. **@retry_count** 매개 변수를 설정하여 패키지 실행이 실패할 경우 다시 시도하는 횟수를 설정합니다.
    
#### <a name="example"></a>예제
다음 예제에서는 규모 확장 시 하나의 규모 확장 작업자에서 package1.dtsx와 package2.dtsx라는 두 개의 패키지를 실행합니다.  

```sql
Declare @execution_id bigint
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package1.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder1', @project_name=N'project1', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runinscaleout=True
Select @execution_id
DECLARE @var0 smallint = 1
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
GO

Declare @execution_id bigint
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package2.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder2', @project_name=N'project2', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runinscaleout=True
Select @execution_id
DECLARE @var0 smallint = 1
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
GO
```

### <a name="permissions"></a>Permissions
규모 확장 시 패키지를 실행하려면 다음 권한 중 하나가 필요합니다.

-   **ssis_admin** 데이터베이스 역할의 멤버 자격  

-   **ssis_cluster_executor** 데이터베이스 역할의 멤버 자격  
  
-   **sysadmin** 서버 역할의 멤버 자격  

## <a name="set-default-execution-mode"></a>기본 실행 모드 설정
"스케일 아웃"를 기본 실행 모드를 설정 하려면 마우스 오른쪽 단추로 클릭는 **SSISDB** 선택한 SSMS의 개체 탐색기의 노드 **속성**합니다.
에 **카탈로그 속성** 대화 상자에서 **서버 차원의 기본 실행 모드** 를 **스케일 아웃**합니다.

이 설정은 이후에 지정할 필요가 없습니다는  **@runinscaleout**  매개 변수가 [catalog]. [ create_execution]입니다. 스케일 아웃에 실행 될 때 자동으로 실행 됩니다. 

![Exe 모드](media\exe-mode.PNG)

기본 실행 모드에는 비-스케일 아웃 모드로 다시 전환할 설정할 **서버 차원의 기본 실행 모드** 를 **서버**합니다.

## <a name="run-package-in-sql-agent-job"></a>SQL 에이전트 작업에서 패키지를 실행 합니다.
Sql 에이전트 작업에서 작업의 한 단계로 SSIS 패키지를 실행 하도록 선택할 수 있습니다. 스케일 아웃에 패키지를 실행 하려면 위의 기본 실행 모드를 활용할 수 있습니다. 기본 실행 모드를 설정 "스케일 아웃"를, 한 후 Sql 에이전트 작업에서 패키지 범위 확장에서 실행 됩니다.
