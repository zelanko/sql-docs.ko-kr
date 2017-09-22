---
title: "만들기 및 Linux에서 SQL Server에 대 한 작업을 실행 | Microsoft Docs"
description: "이 자습서에서는 Linux에서 SQL Server 에이전트 작업을 실행 하는 방법을 보여 줍니다."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 1d93d95e-9c89-4274-9b3f-fa2608ec2792
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 8d05ec1ae3be89b7a087938c44b356ccc9dbca43
ms.contentlocale: ko-kr
ms.lasthandoff: 09/21/2017

---
# <a name="create-and-run-sql-server-agent-jobs-on-linux"></a>만들기 및 Linux에서 SQL Server 에이전트 작업 실행

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

SQL Server 작업이 정기적으로 SQL Server 데이터베이스에 동일한 명령 시퀀스를 수행 하는 데 사용 됩니다. 이 항목에서는 TRANSACT-SQL 및 SQL Server Management Studio (SSMS)를 모두 사용 하 여 Linux에서 SQL Server 에이전트 작업을 만드는 방법의 예제.

이 릴리스에서 SQL Server 에이전트와 알려진된 문제에 대 한 참조는 [릴리스 정보](sql-server-linux-release-notes.md)합니다.

## <a name="prerequisites"></a>필수 구성 요소 
을 만들고 작업을 실행 하려면 먼저 SQL Server 에이전트 서비스를 설치 해야 합니다. 설치 지침에 대 한 참조는 [SQL Server 에이전트 설치 항목](sql-server-linux-setup-sql-agent.md)합니다.

## <a name="create-a-job-with-transact-sql"></a>Transact SQL 있는 job 만들기

다음 TRANSACT-SQL 명령을 사용 하 여 Linux에서 SQL Server 에이전트 작업을 만드는 방법의 예를 제공 합니다. 이 예제에서 이러한 작업 예제 데이터베이스에서 매일 백업을 실행 `SampleDB`합니다. 


> [!TIP]
> 이러한 명령을 실행 하는 T-SQL 클라이언트를 사용할 수 있습니다. 예를 들어 Linux에서 사용할 수 있습니다 [sqlcmd](sql-server-linux-setup-tools.md) 또는 [Visual Studio Code](sql-server-linux-develop-use-vscode.md)합니다. 원격 Windows 서버에서 SQL Server Management Studio (SSMS) 쿼리를 실행 하거나 다음 섹션에 설명 된 작업 관리에 대 한 UI 인터페이스를 사용 하 여 수도 있습니다.

1. **작업을 만들어**합니다. 다음 예제에서는 [sp_add_job](/sql-docs/docs/relational-databases/system-stored-procedures/sp-add-job-transact-sql) 라는 작업을 만들려면 `Daily AdventureWorks Backup`합니다.

    ```tsql
     -- Adds a new job executed by the SQLServerAgent service 
     -- called 'Daily SampleDB Backup'  
     CREATE DATABASE SampleDB
     USE msdb ;  
     GO  
     EXEC dbo.sp_add_job  
         @job_name = N'Daily SampleDB Backup' ;  
     GO

    ```

2. **하나 이상의 작업 단계를 추가**합니다. 다음 TRANSACT-SQL 스크립트를 사용 하 여 [sp_add_jobstep](/sql-docs/docs/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql) 의 백업을 만드는 작업 단계를 만들려면는 `AdventureWlorks2014` 데이터베이스입니다.

    ```tsql
    -- Adds a step (operation) to the job  
    EXEC sp_add_jobstep  
      @job_name = N'Daily SampleDB Backup',  
      @step_name = N'Backup database',  
      @subsystem = N'TSQL',  
      @command = N'BACKUP DATABASE SampleDB TO DISK = \
      N''/var/opt/mssql/data/SampleDB.bak'' WITH NOFORMAT, NOINIT, \
              NAME = ''SampleDB-full'', SKIP, NOREWIND, NOUNLOAD, STATS = 10',   
      @retry_attempts = 5,  
      @retry_interval = 5 ;  
    GO
    ```

3. **작업 일정을 만들**합니다. 이 예에서는 [sp_add_schedule](/sql-docs/docs/relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql) 작업에 대 한 일별 일정을 만듭니다.

    ```tsql
    -- Creates a schedule called 'Daily'  
    EXEC dbo.sp_add_schedule  
     @schedule_name = N'Daily SampleDB',  
     @freq_type = 4,  
     @freq_interval = 1,
     @active_start_time = 233000 ;  
   USE msdb ;  
   GO
    ```

4. **작업에 작업 일정을 연결**합니다. 사용 하 여 [sp_attach_schedule](/sql-docs/docs/relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql) 작업에 작업 일정을 연결 합니다.

    ```tsql
    -- Sets the 'Daily' schedule to the 'Daily AdventureWorks Backup' Job  
    EXEC sp_attach_schedule  
     @job_name = N'Daily SampleDB Backup',  
     @schedule_name = N'Daily SampleDB';  
    GO
    ```

5. **대상 서버에 작업 할당**합니다. 사용 하 여 대상 서버에 작업 할당 [sp_add_jobserver](/sql-docs/docs/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql)합니다. 이 예제에서는 로컬 서버에는 대상이 됩니다.

    ```tsql
    EXEC dbo.sp_add_jobserver  
     @job_name = N'Daily SampleDB Backup',  
     @server_name = N'(LOCAL)';  
    GO
    ```
6. **작업을 시작**합니다. 

    ```tsql
    EXEC dbo.sp_start_job N' Daily SampleDB Backup' ;
    GO
    ```
## <a name="create-a-job-with-ssms"></a>SSMS 있는 job 만들기

만들고 및 원격으로 SQL Server Management Studio (SSMS)를 사용 하 여 Windows에서 작업을 관리할 수도 있습니다.

1. **Windows에서 SSMS를 시작 하 고 Linux SQL Server 인스턴스에 연결 합니다.** 자세한 내용은 참조 [linux SSMS로 SQL Server 관리](sql-server-linux-develop-use-ssms.md)합니다.

1. **SampleDB 라는 이름의 새 데이터베이스 만들기**합니다.

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-0.png" alt="Create a SampleDB database" style="width: 550px;"/>

2. **SQL 에이전트를 설치 하 고 올바르게 구성 되어 있는지 확인 합니다.** 개체 탐색기에서 SQL Server 에이전트 옆의 더하기 기호를 찾습니다. SQL Server 에이전트가 설치 되지 않은 경우 참조 [Linux에서 SQL Server 에이전트 설치](sql-server-linux-setup-sql-agent.md)합니다.

    ![SQL Server 에이전트 설치 확인](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-1.png)


3. **새 작업을 만듭니다.**

    ![새 작업 만들기](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-2.png)


4. **작업 이름을 지정 하 고 작업 단계를 만듭니다.**

    ![작업 단계 만들기](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-3.png)


5. **작업 단계에서 수행 해야 하 고 사용 하려는 하위 시스템을 지정 합니다.**

    ![작업 하위 시스템](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-4.png)

    ![작업 단계 동작](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-5.png)

6. **새 작업 일정을 만듭니다.**

    ![작업 일정](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-6.png)
  
    ![작업 일정](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-8.png)

7. **작업을 시작 합니다.**

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-9.png" alt="Start the SQL Server Agent job" style="width: 550px;"/>

## <a name="next-steps"></a>다음 단계

만들기 및 SQL Server 에이전트 작업을 관리 하는 방법에 대 한 자세한 내용은 참조 [SQL Server 에이전트](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent)합니다.

