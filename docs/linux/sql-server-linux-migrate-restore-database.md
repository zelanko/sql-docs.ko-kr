---
title: Linux에서 Windows SQL Server 데이터베이스 마이그레이션 | Microsoft Docs
description: 이 자습서에서는 Windows에서 SQL Server 데이터베이스 백업을 수행 하 여 SQL Server를 실행 하는 Linux 컴퓨터를 복원 하는 방법을 보여 줍니다.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/16/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 9ac64d1a-9fe5-446e-93c3-d17b8f55a28f
ms.openlocfilehash: 0da1e0c866d0934671ebe6291c39d2247a28de07
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47729421"
---
# <a name="migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restore"></a>백업 및 복원을 사용 하 여 Linux를 Windows에서 SQL Server 데이터베이스 마이그레이션

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server의 백업 및 복원 기능은 Windows의 SQL Server에서 Linux의 SQL Server로 데이터베이스를 마이그레이션하는 것이 좋습니다. 이 자습서에서는 Linux에 백업을 사용 하 여 데이터베이스를 이동 하 고 복원 기술 하는 데 필요한 단계를 안내 합니다.

> [!div class="checklist"]
> * SSMS를 사용 하 여 Windows에서 백업 파일 만들기
> * Windows에서 Bash 셸을 설치합니다
> * Bash 셸에서 백업 파일을 Linux로 이동 합니다.
> * TRANSACT-SQL을 사용 하 여 Linux에서 백업 파일 복원
> * 마이그레이션을 확인 하려면 쿼리를 실행 합니다.

SQL Server Always On 가용성 그룹에서 Linux Windows에서 SQL Server 데이터베이스 마이그레이션도 만들 수 있습니다. 참조 [sql-server-linux-availability-group-cross-platform](sql-server-linux-availability-group-cross-platform.md)합니다.

## <a name="prerequisites"></a>사전 요구 사항

이 자습서를 완료 하려면 다음 필수 조건이 필요 합니다.

* 다음을 사용 하 여 Windows 컴퓨터:
  * [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016-editions) 설치 합니다.
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 설치 합니다.
  * 마이그레이션할 대상 데이터베이스입니다.

* 다음을 설치를 사용 하 여 Linux 컴퓨터:
  * SQL Server ([RHEL](quickstart-install-connect-red-hat.md)하십시오 [SLES](quickstart-install-connect-suse.md), 또는 [Ubuntu](quickstart-install-connect-ubuntu.md)) 명령줄 도구를 사용 합니다.

## <a name="create-a-backup-on-windows"></a>Windows에서 백업을 만들기

Windows에서 데이터베이스의 백업 파일을 만들려고 하는 방법은 여러 가지가 있습니다. 다음 단계에서는 SQL Server Management Studio (SSMS)를 사용 합니다.

1. 시작 **SQL Server Management Studio** Windows 컴퓨터에 있습니다.

1. 연결 대화 상자에서 입력 **localhost**합니다.

1. 개체 탐색기에서 확장 **데이터베이스**합니다.

1. 대상 데이터베이스를 마우스 오른쪽 단추로 클릭 한 다음를 선택 합니다 **태스크**를 클릭 하 고 **백업 하는 중...** .

   ![SSMS를 사용 하 여 백업 파일을 만들려면](./media/sql-server-linux-migrate-restore-database/ssms-create-backup.png)

