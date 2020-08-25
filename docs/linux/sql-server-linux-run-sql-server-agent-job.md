---
title: SQL Server on Linux에 대한 작업 만들기 및 실행
description: Transact-SQL 및 SSMS(SQL Server Management Studio)를 둘 다 사용하여 Linux에서 SQL Server 에이전트 작업을 만드는 방법에 대해 알아봅니다.
author: VanMSFT
ms.author: vanto
ms.date: 02/20/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1d93d95e-9c89-4274-9b3f-fa2608ec2792
ms.openlocfilehash: 49d8dab49fef03b3bf06269ef4397656dfa888e3
ms.sourcegitcommit: 3ea082c778f6771b17d90fb597680ed334d3e0ec
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/11/2020
ms.locfileid: "88088823"
---
# <a name="create-and-run-sql-server-agent-jobs-on-linux"></a>Linux에서 SQL Server 에이전트 작업 만들기 및 실행

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

SQL Server 작업은 SQL Server 데이터베이스에서 정기적으로 동일한 명령 시퀀스를 수행하는 데 사용됩니다. 이 자습서에서는 Transact-SQL 및 SSMS(SQL Server Management Studio)를 사용하여 Linux에서 SQL Server 에이전트 작업을 만드는 방법에 대한 예제를 제공합니다.

> [!div class="checklist"]
> * Linux에 SQL Server 에이전트 설치
> * 일별 데이터베이스 백업을 수행하는 새 작업 만들기
> * 작업 예약 및 실행
> * SSMS에서 동일한 단계를 수행합니다(선택 사항).

Linux의 SQL Server 에이전트에 대한 알려진 문제는 [릴리스 정보](sql-server-linux-release-notes.md)를 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

이 자습서를 완료하려면 다음 필수 조건이 필요합니다.

* 다음 필수 조건이 있는 Linux 머신:
  * 명령줄 도구를 사용하는 SQL Server([RHEL](quickstart-install-connect-red-hat.md), [SLES](quickstart-install-connect-suse.md) 또는 [Ubuntu](quickstart-install-connect-ubuntu.md)).

선택적 필수 조건은 다음과 같습니다.

* SSMS를 사용하는 Windows 머신:
  * 선택적 SSMS 단계를 위한 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="enable-sql-server-agent"></a>SQL Server 에이전트 사용

Linux에서 SQL Server 에이전트를 사용하려면 먼저 SQL Server가 설치되어 있는 머신에서 SQL Server 에이전트를 사용하도록 설정해야 합니다.

1. SQL Server 에이전트를 사용하도록 설정하려면 다음 단계를 수행합니다.
  ```bash
  sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
  ```

1. 다음 명령을 사용하여 SQL Server를 다시 시작합니다.
  ```bash
  sudo systemctl restart mssql-server
  ```

> [!NOTE]
> SQL Server 2017 CU4부터 SQL Server 에이전트는 **mssql-server** 패키지에 포함되어 있으며 기본적으로 사용하지 않도록 설정됩니다. CU4 이전 에이전트 설정에 대해서는 [Linux에 SQL Server 에이전트 설치](sql-server-linux-setup-sql-agent.md)를 참조하세요.

## <a name="create-a-sample-database"></a>예제 데이터베이스 만들기

다음 단계를 사용하여 **SampleDB**라는 샘플 데이터베이스를 만듭니다. 이 데이터베이스는 일별 백업 작업에 사용됩니다.

1. Linux 머신에서 bash 터미널 세션을 엽니다.

1. **sqlcmd**를 사용하여 Transact-SQL **CREATE DATABASE** 명령을 실행합니다.

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -Q 'CREATE DATABASE SampleDB'
   ```

1. 서버에 데이터베이스를 나열하여 데이터베이스가 생성되었는지 확인합니다.

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -Q 'SELECT Name FROM sys.Databases'
   ```

## <a name="create-a-job-with-transact-sql"></a>Transact-SQL을 사용하여 작업 만들기

다음 단계에서는 Transact-SQL 명령을 사용하여 Linux에서 SQL Server 에이전트 작업을 만듭니다. 이 작업은 샘플 데이터베이스 **SampleDB**의 일별 백업을 실행합니다.

> [!TIP]
> 모든 T-SQL 클라이언트를 사용하여 이 명령을 실행할 수 있습니다. 예를 들어 Linux에서 [sqlcmd](sql-server-linux-setup-tools.md) 또는 [Visual Studio Code](sql-server-linux-develop-use-vscode.md)를 사용할 수 있습니다. 원격 Windows Server에서는 SSMS(SQL Server Management Studio)에서 쿼리를 실행하거나 다음 섹션에 설명된 대로 작업 관리에 UI 인터페이스를 사용할 수도 있습니다.

