---
title: Azure에서 SSIS 패키지 예약 | Microsoft Docs
description: Azure SQL Database에 배포된 SSIS 패키지의 실행을 예약하는 데 사용할 수 있는 방법의 개요를 제공합니다.
ms.date: 05/29/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: maghan
ms.openlocfilehash: 4217acf163e8603c5993cfa8ade4207c9a79c6cf
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68054557"
---
# <a name="schedule-the-execution-of-sql-server-integration-services-ssis-packages-deployed-in-azure"></a>Azure에 배포된 SSIS(SQL Server Integration Services) 실행 예약

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



이 문서에 설명된 메서드 중 하나를 선택하여 Azure SQL Database 서버의 SSISDB 카탈로그에 배포된 SSIS 패키지의 실행을 예약할 수 있습니다. 패키지를 직접 예약하거나 Azure Data Factory 파이프라인의 일부로 패키지를 간접적으로 예약할 수 있습니다. Azure의 SSIS에 대한 개요는 [SQL Server Integration Services 워크로드를 클라우드로 리프트 앤 시프트](ssis-azure-lift-shift-ssis-packages-overview.md)를 참조하세요.

- 패키지 직접 예약

  - [SSMS(SQL Server Management Studio)의 일정 옵션을 사용하여 예약](#ssms)

  - [SQL Database 탄력적 작업](#elastic)

  - [SQL Server 에이전트](#agent)

- [Azure Data Factory 파이프라인의 일부로 패키지를 간접적으로 예약](#activity)


## <a name="ssms"></a> SSMS를 사용하여 패키지 예약

SSMS(SQL Server Management Studio)에서 SSIS 카탈로그 데이터베이스인 SSISDB에 배포된 패키지를 마우스 오른쪽 단추로 클릭하고, **일정**을 선택하여 **새 일정** 대화 상자를 열 수 있습니다. 자세한 내용은 [SSMS를 사용하여 Azure에서 SSIS 패키지 예약](ssis-azure-schedule-packages-ssms.md)을 참조합니다.

이 기능을 사용하려면 SQL Server Management Studio 버전 17.7 이상이 필요합니다. SSMS의 최신 버전을 다운로드하려면 [Download SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md)(SSMS(SQL Server Management Studio) 다운로드)를 참조하세요.

## <a name="elastic"></a> SQL Database 탄력적 작업을 사용하여 패키지 예약

SQL Database의 탄력적 작업에 대한 자세한 내용은 [규모가 확장된 클라우드 데이터베이스 관리](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview)를 참조하세요.

### <a name="prerequisites"></a>사전 요구 사항

탄력적 작업을 사용하여 Azure SQL Database 서버의 SSISDB 카탈로그 데이터베이스에 저장된 SSIS 패키지를 예약하려면 다음 작업을 수행해야 합니다.

1.  Elastic Database 작업 구성 요소를 설치하고 구성합니다. 자세한 내용은 [Elastic Database 작업 설치 개요](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-service-installation)를 참조하세요.

2. 작업에서 SSIS 카탈로그 데이터베이스에 명령을 보내는 데 사용할 수 있는 데이터베이스 범위 자격 증명을 만듭니다. 자세한 내용은 [CREATE DATABASE SCOPED CREDENTIAL(Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)을 참조하세요.

### <a name="create-an-elastic-job"></a>탄력적 작업 만들기

다음 예제에 표시된 스크립트와 비슷한 Transact-SQL 스크립트를 사용하여 작업을 만듭니다.

```sql
-- Create Elastic Jobs target groupÂ 
EXECÂ jobs.sp_add_target_group 'TargetGroup'Â 

-- Add Elastic Jobs target group memberÂ 
EXECÂ jobs.sp_add_target_group_memberÂ @target_group_name='TargetGroup',Â 
    @target_type='SqlDatabase',Â @server_name='YourSQLDBServer.database.windows.net',
    @database_name='SSISDB'Â 

-- Add a job to schedule SSIS package execution
EXECÂ jobs.sp_add_jobÂ @job_name='ExecutePackageJob',Â @description='Description',Â 
    @schedule_interval_type='Minutes',Â @schedule_interval_count=60

-- Add a job step to create/start SSIS package execution using SSISDB catalog stored procedures
EXECÂ jobs.sp_add_jobstepÂ @job_name='ExecutePackageJob',Â 
    @command=N'DECLAREÂ @exe_idÂ bigintÂ 
        EXEC [SSISDB].[catalog].[create_execution]
            @folder_name=N''folderName'', @project_name=N''projectName'',
            @package_name=N''packageName'', @use32bitruntime=0,
            @runinscaleout=1, @useanyworker=1,Â 
            @execution_id=@exe_idÂ OUTPUT       Â 
        EXEC [SSISDB].[catalog].[start_execution] @exe_id, @retry_count=0',Â 
    @credential_name='YourDBScopedCredentials',Â 
    @target_group_name='TargetGroup'Â 

-- Enable the job scheduleÂ 
EXECÂ jobs.sp_update_jobÂ @job_name='ExecutePackageJob',Â @enabled=1,Â 
    @schedule_interval_type='Minutes',Â @schedule_interval_count=60Â 
```

## <a name="agent"></a> 프레미스에서 SQL Server 에이전트를 사용하여 패키지 예약

SQL Server 에이전트에 대한 자세한 내용은 [패키지에 대한 SQL Server 에이전트 작업](../packages/sql-server-agent-jobs-for-packages.md)을 참조하세요.

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
        @location='',
        @provstr='',
        @catalog='SSISDB'  -- Add SSISDB as the initial catalog
    ```

2.  **연결된 서버 자격 증명 설정**

    ```sql
    -- Add your Azure SQL DB server admin credentials
    EXEC sp_addlinkedsrvlogin
        @rmtsrvname = 'myLinkedServer',
        @useself = 'false',
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
    DECLARE @return_valueÂ int,Â @exe_idÂ bigintÂ 

    EXEC @return_valueÂ =Â [YourLinkedServer].[SSISDB].[catalog].[create_execution]Â 
        @folder_name=N'folderName',Â @project_name=N'projectName',Â 
        @package_name=N'packageName',Â @use32bitruntime=0,Â @runincluster=1,Â @useanyworker=1,
        @execution_id=@exe_idÂ OUTPUTÂ 

    EXEC [YourLinkedServer].[SSISDB].[catalog].[set_execution_parameter_value] @exe_id,
        @object_type=50, @parameter_name=N'SYNCHRONIZED', @parameter_value=1

    EXEC [YourLinkedServer].[SSISDB].[catalog].[start_execution]Â @execution_id=@exe_id
    ```

6.  작업 구성 및 예약을 완료합니다.

## <a name="activity"></a> Azure Data Factory 파이프라인의 일부로 패키지 예약

SSIS 패키지를 실행하는 Azure Data Factory 파이프라인을 실행하려면 트리거를 사용하여 패키지를 간접적으로 예약할 수 있습니다.

Data Factory 파이프라인을 예약하려면 다음 트리거 중 하나를 사용합니다.

- [일정 트리거](https://docs.microsoft.com/azure/data-factory/how-to-create-schedule-trigger)

- [연속 창(tumbling window) 트리거](https://docs.microsoft.com/azure/data-factory/how-to-create-tumbling-window-trigger)

- [이벤트 기반 트리거](https://docs.microsoft.com/azure/data-factory/how-to-create-event-trigger)

Data Factory 파이프라인의 일부로 SSIS 패키지를 실행하려면 다음 작업 중 하나를 사용합니다.

- [SSIS 패키지 작업 실행](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity).

- [저장 프로시저 작업](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-stored-procedure-activity).

## <a name="next-steps"></a>다음 단계

Azure에 배포된 SSIS 패키지를 실행하기 위한 옵션을 검토합니다. 자세한 내용은 [Azure에서 SSIS 패키지 실행](ssis-azure-run-packages.md)을 참조합니다.
