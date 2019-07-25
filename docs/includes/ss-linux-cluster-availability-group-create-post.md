---
ms.openlocfilehash: 0cdc343bf4ea6866d1a55672187451a3b6d95ec1
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68215585"
---

## <a name="add-a-database-to-the-availability-group"></a>가용성 그룹에 데이터베이스 추가

가용성 그룹에 추가하는 데이터베이스는 전체 복구 모드여야 하고 유효한 로그 백업이 있어야 합니다. 테스트 데이터베이스이거나 새로 만든 데이터베이스인 경우 데이터베이스 백업을 수행합니다. 기본 SQL Server에서 다음 Transact-SQL 스크립트를 실행하여 `db1`이라는 데이터베이스를 만들고 백업합니다.

```sql
CREATE DATABASE [db1];
ALTER DATABASE [db1] SET RECOVERY FULL;
BACKUP DATABASE [db1] 
   TO DISK = N'/var/opt/mssql/data/db1.bak';
```

기본 SQL Server 복제본에서 다음 Transact-SQL 스크립트를 실행하여 `db1` 데이터베이스를 가용성 그룹 `ag1`에 추가합니다.

```sql
ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [db1];
```

### <a name="verify-that-the-database-is-created-on-the-secondary-servers"></a>데이터베이스가 보조 서버에 생성되었는지 확인

각 보조 SQL Server 복제본에서 다음 쿼리를 실행하여 `db1` 데이터베이스가 생성되고 동기화되었는지 확인합니다.

```sql
SELECT * FROM sys.databases WHERE name = 'db1';
GO
SELECT DB_NAME(database_id) AS 'database', synchronization_state_desc FROM sys.dm_hadr_database_replica_states;
```
