---
title: 보조 복제본에 대한 자동 시드
description: 자동 시드를 사용하여 SQL 2016 이상의 Always On 가용성 그룹의 일부로 보조 복제본을 초기화하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 11/27/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
helpviewer_keywords:
- Automatic seeding [SQL Server], secondary replica
ms.assetid: ''
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 67d111336f6ce2d674e4ac4f6aa31f62878718a2
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91114663"
---
# <a name="use-automatic-seeding-to-initialize-a-secondary-replica-for-an-always-on-availability-group"></a>자동 시드를 사용하여 Always On 가용성 그룹의 보조 복제본을 초기화합니다.
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

SQL Server 2012 및 2014에서 SQL Server Always On 가용성 그룹의 보조 복제본을 초기화하는 유일한 방법은 백업, 복사 및 복원을 사용하는 것입니다. SQL Server 2016에서는 보조 복제본을 초기화하는 *자동 시드* 기능을 새로 도입했습니다. 자동 시드는 VDI를 사용하여 구성된 엔드포인트를 사용하는 가용성 그룹의 각 데이터베이스에 대한 보조 복제본으로 백업을 스트리밍하기 위해 로그 스트림 전송을 사용합니다. 새로운 이 기능은 가용성 그룹을 처음 만드는 중에 또는 데이터베이스를 추가할 때 사용할 수 있습니다. 자동 시드는 Always On 가용성 그룹을 지원하는 모든 버전의 SQL Server에 포함되어 있으며, 기존 가용성 그룹과 [분산 가용성 그룹](distributed-availability-groups.md) 모두에서 사용할 수 있습니다.

## <a name="security"></a>보안

보안 권한은 초기화되는 복제 유형에 따라 다릅니다.

* 기존 가용성 그룹의 경우 보조 복제본이 가용성 그룹에 가입될 때 해당 보조 복제본의 가용성 그룹에 권한을 부여해야 합니다. Transact SQL에서 `ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE` 명령을 사용합니다.
* 만들고 있는 복제본의 데이터베이스가 두 번째 가용성 그룹의 주 복제본에 있는 분산 가용성 그룹의 경우 이미 주 복제본이므로 추가 권한이 필요하지 않습니다.
* 분산 가용성 그룹의 두 번째 가용성 그룹에 있는 보조 복제본의 경우 `ALTER AVAILABILITY GROUP [<2ndAGName>] GRANT CREATE ANY DATABASE` 명령을 사용해야 합니다. 이 보조 복제본은 두 번째 가용성 그룹의 주 복제본에서 시드됩니다.

## <a name="performance-and-transaction-log-impact-on-the-primary-replica"></a>주 복제본에 대한 성능 및 트랜잭션 로그 영향

자동 시드는 데이터베이스 크기, 네트워크 속도 및 주 복제본과 보조 복제본 간의 거리에 따라 보조 복제본을 초기화하는 데 적합하지 않을 수도 있습니다. 예를 들어 다음과 같은 조건이 있습니다.

* 데이터베이스 크기는 5TB입니다.
* 네트워크 속도는 1Gb/초입니다.
* 두 사이트 간의 거리는 1,600Km입니다.

전체 대역폭을 사용할 수 있는 경우 1GB/초의 네트워크에서는 125MB/초의 지속적인 처리량을 제공합니다. 이 예의 경우 자동 시드는 11시간 정도 걸릴 것입니다. 거리가 멀수록 네트워크 신호가 약해지고 링크가 네트워크의 다른 리소스와 공유되기 때문에 자동 시드 프로세스는 실제로 느립니다. 시드하는 동안 주 복제본에 있는 데이터베이스의 트랜잭션 로그는 계속 증가하며, 해당 데이터베이스의 자동 시드를 완료할 때까지 잘릴 수 없습니다.  그런 다음 트랜잭션 로그 백업을 사용하여 트랜잭션 로그를 자를 수 있습니다.

자동 시드는 최대 5개의 데이터베이스를 처리할 수 있는 단일 스레드 프로세스입니다. 특히 가용성 그룹에 둘 이상의 데이터베이스가 있는 경우 단일 스레딩이 성능에 영향을 미칠 수 있습니다.

