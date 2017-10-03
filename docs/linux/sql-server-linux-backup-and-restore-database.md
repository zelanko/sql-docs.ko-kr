---
title: "Linux에서 SQL Server 데이터베이스 백업 및 복원 | Microsoft Docs"
description: "Linux에서 SQL Server 데이터베이스 백업 및 복원 하는 방법에 알아봅니다."
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: d30090fb-889f-466e-b793-5f284fccc4e6
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: a34954f14ad4c40fdc7376f3f35c6a3def6e2ec7
ms.contentlocale: ko-kr
ms.lasthandoff: 10/02/2017

---
# <a name="backup-and-restore-sql-server-databases-on-linux"></a>Linux에서 SQL Server 데이터베이스 백업 및 복원

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

다른 플랫폼으로 같은 도구를 사용 SQL Server 2017 linux에서 데이터베이스의 백업을 수행할 수 있습니다. Linux 서버에서 사용할 수 있습니다 `sqlcmd` SQL Server에 연결 하 고 백업을 수행 합니다. Windows에서는 Linux에서 SQL Server에 연결할 수 있으며 사용자 인터페이스와 백업을 수행할 수 있습니다. 백업 기능은 플랫폼에서 동일 합니다. 로컬, 원격 드라이브 또는 데이터베이스를 백업할 수 예를 들어 [Microsoft Azure Blob 저장소 서비스](http://msdn.microsoft.com/library/dn435916.aspx)합니다. 

## <a name="backup-with-sqlcmd"></a>Sqlcmd 사용 하 여 백업

다음 예에서 `sqlcmd` 로컬 SQL Server 인스턴스에 연결 하 고 전체 라는 사용자 데이터베이스의 백업을 가져갑니다 `demodb`합니다.

```bash
sqlcmd -H localhost -U SA -Q "BACKUP DATABASE [demodb] TO DISK = N'var/opt/mssql/data/demodb.bak' WITH NOFORMAT, NOINIT, NAME = 'demodb-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
```

명령을 실행 하면 SQL Server 암호를 입력 합니다. 암호를 입력 한 후 셸 백업 진행률 결과 반환 합니다. 예를 들어

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

### <a name="backup-log-with-sqlcmd"></a>Sqlcmd 사용 하 여 백업 로그

다음 예에서 `sqlcmd` 로컬 SQL Server 인스턴스에 연결 하 고 비상 로그 백업입니다. 비상 로그 백업이 완료 된 후 데이터베이스를 복원 상태로 됩니다. 

```bash
sqlcmd -H localhost -U SA -Q "BACKUP LOG [demodb] TO  DISK = N'var/opt/mssql/data/demodb_LogBackup_2016-11-14_18-09-53.bak' WITH NOFORMAT, NOINIT,  NAME = N'demodb_LogBackup_2016-11-14_18-09-53', NOSKIP, NOREWIND, NOUNLOAD,  NORECOVERY ,  STATS = 5"
```


## <a name="restore-with-sqlcmd"></a>Sqlcmd를 사용 하 여 복원

다음 예에서 `sqlcmd` SQL Server의 로컬 인스턴스에 연결 하 고 데이터베이스를 복원 합니다.

```bash
sqlcmd -H localhost -U SA -Q "RESTORE DATABASE [demodb] FROM  DISK = N'var/opt/mssql/data/demodb.bak' WITH  FILE = 1,  NOUNLOAD,  REPLACE,  STATS = 5"
```

## <a name="backup-and-restore-with-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)를 사용한 백업 및 복원

Linux 데이터베이스에 연결 하 고 사용자 인터페이스를 통해 백업을 수행 하려면 Windows 컴퓨터에서 SSMS를 사용할 수 있습니다. 

>[!NOTE] 
> 최신 버전의 SSMS 사용 하 여 SQL Server에 연결 합니다. 참조를 다운로드 하 여 최신 버전을 설치 하려면 [SSMS 다운로드](http://msdn.microsoft.com/library/mt238290.aspx)합니다. 

다음 단계 SSMS 사용 하 여 백업을 수행 하는 과정을 안내 합니다. 

1. SSMS를 시작 하 고 SQL Server 2017 linux에 서버에 연결 합니다.

1. 개체 탐색기에서 마우스 오른쪽 단추로 클릭 하면 데이터베이스를 클릭 **작업**, 클릭 하 고 **백업...** .

1. 에 **데이터베이스 백업** 대화 상자에서 매개 변수 및 옵션을 확인 하 고 클릭 **확인**합니다.
 
SQL Server 데이터베이스 백업을 완료합니다.

자세한 내용은 참조 [Linux에서 SQL Server 관리를 사용 하 여 SSMS](sql-server-linux-manage-ssms.md)합니다.

### <a name="restore-with-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)를 사용 하 여 복원 

다음 단계 과정을 단계별로 SSMS 사용 하 여 데이터베이스를 복원 합니다.

1. SSMS에서 마우스 오른쪽 단추로 클릭 **데이터베이스** 클릭 **데이터베이스 복원...** . 

1. 아래 **소스** 클릭 **장치:** 한 다음 줄임표 (...)를 클릭 합니다.

1. 데이터베이스 백업 파일을 찾아 클릭 **확인**합니다. 

1. 아래 **복원 계획**, 백업 파일 및 설정을 확인 합니다. **확인**을 클릭합니다. 

1. SQL Server 데이터베이스를 복원합니다. 

## <a name="see-also"></a>참고 항목

* [전체 데이터베이스 백업 (SQL Server) 만들기](http://msdn.microsoft.com/library/ms187510.aspx)
* [트랜잭션 로그 (SQL Server)를 백업](http://msdn.microsoft.com/library/ms179478.aspx)
* [BACKUP(Transact-SQL)](http://msdn.microsoft.com/library/ms186865.aspx)
* [URL에 대한 SQL Server 백업](http://msdn.microsoft.com/library/dn435916.aspx)

