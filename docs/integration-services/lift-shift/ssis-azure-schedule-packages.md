---
title: "Azure에서 SSIS 패키지 실행을 예약 합니다. | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 2f28400200105e8e63f787cbcda58c183ba00da5
ms.openlocfilehash: 2130e68d5e29671a2881d8762666cf852ff51259
ms.contentlocale: ko-kr
ms.lasthandoff: 10/18/2017

---
# <a name="schedule-the-execution-of-an-ssis-package-on-azure"></a>Azure에서 SSIS 패키지의 실행 일정
다음 일정 옵션 중 하나를 선택 하 여 Azure SQL 데이터베이스 서버에 SSISDB 카탈로그 데이터베이스에 저장 된 패키지의 실행을 예약할 수 있습니다.
-   [SQL Server 에이전트](#agent)
-   [SQL 데이터베이스 탄력적 작업](#elastic)
-   [Azure 데이터 팩터리 SQL Server 저장 프로시저 작업](#sproc)

## <a name="agent"></a>SQL Server 에이전트를 사용 하 여 패키지 예약

### <a name="prerequisite"></a>필수 구성 요소

Azure SQL 데이터베이스 서버에 저장 된 패키지의 실행 일정을 온-프레미스 SQL Server 에이전트를 사용 하려면, 먼저 연결 된 서버로 SQL 데이터베이스 서버를 추가 해야 합니다. 자세한 내용은 참조 하십시오. [연결 된 서버 만들기](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md) 및 [연결 된 서버](../../relational-databases/linked-servers/linked-servers-database-engine.md)합니다.

### <a name="create-a-sql-server-agent-job"></a>SQL Server 에이전트 작업 만들기

일정을 온-프레미스 SQL Server 에이전트를 사용 하 여 패키지를 SSIS 카탈로그를 호출 하는 작업 단계와 작업을 만드는 저장 프로시저 `[catalog].[create_execution]` 차례로 `[catalog].[start_execution]`합니다. 자세한 내용은 참조 하십시오. [패키지에 대 한 SQL Server 에이전트 작업](../packages/sql-server-agent-jobs-for-packages.md)합니다.

1.  SQL Server Management Studio에서 작업을 만드는 데 사용할 온-프레미스 SQL Server 데이터베이스에 연결 합니다.

2.  마우스 오른쪽 단추로 클릭는 **SQL Server 에이전트** 노드를 선택 **새로**를 선택한 후 **작업** 열려는 **새 작업** 대화 상자.

3.  에 **새 작업** 대화 상자는 **단계** 페이지를 선택한 다음 선택 **새로** 를 열려면는 **새 작업 단계** 대화 상자.

4.  에 **새 작업 단계** 대화 상자에서 `SSISDB` 로 **데이터베이스입니다.**

5.  명령 필드에서 다음 예제와 같이 스크립트와 유사한 Transact SQL 스크립트를 입력 합니다.

    ```sql
    DECLARE @return_value int, @exe_id bigint 

    EXEC @return_value = [YourLinkedServer].[SSISDB].[catalog].[create_execution] 
    @folder_name=N'folderName', @project_name=N'projectName', 
    @package_name=N'packageName', @use32bitruntime=0, 
    @runinscaleout=1, @useanyworker=1, @execution_id=@exe_id OUTPUT 
 
    EXEC [YourLinkedServer].[SSISDB].[catalog].[start_execution] @execution_id=@exe_id

    GO
    ```

6.  구성 하는 작업을 예약 하 고 완료 합니다.

## <a name="elastic"></a>SQL 데이터베이스 탄력적 작업을 사용 하 여 패키지 예약

SQL 데이터베이스 탄력적 작업에 대 한 자세한 내용은 참조 하십시오. [관리 확장 클라우드 데이터베이스](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-jobs-overview)합니다.

### <a name="prerequisites"></a>필수 구성 요소

Azure SQL 데이터베이스 서버에 SSISDB 카탈로그 데이터베이스에 저장 하는 SSIS 패키지를 예약 하 탄력적 작업을 사용 하려면 먼저 다음 작업을 수행 해야 합니다.

1.  설치 하 고 탄력적 데이터베이스 작업 구성 요소를 구성 합니다. 자세한 내용은 참조 하십시오. [설치 탄력적 데이터베이스 작업 개요](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-jobs-service-installation)합니다.

2. 작업은 SSIS 카탈로그 데이터베이스에 명령을 보냅니다 하는 데 사용할 수 있는 데이터베이스 범위 자격 증명을 만듭니다. 자세한 내용은 참조 하십시오. [만들 데이터베이스 범위 자격 증명 (Transact SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)합니다.

### <a name="create-an-elastic-job"></a>탄력적 작업 만들기

다음 예제와 같이 스크립트와 유사한 Transact SQL 스크립트를 사용 하 여 작업을 만듭니다.

```sql
-- Create Elastic Jobs target group 
EXEC jobs.sp_add_target_group 'TargetGroup' 
? 
-- Add Elastic Jobs target group member 
EXEC jobs.sp_add_target_group_member @target_group_name='TargetGroup', 
    @target_type='SqlDatabase', @server_name='YourSQLDBServer.database.windows.net',
    @database_name='SSISDB' 
? 
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

## <a name="sproc"></a>Azure 데이터 팩터리 SQL Server 저장 프로시저 활동을 사용 하 여 패키지 예약

> [!IMPORTANT]
> JSON 스크립트를 사용 하 여 Azure 데이터 팩터리 버전 1 다음 예제에서 저장 프로시저 작업 합니다.

Azure 데이터 팩터리 SQL Server 저장 프로시저 활동을 사용 하 여 패키지를 예약 하려면 다음 작업을 수행 합니다.

1.  데이터 팩터리를 만듭니다.

2.  SSISDB를 호스팅하는 SQL 데이터베이스에 대 한 연결 된 서비스를 만들었습니다.

3.  일정을 구동 하는 출력 데이터 집합을 만듭니다.

4.  SQL Server 저장 프로시저 활동을 사용 하 여 SSIS 패키지를 실행 하는 데이터 팩터리 파이프라인을 만듭니다.

이 섹션에서는 이러한 단계의 개요를 제공 합니다. 전체 데이터 팩터리의 자습서는이 문서의 범위를 벗어납니다. 자세한 내용은 참조 하십시오. [SQL Server 저장 프로시저 작업](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-stored-proc-activity)합니다.

### <a name="created-a-linked-service-for-the-sql-database-that-hosts-ssisdb"></a>SSISDB를 호스팅하는 SQL 데이터베이스에 대 한 연결 된 서비스를 만들었습니다.
연결 된 서비스 데이터 팩터리의 SSISDB에 연결할 수 있습니다.

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
출력 데이터 집합의 일정 정보를 포함합니다.

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
### <a name="create-a-data-factory-pipeline"></a>데이터 팩터리 파이프라인 만들기
SQL Server 저장 프로시저 활동을 사용 하 여 SSIS 패키지를 실행 하는 파이프라인입니다.

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

SSIS 패키지 실행 생성 및 시작 하는 데 필요한 TRANSACT-SQL 명령을 캡슐화 하는 새 저장된 프로시저를 만들 필요가 없습니다. 값으로 전체 스크립트를 제공할 수 있습니다는 `stmt` 앞의 예제 JSON 매개 변수입니다. 샘플 스크립트는 다음과 같습니다.

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

이 스크립트의 코드에 대 한 자세한 내용은 참조 하십시오. [배포 및 저장 프로시저를 사용 하 여 SSIS 패키지 실행](../packages/deploy-integration-services-ssis-projects-and-packages.md#deploy-and-execute-ssis-packages-using-stored-procedures)합니다.

## <a name="next-steps"></a>다음 단계
SQL Server 에이전트에 대 한 자세한 내용은 참조 하십시오. [패키지에 대 한 SQL Server 에이전트 작업](../packages/sql-server-agent-jobs-for-packages.md)합니다.

SQL 데이터베이스 탄력적 작업에 대 한 자세한 내용은 참조 하십시오. [관리 확장 클라우드 데이터베이스](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-jobs-overview)합니다.
