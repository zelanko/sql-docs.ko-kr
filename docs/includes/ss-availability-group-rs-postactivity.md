
## <a name="add-a-database-to-the-availability-group"></a>가용성 그룹에 데이터베이스 추가

가용성 그룹에 추가하는 데이터베이스는 전체 복구 모드여야 하고 유효한 로그 백업이 있어야 합니다. 데이터베이스가 테스트 데이터베이스이거나 새로 만든 데이터베이스인 경우 데이터베이스 백업을 수행합니다. `db1`이라는 데이터베이스를 만들고 백업하려면 기본 SQL Server 인스턴스에서 다음 Transact-SQL 스크립트를 실행합니다.

```sql
CREATE DATABASE [db1];
ALTER DATABASE [db1] SET RECOVERY FULL;
BACKUP DATABASE [db1]
   TO DISK = N'c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Backup\db1.bak';
```

`db1`이라는 데이터베이스를 `ag1`이라는 가용성 그룹에 추가하려면 기본 SQL Server 복제본에서 다음 Transact-SQL 스크립트를 실행합니다.

```sql
ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [db1];
```

### <a name="verify-that-the-database-is-created-on-the-secondary-servers"></a>데이터베이스가 보조 서버에 생성되었는지 확인

`db1` 데이터베이스가 생성되고 동기화되었는지 확인하려면 각 보조 SQL Server 복제본에서 다음 쿼리를 실행합니다.

```sql
SELECT * FROM sys.databases WHERE name = 'db1';
GO
SELECT DB_NAME(database_id) AS 'database', synchronization_state_desc FROM sys.dm_hadr_database_replica_states;
```