압축은 자동 시드에 사용할 수 있지만 기본적으로 사용되지 않습니다. 압축을 사용하면 네트워크 대역폭을 줄이고 프로세스 속도를 높이지만 추가적인 프로세서 오버헤드가 있습니다. 자동 시드 중에 압축을 사용하려면 9567 추적 플래그를 사용하도록 설정합니다([가용성 그룹에 대한 압축 성능 조정](tune-compression-for-availability-group.md) 참조).

## <a name="disk-layout"></a><a name = "disklayout"></a> 디스크 레이아웃

SQL Server 2016 및 이전 버전에서 자동 시드로 데이터베이스가 만들어진 폴더는 이미 존재해야 하며 주 복제본의 경로와 동일해야 합니다. 

SQL Server 2017에서는 가용성 그룹에 참여하는 모든 복제본에서 동일한 데이터 및 로그 파일 경로를 사용하는 것이 좋지만 필요한 경우 다른 데이터 및 경로를 사용할 수 있습니다. 예를 들어 플랫폼 간 가용성 그룹에서 SQL Server의 인스턴트 하나는 Windows에 있고 다른 하나는 Linux에 있는 경우가 있습니다. 서로 다른 플랫폼의 기본 경로는 모두 다릅니다. SQL Server 2017은 기본 경로가 다른 SQL Server의 인스턴스에서 가용성 그룹 복제본을 지원합니다.

다음 표는 자동 시드를 지원할 수 있는 지원되는 데이터 디스크 레이아웃의 예를 보여줍니다.

|주 인스턴스</br>기본 데이터 경로|보조 인스턴스</br>기본 데이터 경로|주 인스턴스</br>원본 파일 위치|보조 인스턴스</br> 대상 파일 위치
|:------|:------|:------|:------
|c:\\data\\ |/var/opt/mssql/data/ |c:\\data\\ |/var/opt/mssql/data/|
|c:\\data\\ |/var/opt/mssql/data/ |c:\\data\\group1\\ |/var/opt/mssql/data/group1/|
|c:\\data\\ |d:\\data\\ |c:\\data\\ |d:\\data\\
|c:\\data\\ |d:\\data\\ |c:\\data\\group1\\ |d:\\data\\group1\

주 및 보조 복제본 데이터 위치가 인스턴스 기본 경로가 아닌 시나리오는 이 변경 사항에 영향을 받지 않습니다. 보조 복제본 파일 경로가 주 복제본 파일 경로와 일치하기 위한 요구 사항은 동일합니다.

|주 인스턴스</br>기본 데이터 경로|보조 인스턴스</br>기본 데이터 경로|주 인스턴스</br>파일 위치|보조 인스턴스</br> 파일 위치
|:------|:------|:------|:------
|c:\\data\\ |c:\\data\\ |d:\\group1\\ |d:\\group1\\
|c:\\data\\ |c:\\data\\ |d:\\data\\ |d:\\data\\
|c:\\data\\ |c:\\data\\ |d:\\data\\group1\\ |d:\\data\\group1\\

주 및 보조 복제본에서 기본 경로와 기본이 아닌 경로가 혼합된 경우 SQL Server 2017은 이전 릴리스와 다르게 작동합니다. 다음 표에서는 SQL Server 2017의 동작을 보여줍니다.

|주 인스턴스</br>기본 데이터 경로 |보조 인스턴스</br>기본 데이터 경로 |주 인스턴스</br>파일 위치 |SQL Server 2016 </br>보조 인스턴스</br>파일 위치 |SQL Server 2017 </br>보조 인스턴스</br>파일 위치
|:------|:------|:------|:------|:------
|c:\\data\\ |d:\\data\\ |c:\\data\\ |c:\\data\\ |d:\\data\\ 
|c:\\data\\ |d:\\data\\ |c:\\data\\group1\\ |c:\\data\\group1\\ |d:\\data\\group1\\

SQL Server 2016 및 이전 버전의 동작으로 되돌리려면 추적 플래그 9571을 설정합니다. 추적 플래그를 설정하는 방법에 대한 자세한 정보는 [DBCC TRACEON(Transact SQL)](../../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)을 참조하세요.


## <a name="create-an-availability-group-with-automatic-seeding"></a>자동 시드로 가용성 그룹 만들기

