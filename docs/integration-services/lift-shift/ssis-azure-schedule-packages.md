---
title: "Azure에서 SSIS 패키지 실행 예약 | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d0b8dbc635523b33a480ad887b73d9f395d71c8d
ms.sourcegitcommit: ffa4ce9bd71ecf363604966c20cbd2710d029831
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="schedule-the-execution-of-an-ssis-package-on-azure"></a>Azure에서 SSIS 패키지 실행 예약
다음 예약 옵션 중 하나를 선택하여 Azure SQL Database 서버의 SSISDB 카탈로그 데이터베이스에 저장된 패키지의 실행을 예약할 수 있습니다.
-   [SQL Server 에이전트](#agent)
-   [SQL Database 탄력적 작업](#elastic)
-   [Azure Data Factory SQL Server 저장 프로시저 작업](#sproc)

## <a name="agent"></a> SQL Server 에이전트를 사용하여 패키지 예약

### <a name="prerequisite"></a>필수 구성 요소

온-프레미스에서 SQL Server 에이전트를 사용하여 Azure SQL Database 서버에 저장된 패키지의 실행을 예약하기 전에 먼저 SQL Database 서버를 연결된 서버로 추가해야 합니다. 자세한 내용은 [연결된 서버 만들기](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md) 및 [연결된 서버](../../relational-databases/linked-servers/linked-servers-database-engine.md)를 참조하세요.

### <a name="create-a-sql-server-agent-job"></a>SQL Server 에이전트 작업 만들기

온-프레미스에서 SQL Server 에이전트를 사용하여 패키지를 예약하려면 `[catalog].[create_execution]` 및 `[catalog].[start_execution]` SSIS 카탈로그 저장 프로시저를 차례로 호출하는 작업 단계가 있는 작업을 만듭니다. 자세한 내용은 [패키지에 대한 SQL Server 에이전트 작업](../packages/sql-server-agent-jobs-for-packages.md)을 참조하세요.

1.  SQL Server Management Studio에서 작업을 만들려는 온-프레미스 SQL Server 데이터베이스에 연결합니다.

2.  **SQL Server 에이전트** 노드를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**, **작업**을 차례로 선택하여 **새 작업** 대화 상자를 엽니다.

3.  **새 작업** 대화 상자에서 **단계** 페이지를 선택한 다음 **새로 만들기**를 선택하여 **새 작업 단계** 대화 상자를 엽니다.

4.  **새 작업 단계** 대화 상자에서 `SSISDB`를 **데이터베이스**로 선택합니다.

5.  명령 필드에서 다음 예제에 표시된 스크립트와 비슷한 Transact-SQL 스크립트를 입력합니다.

    ```sql
    DECLARE @return_value int, @exe_id bigint 

    EXEC @return_value = [YourLinkedServer].[SSISDB].[catalog].[create_execution] 
    @folder_name=N'folderName', @project_name=N'projectName', 
    @package_name=N'packageName', @use32bitruntime=0, 
    @runinscaleout=1, @useanyworker=1, @execution_id=@exe_id OUTPUT 
 
    EXEC [YourLinkedServer].[SSISDB].[catalog].[start_execution] @execution_id=@exe_id

    GO
    ```

6.  작업 구성 및 예약을 완료합니다.

## <a name="elastic"></a> SQL Database 탄력적 작업을 사용하여 패키지 예약

SQL Database의 탄력적 작업에 대한 자세한 내용은 [규모가 확장된 클라우드 데이터베이스 관리](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview)를 참조하세요.

### <a name="prerequisites"></a>필수 구성 요소

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

> [!IMPORTANT]
> Azure Data Factory 버전 1 저장 프로시저 작업이 포함된 다음 예제의 JSON 스크립트를 사용합니다.

Azure Data Factory SQL Server 저장 프로시저 작업을 사용하여 패키지를 예약하려면 다음 작업을 수행합니다.

1.  Data Factory 만들기

2.  SSISDB를 호스팅하는 SQL Database에 대한 연결된 서비스를 만들었습니다.

3.  예약을 구동하는 출력 데이터 집합을 만듭니다.

4.  SQL Server 저장 프로시저 작업을 사용하여 SSIS 패키지를 실행하는 Data Factory 파이프라인을 만듭니다.

이 섹션에서는 이러한 단계에 대한 개요를 제공합니다. 완전한 Data Factory 자습서는 이 문서의 범위를 벗어납니다. 자세한 내용은 [SQL Server 저장 프로시저 작업](https://docs.microsoft.com/azure/data-factory/data-factory-stored-proc-activity)을 참조하세요.

예약된 실행이 실패하고 ADF 저장 프로시저 작업이 실패한 실행에 대한 실행 ID를 제공하는 경우 SSIS 카탈로그의 SSMS에서 해당 ID에 대한 실행 보고서를 확인합니다.

### <a name="created-a-linked-service-for-the-sql-database-that-hosts-ssisdb"></a>SSISDB를 호스팅하는 SQL Database에 대한 연결된 서비스를 만들었습니다.
연결된 서비스를 통해 Data Factory에서 SSISDB에 연결할 수 있습니다.

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "description": "",
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Data Source = tcp: YourSQLDBServer.database.windows.net, 1433; Initial Catalog = SSISDB; User ID = YourUsername; Password = YourPassword; Integrated Security = False; Encrypt = True; Connect Timeout = 30"
        }
    }
}
```

### <a name="create-an-output-dataset"></a>출력 데이터 집합 만들기
출력 데이터 집합에는 예약된 일정 정보가 포함됩니다.

```json
{
    "name": "sprocsampleout",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
### <a name="create-a-data-factory-pipeline"></a>Data Factory 파이프라인 만들기
파이프라인에서 SQL Server 저장 프로시저 작업을 사용하여 SSIS 패키지를 실행합니다.

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [{
            "name": "SprocActivitySample",
            "type": "SqlServerStoredProcedure",
            "typeProperties": {
                "storedProcedureName": "sp_executesql",
                "storedProcedureParameters": {
                    "stmt": "Transact-SQL script to create and start SSIS package execution using SSISDB catalog stored procedures"
                }
            },
            "outputs": [{
                "name": "sprocsampleout"
            }],
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            }
        }],
        "start": "2017-10-01T00:00:00Z",
        "end": "2017-10-01T05:00:00Z",
        "isPaused": false
    }
}
```

SSIS 패키지 실행을 만들고 시작하는 데 필요한 Transact-SQL 명령을 캡슐화하는 새 저장 프로시저를 만들 필요가 없습니다. 앞의 JSON 샘플에서 `stmt` 매개 변수의 값으로 전체 스크립트를 제공할 수 있습니다. 다음은 샘플 스크립트입니다.

```sql
-- T-SQL script to create and start SSIS package execution using SSISDB catalog stored procedures
DECLARE @return_value INT,@exe_id BIGINT,@err_msg NVARCHAR(150)

