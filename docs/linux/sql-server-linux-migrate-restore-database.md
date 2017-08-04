---
title: "Linux를 Windows에서 SQL Server 데이터베이스 마이그레이션 | Microsoft Docs"
description: "이 항목에서는 Windows에서 SQL Server 데이터베이스 백업을 수행 하 고 SQL Server 2017 r c 2를 실행 하는 Linux 컴퓨터를 복원 하는 방법을 보여 줍니다."
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9ac64d1a-9fe5-446e-93c3-d17b8f55a28f
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 2e23ba46381b1fb80b8ac335f6d7630f02a222bb
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restore"></a>Linux 백업 및 복원을 사용 하 여 Windows에서 SQL Server 데이터베이스 마이그레이션

SQL Server의 백업 및 복원 기능은 Linux에서 SQL Server 2017 r c 2로 Windows에서 SQL Server에서 데이터베이스를 마이그레이션하는 것이 좋습니다. 이 항목에서는이 기법에 대 한 단계별 지침을 제공 합니다. 이 자습서에서는 다음을 수행합니다.

- Windows 컴퓨터에 AdventureWorks 백업 파일을 다운로드 합니다.
- Linux 컴퓨터를 백업 전송
- TRANSACT-SQL 명령을 사용 하 여 데이터베이스 복원

> [!NOTE] 
> 이 자습서를 설치 하는 것으로 가정 [SQL Server 2017 RC2](sql-server-linux-setup.md) 및 [SQL Server 도구](sql-server-linux-setup-tools.md) 대상 Linux 서버에 있습니다.

## <a name="download-the-adventureworks-database-backup"></a>AdventureWorks 데이터베이스 백업 다운로드

모든 데이터베이스를 복원 하려면 동일한 단계를 사용 하 여 있지만 AdventureWorks 예제 데이터베이스는 좋은 예를 제공 합니다. 기존 데이터베이스 백업 파일을 제공 합니다.

>[!NOTE] 
> Linux에서 SQL Server로 데이터베이스를 복원 하려면 원본 백업은 SQL Server 2014 또는 SQL Server 2016에서 수행 해야 합니다. SQL Server 빌드 번호는 백업 해야 복원 SQL Server 빌드 번호 보다 클 수 없습니다.  

