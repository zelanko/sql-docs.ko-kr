---
title: Linux에서 SQL Server 데이터베이스 백업 및 복원
description: Linux에서 SQL Server 데이터베이스를 백업 및 복원하는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 11/14/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: d30090fb-889f-466e-b793-5f284fccc4e6
ms.openlocfilehash: f90d612eb9064025db8b9ac942dd7f664cedb67e
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85882340"
---
# <a name="backup-and-restore-sql-server-databases-on-linux"></a>Linux에서 SQL Server 데이터베이스 백업 및 복원

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

다른 옵션을 사용하여 SQL Server 2017 on Linux에서 데이터베이스 백업을 수행할 수 있습니다. Linux 서버에서 **sqlcmd**를 사용하여 SQL Server에 연결하고 백업을 수행할 수 있습니다. Windows에서 SQL Server on Linux에 연결하고 사용자 인터페이스를 사용하여 백업을 수행할 수 있습니다. 백업 기능은 플랫폼 간에 동일합니다. 예를 들어 데이터베이스를 로컬에서 원격 드라이브 또는 [Microsoft Azure Blob Storage 서비스](../relational-databases/backup-restore/sql-server-backup-to-url.md)로 백업할 수 있습니다.

## <a name="backup-a-database"></a>데이터베이스 백업

다음 예제에서 **sqlcmd**는 로컬 SQL Server 인스턴스에 연결하고 `demodb`라는 사용자 데이터베이스의 전체 백업을 수행합니다.

```bash
sqlcmd -S localhost -U SA -Q "BACKUP DATABASE [demodb] TO DISK = N'/var/opt/mssql/data/demodb.bak' WITH NOFORMAT, NOINIT, NAME = 'demodb-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
```

명령을 실행하면 SQL Server에서 암호를 입력하라는 메시지가 표시됩니다. 암호를 입력하면 셸에서 백업 진행 결과를 반환합니다. 다음은 그 예입니다.

```
Password:
10 percent processed.
21 percent processed.
32 percent processed.
40 percent processed.
51 percent processed.
61 percent processed.
72 percent processed.
80 percent processed.
91 percent processed.
Processed 296 pages for database 'demodb', file 'demodb' on file 1.
100 percent processed.
Processed 2 pages for database 'demodb', file 'demodb_log' on file 1.
BACKUP DATABASE successfully processed 298 pages in 0.064 seconds (36.376 MB/sec).
```

### <a name="backup-the-transaction-log"></a>트랜잭션 로그 백업

데이터베이스가 전체 복구 모델에 있는 경우 더 세분화된 복원 옵션을 위해 트랜잭션 로그 백업을 수행할 수도 있습니다. 다음 예제에서 **sqlcmd**는 로컬 SQL Server 인스턴스에 연결하고 트랜잭션 로그 백업을 수행합니다.

```bash
sqlcmd -S localhost -U SA -Q "BACKUP LOG [demodb] TO DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak' WITH NOFORMAT, NOINIT, NAME = N'demodb_LogBackup', NOSKIP, NOREWIND, NOUNLOAD, STATS = 5"
```

## <a name="restore-a-database"></a>데이터베이스 복원

다음 예제에서 **sqlcmd**는 SQL Server의 로컬 인스턴스에 연결하고 demodb 데이터베이스를 복원합니다. `NORECOVERY` 옵션은 로그 파일 백업의 추가 복원을 허용하는 데 사용됩니다. 추가 로그 파일을 복원하지 않으려면 `NORECOVERY` 옵션을 제거합니다.

```bash
sqlcmd -S localhost -U SA -Q "RESTORE DATABASE [demodb] FROM DISK = N'/var/opt/mssql/data/demodb.bak' WITH FILE = 1, NOUNLOAD, REPLACE, NORECOVERY, STATS = 5"
```

> [!TIP]
> 실수로 NORECOVERY를 사용하지만 추가 로그 파일 백업이 없는 경우에는 추가 매개 변수 없이 `RESTORE DATABASE demodb` 명령을 실행합니다. 그러면 복원이 완료되고 데이터베이스가 계속 작동합니다.

### <a name="restore-the-transaction-log"></a>트랜잭션 로그를 복원합니다.

다음 명령은 이전 트랜잭션 로그 백업을 복원합니다.

```bash
sqlcmd -S localhost -U SA -Q "RESTORE LOG demodb FROM DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak'"
```

## <a name="backup-and-restore-with-sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio)를 사용하여 백업 및 복원

Windows 컴퓨터에서 SSMS를 사용하여 Linux 데이터베이스에 연결하고 사용자 인터페이스를 통해 백업을 수행할 수 있습니다.

>[!NOTE] 
> 최신 버전의 SSMS를 사용하여 SQL Server에 연결합니다. 최신 버전을 다운로드하여 설치하려면 [SSMS 다운로드](../ssms/download-sql-server-management-studio-ssms.md)를 참조하세요. SSMS 사용 방법에 대한 자세한 내용은 [SSMS를 사용하여 SQL Server on Linux 관리](sql-server-linux-manage-ssms.md)를 참조하세요.

다음 단계에서는 SSMS를 사용하여 백업을 수행하는 과정을 안내합니다. 

1. SQL Server 2017 on Linux에서 SSMS를 시작하고 서버에 연결합니다.

1. 개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **작업**을 클릭한 후 **백업...** 을 클릭합니다.

1. **데이터베이스 백업** 대화 상자에서 매개 변수 및 옵션을 확인하고 **확인**을 클릭합니다.
 
SQL Server가 데이터베이스 백업을 완료합니다.

### <a name="restore-with-sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio)를 사용하여 복원 

다음 단계에서는 SSMS를 사용하여 데이터베이스를 복원하는 과정을 안내합니다.

1. SSMS에서 **데이터베이스**를 마우스 오른쪽 단추로 클릭하고 **데이터베이스 복원...** 을 클릭합니다. 

1. **원본**에서 **디바이스:** 를 클릭한 후 줄임표(...)를 클릭합니다.

1. 데이터베이스 백업 파일을 찾고 **확인**을 클릭합니다. 

1. **복원 계획**에서 백업 파일 및 설정을 확인합니다. **확인**을 클릭합니다. 

1. SQL Server가 데이터베이스를 복원합니다. 

## <a name="see-also"></a>참고 항목

* [전체 데이터베이스 백업 만들기(SQL Server)](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)
* [트랜잭션 로그 백업(SQL Server)](../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)
* [BACKUP(Transact-SQL)](../t-sql/statements/backup-transact-sql.md)
* [URL에 SQL Server Backup](../relational-databases/backup-restore/sql-server-backup-to-url.md)
