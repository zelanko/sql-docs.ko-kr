---
title: SSIS(SQL Server Integration Services) Scale Out에서 패키지 실행 | Microsoft Docs
description: 이 문서에서는 Scale Out에서 SSIS 패키지를 실행하는 방법 설명
ms.custom: performance
ms.date: 12/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: maghan
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
f1_keywords:
- sql13.ssis.ssms.ispackageexecuteinscaleout.f1
ms.openlocfilehash: 68a24188a307dd84a28342d89559630efa9a9d80
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "72305076"
---
# <a name="run-packages-in-integration-services-ssis-scale-out"></a>Integration Services(SSIS) Scale Out에서 패키지 실행

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Integration Services 서버에 패키지를 배포한 후 다음 방법 중 하나를 사용하여 Scale Out에서 패키지를 실행할 수 있습니다.

-   [Scale Out에서 패키지 실행 대화 상자](#scale_out_dialog)

-   [저장 프로시저](#stored_proc)

-   [SQL Server 에이전트 작업](#sql_agent)

## <a name="run-packages-with-the-execute-package-in-scale-out-dialog-box"></a><a name="scale_out_dialog"></a> Scale Out에서 패키지 실행 대화 상자를 사용하여 패키지 실행

1. Scale Out에서 패키지 실행 대화 상자를 엽니다.

    [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)]에서 Integration Services 서버에 연결합니다. 개체 탐색기에서 트리를 확장하여 **Integration Services 카탈로그**아래의 노드를 표시합니다. **SSISDB** 노드 또는 실행하려는 프로젝트나 패키지를 마우스 오른쪽 단추로 클릭한 다음 **Execute in Scale Out(규모 확장 시 실행)** 을 클릭합니다.

2. 패키지를 선택하고 옵션을 설정합니다.

    **패키지 선택** 페이지에서 실행할 하나 이상의 패키지를 선택합니다. 각 패키지의 환경, 매개 변수, 연결 관리자 및 고급 옵션을 설정합니다. 이러한 옵션을 설정할 패키지를 클릭합니다.
    
    **고급** 탭에서 **재시도 횟수**라는 Scale Out 옵션을 설정하여 패키지 실행이 실패할 경우의 재시도 횟수를 지정합니다.

    > [!NOTE]
    > **오류 시 덤프** 옵션은 Scale Out 작업자 서비스를 실행하는 계정이 로컬 컴퓨터의 관리자인 경우에만 적용됩니다.

3. 작업자 컴퓨터를 선택합니다.

    **컴퓨터 선택** 페이지에서 패키지를 실행할 Scale Out 작업자 컴퓨터를 선택합니다. 기본적으로 모든 컴퓨터에서 패키지를 실행할 수 있습니다. 

   > [!NOTE] 
   > 패키지는 Scale Out 작업자 서비스의 사용자 계정 자격 증명을 사용하여 실행됩니다. **컴퓨터 선택** 페이지에서 이러한 자격 증명을 검토합니다. 기본적으로 이 계정은 `NT Service\SSISScaleOutWorker140`입니다.

   > [!WARNING]
   > 동일한 작업자에서 여러 사용자가 트리거한 패키지 실행은 동일한 자격 증명으로 실행됩니다. 이러한 실행 사이에는 보안 경계가 없습니다. 

4. 패키지를 실행하고 보고서를 봅니다.

    **확인** 을 클릭하여 패키지 실행을 시작합니다. 패키지에 대한 실행 보고서를 보려면 개체 탐색기에서 패키지를 마우스 오른쪽 단추로 클릭하고 **보고서**, **모든 실행**을 차례로 클릭한 다음 실행을 찾습니다.
    
## <a name="run-packages-with-stored-procedures"></a><a name="stored_proc"></a> 저장 프로시저를 사용하여 패키지 실행

1.  실행을 만듭니다.

    각 패키지에 `[catalog].[create_execution]`을 호출합니다. 매개 변수 **\@runinscaleout**을 `True`로 설정합니다. 일부 Scale Out 작업자 컴퓨터에서 패키지를 실행할 수 없는 경우 **\@useanyworker** 매개 변수를 `False`로 설정합니다. 이 저장 프로시저 및 **\@useanyworker** 매개 변수에 대한 자세한 내용은 [catalog.create_execution](../system-stored-procedures/catalog-create-execution-ssisdb-database.md)을 참조합니다. 

2. 실행 매개 변수를 설정합니다.

    각 실행에 `[catalog].[set_execution_parameter_value]`를 호출합니다.

3. Scale Out 작업자를 설정합니다.

    `[catalog].[add_execution_worker]`을 호출합니다. 모든 컴퓨터에서 패키지를 실행할 수 있는 경우 이 저장 프로시저를 호출할 필요가 없습니다. 

4. 실행을 시작합니다.

    `[catalog].[start_execution]`을 호출합니다. **\@retry_count** 매개 변수를 설정하여 패키지 실행이 실패할 경우 다시 시도하는 횟수를 설정합니다.
    
### <a name="example"></a>예제
다음 예제에서는 Scale Out에서 하나의 Scale Out 작업자를 사용하여 `package1.dtsx`와 `package2.dtsx`라는 두 개의 패키지를 실행합니다.  

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

### <a name="permissions"></a>사용 권한
Scale Out에서 패키지를 실행하려면 다음 권한 중 하나가 있어야 합니다.

-   **ssis_admin** 데이터베이스 역할의 멤버 자격  

-   **ssis_cluster_executor** 데이터베이스 역할의 멤버 자격  
  
-   **sysadmin** 서버 역할의 멤버 자격  

## <a name="set-default-execution-mode"></a>기본 실행 모드 설정
패키지의 기본 실행 모드를 **Scale Out**으로 설정하려면 다음을 수행합니다.

1.  SSMS의 개체 탐색기에서 **SSISDB** 노드를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.

2.  **카탈로그 속성** 대화 상자에서 **서버 차원의 기본 실행 모드**를 **Scale Out**으로 설정합니다.

이 기본 실행 모드를 설정하면 `[catalog].[create_execution]` 저장 프로시저를 호출할 때 **\@runinscaleout** 매개 변수를 더 이상 지정할 필요가 없습니다. 패키지가 Scale Out 모드로 자동 실행됩니다. 

![실행 모드](media/exe-mode.PNG)

패키지가 더 이상 Scale Out 모드에서 기본적으로 실행되지 않도록 기본 실행 모드를 다시 전환하려면 **서버 차원의 기본 실행 모드**를 **서버**로 설정합니다.

## <a name="run-package-in-sql-server-agent-job"></a><a name="sql_agent"></a> SQL Server 에이전트 작업에서 패키지 실행
SQL Server 작업에서 작업의 한 단계로 SSIS 패키지를 실행할 수 있습니다. Scale Out에서 패키지를 실행하려면 기본 실행 모드를 **Scale Out**으로 설정합니다. 기본 실행 모드를 **Scale Out**으로 설정하면 SQL Server 에이전트 작업의 패키지가 Scale Out 모드에서 실행됩니다.

## <a name="next-steps"></a>다음 단계
-   [Scale Out 문제 해결](troubleshooting-scale-out.md)
