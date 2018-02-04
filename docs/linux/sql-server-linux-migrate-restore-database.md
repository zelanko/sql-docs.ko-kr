---
title: "Linux를 Windows에서 SQL Server 데이터베이스 마이그레이션 | Microsoft Docs"
description: "이 자습서에서는 Windows에서 SQL Server 데이터베이스 백업을 수행 하 고 SQL Server 2017을 실행 하는 Linux 컴퓨터를 복원 하는 방법을 보여 줍니다."
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/16/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 9ac64d1a-9fe5-446e-93c3-d17b8f55a28f
ms.workload: On Demand
ms.openlocfilehash: c97bdbafa557f8d3fe9346431926b9f1a490a286
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2018
---
# <a name="migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restore"></a>Linux 백업 및 복원을 사용 하 여 Windows에서 SQL Server 데이터베이스 마이그레이션

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server의 백업 및 복원 기능은 Windows에서 SQL Server에서 SQL Server 2017 Linux에서 데이터베이스를 마이그레이션하는 것이 좋습니다. 이 자습서에서는 Linux를 백업으로 데이터베이스를 이동한 복원 기술 하는 데 필요한 단계를 안내 합니다.

> [!div class="checklist"]
> * SSMS로 Windows에서 백업 파일을 만듭니다.
> * Bash 셸의 Windows에 설치
> * Bash 셸의에서 백업 파일을 Linux로 이동 합니다.
> * TRANSACT-SQL로 Linux에서 백업 파일을 복원
> * 마이그레이션을 확인 하려면 쿼리를 실행 합니다.

## <a name="prerequisites"></a>필수 구성 요소

이 자습서를 완료 하려면 다음 필수 구성 요소가 필요 합니다.

* 다음으로 Windows 컴퓨터:
  * [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016-editions) 설치 합니다.
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 설치 합니다.
  * 마이그레이션할 대상 데이터베이스입니다.

* 다음을 설치 된 Linux 컴퓨터:
  * SQL Server 2017 ([RHEL](quickstart-install-connect-red-hat.md), [SLES](quickstart-install-connect-suse.md), 또는 [Ubuntu](quickstart-install-connect-ubuntu.md)) 명령줄 도구를 사용 합니다.

## <a name="create-a-backup-on-windows"></a>Windows에서 백업을 만들기

여러 가지 방법으로 Windows에서 데이터베이스의 백업 파일을 만듭니다. 다음 단계에서는 SQL Server Management Studio (SSMS)를 사용 합니다.

1. 시작 **SQL Server Management Studio** Windows 컴퓨터에 있습니다.

1. 연결 대화 상자에 입력 **localhost**합니다.

1. 개체 탐색기에서 확장 **데이터베이스**합니다.

1. 대상 데이터베이스를 마우스 오른쪽 단추로 클릭, 선택 **작업**, 클릭 하 고 **백업...** .

   ![SSMS를 사용 하 여 백업 파일을 만들려면](./media/sql-server-linux-migrate-restore-database/ssms-create-backup.png)

