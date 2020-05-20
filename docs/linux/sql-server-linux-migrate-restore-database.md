---
title: Windows에서 Linux로 SQL Server 데이터베이스 마이그레이션
description: 이 자습서에서는 Windows에서 SQL Server 데이터베이스 백업을 수행하고 SQL Server를 실행하는 Linux 머신으로 복원하는 방법을 보여 줍니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/16/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 9ac64d1a-9fe5-446e-93c3-d17b8f55a28f
ms.openlocfilehash: 148b887497cf9411aad72936a201805000c717ec
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75558565"
---
# <a name="migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restore"></a>백업 및 복원을 사용하여 Windows에서 Linux로 SQL Server 데이터베이스 마이그레이션

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server의 백업 및 복원 기능은 SQL Server on Windows에서 SQL Server on Linux로 데이터베이스를 마이그레이션하는 권장 방법입니다. 이 자습서에서는 백업 및 복원 방법을 사용하여 데이터베이스를 Linux로 이동하는 데 필요한 단계를 안내합니다.

> [!div class="checklist"]
> * SSMS를 사용하여 Windows에서 백업 파일 만들기
> * Windows에 Bash 셸 설치
> * Bash 셸을 통해 Linux로 백업 파일 이동
> * Transact-SQL을 사용하여 Linux에서 백업 파일 복원
> * 쿼리를 실행하여 마이그레이션 확인

SQL Server Always On 가용성 그룹을 만들어 Windows에서 Linux로 SQL Server 데이터베이스를 마이그레이션할 수도 있습니다. [sql-server-linux-availability-group-cross-platform](sql-server-linux-availability-group-cross-platform.md)을 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

이 자습서를 완료하려면 다음 필수 조건이 필요합니다.

* 다음 조건을 충족하는 Windows 머신:
  * [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016-editions)가 설치되어 있음
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)
  * 마이그레이션할 대상 데이터베이스

* 다음 조건을 충족하는 Linux 머신:
  * 명령줄 도구를 사용하는 SQL Server([RHEL](quickstart-install-connect-red-hat.md), [SLES](quickstart-install-connect-suse.md) 또는 [Ubuntu](quickstart-install-connect-ubuntu.md)).

## <a name="create-a-backup-on-windows"></a>Windows에서 백업 만들기

Windows에서 데이터베이스 백업 파일을 만드는 방법에는 여러 가지가 있습니다. 다음 단계에서는 SSMS(SQL Server Management Studio)를 사용합니다.

1. Windows 머신에서 **SQL Server Management Studio**를 시작합니다.

1. 연결 대화 상자에서 **localhost**를 입력합니다.

1. 개체 탐색기에서 **데이터베이스**를 확장합니다.

1. 대상 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **작업**을 선택한 다음, **백업...** 을 클릭합니다.

   ![SSMS를 사용하여 백업 파일 만들기](./media/sql-server-linux-migrate-restore-database/ssms-create-backup.png)