Transact-SQL 또는 SSMS(SQL Server Management Studio) 버전 17 이상에서 자동 시드를 사용하여 가용성 그룹을 만듭니다. SSMS에서 가용성 그룹 마법사를 사용하려면 [여기에 나오는 지침](use-the-availability-group-wizard-sql-server-management-studio.md)을 따릅니다. 9단계에 도달하면 자동 시드가 첫 번째 및 기본 옵션으로 표시됩니다.

![초기 데이터 동기화 선택][1]

다음 예제에서는 Transact-SQL을 사용하여 자동 시드가 포함된 가용성 그룹을 만듭니다. [가용성 그룹 만들기(Transact-SQL)](create-an-availability-group-transact-sql.md) 항목도 참조하세요. `SEEDING_MODE` 옵션을 `AUTOMATIC`으로 설정하여 보조 복제본에서 시드를 사용하도록 설정할 수 있습니다. 기본 동작은 `MANUAL`이며, 이는 주 복제본에 데이터베이스를 백업하고, 보조 복제본에 백업 파일을 복사하고, `WITH NORECOVERY`를 사용하여 백업을 복원해야 하는 SQL Server 2016 이전 버전의 동작입니다.

```sql
CREATE AVAILABILITY GROUP [<AGName>]
  FOR DATABASE db1
  REPLICA ON N'Primary_Replica'
WITH (
  ENDPOINT_URL = N'TCP://Primary_Replica.Contoso.com:5022', 
  FAILOVER_MODE = AUTOMATIC, 
  AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
),
  N'Secondary_Replica' WITH (
    ENDPOINT_URL = N'TCP://Secondary_Replica.Contoso.com:5022', 
    FAILOVER_MODE = AUTOMATIC, 
    SEEDING_MODE = AUTOMATIC);
 GO
```

