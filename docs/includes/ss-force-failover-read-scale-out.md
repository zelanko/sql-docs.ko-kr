각 가용성 그룹에는 하나의 주 복제본만 있습니다. 주 복제본은 읽기 및 쓰기를 허용합니다. 복제본은 주를 변경 하려면 조치할 수 있습니다. 고가용성을 위한 가용성 그룹에서 클러스터 관리자는 장애 조치 프로세스를 자동화합니다. 읽기 확장 가용성 그룹에서는 장애 조치 프로세스가 수동입니다. 

두 가지 방법으로 읽기 확장성이 가용성 그룹에서 주 복제본 장애 조치할 수 있습니다.

- 데이터 손실 강제 수동 장애 조치
- 데이터 손실 없이 수동 장애 조치

### <a name="forced-manual-failover-with-data-loss"></a>데이터 손실 강제 수동 장애 조치

주 복제본 사용할 수 없고 복구할 수 없는 경우이 메서드를 사용 합니다. 

데이터 손실 될 수 있는 장애 조치를 강제로 표시 하려면 대상 보조 복제본과 실행을 호스팅하는 SQL Server 인스턴스에 연결:

```SQL
ALTER AVAILABILITY GROUP [ag1] FORCE_FAILOVER_ALLOW_DATA_LOSS;
```

### <a name="manual-failover-without-data-loss"></a>데이터 손실 없이 수동 장애 조치

주 복제본을 사용할 수 있지만 이 구성을 일시적 또는 영구적으로 변경하고 주 복제본을 호스팅하는 SQL Server 인스턴스를 변경해야 하는 경우 이 방법을 사용합니다. 수동 장애 조치를 실행 하기 전에 대상 보조 복제본 잠재적 데이터 손실을 방지 하기 위해 최신 상태 인지 확인 합니다. 

수동으로 장애 조치 데이터 손실 없이:

1. 대상 보조 복제본을 확인 `SYNCHRONOUS_COMMIT`합니다.

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        MODIFY REPLICA ON N'**<node2>*' 
        WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
   ```

2. 활성 트랜잭션이 주 복제본과 동기 보조 복제본이 하나 이상에 커밋됩니다 식별 하려면 다음 쿼리를 실행 합니다. 

   ```SQL
   SELECT ag.name, 
      drs.database_id, 
      drs.group_id, 
      drs.replica_id, 
      drs.synchronization_state_desc, 
      ag.sequence_number
   FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
   WHERE drs.group_id = ag.group_id; 
   ```

   보조 복제본이 `synchronization_state_desc`가 `SYNCHRONIZED`일 때 동기화됩니다.

3. 업데이트 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 1입니다.

   다음 스크립트 집합 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 라는 가용성 그룹에 1로 `ag1`합니다. 다음 스크립트를 실행 하기 전에 대체 `ag1` 가용성 그룹의 이름으로:

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = 1;
   ```

   이 설정은 모든 활성 트랜잭션이 커밋 주 복제본과 동기 보조 복제본이 하나 이상에 되는지 확인 합니다. 

4. 주 복제본을 보조 복제본의 수준을 내립니다. 주 복제본 강등 된 읽기 전용입니다. 이 명령을 실행 하는 역할을 업데이트 하려면 주 복제본을 호스팅하는 SQL Server 인스턴스에서 `SECONDARY`:

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET (ROLE = SECONDARY); 
   ```

5. 대상 보조 복제본을 주 복제본으로 승격합니다. 

   ```SQL
   ALTER AVAILABILITY GROUP ag1 FORCE_FAILOVER_ALLOW_DATA_LOSS; 
   ```  

   > [!NOTE] 
   > 가용성 그룹을 삭제 하려면 사용 [DROP AVAILABILITY GROUP](https://docs.microsoft.com/en-us/sql/t-sql/statements/drop-availability-group-transact-sql)합니다. CLUSTER_TYPE 없음 또는 외부를 사용 하 여 만든 가용성 그룹에 대 한이 명령은 가용성 그룹의 일부가 되는 모든 복제본에서 실행 되어야 합니다.