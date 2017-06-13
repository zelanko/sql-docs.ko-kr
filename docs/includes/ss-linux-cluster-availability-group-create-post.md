
## <a name="add-a-database-to-the-availability-group"></a>가용성 그룹에 데이터베이스 추가

가용성 그룹에 추가 하는 데이터베이스는 전체 복구 모드에 있고 유효한 로그 백업을 확인 합니다. 데이터베이스 백업을 수행 하는 테스트 데이터베이스 또는 새 데이터베이스를 만들지 인 경우. 주 SQL Server에서 만들고 라는 데이터베이스를 백업 하려면 다음 TRANSACT-SQL 실행 `db1`합니다.

```Transact-SQL
CREATE DATABASE [db1];
ALTER DATABASE [db1] SET RECOVERY FULL;
BACKUP DATABASE [db1] 
   TO DISK = N'var/opt/mssql/data/db1.bak';
```

기본 SQL Server 복제 데이터베이스 라는 데이터베이스를 추가 하려면 다음 TRANSACT-SQL 실행 `db1` 라는 가용성 그룹에 `ag1`합니다.

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [db1];
```

### <a name="verify-that-the-database-is-created-on-the-secondary-servers"></a>보조 서버에서 데이터베이스 생성 되었는지 확인

SQL Server 각 보조 복제본에서 있는지 다음 쿼리를 실행 된 `db1` 데이터베이스를 만들고 동기화 됩니다.

```Transact-SQL
SELECT * FROM sys.databases WHERE name = 'db1';
GO
SELECT DB_NAME(database_id) AS 'database', synchronization_state_desc FROM sys.dm_hadr_database_replica_states;
```
