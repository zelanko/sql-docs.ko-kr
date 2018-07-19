---
title: Linux의 SQL Server 데이터베이스 백업 및 복원 | Microsoft Docs
description: Linux의 SQL Server 데이터베이스 백업 및 복원 하는 방법에 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 11/14/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: d30090fb-889f-466e-b793-5f284fccc4e6
ms.openlocfilehash: 6e4699fb2ffadc3aaad73c4032073ff8567c856c
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38006095"
---
# <a name="backup-and-restore-sql-server-databases-on-linux"></a>Linux에서 SQL Server 데이터베이스를 백업 및 복원

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

다른 플랫폼 것과 동일한 도구를 사용 하 여 Linux의 SQL Server 2017에서 데이터베이스의 백업을 수행할 수 있습니다. Linux 서버에서 사용할 수 있습니다 **sqlcmd** SQL Server에 연결 하 여 백업을 수행 합니다. Windows, Linux의 SQL Server에 연결할 수 있으며 사용자 인터페이스를 사용 하 여 백업을 수행할 수 있습니다. 백업 기능을이 플랫폼에서 동일 합니다. 예를 들어, 로컬, 원격 드라이브 또는 데이터베이스 백업할 수 있습니다 [Microsoft Azure Blob 저장소 서비스](../relational-databases/backup-restore/sql-server-backup-to-url.md)합니다.

## <a name="backup-a-database"></a>데이터베이스 백업

다음 예에서 **sqlcmd** 로컬 SQL Server 인스턴스에 연결 하 고 전체 호출 사용자 데이터베이스의 백업 `demodb`합니다.

```bash
sqlcmd -S localhost -U SA -Q "BACKUP DATABASE [demodb] TO DISK = N'/var/opt/mssql/data/demodb.bak' WITH NOFORMAT, NOINIT, NAME = 'demodb-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
```

명령을 실행 하는 경우 SQL Server 암호를 입력 합니다. 암호를 입력 하면 셸에서 백업 진행 상황의 결과 반환 합니다. 예를 들어:

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

데이터베이스가 전체 복구 모델의 경우 더 세분화 된 복원 옵션에 대 한 트랜잭션 로그 백업도 만들 수 있습니다. 다음 예에서 **sqlcmd** 로컬 SQL Server 인스턴스에 연결 하 고 트랜잭션 로그 백업입니다.

```bash
sqlcmd -S localhost -U SA -Q "BACKUP LOG [demodb] TO DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak' WITH NOFORMAT, NOINIT, NAME = N'demodb_LogBackup', NOSKIP, NOREWIND, NOUNLOAD, STATS = 5"
```

## <a name="restore-a-database"></a>데이터베이스 복원

다음 예에서 **sqlcmd** SQL Server의 로컬 인스턴스에 연결 하 고 demodb 데이터베이스를 복원 합니다. `NORECOVERY` 옵션은 로그 파일 백업의 추가 복원에 대 한 허용 하는 데 사용 됩니다. 추가 로그 파일을 복원 하지 않으려는 경우 제거 된 `NORECOVERY` 옵션입니다.

```bash
sqlcmd -S localhost -U SA -Q "RESTORE DATABASE [demodb] FROM DISK = N'/var/opt/mssql/data/demodb.bak' WITH FILE = 1, NOUNLOAD, REPLACE, NORECOVERY, STATS = 5"
```

> [!TIP]
> 하면 실수로 NORECOVERY를 사용 하지만 추가 로그 파일 백업이 없는 경우 명령을 실행 `RESTORE DATABASE demodb` 추가 매개 변수 없이 합니다. 이 복원이 완료 되 고 데이터베이스를 운영 유지 합니다.

### <a name="restore-the-transaction-log"></a>트랜잭션 로그 복원

다음 명령은 이전 트랜잭션 로그 백업을 복원합니다.

```bash
sqlcmd -S localhost -U SA -Q "RESTORE LOG demodb FROM DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak'"
```

## <a name="backup-and-restore-with-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)로 백업 및 복원

Linux 데이터베이스에 연결 하 여 사용자 인터페이스를 통해 백업을 수행 하는 Windows 컴퓨터에서 SSMS를 사용할 수 있습니다.

>[!NOTE] 
> 최신 버전의 SSMS 사용 하 여 SQL Server에 연결 합니다. 다운로드 하 고 최신 버전 설치를 참조 하세요 [SSMS 다운로드](../ssms/download-sql-server-management-studio-ssms.md)합니다. SSMS를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [Linux의 SQL Server 관리를 사용 하 여 SSMS](sql-server-linux-manage-ssms.md)합니다.

다음 단계를 통해 SSMS 사용 하 여 백업을 수행 방법을 설명 합니다. 

1. SSMS를 시작 하 고 Linux의 SQL Server 2017에서 서버에 연결 합니다.

1. 개체 탐색기에서 마우스 오른쪽 단추로 클릭 하면 데이터베이스를 클릭 **태스크**를 클릭 하 고 **백업 하는 중...** .

1. 에 **데이터베이스 백업** 대화 상자에서 매개 변수 및 옵션을 확인 하 고 클릭 **확인**합니다.
 
SQL Server 데이터베이스 백업을 완료 합니다.

### <a name="restore-with-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)를 사용 하 여 복원 

다음 단계를 안내 SSMS 사용 하 여 데이터베이스를 복원 합니다.

1. SSMS에서 마우스 오른쪽 단추로 클릭 **데이터베이스** 를 클릭 하 고 **데이터베이스 복원...** . 

1. 아래 **소스** 클릭 **장치:** 다음 줄임표 (...)를 클릭 합니다.

1. 데이터베이스 백업 파일을 찾아 클릭 **확인**합니다. 

1. 아래 **복원 계획**, 백업 파일 및 설정을 확인 합니다. **확인**을 클릭합니다. 

1. SQL Server 데이터베이스를 복원합니다. 

## <a name="see-also"></a>참고자료

* [전체 데이터베이스 백업 (SQL Server) 만들기](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)
* [트랜잭션 로그 (SQL Server)](../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)
* [BACKUP(Transact-SQL)](../t-sql/statements/backup-transact-sql.md)
* [URL에 대한 SQL Server 백업](../relational-databases/backup-restore/sql-server-backup-to-url.md)