-- Create the exectuion
EXEC @return_value=[SSISDB].[catalog].[create_execution] @folder_name=N'folderName', @project_name=N'projectName', @package_name=N'packageName', @use32bitruntime=0, @runinscaleout=1,@useanyworker=1, @execution_id=@exe_id OUTPUT

-- To synchronize SSIS package execution, set the SYNCHRONIZED execution parameter
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @exe_id, @object_type=50, @parameter_name=N'SYNCHRONIZED', @parameter_value=1

-- Start the execution                                                         
EXEC [SSISDB].[catalog].[start_execution] @execution_id=@exe_id,@retry_count=0
                                          
-- Raise an error for unsuccessful package execution
-- Execution status values include the following:
-- created (1)
-- running (2)
-- canceled (3)
-- failed (4)
-- pending (5)
-- ended unexpectedly (6)
-- succeeded (7)
-- stopping (8)
-- completed (9) 
IF(SELECT [status]
   FROM [SSISDB].[catalog].[executions]
   WHERE execution_id=@exe_id)<>7
BEGIN
    SET @err_msg=N'Your package execution did not succeed for execution ID: ' + CAST(@exe_id AS NVARCHAR(20))
    RAISERROR(@err_msg,15,1)
END
GO
```

위에 `stmt` 매개 변수 값으로 표시된 SQL 스크립트를 제공하려면 일반적으로 다음 예에 표시된 것처럼 전체 스크립트를 한 줄에 포함해야 합니다. ([JSON 표준](https://json.org/)은 다른 언어에서 여러 줄 문자열의 줄을 구분하는 데 사용되는 `\n` 줄 바꿈 제어 문자를 비롯한 제어 문자를 지원하지 않습니다.)

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_executesql",
                    "storedProcedureParameters": {
                        "stmt": "DECLARE @return_value INT, @exe_id BIGINT, @err_msg NVARCHAR(150)    EXEC @return_value=[SSISDB].[catalog].[create_execution] @folder_name=N'test', @project_name=N'TestProject', @package_name=N'STestPackage.dtsx', @use32bitruntime=0, @runinscaleout=1, @useanyworker=1, @execution_id=@exe_id OUTPUT    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @exe_id, @object_type=50, @parameter_name=N'SYNCHRONIZED', @parameter_value=1    EXEC [SSISDB].[catalog].[start_execution] @execution_id=@exe_id, @retry_count=0    IF(SELECT [status] FROM [SSISDB].[catalog].[executions] WHERE execution_id=@exe_id)<>7 BEGIN SET @err_msg=N'Your package execution did not succeed for execution ID: ' + CAST(@exe_id AS NVARCHAR(20)) RAISERROR(@err_msg,15,1) END"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout"
                    }
                ],
                "scheduler": {
                    "frequency": "Minute",
                    "interval": 15
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2017-12-06T12:00:00Z",
        "end": "2017-12-06T12:30:00Z",
        "isPaused": false,
        "hubName": "test_hub",
        "pipelineMode": "Scheduled"
    }
}
```

이 스크립트의 코드에 대한 자세한 내용은 [저장 프로시저를 사용하여 SSIS 패키지 배포 및 실행](../packages/deploy-integration-services-ssis-projects-and-packages.md#deploy-and-execute-ssis-packages-using-stored-procedures)을 참조하세요.

## <a name="next-steps"></a>다음 단계
SQL Server 에이전트에 대한 자세한 내용은 [패키지에 대한 SQL Server 에이전트 작업](../packages/sql-server-agent-jobs-for-packages.md)을 참조하세요.

SQL Database의 탄력적 작업에 대한 자세한 내용은 [규모가 확장된 클라우드 데이터베이스 관리](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview)를 참조하세요.
