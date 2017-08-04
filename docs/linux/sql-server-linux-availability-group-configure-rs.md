---
title: "Linux에서 SQL Server에 대 한 읽기 확장 가용성 그룹 구성 | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 06/14/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: cf249ff8e6d2e82d1cf413bdec0272e3796b72cb
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---

# <a name="configure-read-scale-out-availability-group-for-sql-server-on-linux"></a>Linux에서 SQL Server에 대 한 읽기 확장 가용성 그룹을 구성 합니다.

Linux에서 SQL Server에 대 한 읽기 확장 가용성 그룹을 구성할 수 있습니다. 가용성 그룹에 대 한 두 아키텍처 가지가 있습니다. A *고가용성* 아키텍처 클러스터 관리자를 사용 하 여 향상 된 비즈니스 연속성을 제공 합니다. 이 아키텍처는 읽기 확장 복제본을 포함할 수도 있습니다. 고가용성 아키텍처를 만들려면 참조 [구성 Always On 가용성 그룹 Linux에서 SQL Server에 대 한](sql-server-linux-availability-group-configure-ha.md)합니다.

이 문서를 만드는 방법을 설명는 *읽기 확장* 클러스터 관리자 없이 가용성 그룹입니다. 이 아키텍처는만 읽기 확장만 제공합니다. 고가용성을 제공 하지는 않습니다.

