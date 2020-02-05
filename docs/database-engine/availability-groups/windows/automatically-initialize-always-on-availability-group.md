---
title: 자동 시드를 사용하여 가용성 그룹 초기화
description: 수동으로 백업 및 복원하지 않고도 자동 시드를 사용하여 Always On 가용성 그룹의 모든 데이터베이스에 대한 보조 복제본을 자동으로 만듭니다.
ms.custom: seo-lt-2019
ms.date: 03/26/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 67c6a601-677a-402b-b3d1-8c65494e9e96
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 38bbab7ea9ae6aa7ddd70ede2161988c01431573
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75254087"
---
# <a name="use-automatic-seeding-to-initialize-an-always-on-availability-group"></a>자동 시드를 사용하여 Always On 가용성 그룹 초기화
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 2016에서는 가용성 그룹의 자동 시드를 도입했습니다. 자동 시드를 사용하여 가용성 그룹을 만들면 SQL Server가 그룹의 모든 데이터베이스에 대해 보조 복제본을 자동으로 만듭니다. 더 이상 보조 복제본을 수동으로 백업 및 복원할 필요가 없습니다. 자동 시드를 사용하려면 T-SQL로 가용성 그룹을 만들거나 SQL Server Management Studio의 최신 버전을 사용하세요.

자세한 내용은 [보조 복제본에 대한 자동 시드](automatic-seeding-secondary-replicas.md)를 참조하세요.
 
## <a name="prerequisites"></a>사전 요구 사항