1. 에 **데이터베이스 백업** 대화 상자에서 되어 있는지 확인 **백업 유형** 은 **전체** 및 **백업할** 은 **디스크**합니다. 참고 이름 및 파일의 위치입니다. 예를 들어 라는 데이터베이스 **YourDB** SQL Server 2016의 기본 백업 경로 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak`합니다.

1. 클릭 **확인** 프로그램 데이터베이스를 백업 합니다.

> [!NOTE]
> 두 번째 방법은 백업 파일을 만드는 TRANSACT-SQL 쿼리를 실행 하는 것입니다. 데이터베이스에 대 한 이전 하는 단계와 동일한 동작을 수행 하는 다음 TRANSACT-SQL 명령을 호출 **YourDB**:
>
> ```sql
> BACKUP DATABASE [YourDB] TO  DISK =
> N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak'
> WITH NOFORMAT, NOINIT, NAME = N'YourDB-Full Database Backup',
> SKIP, NOREWIND, NOUNLOAD, STATS = 10
> GO
> ```

## <a name="install-a-bash-shell-on-windows"></a>Bash 셸의 Windows에 설치

데이터베이스를 복원 하려면 먼저를 전송 해야 백업 파일에서 Windows 컴퓨터 대상 Linux 컴퓨터입니다. 이 자습서에서는 파일을 붙여 Linux Bash 셸의 (터미널 창)에서 Windows에서 실행 합니다.

1. Bash 셸의 지 원하는 Windows 컴퓨터에 설치 된 **scp** (복사본 안전함) 및 **ssh** (원격 로그인) 명령. 두 가지 예는 다음과 같습니다.

   * [Linux에 대 한 Windows 하위](https://msdn.microsoft.com/commandline/wsl/about) (Windows 10)
   * Git Bash 셸의 ([https://git-scm.com/downloads](https://git-scm.com/downloads))

1. Windows에서 Bash 세션을 엽니다.

## <a id="scp"></a>Linux 백업 파일 복사

1. Bash 세션에서는 백업 파일에 포함 된 디렉터리로 이동 합니다. 예를 들어

   ```bash
   cd 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\'
   ```

1. 사용 하 여는 **scp** 명령 대상 Linux 컴퓨터에 파일을 전송 합니다. 다음 예제에서는 전송을 **YourDB.bak** 의 홈 디렉터리로 *user1* 의 IP 주소와 Linux 서버에 *192.0.2.9*:

   ```bash
   scp YourDB.bak user1@192.0.2.9:./
   ```
   ![scp 명령](./media/sql-server-linux-migrate-restore-database/scp-command.png)

> [!TIP]
> 파일 전송에 대 한 scp에 대 한 대안 있습니다. 하나를 사용 하는 것 [Samba](https://help.ubuntu.com/community/Samba) 창과 Linux 사이의 SMB 네트워크 공유를 구성 합니다. Ubuntu 연습을 참조 하십시오. [는 네트워크 공유를 통해 Samba를 만드는 방법을](https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!)합니다. 설정 되 고 나면 네트워크 파일에으로 액세스할 수 있습니다 windows에서 같은 공유  **\\ \\machinenameorip\\공유**합니다.

## <a name="move-the-backup-file-before-restoring"></a>복원 하기 전에 백업 파일을 이동

이 시점에서 백업 파일은 사용자의 홈 디렉터리에서 Linux 서버에 있습니다. 하위 디렉터리에 백업 배치 해야 하는 SQL Server로 데이터베이스를 복원 하기 전에 **/var/opt/mssql**합니다.

1. Windows를 이용한 적 동일한 세션에서와 대상 Linux 컴퓨터에 원격으로 연결할 **ssh**합니다. 다음 예제에서는 Linux 컴퓨터에 연결 **192.0.2.9** 사용자로 **user1**합니다.

   ```bash
   ssh user1@192.0.2.9
   ```

   이제에서 실행 하는 명령을 원격 Linux 서버.

1. 슈퍼 사용자 모드를 입력 합니다.

   ```bash
   sudo su
   ```

1. 새 백업 디렉터리를 만듭니다. 디렉터리가 이미 있는 경우-p 매개 변수는 아무 작업도 수행 합니다.

   ```bash
   mkdir -p /var/opt/mssql/backup
   ```

1. 해당 디렉터리에 백업 파일을 이동 합니다. 다음 예제에서는 백업 파일의 홈 디렉터리에 있는 *user1*합니다. 백업 파일의 위치와 파일 이름과 일치 하도록 명령을 변경 합니다.

   ```bash
   mv /home/user1/YourDB.bak /var/opt/mssql/backup/
   ```

1. 슈퍼 사용자 모드를 종료 합니다.

   ```bash
   exit
   ```

## <a name="restore-your-database-on-linux"></a>Linux에서 데이터베이스 복원

데이터베이스 백업을 복원 하려면 사용할 수 있습니다는 **데이터베이스 복원** TRANSACT-SQL (TQL) 명령입니다.

> [!NOTE]
> 다음 단계를 사용 하 여 **sqlcmd** 도구입니다. 설치 하지 않은 경우 SQL Server 도구 참조 [Linux에서 SQL Server 설치 명령줄 도구](sql-server-linux-setup-tools.md)합니다.

1. 동일한 터미널 시작 **sqlcmd**합니다. 다음 예제에서는 연결을 사용 하 여 로컬 SQL Server 인스턴스는 **SA** 사용자입니다. 메시지가 표시 되 면 암호를 입력 하거나 추가 하 여 암호를 지정 된 **-P** 매개 변수입니다.

   ```bash
   sqlcmd -S localhost -U SA
   ```

1. 에 `>1` 프롬프트에서 다음 입력 **데이터베이스 복원** 명령에서 각 줄 (없습니다 복사 및 붙여 전체 여러 줄 명령을 한 번에). 모든 항목을 바꿉니다 `YourDB` 데이터베이스의 이름으로 합니다.

   ```sql
   RESTORE DATABASE YourDB
   FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',
   MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'
   GO
   ```

   데이터베이스를 성공적으로 복원 하는 메시지가 나타납니다.

1. 모든 서버에서 데이터베이스를 나열 하 여 복원을 확인 합니다. 복원된 된 데이터베이스를 나열 합니다.

   ```sql
   SELECT Name FROM sys.Databases
   GO
   ```

1. 마이그레이션된 데이터베이스에서 다른 쿼리를 실행 합니다. 다음 명령에 대 한 컨텍스트를 전환 합니다.는 **YourDB** 데이터베이스 및 테이블 중 하나에서 행을 선택 합니다.

   ```sql
   USE YourDB
   SELECT * FROM YourTable
   GO
   ```

1. 완료 되 면 사용 하 여 **sqlcmd**, 형식 `exit`합니다.

1. 완료 되 면 원격에서 작업 **ssh** 세션을 입력 `exit` 다시 합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 Windows에서 데이터베이스를 백업 하 고 SQL Server 2017을 실행 하는 Linux 서버를 이동 하는 방법을 배웠습니다. 방법에 대해 배웠습니다에:
> [!div class="checklist"]
> * SSMS 및 Transact SQL을 사용 하 여 Windows에서 백업 파일을 만들려면
> * Bash 셸의 Windows에 설치
> * 사용 하 여 **scp** Linux를 Windows에서 백업 파일을 이동 하려면
> * 사용 하 여 **ssh** 원격으로 Linux 컴퓨터에 연결
> * 백업 파일에 대 한 복원을 준비 재배치
> * 사용 하 여 **sqlcmd** TRANSACT-SQL 명령을 실행 하려면
> * 사용 하 여 데이터베이스 백업을 복원는 **데이터베이스 복원** 명령 
> * 마이그레이션을 확인 하려면 쿼리를 실행 합니다.

다음으로 Linux에서 SQL Server에 대 한 다른 마이그레이션 시나리오를 탐색 합니다. 

> [!div class="nextstepaction"]
>[Linux에서 SQL Server로 데이터베이스 마이그레이션](sql-server-linux-migrate-overview.md)