[!INCLUDE [Create prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-availability-group"></a>가용성 그룹 만들기

가용성 그룹을 만듭니다. Set `CLUSTER_TYPE = NONE`. 또한 각 복제본으로 설정할 `FAILOVER_MODE = NONE`합니다. 클라이언트 응용 프로그램 분석을 실행 또는 워크 로드를 보고 직접 수 보조 데이터베이스에 연결 합니다. 읽기 전용 라우팅 목록도 만들 수 있습니다. 앞으로 주 복제본에 대 한 연결 라운드 로빈 방식에서 라우팅 목록에서 각 보조 복제본에 연결 요청을 읽습니다.

다음 TRANSACT-SQL 스크립트 가용성 그룹 이름의 만듭니다 `ag1`합니다. 스크립트는 구성 된 가용성 그룹 복제본 `SEEDING_MODE = AUTOMATIC`합니다. 이렇게이 설정 하면 SQL Server를 자동으로 가용성 그룹에 추가 된 후 각 보조 서버에 데이터베이스를 만듭니다. 사용자 환경에 대 한 다음 스크립트를 업데이트 합니다. 대체는 `**<node1>**` 및 `**<node2>**` 복제본을 호스팅하는 SQL Server 인스턴스 이름 사용 하 여 값입니다. 대체는 `**<5022>**` 포트와의 끝점에 대해 설정 합니다. 기본 SQL Server 복제에서 다음 TRANSACT-SQL을 실행 합니다.

```Transact-SQL
CREATE AVAILABILITY GROUP [ag1]
    WITH (CLUSTER_TYPE = NONE)
    FOR REPLICA ON
        N'**<node1>**' WITH (
            ENDPOINT_URL = N'tcp://**<node1>:**<5022>**',
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
                    SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            ),
        N'**<node2>**' WITH ( 
            ENDPOINT_URL = N'tcp://**<node2>**:**<5022>**', 
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
            SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            );
        
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

### <a name="join-secondary-sql-servers-to-the-availability-group"></a>보조 SQL Server 가용성 그룹에 조인

다음 TRANSACT-SQL 스크립트 라는 가용성 그룹에는 서버를 가입 시킵니다. `ag1`합니다. 사용자 환경에 대 한 스크립트를 업데이트 합니다. SQL Server 각 보조 복제본에서 가용성 그룹에 참가 하려면 다음 TRANSACT-SQL을 실행 합니다.

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

이 항상 사용 가능한 구성, 고가용성이 필요한 경우의 지침에 따라 [구성 Always On 가용성 그룹 Linux에서 SQL Server에 대 한](sql-server-linux-availability-group-configure-ha.md)합니다. 특히 가용성 그룹을 만들 `CLUSTER_TYPE=WSFC` (Windows)에 또는 `CLUSTER_TYPE=EXTERNAL` (Linux)에서 클러스터 관리자-WSFC windows 또는 Linux에서 Pacemaker와 통합 합니다.

## <a name="connect-to-read-only-secondary-replicas"></a>읽기 전용 보조 복제본에 연결

읽기 전용 보조 복제본에 연결 하는 방법은 두 가지가 있습니다. 응용 프로그램에서 보조 복제본을 호스팅하는 SQL Server 인스턴스에 직접 연결 하 고는 데이터베이스를 쿼리할 수 또는 읽기 전용 라우팅을 사용할 수 있습니다. 읽기 전용 라우팅이 수신기가 필요합니다.

[읽기 가능한 보조 복제본](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)

[읽기 전용 라우팅](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md#ConnectToSecondary)

## <a name="fail-over-primary-replica-on-read-scale-out-availability-group"></a>장애 조치 읽기 확장 가용성 그룹에 주 복제본

각 가용성 그룹에 주 복제본이 하나만 있습니다. 주 복제본 읽기만 허용 하 고 씁니다. 이 주 복제본을 변경 하려면 조치할 수 있습니다. 고가용성을 위한 가용성 그룹을 클러스터 관리자에서 장애 조치 프로세스 자동화합니다. 읽기 확장 가용성 그룹 장애 조치 프로세스는 수동입니다. 두 가지 방법으로 읽기 배율 가용성 그룹에서 주 복제본 장애 조치할 수 있습니다.

- 데이터 손실에 수동 장애를 강제로

- 데이터 손실 없이 수동 장애 조치

### <a name="forced-fail-over-with-data-loss"></a>데이터 손실 될 수 있는 강제 장애 조치

이 메서드를 사용 하 여 주 복제본 사용할 수 있고 복구할 수 있습니다. 데이터 손실에 강제 장애 조치에 대 한 자세한 정보를 찾을 수 [강제 수동 장애 조치를 수행](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)합니다.

장애 조치 데이터 손실를 적용 하려면 대상 보조 복제본을 호스팅하는 SQL 인스턴스에 연결을 실행 합니다.
```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] FORCE_FAILOVER_ALLOW_DATA_LOSS;
```

### <a name="manual-fail-over-without-data-loss"></a>데이터 손실 없이 수동 장애 조치

주 복제본은 주 복제본을 사용할 수 없지만 일시적 또는 영구적으로 구성을 변경 하 고 호스팅하는 SQL Server 인스턴스를 변경 해야 하는 경우이 메서드를 사용 합니다. 수동 장애 조치를 발급 하기 전에 잠재적인 데이터 손실 없이 되도록 대상 보조 복제본을 최신 상태로 인지를 확인 합니다. 

다음 단계에는 데이터 손실 없이 수동 장애 조치 하는 방법을 설명 합니다.

1. 대상 보조 복제본 동기 커밋을 확인 하십시오.

   ```Transact-SQL
   ALTER AVAILABILITY GROUP [ag1] MODIFY REPLICA ON N'**<node2>*' WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
   ```
1. 업데이트 `required_synchronized_secondaries_to_commit`1입니다.

   이 설정은 모든 활성 트랜잭션이 커밋 주 복제본과 동기 보조 데이터베이스를 하나 이상에 되는지 확인 합니다. 가용성 그룹이 장애 조치는 synchronization_state_desc 동기화 되어 있을 때 준비가 고는 sequence_number은 모두 기본에 대 한 동일한과 대상 보조 복제본입니다. 확인 하려면이 쿼리를 실행 합니다.

   ```Transact-SQL
   SELECT ag.name, 
      drs.database_id, 
      drs.group_id, 
      drs.replica_id, 
      drs.synchronization_state_desc, 
      ag.sequence_number
   FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
   WHERE drs.group_id = ag.group_id; 
   ```

1. 주 복제본을 보조 복제본의 수준을 내립니다. 주 복제본 강등 된 읽기 전용입니다. 보조 역할을 업데이트 하려면 주 복제본을 호스팅하는 SQL 인스턴스에서이 명령을 실행 합니다.

   ```Transact-SQL
   ALTER AVAILABILITY GROUP [ag1] SET (ROLE = SECONDARY); 
   ```

1. 대상 보조 복제본이 주을 승격 합니다. 

   ```Transact-SQL
   ALTER AVAILABILITY GROUP distributedag FORCE_FAILOVER_ALLOW_DATA_LOSS; 
   ```  

   > [!NOTE] 
   > 가용성 그룹 사용을 삭제 하려면 [DROP AVAILABILITY GROUP](https://docs.microsoft.com/en-us/sql/t-sql/statements/drop-availability-group-transact-sql)합니다. CLUSTER_TYPE 없음 또는 외부를 사용 하 여 만든 가용성 그룹에 대 한 가용성 그룹의 모든 복제본 일부에서 실행 되어야 하는 명령에 있습니다.

## <a name="next-steps"></a>다음 단계

[분산형된 가용성 그룹 구성](..\database-engine\availability-groups\windows\distributed-availability-groups-always-on-availability-groups.md)

[가용성 그룹에 대 한 자세한 정보](..\database-engine\availability-groups\windows\overview-of-always-on-availability-groups-sql-server.md)