1. Windows 컴퓨터에서로 이동 [https://msftdbprodsamples.codeplex.com/downloads/get/880661](https://msftdbprodsamples.codeplex.com/downloads/get/880661) 다운로드 하 고는 **Adventure Works 2014 전체 데이터베이스 Backup.zip**합니다.

   > [!TIP] 
   > 이 자습서에서 백업 및 복원 Windows와 Linux 사이의 설명 하지만 직접 Linux 컴퓨터에 AdventureWorks 예제를 다운로드 하려면 Linux에서 브라우저를도 사용할 수 있습니다.

2. Zip 파일을 열고 컴퓨터에 AdventureWorks2014.bak 파일 폴더에 추출 합니다.

## <a name="transfer-the-backup-file-to-linux"></a>Linux 백업 파일 전송

데이터베이스를 복원 하려면 먼저를 전송 해야 백업 파일에서 Windows 컴퓨터 대상 Linux 컴퓨터입니다.

1. Windows, Bash 셸의 설치 합니다. 다음과 같은 여러 옵션이 있습니다.

   - 와 같은 오픈 소스 Bash 셸의 다운로드 [PuTTY](http://www.putty.org/)합니다.
   - 또는 Windows 10에서 사용 하 여 새 [기본 제공 Bash 셸의 (베타)](https://msdn.microsoft.com/en-us/commandline/wsl/about)합니다.
   - 또는 Git를 사용 하는 경우 사용 된 [Git Bash 셸의](https://git-scm.com/downloads)합니다.

2. Bash 셸의 (터미널)을 열고 포함 된 디렉터리를 이동 **AdventureWorks2014.bak**합니다.

3. 사용 하 여는 **scp** (안전한 복사) 명령 대상 Linux 컴퓨터에 파일을 전송 합니다. 다음 예제에서는 전송을 **AdventureWorks2014.bak** 의 홈 디렉터리로 *user1* 라는 서버에 *linuxserver1*합니다.

   ```bash
   sudo scp AdventureWorks2014.bak user1@linuxserver1:./
   ```
   
   이전 예에서 대신 서버 이름 대신 IP 주소를 제공할 수 있습니다.

Scp를 사용 하 여 여러 가지 대안이 있습니다. 하나를 사용 하는 것 [Samba](https://help.ubuntu.com/community/Samba) 창과 Linux 사이의 SMB 네트워크 공유를 설정 합니다. Ubuntu 연습을 참조 하십시오. [는 네트워크 공유를 통해 Samba를 만드는 방법을](https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!)합니다. 설정 되 고 나면 네트워크 파일에으로 액세스할 수 있습니다 windows에서 같은 공유  **\\ \\machinenameorip\\공유**합니다.

## <a name="move-the-backup-file"></a>백업 파일 이동

이 시점에서 백업 파일에 있는 경우 Linux 서버 하위 디렉터리에 백업 배치 해야 하는 SQL Server로 데이터베이스를 복원 하기 전에 **/var/opt/mssql**합니다.

1. 백업이 포함 된 대상 Linux 컴퓨터에서 터미널을 엽니다.

2. 슈퍼 사용자 모드를 입력 합니다.

   ```bash
   sudo su
   ```

3. 새 백업 디렉터리를 만듭니다. 디렉터리가 이미 있는 경우-p 매개 변수는 아무 작업도 수행 합니다.

   ```bash
   mkdir -p /var/opt/mssql/backup
   ```

4. 해당 디렉터리에 백업 파일을 이동 합니다. 다음 예제에서는 백업 파일의 홈 디렉터리에 있는 *user1*합니다. 위치와 일치 하도록 명령을 변경 **AdventureWorks2014.bak** 컴퓨터에 있습니다.

   ```bash
   mv /home/user1/AdventureWorks2014.bak /var/opt/mssql/backup/
   ```

5. 슈퍼 사용자 모드를 종료 합니다.

   ```bash
   exit
   ```

## <a name="restore-the-database-backup"></a>데이터베이스 백업 복원

백업, 복원 하려면 복원 데이터베이스 TRANSACT-SQL (TQL) 명령을 사용할 수 있습니다.

> [!NOTE] 
> 다음 단계는 sqlcmd 도구를 사용 합니다. 설치 하지 않은 경우 SQL Server 도구 참조 [Linux에서 SQL Server 설치](sql-server-linux-setup.md)합니다.

1. 동일한 터미널 시작 **sqlcmd**합니다. 다음 예제에서는 연결을 사용 하 여 로컬 SQL Server 인스턴스는 *SA* 사용자입니다. -P 매개 변수와 함께 암호를 지정 하거나 메시지가 표시 되 면 암호를 입력 합니다.

   ```bash
   sqlcmd -S localhost -U SA
   ```

2. 에 연결한 후 다음과 같이 입력 **데이터베이스 복원** 명령에서 각 줄 뒤 ENTER 키를 누릅니다. 복원 아래 예제에서는 **AdventureWorks2014.bak** 에서 파일의 */var/opt/mssql/backup* 디렉터리입니다.

   ```sql
   RESTORE DATABASE AdventureWorks
   FROM DISK = '/var/opt/mssql/backup/AdventureWorks2014.bak'
   WITH MOVE 'AdventureWorks2014_Data' TO '/var/opt/mssql/data/AdventureWorks2014_Data.mdf',
   MOVE 'AdventureWorks2014_Log' TO '/var/opt/mssql/data/AdventureWorks2014_Log.ldf'
   GO
   ```

   데이터베이스를 성공적으로 복원 하는 메시지가 나타납니다.

3. AdventureWorks 데이터베이스에 첫 번째 컨텍스트를 변경 하 여 복원을 확인 합니다. 

   ```sql
   USE AdventureWorks
   GO
   ```

4. 상위 10 개의 제품을 나열 하는 다음 쿼리를 실행 하는 **Production.Products** 테이블입니다.

   ```sql
   SELECT TOP 10 Name, ProductNumber FROM Production.Product ORDER BY Name
   GO
   ```

![Production.Products 쿼리의 출력](./media/sql-server-linux-migrate-restore-database/sql-server-linux-adventureworks-query.png)

## <a name="next-steps"></a>다음 단계

다른 데이터베이스 및 데이터 마이그레이션 방법에 대 한 자세한 내용은 참조 하십시오. [Linux에서 SQL Server로 데이터베이스 마이그레이션](sql-server-linux-migrate-overview.md)합니다. 