1. **데이터베이스 백업** 대화 상자에서 **백업 유형**이 **전체**이고 **백업할 위치**가 **디스크**인지 확인합니다. 파일의 이름과 위치를 적어 둡니다. 예를 들어 SQL Server 2016의 **YourDB** 데이터베이스는 기본 백업 경로가 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak`입니다.

1. **확인**을 클릭하여 데이터베이스를 백업합니다.

> [!NOTE]
> 또 다른 옵션은 Transact-SQL 쿼리를 실행하여 백업 파일을 만드는 것입니다. 다음 Transact-SQL 명령은 **YourDB** 데이터베이스에 대해 이전 단계와 동일한 작업을 수행합니다.
>
> ```sql
> BACKUP DATABASE [YourDB] TO  DISK =
> N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak'
> WITH NOFORMAT, NOINIT, NAME = N'YourDB-Full Database Backup',
> SKIP, NOREWIND, NOUNLOAD, STATS = 10
> GO
> ```

## <a name="install-a-bash-shell-on-windows"></a>Windows에 Bash 셸 설치

데이터베이스를 복원하려면 먼저 Windows 머신에서 대상 Linux 머신으로 백업 파일을 전송해야 합니다. 이 자습서에서는 Windows에서 실행되는 Bash 셸(터미널 창)을 통해 파일을 Linux로 이동합니다.

1. **scp**(보안 복사) 및 **ssh**(원격 로그인) 명령을 지원하는 Windows 머신에 Bash 셸을 설치합니다. 다음 두 가지 예가 있습니다.

   * [Linux용 Windows 하위 시스템](https://msdn.microsoft.com/commandline/wsl/about)(Windows 10)
   * Git Bash 셸([)https://git-scm.com/downloads](https://git-scm.com/downloads)

1. Windows에서 Bash 세션을 엽니다.

## <a name="copy-the-backup-file-to-linux"></a><a id="scp"></a> Linux에 백업 파일 복사

1. Bash 세션에서 백업 파일이 포함된 디렉터리로 이동합니다. 다음은 그 예입니다.

   ```bash
   cd 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\'
   ```

1. **scp** 명령을 사용하여 파일을 대상 Linux 머신으로 전송합니다. 다음 예제에서는 IP 주소가 *192.0.2.9*인 Linux 서버에 있는 *user1*의 홈 디렉터리로 **YourDB.bak**를 전송합니다.

   ```bash
   scp YourDB.bak user1@192.0.2.9:./
   ```
   ![scp 명령](./media/sql-server-linux-migrate-restore-database/scp-command.png)

> [!TIP]
> 파일 전송에 scp 대신 사용할 수 있는 여러 가지 방법이 있습니다. [Samba](https://help.ubuntu.com/community/Samba)를 사용하여 Windows와 Linux 간에 SMB 네트워크 공유를 구성하는 것도 이러한 방법 중 하나입니다. Ubuntu 관련 연습은 [Samba를 통해 네트워크 공유를 만드는 방법](https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!)을 참조하세요. 설정되고 나면, Windows에서 **\\\\machinenameorip\\share**와 같이 네트워크 파일 공유로 액세스할 수 있습니다.

## <a name="move-the-backup-file-before-restoring"></a>복원 전에 백업 파일 이동

이 시점에는 백업 파일이 Linux 서버의 사용자 홈 디렉터리에 있습니다. 데이터베이스를 SQL Server로 복원하기 전에 **/var/opt/mssql** 하위 디렉터리에 백업을 저장해야 합니다.

1. 동일한 Windows Bash 세션에서 **ssh**를 사용하여 대상 Linux 머신에 원격으로 연결합니다. 다음 예제에서는 사용자 **user1**로 Linux 머신 **192.0.2.9**에 연결합니다.

   ```bash
   ssh user1@192.0.2.9
   ```

   이제 원격 Linux 서버에서 명령을 실행하고 있습니다.

1. 슈퍼 사용자 모드로 전환합니다.

   ```bash
   sudo su
   ```

1. 새 백업 디렉터리를 만듭니다. 디렉터리가 이미 있는 경우에는 -p 매개 변수가 아무 작업도 수행하지 않습니다.

   ```bash
   mkdir -p /var/opt/mssql/backup
   ```

1. 백업 파일을 해당 디렉터리로 이동합니다. 다음 예제에서는 백업 파일이 *user1*의 홈 디렉터리에 상주합니다. 백업 파일의 위치 및 파일 이름과 일치하도록 명령을 변경합니다.

   ```bash
   mv /home/user1/YourDB.bak /var/opt/mssql/backup/
   ```

1. 슈퍼 사용자 모드를 종료합니다.

   ```bash
   exit
   ```

## <a name="restore-your-database-on-linux"></a>Linux에서 데이터베이스 복원

데이터베이스 백업을 복원하려면 **RESTORE DATABASE** TQL(Transact-SQL) 명령을 사용할 수 있습니다.

> [!NOTE]
> 다음 단계에서는 **sqlcmd** 도구를 사용합니다. SQL Server 도구를 설치하지 않은 경우 [Linux에서 SQL Server 명령줄 도구 설치](sql-server-linux-setup-tools.md)를 참조하세요.

1. 동일한 터미널에서 **sqlcmd**를 시작합니다. 다음 예제에서는 **SA** 사용자로 로컬 SQL Server 인스턴스에 연결합니다. 메시지가 표시되면 암호를 입력하거나 **-P** 매개 변수를 추가하여 암호를 지정합니다.

   ```bash
   sqlcmd -S localhost -U SA
   ```

1. `>1` 프롬프트에 다음 **RESTORE DATABASE** 명령을 입력하고 각 줄 뒤에 Enter 키를 누릅니다. 여러 줄로 이루어진 전체 명령을 한 번에 복사하여 붙여넣을 수는 없습니다. 모든 `YourDB` 항목을 데이터베이스 이름으로 바꿉니다.

   ```sql
   RESTORE DATABASE YourDB
   FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',
   MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'
   GO
   ```

   데이터베이스가 복원되었다는 메시지가 표시되어야 합니다.

   `RESTORE DATABASE`에서 다음 예제와 같은 오류가 반환될 수도 있습니다.

   ```bash
   File 'YourDB_Product' cannot be restored to 'Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf'. Use WITH MOVE to identify a valid location for the file.
   Msg 5133, Level 16, State 1, Server servername, Line 1
   Directory lookup for the file "Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf" failed with the operating system error 2(The system cannot find the file specified.).
   ```
   
   이 경우에는 데이터베이스에 보조 파일이 포함되어 있습니다. `RESTORE DATABASE`의 `MOVE` 절에 이 파일을 지정하지 않으면 복원 프로시저에서 원래 서버와 동일한 경로에 파일을 만듭니다. 

   다음 명령을 실행하여 백업에 포함된 모든 파일을 나열할 수 있습니다.
   ```sql
   RESTORE FILELISTONLY FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   GO
   ```
   아래와 같은 목록(처음 두 개의 열만 나열됨)이 표시됩니다.
   ```sql
   LogicalName         PhysicalName                                                                 ..............
   ----------------------------------------------------------------------------------------------------------------------
   YourDB              Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB.mdf          ..............
   YourDB_Product      Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf  ..............
   YourDB_Customer     Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Customer.ndf ..............
   YourDB_log          Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Log.ldf      ..............
   ```
   
   이 목록을 사용하여 추가 파일에 대한 `MOVE` 절을 만들 수 있습니다. 이 예제에서 `RESTORE DATABASE`는 다음과 같습니다.

   ```sql
   RESTORE DATABASE YourDB
   FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',
   MOVE 'YourDB_Product' TO '/var/opt/mssql/data/YourDB_Product.ndf',
   MOVE 'YourDB_Customer' TO '/var/opt/mssql/data/YourDB_Customer.ndf',
   MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'
   GO
   ```


1. 서버에 있는 데이터베이스를 모두 나열하여 복원을 확인합니다. 복원된 데이터베이스가 나열됩니다.

   ```sql
   SELECT Name FROM sys.Databases
   GO
   ```

1. 마이그레이션된 데이터베이스에서 다른 쿼리를 실행합니다. 다음 명령은 컨텍스트를 **YourDB** 데이터베이스로 전환하고 해당 테이블 중 하나에서 행을 선택합니다.

   ```sql
   USE YourDB
   SELECT * FROM YourTable
   GO
   ```

1. **sqlcmd**사용을 마쳤으면 `exit`를 입력합니다.

1. 원격 **ssh** 세션 작업을 마쳤으면 `exit`를 다시 입력합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 Windows에서 데이터베이스를 백업하고 SQL Server를 실행하는 Linux 서버로 이동하는 방법을 알아보았습니다. 구체적으로 다음 작업 방법을 알아보았습니다.
> [!div class="checklist"]
> * SSMS 및 Transact-SQL을 사용하여 Windows에서 백업 파일 만들기
> * Windows에 Bash 셸 설치
> * **scp**를 사용하여 Windows에서 Linux로 백업 파일 이동
> * **ssh**를 사용하여 Linux 머신에 원격으로 연결
> * 복원 준비를 위해 백업 파일 재배치
> * **sqlcmd**를 사용하여 Transact-SQL 명령 실행
> * **RESTORE DATABASE** 명령을 사용하여 데이터베이스 백업 복원 
> * 쿼리를 실행하여 마이그레이션 확인

다음에는 SQL Server on Linux의 다른 마이그레이션 시나리오를 살펴보겠습니다. 

> [!div class="nextstepaction"]
>[SQL Server on Linux로 데이터베이스 마이그레이션](sql-server-linux-migrate-overview.md)
