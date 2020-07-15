---
title: 데이터베이스의 증분 복원 - 메모리 최적화 테이블
description: 메모리 최적화 테이블이 있는 데이터베이스는 SQL Server에서 증분 복원을 지원합니다. 증분 백업 및 복원 관련 주요 시나리오에 대해 알아보세요.
ms.custom: seo-dt-2019
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 732c9721-8dd4-481d-8ff9-1feaaa63f84f
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7d484e919fca78b3b77546f659ed198cdea7ab1b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85722401"
---
# <a name="piecemeal-restore-of-databases-with-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블이 있는 데이터베이스의 증분 복원

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  증분 복원은 아래에 설명된 한 가지 제한 사항을 제외하고 메모리 최적화 테이블이 있는 데이터베이스에서 지원됩니다. 증분 백업 및 복원에 대한 자세한 내용은 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md) 및 [증분 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)을 참조하세요.  
  
 메모리 최적화 파일 그룹은 주 파일 그룹과 함께 백업하고 복원해야 합니다.  
  
-   주 파일 그룹을 백업(또는 복원)하는 경우 메모리 최적화 파일 그룹을 지정해야 합니다.  
  
-   메모리 최적화 파일 그룹을 백업(또는 복원)하는 경우 주 파일 그룹을 지정해야 합니다.  
  
 증분 백업 및 복원에 대한 주요 시나리오는 다음과 같습니다.  
  
-   증분 백업을 사용하면 백업 크기를 줄일 수 있습니다. 몇 가지 예는 다음과 같습니다.  
  
    -   작업에 미치는 영향을 최소화하기 위해 데이터베이스 백업이 몇 차례에 걸쳐 서로 다른 시간이나 서로 다른 날에 수행되도록 구성합니다. 한 가지 예는 전체 데이터베이스 백업을 데이터베이스 유지 관리에 할당된 시간 안에 완료할 수 없을 정도로 매우 큰 데이터베이스(1TB 이상)입니다. 이 경우 증분 백업을 사용하여 전체 데이터베이스를 여러 증분 백업에서 백업할 수 있습니다.  
  
    -   파일 그룹이 읽기 전용으로 표시된 경우 읽기 전용으로 표시된 후에는 트랜잭션 로그 백업이 필요하지 않습니다. 읽기 전용으로 표시한 후에 한 번만 파일 그룹을 백업하도록 선택할 수 있습니다.  
  
-   증분 복원  
  
    -   증분 복원의 목표는 모든 데이터를 기다리지 않고 데이터베이스의 중요한 부분을 온라인 상태로 만드는 것입니다. 한 가지 예는 데이터베이스에 분할된 데이터가 있고 이전 파티션이 드물게만 사용되는 경우입니다. 필요한 경우에만 이전 파티션을 복원할 수 있습니다. 기록 데이터 등을 포함하는 파일 그룹의 경우에도 이와 유사합니다.  
  
    -   페이지 복구를 사용하면 페이지를 특정하게 복원하여 페이지 손상을 수정할 수 있습니다. 자세한 내용은 [페이지 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)을 참조하세요.  
  
## <a name="samples"></a>샘플  
 다음 예에서는 아래의 스키마를 사용합니다.  
  
```sql
CREATE DATABASE imoltp
    ON PRIMARY (
        name = imoltp_primary1,
        filename = 'c:\data\imoltp_data1.mdf')
    LOG ON (
        name = imoltp_log,
        filename = 'c:\data\imoltp_log.ldf');
    GO  
  
ALTER DATABASE imoltp
    ADD FILE (
        name = imoltp_primary2,
        filename = 'c:\data\imoltp_data2.ndf');
GO  
  
ALTER DATABASE imoltp
    ADD FILEGROUP imoltp_secondary;

ALTER DATABASE imoltp
    ADD FILE (
        name = imoltp_secondary,
        filename = 'c:\data\imoltp_secondary.ndf')
            TO FILEGROUP imoltp_secondary;
GO  
  
ALTER DATABASE imoltp
    ADD FILEGROUP imoltp_mod
    CONTAINS MEMORY_OPTIMIZED_DATA;

ALTER DATABASE imoltp
    ADD FILE (
        name = 'imoltp_mod1',
        filename = 'c:\data\imoltp_mod1')
            TO FILEGROUP imoltp_mod;

ALTER DATABASE imoltp
    ADD FILE (
        name = 'imoltp_mod2',
        filename = 'c:\data\imoltp_mod2')
            TO FILEGROUP imoltp_mod;
GO  
```  
  
### <a name="backup"></a>Backup  
 이 샘플에서는 주 파일 그룹과 메모리 최적화 파일 그룹을 백업하는 방법을 보여 줍니다. 주 파일 그룹과 메모리 최적화 파일 그룹을 함께 지정해야 합니다.  
  
```sql
BACKUP database imoltp
    filegroup = 'primary',
    filegroup = 'imoltp_mod'
    to disk = 'c:\data\imoltp.dmp'
    with init;
```
  
 다음 샘플에서는 주 파일 그룹과 메모리 최적화 파일 그룹을 제외한 파일 그룹의 백업이 메모리 최적화 테이블이 없는 데이터베이스와 유사하게 작동되는 것을 보여 줍니다. 다음 명령은 보조 파일 그룹을 백업합니다.  
  
```sql
BACKUP database imoltp
    filegroup = 'imoltp_secondary'
    to disk = 'c:\data\imoltp_secondary.dmp'
    with init;
```
  
### <a name="restore"></a>복원  
 다음 예제에서는 주 파일 그룹과 메모리 최적화 파일 그룹을 함께 복원하는 방법을 보여 줍니다.  

```sql
RESTORE database imoltp
    filegroup = 'primary',
    filegroup = 'imoltp_mod'
    from disk = 'c:\data\imoltp.dmp'
    with
        partial,
        norecovery;

-- Restore the transaction log.

RESTORE LOG [imoltp]
    FROM DISK = N'c:\data\imoltp_log.dmp'
    WITH
        FILE = 1,
        NOUNLOAD,
        STATS = 10;
GO
```
  
 다음 예제에서는 주 파일 그룹과 메모리 최적화 파일 그룹을 제외한 파일 그룹의 복원이 메모리 최적화 테이블이 없는 데이터베이스와 유사하게 수행되는 것을 보여 줍니다.  
  
```sql
RESTORE DATABASE [imoltp]
    FILE = N'imoltp_secondary'
    FROM DISK = N'c:\data\imoltp_secondary.dmp'
    WITH
        FILE = 1,
        RECOVERY,
        NOUNLOAD,
        STATS = 10;
GO
```

## <a name="see-also"></a>참고 항목  
 [메모리 액세스에 최적화된 테이블의 백업, 복원 및 복구](https://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)  