1. 에 **데이터베이스 백업** 대화 상자에서 확인 **백업 유형** 은 **전체** 및 **백업할** 는 **디스크**. 노트 이름 및 파일의 위치입니다. 예를 들어, 명명 된 데이터베이스 **YourDB** SQL Server 2016의 기본 백업 경로 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak`입니다.

1. 클릭 **확인** 에 데이터베이스를 백업 합니다.

> [!NOTE]
> 백업 파일을 만드는 TRANSACT-SQL 쿼리를 실행 하는 방법도 있습니다. 데이터베이스에 대해 이전 단계와 동일한 동작을 수행 하는 다음 TRANSACT-SQL 명령을 호출 **YourDB**:
>
> ```sql
> BACKUP DATABASE [YourDB] TO  DISK =
> N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak'
> WITH NOFORMAT, NOINIT, NAME = N'YourDB-Full Database Backup',
> SKIP, NOREWIND, NOUNLOAD, STATS = 10
> GO
> ```

## <a name="install-a-bash-shell-on-windows"></a>Windows에서 Bash 셸을 설치합니다

데이터베이스를 복원 하려면 대상 Linux 컴퓨터에 Windows 컴퓨터에서 백업 파일을 먼저 전송 해야 있습니다. 이 자습서에서는 파일을 Linux에서는 Bash 셸 (터미널 창)에서 Windows를 실행 이동 했습니다.

1. Bash 셸을 지 원하는 Windows 컴퓨터에 설치 합니다 **scp** (보안 복사) 및 **ssh** (원격 로그인) 명령입니다. 두 가지 예입니다.

   * 합니다 [Linux 용 Windows 하위 시스템](https://msdn.microsoft.com/commandline/wsl/about) (Windows 10)
   * Git Bash 셸 ([https://git-scm.com/downloads](https://git-scm.com/downloads))

1. Windows에서 Bash 세션을 엽니다.

## <a id="scp"></a> Linux 백업 파일 복사

1. Bash 세션에서 백업 파일이 있는 디렉터리로 이동 합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.

   ```bash
   cd 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\'
   ```

1. 사용 된 **scp** 명령 대상 Linux 컴퓨터에 파일을 전송 합니다. 다음 예제에서는 전송을 **YourDB.bak** 의 홈 디렉터리로 *user1* 의 IP 주소를 사용 하 여 Linux 서버의 *192.0.2.9*:

   ```bash
   scp YourDB.bak user1@192.0.2.9:./
   ```
   ![scp 명령](./media/sql-server-linux-migrate-restore-database/scp-command.png)

> [!TIP]
> 파일 전송에 대 한 scp를 사용 하는 대안이 있습니다. 하나를 사용 하는 것 [Samba](https://help.ubuntu.com/community/Samba) Windows와 Linux SMB 네트워크 공유를 구성 합니다. Ubuntu의 연습을 참조 하세요 [는 네트워크 공유를 통해 Samba를 만드는 방법](https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!)합니다. 설정 되 면 네트워크 파일으로 액세스할 수 있습니다 Windows에서 같이 공유  **\\ \\machinenameorip\\공유**합니다.

## <a name="move-the-backup-file-before-restoring"></a>복원 전에 백업 파일을 이동 합니다.

이 시점에서 사용자의 홈 디렉터리에서 Linux 서버에는 백업 파일입니다. 하위 디렉터리에 백업을 배치 해야 하는 SQL server 데이터베이스를 복원 하기 전에 **/var/opt/mssql**합니다.

1. 동일한 Windows Bash 세션에서 사용 하 여 대상 Linux 컴퓨터에 원격으로 연결할 **ssh**합니다. 다음 예제에서는 Linux 컴퓨터에 연결 **192.0.2.9** 사용자로 **user1**합니다.

   ```bash
   ssh user1@192.0.2.9
   ```

   이제 원격 Linux 서버에서 명령을 실행 하는 있습니다.

1. 슈퍼 사용자 모드를 입력 합니다.

   ```bash
   sudo su
   ```

1. 새 백업 디렉터리를 만듭니다. -P 매개 변수는 아무 효과도 없습니다 디렉터리가 이미 있습니다.

   ```bash
   mkdir -p /var/opt/mssql/backup
   ```

1. 해당 디렉터리에 백업 파일을 이동 합니다. 다음 예제에서는 백업 파일의 홈 디렉터리에 상주 *user1*합니다. 백업 파일의 위치 및 파일 이름과 일치 하도록 명령을 변경 합니다.

   ```bash
   mv /home/user1/YourDB.bak /var/opt/mssql/backup/
   ```

1. 슈퍼 사용자 모드를 종료 합니다.

   ```bash
   exit
   ```

## <a name="restore-your-database-on-linux"></a>Linux에서 데이터베이스 복원

데이터베이스 백업을 복원 하려면 사용 합니다 **RESTORE DATABASE** TRANSACT-SQL (TQL) 명령.

> [!NOTE]
> 다음 단계를 사용 합니다 **sqlcmd** 도구입니다. 설치 하지 않은 경우 SQL Server 도구를 참조 하세요 [Linux의 SQL Server 설치 명령줄 도구](sql-server-linux-setup-tools.md)합니다.

1. 동일한 터미널에서 시작 **sqlcmd**합니다. 다음 예제에서는 로컬 SQL Server 인스턴스에 연결 합니다 **SA** 사용자입니다. 메시지가 표시 되 면 암호를 입력 하거나 추가 하 여 암호를 지정 합니다 **-P** 매개 변수입니다.

   ```bash
   sqlcmd -S localhost -U SA
   ```

1. 에 `>1` 프롬프트에서 다음을 입력 합니다 **RESTORE DATABASE** (있습니다 수 없습니다. 복사 및 붙여넣기 전체 여러 줄 명령을 한 번에) 각 줄 뒤 ENTER 키를 눌러 명령입니다. 모든 항목을 바꿀 `YourDB` 데이터베이스의 이름입니다.

   ```sql
   RESTORE DATABASE YourDB
   FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',
   MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'
   GO
   ```

   데이터베이스를 복원 했습니다. 메시지를 가져와야 합니다.

   `RESTORE DATABASE` 다음 예제와 같이 오류를 반환할 수 있습니다.

   ```bash
   File 'YourDB_Product' cannot be restored to 'Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf'. Use WITH MOVE to identify a valid location for the file.
   Msg 5133, Level 16, State 1, Server servername, Line 1
   Directory lookup for the file "Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf" failed with the operating system error 2(The system cannot find the file specified.).
   ```
   
   이 경우 데이터베이스는 보조 파일을 포함합니다. 이러한 파일에 지정 되지 않은 경우는 `MOVE` 절의 `RESTORE DATABASE`, 복원 절차는 원본 서버와 동일한 경로에 만들려고 시도 합니다. 

   백업에 포함 된 모든 파일을 나열할 수 있습니다.
   ```sql
   RESTORE FILELISTONLY FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   GO
   ```
   (첫 번째 두 개의 열만 나열) 아래와 같은 목록을 얻게 됩니다.
   ```sql
   LogicalName         PhysicalName                                                                 ..............
   ----------------------------------------------------------------------------------------------------------------------
   YourDB              Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB.mdf          ..............
   YourDB_Product      Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf  ..............
   YourDB_Customer     Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Customer.ndf ..............
   YourDB_log          Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Log.ldf      ..............
   ```
   
   이 목록을 사용 하 여 만들려는 `MOVE` 절 추가 파일에 대 한 합니다. 이 예제에서는 `RESTORE DATABASE` 됩니다.

   ```sql
   RESTORE DATABASE YourDB
   FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',
   MOVE 'YourDB_Product' TO '/var/opt/mssql/data/YourDB_Product.ndf',
   MOVE 'YourDB_Customer' TO '/var/opt/mssql/data/YourDB_Customer.ndf',
   MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'
   GO
   ```


1. 모든 서버에서 데이터베이스를 나열 하 여 복원 작업을 확인 합니다. 복원된 된 데이터베이스 나열 되어야 합니다.

   ```sql
   SELECT Name FROM sys.Databases
   GO
   ```

1. 마이그레이션된 데이터베이스에서 다른 쿼리를 실행 합니다. 명령을 컨텍스트를 전환 합니다 **YourDB** 데이터베이스 및 테이블 중 하나에서 행을 선택 합니다.

   ```sql
   USE YourDB
   SELECT * FROM YourTable
   GO
   ```

1. 완료 되 면 사용 하 여 **sqlcmd**, 형식 `exit`합니다.

1. 완료 되 면 원격에서 작업 **ssh** 세션을 입력 `exit` 다시 합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 Windows에서 데이터베이스를 백업 하 고 SQL Server를 실행 하는 Linux 서버로 이동 하는 방법을 알아보았습니다. 방법을 배웠습니다에:
> [!div class="checklist"]
> * SSMS 및 TRANSACT-SQL을 사용 하 여 Windows에서 백업 파일을 만들려면
> * Windows에서 Bash 셸을 설치합니다
> * 사용 하 여 **scp** 백업 파일을 Windows에서 Linux을 이동 하려면
> * 사용 하 여 **ssh** Linux 컴퓨터에 원격으로 연결
> * 백업 파일에 대 한 복원을 준비 재배치
> * 사용 하 여 **sqlcmd** TRANSACT-SQL 명령을 실행 하려면
> * 사용 하 여 데이터베이스 백업을 복원 합니다 **RESTORE DATABASE** 명령 
> * 마이그레이션을 확인 하려면 쿼리를 실행 합니다.

다음으로, Linux의 SQL Server에 대 한 다른 마이그레이션 시나리오를 살펴봅니다. 

> [!div class="nextstepaction"]
>[Linux에서 SQL Server로 데이터베이스 마이그레이션](sql-server-linux-migrate-overview.md)
