---
title: 가용성 그룹에 대한 SQL Server 강제 장애 조치(failover)
description: 클러스터 형식이 NONE인 가용성 그룹의 강제 장애 조치(failover)
services: ''
author: MikeRayMSFT
ms.topic: include
ms.date: 02/05/2018
ms.author: mikeray
ms.custom: include file
ms.openlocfilehash: 87fce17db46dc590fbffe0bae0b27c17bd54320e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68213083"
---
각 가용성 그룹에는 하나의 주 복제본만 있습니다. 주 복제본은 읽기 및 쓰기를 허용합니다. 주 복제본을 변경하기 위해 장애 조치(failover)를 수행할 수 있습니다. 고가용성을 위한 가용성 그룹에서 클러스터 관리자는 장애 조치 프로세스를 자동화합니다. 클러스터 형식이 NONE인 가용성 그룹에서 장애 조치(failover) 프로세스는 수동입니다. 

클러스터 형식이 NONE인 가용성 그룹에서 두 가지 방법으로 주 복제본을 장애 조치(failover)할 수 있습니다.

- 데이터 손실이 있는 강제 수동 장애 조치(Failover)
- 데이터가 손실되지 않는 수동 장애 조치(Failover)

### <a name="forced-manual-failover-with-data-loss"></a>데이터 손실이 있는 강제 수동 장애 조치(Failover)

주 복제본을 사용할 수 없고 복구할 수 없는 경우 이 방법을 사용합니다. 

데이터 손실이 있는 강제 장애 조치(failover)를 수행하려면 대상 보조 복제본을 호스팅하는 SQL Server 인스턴스에 연결하고 다음 명령을 실행합니다.

```SQL
ALTER AVAILABILITY GROUP [ag1] FORCE_FAILOVER_ALLOW_DATA_LOSS;
```

이전 주 복제본이 복구되면 주 역할도 복구되는 것으로 가정됩니다. 이전 주 복제본이 보조 역할로 전환되도록 하려면 이전 주 복제본에 대해 다음 명령을 실행합니다.

```SQL
ALTER AVAILABILITY GROUP [ag1]  SET (ROLE = SECONDARY);
```

### <a name="manual-failover-without-data-loss"></a>데이터가 손실되지 않는 수동 장애 조치(Failover)

주 복제본을 사용할 수 있지만 이 구성을 일시적 또는 영구적으로 변경하고 주 복제본을 호스팅하는 SQL Server 인스턴스를 변경해야 하는 경우 이 방법을 사용합니다. 잠재적인 데이터 손실을 방지하려면 수동 장애 조치(failover)를 실행하기 전에 대상 보조 복제본이 최신 상태인지 확인합니다. 

데이터 손실이 없는 수동 장애 조치(Failover)를 수행하려면:

1. 대상 보조 복제본 `SYNCHRONOUS_COMMIT`를 만듭니다.

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        MODIFY REPLICA ON N'<node2>' 
        WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
   ```

2. 활성 트랜잭션이 주 복제본과 적어도 하나의 동기 보조 복제본에 커밋되었는지 확인하려면 다음 쿼리를 실행합니다. 

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

3. `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`을 1로 업데이트합니다.

   다음 스크립트에서는 `ag1` 가용성 그룹에서 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`을 1로 설정합니다. 다음 스크립트를 실행하기 전에 `ag1`을 가용성 그룹의 이름으로 바꿉니다.

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = 1;
   ```

   이 설정은 모든 활성 트랜잭션이 주 복제본과 적어도 하나의 동기 보조 복제본에 커밋되었는지 확인합니다. 

4. 주 복제본을 보조 복제본으로 강등합니다. 주 복제본이 강등되면 읽기 전용입니다. 역할을 `SECONDARY`로 업데이트하려면 주 복제본을 호스팅하는 SQL Server 인스턴스에서 이 명령을 실행합니다.

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET (ROLE = SECONDARY); 
   ```

5. 대상 보조 복제본을 주 복제본으로 승격합니다. 

   ```SQL
   ALTER AVAILABILITY GROUP ag1 FORCE_FAILOVER_ALLOW_DATA_LOSS; 
   ```  

   > [!NOTE] 
   > 가용성 그룹 사용을 삭제하려면 [DROP AVAILABILITY GROUP](https://docs.microsoft.com/sql/t-sql/statements/drop-availability-group-transact-sql)을 사용합니다. NONE 또는 EXTERNAL 클러스터 형식을 사용하여 만든 가용성 그룹의 경우 가용성 그룹의 일부인 모든 복제본에서 명령을 실행합니다.
