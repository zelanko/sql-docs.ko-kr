---
title: "Azure에서 SSIS 패키지 실행 예약 | Microsoft Docs"
ms.date: 01/16/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4724d7a306e59e05d17f466643146d868f372a7f
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="schedule-the-execution-of-an-ssis-package-on-azure"></a>Azure에서 SSIS 패키지 실행 예약
다음 예약 옵션 중 하나를 선택하여 Azure SQL Database 서버의 SSISDB 카탈로그 데이터베이스에 저장된 패키지의 실행을 예약할 수 있습니다.
-   [SQL Server 에이전트](#agent)
-   [SQL Database 탄력적 작업](#elastic)
-   [Azure Data Factory SQL Server 저장 프로시저 작업](#sproc)

## <a name="agent"></a> SQL Server 에이전트를 사용하여 패키지 예약

### <a name="prerequisite---create-a-linked-server"></a>필수 구성 요소 - 연결된 서버 만들기

온-프레미스에서 SQL Server 에이전트를 사용하여 Azure SQL Database 서버에 저장된 패키지의 실행을 예약하기 전에 먼저 SQL Database 서버를 연결된 서버로 온-프레미스 SQL Server에 추가해야 합니다.

1.  **연결된 서버 설정**

    ```sql
    -- Add the SSISDB database on your Azure SQL Database as a linked server to your SQL Server on premises
    EXEC sp_addlinkedserver
        @server='myLinkedServer', -- Name your linked server
        @srvproduct='',     
        @provider='sqlncli', -- Use SQL Server native client
        @datasrc='<server_name>.database.windows.net', -- Add your Azure SQL Database server endpoint
        @location=‘’,
        @provstr=‘’,
        @catalog='SSISDB'  -- Add SSISDB as the initial catalog
    ```

2.  **연결된 서버 자격 증명 설정**

    ```sql
    -- Add your Azure SQL DB server admin credentials
    EXEC sp_addlinkedsrvlogin
        @rmtsrvname = 'myLinkedServer’,
        @useself = 'false’,
        @rmtuser = 'myUsername', -- Add your server admin username
        @rmtpassword = 'myPassword' -- Add your server admin password
    ```

3.  **연결된 서버 옵션 설정**

    ```sql
    EXEC sp_serveroption 'myLinkedServer', 'rpc out', true;
    ```

자세한 내용은 [연결된 서버 만들기](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md) 및 [연결된 서버](../../relational-databases/linked-servers/linked-servers-database-engine.md)를 참조하세요.

### <a name="create-a-sql-server-agent-job"></a>SQL Server 에이전트 작업 만들기

온-프레미스에서 SQL Server 에이전트를 사용하여 패키지를 예약하려면 `[catalog].[create_execution]` 및 `[catalog].[start_execution]` SSIS 카탈로그 저장 프로시저를 차례로 호출하는 작업 단계가 있는 작업을 만듭니다. 자세한 내용은 [패키지에 대한 SQL Server 에이전트 작업](../packages/sql-server-agent-jobs-for-packages.md)을 참조하세요.

1.  SQL Server Management Studio에서 작업을 만들려는 온-프레미스 SQL Server 데이터베이스에 연결합니다.

2.  **SQL Server 에이전트** 노드를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**, **작업**을 차례로 선택하여 **새 작업** 대화 상자를 엽니다.

3.  **새 작업** 대화 상자에서 **단계** 페이지를 선택한 다음 **새로 만들기**를 선택하여 **새 작업 단계** 대화 상자를 엽니다.

4.  **새 작업 단계** 대화 상자에서 `SSISDB`를 **데이터베이스**로 선택합니다.

5.  **명령** 필드에서 다음 예제에 표시된 스크립트와 비슷한 Transact-SQL 스크립트를 입력합니다.

    ```sql
    -- T-SQL script to create and start SSIS package execution using SSISDB stored procedures
    DECLARE @return_value int, @exe_id bigint 

    EXEC @return_value = [YourLinkedServer].[SSISDB].[catalog].[create_execution] 
        @folder_name=N'folderName', @project_name=N'projectName', 
        @package_name=N'packageName', @use32bitruntime=0, @runincluster=1, @useanyworker=1,
        @execution_id=@exe_id OUTPUT 

    EXEC [YourLinkedServer].[SSISDB].[catalog].[set_execution_parameter_value] @exe_id,
        @object_type=50, @parameter_name=N'SYNCHRONIZED', @parameter_value=1

    EXEC [YourLinkedServer].[SSISDB].[catalog].[start_execution] @execution_id=@exe_id
    ```

6.  작업 구성 및 예약을 완료합니다.

## <a name="elastic"></a> SQL Database 탄력적 작업을 사용하여 패키지 예약

SQL Database의 탄력적 작업에 대한 자세한 내용은 [규모가 확장된 클라우드 데이터베이스 관리](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview)를 참조하세요.

### <a name="prerequisites"></a>사전 요구 사항

탄력적 작업을 사용하여 Azure SQL Database 서버의 SSISDB 카탈로그 데이터베이스에 저장된 SSIS 패키지를 예약하려면 다음 작업을 수행해야 합니다.

1.  Elastic Database 작업 구성 요소를 설치하고 구성합니다. 자세한 내용은 [Elastic Database 작업 설치 개요](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-service-installation)를 참조하세요.

2. 작업에서 SSIS 카탈로그 데이터베이스에 명령을 보내는 데 사용할 수 있는 데이터베이스 범위 자격 증명을 만듭니다. 자세한 내용은 [CREATE DATABASE SCOPED CREDENTIAL(Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)을 참조하세요.

### <a name="create-an-elastic-job"></a>탄력적 작업 만들기

다음 예제에 표시된 스크립트와 비슷한 Transact-SQL 스크립트를 사용하여 작업을 만듭니다.

```sql
-- Create Elastic Jobs target group 
EXEC jobs.sp_add_target_group 'TargetGroup' 

-- Add Elastic Jobs target group member 
EXEC jobs.sp_add_target_group_member @target_group_name='TargetGroup', 
    @target_type='SqlDatabase', @server_name='YourSQLDBServer.database.windows.net',
    @database_name='SSISDB' 

-- Add a job to schedule SSIS package execution
EXEC jobs.sp_add_job @job_name='ExecutePackageJob', @description='Description', 
    @schedule_interval_type='Minutes', @schedule_interval_count=60

-- Add a job step to create/start SSIS package execution using SSISDB catalog stored procedures
EXEC jobs.sp_add_jobstep @job_name='ExecutePackageJob', 
    @command=N'DECLARE @exe_id bigint 
        EXEC [SSISDB].[catalog].[create_execution]
            @folder_name=N''folderName'', @project_name=N''projectName'',
            @package_name=N''packageName'', @use32bitruntime=0,
            @runinscaleout=1, @useanyworker=1, 
            @execution_id=@exe_id OUTPUT         
        EXEC [SSISDB].[catalog].[start_execution] @exe_id, @retry_count=0', 
    @credential_name='YourDBScopedCredentials', 
    @target_group_name='TargetGroup' 

-- Enable the job schedule 
EXEC jobs.sp_update_job @job_name='ExecutePackageJob', @enabled=1, 
    @schedule_interval_type='Minutes', @schedule_interval_count=60 
```

## <a name="sproc"></a> Azure Data Factory SQL Server 저장 프로시저 작업을 사용하여 패키지 예약

Azure Data Factory 저장 프로시저 작업을 사용하여 SSIS 패키지를 예약하는 방법에 대한 내용은 다음 문서를 참조하세요.

-   Data Factory 버전 2의 경우: [Azure Data Factory에서 저장 프로시저 작업을 사용하여 SSIS 패키지 호출](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-stored-procedure-activity)

-   Data Factory 버전 1의 경우: [Azure Data Factory에서 저장 프로시저 작업을 사용하여 SSIS 패키지 호출](https://docs.microsoft.com/azure/data-factory/v1/how-to-invoke-ssis-package-stored-procedure-activity)

## <a name="next-steps"></a>다음 단계
SQL Server 에이전트에 대한 자세한 내용은 [패키지에 대한 SQL Server 에이전트 작업](../packages/sql-server-agent-jobs-for-packages.md)을 참조하세요.

SQL Database의 탄력적 작업에 대한 자세한 내용은 [규모가 확장된 클라우드 데이터베이스 관리](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview)를 참조하세요.