1. [sp_add_job](../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)을 사용하여 `Daily SampleDB Backup` 작업을 만듭니다.

   ```sql
   -- Adds a new job executed by the SQLServerAgent service
   -- called 'Daily SampleDB Backup'
   USE msdb ;
   GO
   EXEC dbo.sp_add_job
      @job_name = N'Daily SampleDB Backup' ;
   GO
   ```

1. [sp_add_jobstep](../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)을 호출하여 `SampleDB` 데이터베이스의 백업을 만드는 작업 단계를 만듭니다.

   ```sql
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

1. 그런 다음, [sp_add_schedule](../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md)을 사용하여 작업의 일별 일정을 만듭니다.

   ```sql
   -- Creates a schedule called 'Daily'
   EXEC dbo.sp_add_schedule
      @schedule_name = N'Daily SampleDB',
      @freq_type = 4,
      @freq_interval = 1,
      @active_start_time = 233000 ;
   USE msdb ;
   GO
   ```

1. [sp_attach_schedule](../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)을 사용하여 작업 일정을 작업에 연결합니다.

   ```sql
   -- Sets the 'Daily' schedule to the 'Daily SampleDB Backup' Job
   EXEC sp_attach_schedule
      @job_name = N'Daily SampleDB Backup',
      @schedule_name = N'Daily SampleDB';
   GO
   ```

1. [sp_add_jobserver](../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)를 사용하여 대상 서버에 작업을 할당합니다. 이 예제에서 대상은 로컬 서버입니다.

   ```sql
   EXEC dbo.sp_add_jobserver
      @job_name = N'Daily SampleDB Backup',
      @server_name = N'(LOCAL)';
   GO
   ```
1. [sp_start_job](../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)을 사용하여 작업을 시작합니다.

   ```sql
   EXEC dbo.sp_start_job N' Daily SampleDB Backup' ;
   GO
   ```

## <a name="create-a-job-with-ssms"></a>SSMS를 사용하여 작업 만들기

Windows에서 SSMS(SQL Server Management Studio)를 사용하여 작업을 원격으로 만들고 관리할 수도 있습니다.

1. Windows에서 SSMS를 시작하고 Linux SQL Server 인스턴스에 연결합니다. 자세한 내용은 [SSMS를 사용하여 SQL Server on Linux 관리](sql-server-linux-manage-ssms.md)를 참조하세요.

1. **SampleDB**라는 샘플 데이터베이스를 만들었는지 확인합니다.

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-0.png" alt="Create a SampleDB database" style="width: 550px;"/>

1. SQL 에이전트가 [설치되고](sql-server-linux-setup-sql-agent.md) 올바르게 구성되어 있는지 확인합니다. 개체 탐색기에서 SQL Server 에이전트 옆에 있는 더하기 기호를 찾습니다. SQL Server 에이전트가 사용하도록 설정되지 않은 경우에는 Linux에서 **mssql-server** 서비스를 다시 시작하세요.

   ![SQL Server 에이전트가 설치되었는지 확인](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-1.png)

1. 새 작업을 만듭니다.

   ![새 작업 만들기](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-2.png)

1. 작업에 이름을 지정하고 작업 단계를 만듭니다.

   ![작업 단계 만들기](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-3.png)

1. 사용할 하위 시스템 및 수행할 작업 단계를 지정합니다.

   ![작업 하위 시스템](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-4.png)

   ![작업 단계 동작](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-5.png)

1. 새 작업 일정을 만듭니다.

   ![작업 일정](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-6.png)

   ![작업 일정](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-8.png)

1. 작업을 시작합니다.

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-9.png" alt="Start the SQL Server Agent job" style="width: 550px;"/>

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 작업 방법을 알아보았습니다.

> [!div class="checklist"]
> * Linux에 SQL Server 에이전트 설치
> * Transact-SQL 및 시스템 저장 프로시저를 사용하여 작업 만들기
> * 일별 데이터베이스 백업을 수행하는 작업 만들기
> * SSMS UI를 사용하여 작업 만들기 및 관리

다음으로, 작업을 만들고 관리하기 위한 다른 기능을 살펴봅니다.

> [!div class="nextstepaction"]
>[SQL Server 에이전트 설명서](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent)