`CREATE AVAILABILITY GROUP` 문에서 주 복제본에 대해 `SEEDING_MODE`를 설정하는 경우 주 복제본에 이미 데이터베이스의 주 읽기/쓰기 복사본이 있으므로 아무런 영향을 주지 않습니다. `SEEDING_MODE`는 다른 복제본이 주 복제본이 되고 데이터베이스가 추가된 경우에만 적용됩니다. 시드 모드는 나중에 변경할 수 있습니다([복제본의 시드 모드 변경](#change-the-seeding-mode-of-a-replica) 참조).

보조 복제본이 되는 인스턴스에서 인스턴스가 조인되면 다음 메시지가 SQL Server 로그에 추가됩니다.

>가용성 그룹 'AGName'에 대해 로컬 가용성 복제본에 데이터베이스를 만드는 권한이 부여되지 않았지만 `AUTOMATIC`의 `SEEDING_MODE`가 있습니다. `ALTER AVAILABILITY GROUP ... GRANT CREATE ANY DATABASE` 명령을 사용하여 주 가용성 복제본에서 시드된 데이터베이스를 만들도록 허용하세요.

### <a name="grant-create-database-permission-on-secondary-replica-to-availability-group"></a><a name = "grantCreate"></a> 보조 복제본에서 가용성 그룹에 데이터베이스 만들기 권한 부여

조인한 후 SQL Server의 보조 복제본 인스턴스에서 가용성 그룹 권한을 부여하여 데이터베이스를 만드세요. 자동 시드를 실행하려면 가용성 그룹에 데이터베이스를 만들 수 있는 권한이 있어야 합니다. 

>[!TIP]
>가용성 그룹이 보조 복제본에서 데이터베이스를 만들 때 데이터베이스 소유자의 소유자로 “sa”(좀 더 구체적으로 0x01 sid를 사용하는 계정)를 설정합니다. 
>
>보조 복제본이 자동으로 데이터베이스를 만든 후 데이터베이스 소유자를 변경하려면 `ALTER AUTHORIZATION`을 실행합니다. [ALTER AUTHORIZATION(Transact-SQL)](../../../t-sql/statements/alter-authorization-transact-sql.md)을 참조하세요.
 
다음 예에서는 AGName이라는 가용성 그룹에 이 권한을 부여합니다.

```sql
ALTER AVAILABILITY GROUP [<AGName>] 
    GRANT CREATE ANY DATABASE
 GO
```

필요한 경우 보조 복제본에서 데이터베이스의 소유자를 설정합니다. 

### <a name="verify-automatic-seeding"></a>자동 시드 확인

성공하면 데이터베이스가 다음 중 하나의 상태로 보조 복제본에 자동으로 만들어집니다.

* SYNCHRONIZED(동기화됨) - 보조 복제본이 동기로 구성되고 데이터가 동기화된 경우
* SYNCHRONIZING(동기화 중) - 보조 복제본이 비동기 데이터 이동으로 구성되었거나 동기로 구성되었지만 주 복제본과 아직 동기화되지 않은 경우

<a name="sql-server-log"></a> 자동 시드의 시작과 완료는 아래에서 설명하는 [동적 관리 뷰](#dynamic-management-views)뿐만 아니라 SQL Server 로그에서도 확인할 수 있습니다.

![SQL Server 로그][2]

## <a name="combine-backup-and-restore-with-automatic-seeding"></a>자동 시드로 백업 및 복원 결합

기존의 백업, 복사 및 복원을 자동 시드와 결합할 수 있습니다. 이 경우 먼저 사용 가능한 트랜잭션 로그 모두를 포함하여 데이터베이스를 보조 복제본에 복원합니다. 다음으로 비상 로그 백업을 복원한 것처럼 보조 복제본의 데이터베이스를 “따라 잡기(catch up)” 위해 가용성 그룹을 만들 때 자동 시드를 사용하도록 설정합니다([비상 로그 백업(SQL Server)](../../../relational-databases/backup-restore/tail-log-backups-sql-server.md) 참조).

## <a name="add-a-database-to-an-availability-group-with-automatic-seeding"></a>자동 시드로 가용성 그룹에 데이터베이스 추가

Transact-SQL 또는 SSMS(SQL Server Management Studio) 버전 17 이상에서 자동 시드를 사용하여 가용성 그룹에 데이터베이스를 추가할 수 있습니다.
보조 복제본을 가용성 그룹에 추가할 때 자동 시드를 사용한 경우 추가로 수행해야 하는 작업이 없습니다. 보조 복제본에서 백업, 복사 및 복원을 사용한 경우 먼저 시드 모드를 변경(다음 섹션 참조)한 다음 데이터베이스를 추가할 때 `GRANT` 문을 사용합니다. [가용성 그룹 - 데이터베이스 추가](availability-group-add-a-database.md)를 참조하세요.

## <a name="change-the-seeding-mode-of-a-replica"></a>복제본의 시드 모드 변경

가용성 그룹을 만든 후에 복제본의 시드 모드를 변경하여 자동 시드를 사용하거나 사용하지 않도록 설정할 수 있습니다. 가용성 그룹을 만든 후에 자동 시드를 사용하도록 설정하면 백업, 복사 및 복원으로 가용성 그룹을 만들었을 때 자동 시드를 사용하여 이 가용성 그룹에 데이터베이스를 추가할 수 있습니다. 다음은 그 예입니다.

```sql
ALTER AVAILABILITY GROUP [AGName]
  MODIFY REPLICA ON 'Replica_Name'
  WITH (SEEDING_MODE = AUTOMATIC)
```

자동 시드를 사용하지 않도록 하려면 MANUAL 값을 사용합니다.

## <a name="prevent-automatic-seeding-after-an-availability-group-is-created"></a>가용성 그룹을 만든 후 자동 시드 방지

보조 복제본에 대해 자동 시드를 완전히 사용하지 않도록 설정하지 않는 한편 보조 복제본에서 데이터베이스를 자동으로 만들지 못하도록 하려면 가용성 그룹 CREATE 권한이 거부됩니다. 이 경우 새 데이터베이스를 가용성 그룹에 추가했지만 가용성 그룹에서 보조 복제본에 데이터베이스를 만들 수 없습니다.

```sql
ALTER AVAILABILITY GROUP [AGName] 
    DENY CREATE ANY DATABASE
GO
```

## <a name="monitor-automatic-seeding"></a>자동 시드 모니터링

자동 시드를 모니터링하고 문제를 해결하는 네 가지 방법이 있습니다.

* 이미 설명한 [SQL Server 로그](#sql-server-log)
* [동적 관리 뷰](#dynamic-management-views)
* [백업 기록 테이블](#backup-history-tables)
* [확장 이벤트](#extended-events)

### <a name="dynamic-management-views"></a>동적 관리 뷰

시드를 모니터링하기 위한 두 가지 DMV(동적 관리 뷰)에는 `sys.dm_hadr_automatic_seeding`과 `sys.dm_hadr_physical_seeding_stats`가 있습니다.

* `sys.dm_hadr_automatic_seeding`은 자동 시드의 일반 상태를 포함하고 자동 시드가 실행될 때마다 기록을 유지합니다(성공 여부와 상관없이). `current_state` 열에는 COMPLETED(완료) 또는 FAILED(실패) 값이 있습니다. 값이 FAILED인 경우 `failure_state_desc`의 값을 사용하여 문제를 진단합니다. 무엇이 잘못되었는지 확인하기 위해 [SQL Server 로그](#sql-server-log)의 내용과 결합해야 할 수도 있습니다. 이 DMV는 주 복제본과 모든 보조 복제본에 채워집니다.

* `sys.dm_hadr_physical_seeding_stats`에서는 실행 중인 자동 시드 작업의 상태를 표시합니다. `sys.dm_hadr_automatic_seeding`과 마찬가지로 주 및 보조 복제본 모두에 대해 값을 반환하지만 이 기록은 저장되지 않습니다. 값은 현재 실행 전용이며 유지되지 않습니다. 관심 있는 열에는 `start_time_utc`, `end_time_utc`, `estimate_time_complete_utc`, `total_disk_io_wait_time_ms`, `total_network_wait_time_ms`가 포함되며 시드 작업이 실패하는 경우 failure_message가 포함됩니다.

### <a name="backup-history-tables"></a>백업 기록 테이블

자동 시드는 백업 및 복원에 대한 기록을 저장하는 `msdb` 테이블에도 항목을 저장합니다. 자동 시드를 받고 있는 보조 복제본에서 `backupmediafamily` 테이블의 physical_device_name 열에는 값에 대한 GUID가 있고, `backupset`의 해당 항목에는 server_name 및 machine_name에 대한 주 복제본의 이름이 있습니다.

### <a name="extended-events"></a>확장 이벤트

자동 시드는 초기화 중에 상태 변경, 오류 및 성능 통계를 추적하기 위한 새로운 확장 이벤트를 추가합니다.
예를 들어 다음 스크립트에서는 자동 시드와 관련된 이벤트를 캡처하는 확장 이벤트 세션을 만듭니다.

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

|속성|Description|
|----|-----------|
|hadr_db_manager_seeding_request_msg|시드 요청 메시지입니다.|
|hadr_physical_seeding_backup_state_change|물리적 시드 백업 관련 상태 변경입니다.|
|hadr_physical_seeding_restore_state_change|물리적 시드 복원 관련 상태 변경입니다.|
|hadr_physical_seeding_forwarder_state_change|물리적 시드 전달자 관련 상태 변경입니다.|
|hadr_physical_seeding_forwarder_target_state_change|물리적 시드 전달자 대상 관련 상태 변경입니다.|
|hadr_physical_seeding_submit_callback|물리적 시드 전송 콜백 이벤트입니다.|
|hadr_physical_seeding_failure|물리적 시드 실패 이벤트입니다.|
|hadr_physical_seeding_progress|물리적 시드 진행 이벤트입니다.|
|hadr_physical_seeding_schedule_long_task_failure|물리적 시드 일정 장기 작업 오류 이벤트입니다.|
|hadr_automatic_seeding_start|자동 시드 작업이 제출될 때 발생합니다.|
|hadr_automatic_seeding_state_transition|자동 시드 작업 상태가 변경될 때 발생합니다.|
|hadr_automatic_seeding_success|자동 시드 작업이 성공할 때 발생합니다.|
|hadr_automatic_seeding_failure|자동 시드 작업이 실패할 때 발생합니다.|
|hadr_automatic_seeding_timeout|자동 시드 작업 시간이 초과할 때 발생합니다.|

## <a name="see-also"></a>참고 항목

[ALTER AVAILABILITY GROUP(Transact-SQL)](/sql/t-sql/statements/alter-availability-group-transact-sql)

[CREATE AVAILABILITY GROUP(Transact-SQL)](../../../t-sql/statements/create-availability-group-transact-sql.md)

[Always On 가용성 그룹 문제 해결 및 모니터링 가이드](https://technet.microsoft.com/library/dn135328.aspx)

<!--Image references-->
[1]: ./media/auto-seed-new-availability-group.png
[2]: ./media/auto-seed-sql-server-log.png