SQL Server 2016에서 자동 시드를 사용하려면 데이터 및 로그 파일 경로가 가용성 그룹에 참여하는 모든 SQL Server 인스턴스에서 동일해야 합니다. SQL Server 2017에서는 다른 경로를 사용할 수 있지만 모든 복제본이 하나의 플랫폼에 호스트된 경우에는 동일한 경로를 사용하는 것이 좋습니다. 복제본에 대한 플랫폼 간 가용성 그룹의 경로는 모두 다릅니다. 자세한 내용은 [디스크 레이아웃](automatic-seeding-secondary-replicas.md#disklayout)을 참조하세요.

가용성 그룹 시드는 데이터베이스 미러링 엔드포인트를 통해 통신합니다. 각 서버에서 미러링 엔드포인트 포트에 대해 인바운드 방화벽 규칙을 엽니다.

가용성 그룹의 데이터베이스가 전체 복구 모델에 포함되어야 합니다. 데이터베이스에 현재 전체 백업 및 트랜잭션 로그 백업이 있어야 합니다. 이러한 백업 파일은 자동 시드에 사용되지 않지만 가용성 그룹에 데이터베이스를 포함하기 전에 필요합니다. 
 
## <a name="create-availability-group-with-automatic-seeding"></a>자동 시드를 사용하여 가용성 그룹 만들기

자동 시드를 사용하여 가용성 그룹을 만들려면 `SEEDING_MODE=AUTOMATIC`을 설정합니다. 

다음 예제에서는 두 개의 노드 Windows Server 장애 조치(failover) 클러스터에 가용성 그룹을 만듭니다. 스크립트를 실행하기 전에 사용자 환경에 대한 값을 업데이트합니다.

1. 엔드포인트를 만듭니다. 각 서버에는 엔드포인트가 필요합니다. 다음 스크립트는 수신기에 대해 TCP 포트 5022를 사용하는 엔드포인트를 만듭니다. `<endpoint_name>` 및 `LISTENER_PORT` 를 사용자 환경에 맞게 설정하고 양쪽 서버 모두에서 스크립트를 실행합니다.

    ```sql
    CREATE ENDPOINT [<endpoint_name>] 
        STATE=STARTED
        AS TCP (LISTENER_PORT = 5022, LISTENER_IP = ALL)
        FOR DATA_MIRRORING (
            ROLE = ALL, 
            AUTHENTICATION = WINDOWS NEGOTIATE, 
            ENCRYPTION = REQUIRED ALGORITHM AES
            )
    GO
    ```

1. 가용성 그룹을 만듭니다. 다음 스크립트는 가용성 그룹을 만듭니다. 그룹 이름, 서버 이름 및 도메인 이름에 대한 꺾쇠 괄호(`<>`) 안의 값을 업데이트하고 SQL Server의 기본 인스턴스에서 실행합니다.  

    ```sql
    CREATE AVAILABILITY GROUP [<availability_group_name>]
        FOR DATABASE db1
        REPLICA ON'<*primary_server*>'
        WITH (ENDPOINT_URL = N'TCP://<primary_server>.<fully_qualified_domain_name>:5022', 
            FAILOVER_MODE = AUTOMATIC, 
            AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
            BACKUP_PRIORITY = 50, 
            SECONDARY_ROLE(ALLOW_CONNECTIONS = NO), 
            SEEDING_MODE = AUTOMATIC),
        N'<secondary_server>' WITH (ENDPOINT_URL = N'TCP://<secondary_server>.<fully_qualified_domain_name>:5022', 
            FAILOVER_MODE = AUTOMATIC, 
            AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
            BACKUP_PRIORITY = 50, 
            SECONDARY_ROLE(ALLOW_CONNECTIONS = NO), 
            SEEDING_MODE = AUTOMATIC);
    GO
    ``` 

1. 가용성 그룹에 보조 서버 인스턴스를 조인하고 데이터베이스를 만들 수 있는 권한을 가용성 그룹에 부여합니다. 다음 스크립트를 업데이트하고 꺾쇠 괄호(`<>`) 안의 값을 환경에 맞게 바꾼 다음 SQL Server의 보조 복제본 인스턴스에서 실행합니다. 
 
    ```sql
    ALTER AVAILABILITY GROUP [<availability_group_name>] JOIN
    GO  
    ALTER AVAILABILITY GROUP [<availability_group_name>] GRANT CREATE ANY DATABASE
    GO
    ```

SQL Server는 보조 서버에서 데이터베이스 복제본을 자동으로 만듭니다. 데이터베이스가 큰 경우 데이터베이스 동기화를 완료하는 데 다소 시간이 걸릴 수 있습니다. 데이터베이스가 자동 시드를 사용하도록 구성된 가용성 그룹에 포함된 경우 `sys.dm_hadr_automatic_seeding` 시스템 뷰를 쿼리하여 시드 프로세스를 모니터링할 수 있습니다. 다음 쿼리는 가용성 그룹에서 자동 시드를 사용하도록 구성된 모든 데이터베이스에 대해 하나의 행을 반환합니다.

```sql 
SELECT start_time,
    ag.name,
    db.database_name,
    current_state,
    performed_seeding,
    failure_state,
    failure_state_desc
FROM sys.dm_hadr_automatic_seeding autos 
    JOIN sys.availability_databases_cluster db 
        ON autos.ag_db_id = db.group_database_id
    JOIN sys.availability_groups ag 
        ON autos.ag_id = ag.group_id
```

## <a name="prevent-automatic-seeding-after-an-availability-group"></a>가용성 그룹 후 자동 시드 방지

주 복제본에서 보조 복제본으로 더 많은 데이터베이스가 시드되는 것을 일시적으로 방지하려면 가용성 그룹의 데이터베이스 만들기 권한을 거부합니다. 가용성 그룹의 복제 데이터베이스 만들기 권한을 거부하려면 보조 복제본을 호스트하는 인스턴스에서 다음 쿼리를 실행합니다.

```sql
ALTER AVAILABILITY GROUP [<availability_group_name>] 
    DENY CREATE ANY DATABASE
GO
```


## <a name="enable-automatic-seeding-on-an-existing-availability-group"></a>기존 가용성 그룹에서 자동 시드를 사용하도록 설정

기존 데이터베이스에서 자동 시드를 설정할 수 있습니다. 다음 명령은 자동 시드를 사용하도록 가용성 그룹을 변경합니다. 주 복제본에서 다음 명령을 실행합니다.

```sql
ALTER AVAILABILITY GROUP [<availability_group_name>] 
    MODIFY REPLICA ON '<secondary_node>' 
    WITH (SEEDING_MODE = AUTOMATIC)
GO
```

필요한 경우 이전 명령은 데이터베이스를 강제로 실행하여 시드를 다시 시작합니다. 예를 들어 보조 복제본에 디스크 공간이 부족하여 시드가 실패한 경우 사용 가능한 공간을 추가한 후 `ALTER AVAILABILITY GROUP ... WITH (SEEDING_MODE=AUTOMATIC)` 명령을 실행하여 시드를 다시 시작할 수 있습니다.

## <a name="stop-automatic-seeding"></a>자동 시드 중지

가용성 그룹에 대한 자동 시드를 중지하려면 주 복제본에서 다음 스크립트를 실행합니다.

```sql
ALTER AVAILABILITY GROUP [<availability_group_name>] 
    MODIFY REPLICA ON '<secondary_node>'   
    WITH (SEEDING_MODE = MANUAL)
GO
```

이전 스크립트는 현재 시드 중인 모든 복제본을 취소하고 SQL Server에서 이 가용성 그룹의 복제본을 자동으로 초기화하는 것을 방지합니다. 이미 초기화된 모든 복제본에 대한 동기화는 중지되지 않습니다. 


## <a name="monitor-automatic-seeding-availability-group"></a>자동 시드 가용성 그룹 만들기

### <a name="use-system-dynamic-management-views-to-monitor-seeding"></a>시스템 동적 관리 뷰를 사용하여 시드 모니터링

다음 시스템 뷰에는 SQL Server 자동 시드의 상태가 표시됩니다.

**sys.dm_hadr_automatic_seeding** 

주 복제본에서 `sys.dm_hadr_automatic_seeding` 을 쿼리하여 자동 시드 프로세스의 상태를 확인합니다. 뷰는 각 시드 프로세스당 한 행을 반환합니다. 다음은 그 예입니다.

```sql
SELECT start_time, 
    completion_time
    is_source,
    current_state,
    failure_state,
    failure_state_desc
FROM sys.dm_hadr_automatic_seeding
```
 
**sys.dm_hadr_physical_seeding_stats** 

주 복제본에서 `sys.dm_hadr_physical_seeding_stats` DMV를 쿼리하여 현재 실행 중인 각 시드 프로세스에 대한 물리적 통계를 볼 수 있습니다. 다음 쿼리는 시드가 실행 중일 때 행을 반환합니다.

```sql
SELECT * FROM sys.dm_hadr_physical_seeding_stats;
```

두 열 *total_disk_io_wait_time_ms* 및 *total_network_wait_time_ms*는 자동 시드 프로세스에서 성능 병목 상태를 확인하는 데 사용할 수 있습니다. 또한 두 열은 확장된 이벤트 *hadr_physical_seeding_progress*에 존재합니다.

**total_disk_io_wait_time_ms**는 디스크에서 대기하는 동안 백업/복원 스레드에서 소요된 시간을 나타냅니다. 이 값은 시드 작업이 시작된 이후 누적됩니다. 디스크가 백업 스트림을 읽거나 쓰는 데 준비되지 않은 경우 백업/복원 스레드가 절전 상태로 전환되고 디스크가 준비되었는지 확인하기 위해 1초 간격으로 다시 시작합니다.
        
**total_network_wait_time_ms**는 주 복제본과 보조 복제본에 대해 다르게 해석됩니다. 주 복제본에서 이 카운터는 네트워크 흐름 제어 시간을 나타냅니다. 보조 복제본에서는 메시지가 디스크를 쓸 수 있을 때까지 복원 스레드가 대기하는 시간을 나타냅니다.

### <a name="diagnose-database-initialization-using-automatic-seeding-in-the-error-log"></a>오류 로그에서 자동 시드를 사용 중인 데이터베이스 초기화 진단

자동 시드를 위해 구성된 가용성 그룹에 데이터베이스를 추가하는 경우 SQL Server는 가용성 그룹 엔드포인트를 통해 VDI 백업을 수행합니다. 백업이 완료되고 보조 복제본이 동기화된 경우 SQL Server 오류 로그에서 정보를 검토합니다.

### <a name="diagnose-database-level-health-with-extended-events"></a>확장 이벤트를 사용하여 데이터베이스 수준 상태 진단

자동 시드에는 초기화 중 상태 변경, 오류 및 성능 통계를 추적하기 위한 새로운 확장 이벤트가 있습니다. 

예를 들어 이 스크립트는 자동 시드와 관련된 이벤트를 캡처하는 확장 이벤트 세션을 만듭니다. 

```sql
CREATE EVENT SESSION [AlwaysOn_autoseed] ON SERVER 
    ADD EVENT sqlserver.hadr_automatic_seeding_state_transition,
    ADD EVENT sqlserver.hadr_automatic_seeding_timeout,
    ADD EVENT sqlserver.hadr_db_manager_seeding_request_msg,
    ADD EVENT sqlserver.hadr_physical_seeding_backup_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_failure,
    ADD EVENT sqlserver.hadr_physical_seeding_forwarder_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_forwarder_target_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_progress,
    ADD EVENT sqlserver.hadr_physical_seeding_restore_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_submit_callback
    ADD TARGET package0.event_file(
        SET filename=N'autoseed.xel',
            max_file_size=(5),
            max_rollover_files=(4)
        )
WITH (
    MAX_MEMORY=4096 KB,
    EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,
    MAX_DISPATCH_LATENCY=30 SECONDS,
    MAX_EVENT_SIZE=0 KB,
    MEMORY_PARTITION_MODE=NONE,
    TRACK_CAUSALITY=OFF,
    STARTUP_STATE=ON
    )
GO 

ALTER EVENT SESSION AlwaysOn_autoseed ON SERVER STATE=START
GO 
```


다음 표에는 자동 시드와 관련된 확장 이벤트가 나열되어 있습니다. 

| 속성 | Description|
|------------ |---------------| 
|hadr_db_manager_seeding_request_msg |  시드 요청 메시지입니다.
|hadr_physical_seeding_backup_state_change |    물리적 시드 백업 관련 상태 변경입니다.
|hadr_physical_seeding_restore_state_change |물리적 시드 복원 관련 상태 변경입니다.
|hadr_physical_seeding_forwarder_state_change | 물리적 시드 전달자 관련 상태 변경입니다.
|hadr_physical_seeding_forwarder_target_state_change |  물리적 시드 전달자 대상 관련 상태 변경입니다.
|hadr_physical_seeding_submit_callback  |물리적 시드 전송 콜백 이벤트입니다.
|hadr_physical_seeding_failure  |물리적 시드 실패 이벤트입니다.
|hadr_physical_seeding_progress |   물리적 시드 진행 이벤트입니다.
|hadr_physical_seeding_schedule_long_task_failure   |물리적 시드 일정 장기 작업 오류 이벤트입니다.
|hadr_automatic_seeding_start   |자동 시드 작업이 제출될 때 발생합니다.
|hadr_automatic_seeding_state_transition    |자동 시드 작업 상태가 변경될 때 발생합니다.
|hadr_automatic_seeding_success |자동 시드 작업이 성공할 때 발생합니다.
|hadr_automatic_seeding_failure |자동 시드 작업이 실패할 때 발생합니다.
|hadr_automatic_seeding_timeout |자동 시드 작업 시간이 초과할 때 발생합니다.

### <a name="other-troubleshooting-considerations"></a>다른 문제 해결 고려 사항

**자동 시드 중 모니터링**

현재 실행 중인 자동 시드 프로세스를 위해 `sys.dm_hadr_physical_seeding_stats` 를 쿼리합니다. 뷰는 각 데이터베이스에 대해 하나의 행을 반환합니다. 다음은 그 예입니다.

```sql
SELECT local_database_name, 
    role_desc, 
    internal_state_desc, 
    transfer_rate_bytes_per_second, 
    transferred_size_bytes, 
    database_size_bytes, 
    start_time_utc, 
    end_time_utc, estimate_time_complete_utc, 
    total_disk_io_wait_time_ms, 
    total_network_wait_time_ms, 
    is_compression_enabled 
FROM sys.dm_hadr_physical_seeding_stats
```

**자동 시드하도록 구성된 가용성 그룹에 데이터베이스가 표시되지 않는 문제 해결**


자동 시드를 사용하도록 설정된 가용성 그룹에 데이터베이스가 나타나지 않는 경우 자동 시드가 실패할 수 있습니다. 이 경우 주 복제본 및 보조 복제본의 가용성 그룹에 데이터베이스를 추가할 수 없습니다. 주 복제본과 보조 복제본에서 `sys.dm_hadr_automatic_seeding` 을 쿼리하세요. 예를 들어 다음 쿼리를 실행하여 자동 시드의 실패 상태를 확인합니다.

```sql
SELECT start_time, 
    completion_time, 
    is_source, 
    current_state, 
    failure_state, 
    failure_state_desc, 
    error_code 
FROM sys.dm_hadr_automatic_seeding
```

## <a name="automatic-seeding-and-performance-considerations"></a>자동 시드 및 성능 고려 사항

SQL Server는 자동 시드를 위해 고정 개수의 스레드를 사용합니다. 주 인스턴스에서 SQL Server는 LUN당 하나의 스레드를 사용하여 변경 내용을 읽습니다. 보조 인스턴스에서 SQL Server는 LUN당 하나의 스레드를 사용하여 데이터베이스를 초기화합니다.

자동 시드 중 주 복제본의 추적 플래그 9567을 설정하여 데이터 스트림 압축을 사용하도록 설정합니다. 이렇게 하면 자동 시드의 전송 시간이 크게 줄어들지만 CPU 사용량은 늘어납니다. 자세한 내용은 [가용성 그룹에 대한 압축 조정](../../../database-engine/availability-groups/windows/tune-compression-for-availability-group.md)을 참조하세요. 


## <a name="when-not-to-use-automatic-seeding"></a>자동 시드를 사용하지 않는 경우

일부 시나리오에서는 보조 복제본을 초기화하는 데 자동 시드가 적합하지 않을 수 있습니다. SQL Server는 자동 시드 중 초기화를 위해 네트워크를 통한 백업을 수행합니다. 데이터베이스가 매우 크거나 보조 복제본이 원격인 경우 이 프로세스가 느려질 수 있습니다. 백업 프로세스 중에는 이러한 데이터베이스에 대한 트랜잭션 로그를 자를 수 없으므로 데이터베이스의 초기화 프로세스가 오래 지속되면 트랜잭션 로그 크기가 크게 증가할 수 있습니다.
자동 시드를 사용하는 가용성 그룹에 데이터베이스를 추가하기 전에 데이터베이스 크기, 부하 및 복제본 간의 사이트 거리를 평가합니다.

## <a name="resources"></a>리소스

[CREATE AVAILABILITY GROUP(Transact-SQL)](../../../t-sql/statements/create-availability-group-transact-sql.md)

[AlwaysOn Availability Groups Troubleshooting and Monitoring Guide](https://technet.microsoft.com/library/dn135328.aspx)

