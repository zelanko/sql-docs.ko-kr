---
title: 분산 가용성 그룹 구성
description: Transact-SQL 예제를 사용하여 분산 가용성 그룹을 구성하는 방법에 대해 알아봅니다. 또한 분산 가용성 그룹에 대한 정보를 어디에서 찾을 수 있는지 알아봅니다.
ms.custom: seodec18
ms.date: 01/28/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
ms.assetid: f7c7acc5-a350-4a17-95e1-e689c78a0900
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5a6e5f2051a0e6937cd26d9ceec06d42ccbeb201
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91115663"
---
# <a name="configure-an-always-on-distributed-availability-group"></a>Always On 분산 가용성 그룹 구성  
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

분산형 가용성 그룹을 만들려면 각각의 자체 수신기를 사용하여 두 개의 가용성 그룹을 만들어야 합니다. 그런 다음 이러한 가용성 그룹을 분산 가용성 그룹으로 결합해야 합니다. 다음 단계는 TRANSACT-SQL에서의 기본 예제를 제공합니다. 이 예제에서는 가용성 그룹 및 수신기를 만드는 데 관련된 자세한 내용을 다루지 않는 대신 주요 요구 사항을 집중적으로 다루고 있습니다.

분산 가용성 그룹에 대한 기술적 개요는 [분산 가용성 그룹](distributed-availability-groups.md)을 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

### <a name="set-the-endpoint-listeners-to-listen-to-all-ip-addresses"></a>모든 IP 주소를 수신 대기하도록 엔드포인트 수신기를 설정합니다.

엔드포인트에서 분배 가용성 그룹의 서로 다른 가용성 그룹 간에 통신할 수 있는지 확인합니다. 하나의 가용성 그룹이 엔드포인트의 특정 네트워크로 설정되면 분산 가용성 그룹이 제대로 작동하지 않습니다. 분산 가용성 그룹에서 복제본을 호스팅하는 각 서버에서 수신기가 모든 IP 주소(`LISTENER_IP = ALL`)를 수신 대기하도록 설정합니다.

#### <a name="create-a-listener-to-listen-to-all-ip-addresses"></a>모든 IP 주소를 수신 대기하도록 수신기 만들기

예를 들어 다음 스크립트에서는 모든 IP 주소에서 수신 대기하는 5022 TCP 포트에 수신기 엔드포인트를 만듭니다.  

```sql
CREATE ENDPOINT [aodns-hadr] 
    STATE=STARTED
    AS TCP (LISTENER_PORT = 5022, LISTENER_IP = ALL)
FOR DATA_MIRRORING (
   ROLE = ALL, 
   AUTHENTICATION = WINDOWS NEGOTIATE,
   ENCRYPTION = REQUIRED ALGORITHM AES
)
GO
```

#### <a name="alter-a-listener-to-listen-to-all-ip-addresses"></a>모든 IP 주소를 수신 대기하도록 수신기 변경

예를 들어 다음 스크립트에서는 모든 IP 주소에서 수신 대기하도록 수신기 엔드포인트를 변경합니다.  

```sql
ALTER ENDPOINT [aodns-hadr] 
    AS TCP (LISTENER_IP = ALL)
GO
```

## <a name="create-first-availability-group"></a>첫 번째 가용성 그룹 만들기

### <a name="create-the-primary-availability-group-on-the-first-cluster"></a>첫 번째 클러스터에 주 가용성 그룹 만들기  
첫 번째 WSFC(Windows Server Failover Cluster)에서 가용성 그룹을 만듭니다.   이 예제에서 `ag1` 데이터베이스에 대한 가용성 그룹 이름은 `db1`입니다. 기본 가용성 그룹의 주 복제본을 분산 가용성 그룹에서 **전역 기본**이라고 합니다. Server1은 이 예제의 전역 기본입니다.        
  
```sql  
CREATE AVAILABILITY GROUP [ag1]   
FOR DATABASE db1   
REPLICA ON N'server1' WITH (ENDPOINT_URL = N'TCP://server1.contoso.com:5022',  
    FAILOVER_MODE = AUTOMATIC,  
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC),   
N'server2' WITH (ENDPOINT_URL = N'TCP://server2.contoso.com:5022',   
    FAILOVER_MODE = AUTOMATIC,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC);   
GO  
  
```  
  
>[!NOTE]
>이전 예제에서는 자동 시드를 사용하며, 복제본 및 분산 가용성 그룹에서 모두 **SEEDING_MODE**가 **AUTOMATIC**으로 설정됩니다. 이 구성은 수동으로 백업하고 주 데이터베이스를 복원할 필요 없이 보조 복제본과 보조 가용성 그룹이 자동으로 채워지도록 설정합니다.  
  
### <a name="join-the-secondary-replicas-to-the-primary-availability-group"></a>보조 복제본을 주 가용성 그룹에 조인  
모든 보조 복제본은 **JOIN** 옵션으로 **ALTER AVAILABILITY GROUP** 이(가) 있는 가용성 그룹에 조인되어야 합니다. 이 예제에서는 자동 시드를 사용하기 때문에 **GRANT CREATE ANY DATABASE** 옵션으로 **ALTER AVAILABILITY GROUP**도 호출해야 합니다. 이 설정을 통해 가용성 그룹이 데이터베이스를 만들고 주 복제본에서 자동으로 시딩을 시작할 수 있습니다.  
  
이 예제에서는 보조 복제본 `server2`에서 다음 명령이 실행되어 가용성 그룹 `ag1` 에 조인됩니다. 그런 다음 가용성 그룹이 보조 가용성 그룹에 데이터베이스를 만들 수 있습니다.  
  
```sql  
ALTER AVAILABILITY GROUP [ag1] JOIN   
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE  
GO  
```  

>[!NOTE]
>보조 복제본에서 가용성 그룹이 데이터베이스를 만들 때 가용성 그룹은 데이터베이스 소유자를 데이터베이스를 만들기 위한 `ALTER AVAILABILITY GROUP` 문을 실행하여 권한을 부여한 계정으로 설정합니다. 자세한 내용은 [보조 복제본에서 가용성 그룹에 데이터베이스 만들기 권한 부여](automatic-seeding-secondary-replicas.md#grantCreate)를 참조하세요.
  
### <a name="create-a-listener-for-the-primary-availability-group"></a>주 가용성 그룹에 대한 수신기 만들기  

그런 다음 첫 번째 WSFC에 주 가용성 그룹에 대한 수신기를 추가합니다. 이 예제에서 수신기 이름은 `ag1-listener`입니다. 수신기를 만드는 방법은 [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)을 참조하세요.  
  
```sql
ALTER AVAILABILITY GROUP [ag1]    
    ADD LISTENER 'ag1-listener' ( 
        WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , 
        PORT = 60173);    
GO  
```  
  

## <a name="create-second-availability-group"></a>두 번째 가용성 그룹 만들기  
 그런 다음 두 번째 WSFC에서 두 번째 가용성 그룹인 `ag2`을(를) 만듭니다. 이 경우 주 가용성 그룹에서 자동으로 시딩되므로 데이터베이스를 지정하지 않습니다.  보조 가용성 그룹의 주 복제본을 분산 가용성 그룹에서 **전달자**라고 합니다. 이 예에서 server3은 전달자입니다. 
  
```sql  
CREATE AVAILABILITY GROUP [ag2]   
FOR   
REPLICA ON N'server3' WITH (ENDPOINT_URL = N'TCP://server3.contoso.com:5022',   
    FAILOVER_MODE = MANUAL,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC),   
N'server4' WITH (ENDPOINT_URL = N'TCP://server4.contoso.com:5022',   
    FAILOVER_MODE = MANUAL,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC);   
GO  
```  
  
> [!NOTE]  
> 보조 가용성 그룹은 동일한 데이터베이스 미러링 엔드포인트(이 예제에서는 5022 포트)를 사용해야 합니다. 그렇지 않으면 로컬 장애 조치(failover) 후 복제가 중지됩니다.  
  
### <a name="join-the-secondary-replicas-to-the-secondary-availability-group"></a>보조 복제본을 보조 가용성 그룹에 조인  
 이 예제에서는 보조 복제본 `server4`에서 다음 명령이 실행되어 가용성 그룹 `ag2` 에 조인됩니다. 그러면 가용성 그룹이 보조 복제본에 데이터베이스를 만들어 자동 시드를 지원할 수 있습니다.  
  
```sql  
ALTER AVAILABILITY GROUP [ag2] JOIN   
ALTER AVAILABILITY GROUP [ag2] GRANT CREATE ANY DATABASE  
GO  
```  
  
### <a name="create-a-listener-for--the-secondary-availability-group"></a>보조 가용성 그룹에 대한 수신기 만들기  
 그런 다음 두 번째 WSFC에 보조 가용성 그룹에 대한 수신기를 추가합니다. 이 예제에서 수신기 이름은 `ag2-listener`입니다. 수신기를 만드는 방법은 [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)을 참조하세요.  
  
```sql  
ALTER AVAILABILITY GROUP [ag2]    
    ADD LISTENER 'ag2-listener' ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173);    
GO  
```  
  
## <a name="create-distributed-availability-group-on-first-cluster"></a>첫 번째 클러스터에 분산 가용성 그룹 만들기  
 첫 번째 WSFC에서 분산형 가용성 그룹(이 예제에서의 이름은 `distributedag` )을 만듭니다. **DISTRIBUTED** 옵션으로 **CREATE AVAILABILITY GROUP** 명령을 사용합니다. **AVAILABILITY GROUP ON** 매개 변수는 멤버 가용성 그룹인 `ag1` 및 `ag2`를 지정합니다.  
  
```sql  
CREATE AVAILABILITY GROUP [distributedag]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener.contoso.com:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener.contoso.com:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO   
```  
  
> [!NOTE]  
>  **LISTENER_URL** 은 가용성 그룹의 데이터베이스 미러링 엔드포인트와 함께 각 가용성 그룹에 대한 수신기를 지정합니다. 이 예제에서 수신기는 `5022` 포트(수신기를 만드는 데 사용된 `60173` 포트 아님)입니다. Azure의 인스턴스 등, 부하 분산 장치를 사용할 경우 [가용성 그룹 포트에 대해 부하 분산 규칙을 추가합니다](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener#add-load-balancing-rule-for-distributed-availability-group). SQL Server 인스턴스 포트 외에도 수신기 포트에 대한 규칙을 추가합니다. 

### <a name="cancel-automatic-seeding-to-forwarder"></a>전달자에 대한 자동 시드 취소

어떤 이유로든, 두 가용성 그룹이 동기화되기 _전에_ 전달자의 초기화를 취소해야 하는 경우 전달자의 SEEDING_MODE 매개 변수를 MANUAL로 설정하여 분산 가용성 그룹을 ALTER하고 즉시 시드를 취소합니다. 전역 기본에서 명령을 실행합니다. 

```sql
-- Cancel automatic seeding.  Connect to global primary but specify DAG AG2
ALTER AVAILABILITY GROUP [distributedag]   
   MODIFY  
   AVAILABILITY GROUP ON  
   'ag2' WITH  
   (  SEEDING_MODE = MANUAL  );   
```

  
## <a name="join-distributed-availability-group-on-second-cluster"></a>두 번째 클러스터에 분산 가용성 그룹 조인  
 그런 다음 두 번째 WSFC에 분산형 가용성 그룹을 조인합니다.  
  
```sql  
ALTER AVAILABILITY GROUP [distributedag]   
   JOIN   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener.contoso.com:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener.contoso.com:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO  
```  

## <a name="join-the-database-on-the-secondary-of-the-second-availability-group"></a><a name="failover"></a> 두 번째 가용성 그룹의 보조에 있는 데이터베이스 조인
두 번째 가용성 그룹의 보조 복제본에 있는 데이터베이스가 복원 상태로 전환된 후 해당 데이터베이스를 가용성 그룹에 수동으로 조인해야 합니다.

```sql  
ALTER DATABASE [db1] SET HADR AVAILABILITY GROUP = [ag2];   
```
  
## <a name="fail-over-to-a-secondary-availability-group"></a><a name="failover"></a> 보조 가용성 그룹에 대한 장애 조치(failover)  

이 경우에는 수동 장애 조치(failover)만 지원됩니다. 분산 가용성 그룹을 수동으로 장애 조치(failover)하려면 다음을 수행합니다.

1. 데이터가 손실되지 않도록 하려면 전역 주 데이터베이스(주 가용성 그룹의 데이터베이스)에서 모든 트랜잭션을 중지한 다음, 분산 가용성 그룹을 동기 커밋으로 설정합니다.
1. 분산 가용성 그룹이 동기화되고 데이터베이스당 동일한 last_hardened_lsn을 포함할 때까지 기다립니다. 
1. 글로벌 기본 복제본에서 분산 가용성 그룹 역할을 `SECONDARY`로 설정합니다.
1. 장애 조치(failover) 준비 상태를 테스트합니다.
1. 기본 가용성 그룹을 장애 조치(failover)합니다.

다음 Transact-SQL 예제에서는 `distributedag`라는 분산 가용성 그룹을 장애 조치(failover)하는 자세한 단계를 보여줍니다.

1. 데이터가 손실되지 않도록 하려면 전역 주 데이터베이스(주 가용성 그룹의 데이터베이스)에서 모든 트랜잭션을 중지합니다. 그런 다음, 전역 기본 및 전달자 ‘모두’에서 다음 코드를 실행하여 분산 가용성 그룹을 동기 커밋으로 설정합니다.   
    
      ```sql  
      -- sets the distributed availability group to synchronous commit 
       ALTER AVAILABILITY GROUP [distributedag] 
       MODIFY 
       AVAILABILITY GROUP ON
       'ag1' WITH 
        ( 
        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT 
        ), 
        'ag2' WITH  
        ( 
        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT 
        );
       
       -- verifies the commit state of the distributed availability group
       select ag.name, ag.is_distributed, ar.replica_server_name, ar.availability_mode_desc, ars.connected_state_desc, ars.role_desc, 
       ars.operational_state_desc, ars.synchronization_health_desc from sys.availability_groups ag  
       join sys.availability_replicas ar on ag.group_id=ar.group_id
       left join sys.dm_hadr_availability_replica_states ars
       on ars.replica_id=ar.replica_id
       where ag.is_distributed=1
       GO

      ```  
   > [!NOTE]
   > 분산 가용성 그룹에서 두 가용성 그룹 간의 동기화 상태는 두 복제본의 가용성 모드에 따라 다릅니다. 동기 커밋 모드의 경우 현재 기본 가용성 그룹과 현재 보조 가용성 그룹 모두 `SYNCHRONOUS_COMMIT` 가용성 모드가 있어야 합니다. 이러한 이유로 글로벌 기본 복제본과 전달자 모두에서 위의 스크립트를 실행해야 합니다.


1. 분산 가용성 그룹의 상태가 `SYNCHRONIZED`로 변경되고 모든 복제본이 동일한 last_hardened_lsn(데이터베이스당)을 포함할 때까지 기다립니다. 기본 가용성 그룹의 주 복제본인 전역 기본 및 전달자에서 둘 다 다음 쿼리를 실행하여 synchronization_state_desc 및 last_hardened_lsn을 확인합니다. 
    
      ```sql  
      -- Run this query on the Global Primary and the forwarder
      -- Check the results to see if synchronization_state_desc is SYNCHRONIZED, and the last_hardened_lsn is the same per database on both the global primary and       forwarder 
      -- If not rerun the query on both side every 5 seconds until it is the case
      --
      SELECT ag.name
             , drs.database_id
             , db_name(drs.database_id) as database_name
             , drs.group_id
             , drs.replica_id
             , drs.synchronization_state_desc
             , drs.last_hardened_lsn  
      FROM sys.dm_hadr_database_replica_states drs 
      INNER JOIN sys.availability_groups ag on drs.group_id = ag.group_id;
      ```  

    가용성 그룹 **synchronization_state_desc**가 `SYNCHRONIZED`가 되고 last_hardened_lsn이 전역 기본 및 전달자에서 둘 다 데이터베이스당 동일해진 후 계속 진행합니다.  **synchronization_state_desc**가 `SYNCHRONIZED`가 아니거나 last_hardened_lsn이 동일하지 않으면 변경될 때까지 5초마다 명령을 실행합니다. **synchronization_state_desc** = `SYNCHRONIZED`가 되고 last_hardened_lsn이 데이터베이스당 동일해질 때까지 진행하지 마세요. 

1. 전역 기본에서 분산 가용성 그룹 역할을 `SECONDARY`로 설정합니다. 

    ```sql
    ALTER AVAILABILITY GROUP distributedag SET (ROLE = SECONDARY); 
    ```  

    이 시점에서 분산 가용성 그룹은 사용할 수 없습니다.

1. 장애 조치(failover) 준비를 테스트합니다. 전역 기본 및 전달자에서 둘 다 다음 쿼리를 실행합니다.

    ```sql
     -- Run this query on the Global Primary and the forwarder
     -- Check the results to see if the last_hardened_lsn is the same per database on both the global primary and forwarder 
     -- The availability group is ready to fail over when the last_hardened_lsn is the same for both availability groups per database
     --
     SELECT ag.name, 
         drs.database_id, 
         db_name(drs.database_id) as database_name,
         drs.group_id, 
         drs.replica_id,
         drs.last_hardened_lsn
     FROM sys.dm_hadr_database_replica_states drs
     INNER JOIN sys.availability_groups ag ON drs.group_id = ag.group_id;
    ```  

    **last_hardened_lsn**이 데이터베이스당 두 가용성 그룹에 대해 모두 동일한 경우 가용성 그룹을 장애 조치(failover)할 준비가 된 것입니다. 일정 시간 후에 last_hardened_lsn이 동일하지 않으면 데이터 손실을 방지하기 위해 전역 기본에서 이 명령을 실행하여 전역 기본으로 장애 복구(failback)한 다음, 두 번째 단계에서 다시 시작합니다. 

    ```sql
    -- If the last_hardened_lsn is not the same after a period of time, to avoid data loss, 
    -- we need to fail back to the global primary by running this command on the global primary 
    -- and then start over from the second step:

    ALTER AVAILABILITY GROUP distributedag FORCE_FAILOVER_ALLOW_DATA_LOSS; 
    ```


1. 주 가용성 그룹에서 보조 가용성 그룹으로 장애 조치(failover)합니다. 보조 가용성 그룹의 주 복제본을 호스트하는 전달자인 SQL Server에서 다음 명령을 실행합니다. 

    ```sql
    -- Once the last_hardened_lsn is the same per database on both sides
    -- We can Fail over from the primary availability group to the secondary availability group. 
    -- Run the following command on the forwarder, the SQL Server instance that hosts the primary replica of the secondary availability group.

    ALTER AVAILABILITY GROUP distributedag FORCE_FAILOVER_ALLOW_DATA_LOSS; 
    ```  

    이 단계가 완료되면 분산 가용성 그룹을 사용할 수 있게 됩니다.
      
위의 단계를 완료한 후 분산 가용성 그룹은 데이터 손실없이 장애 조치(failover)됩니다. 가용성 그룹이 지연이 발생하는 지리적 거리 위치에 있는 경우에는 가용성 모드를 다시 ASYNCHRONOUS_COMMIT으로 변경하는 것이 좋습니다. 
  
## <a name="remove-a-distributed-availability-group"></a>분산형 가용성 그룹 제거  
 다음 Transact-SQL 문은 `distributedag`라는 이름의 분산형 가용성 그룹을 삭제합니다.  
  
```sql  
DROP AVAILABILITY GROUP [distributedag]  
```  

## <a name="create-distributed-availability-group-on-failover-cluster-instances"></a>장애 조치 클러스터 인스턴스에 분산 가용성 그룹 만들기

FCI(장애 조치 클러스터 인스턴스)에서 가용성 그룹을 사용하여 분산 가용성 그룹을 만들 수 있습니다. 이 경우 가용성 그룹 수신기가 필요 없습니다. FCI 인스턴스의 주 복제본에 VNN(가상 네트워크 이름)을 사용합니다. 다음 예제에서는 SQLFCIDAG 라는 분산 가용성 그룹을 보여 줍니다. 가용성 그룹으로 SQLFCIAG가 하나 있으며, SQLFCIAG에는 FCI 복제본이 2개 있습니다. 주 FCI 복제본의 VNN은 SQLFCIAG-1이며 보조 FCI 복제본의 VNN은 SQLFCIAG-2입니다. 재해 복구를 위해 분산 가용성 그룹에는 재해 복구를 위해 SQLAG-DR도 포함됩니다.

![배포되는 Always On 가용성 그룹](../../../database-engine/availability-groups/windows/media/always-on-availability-group-distributed.png)

 
 
 다음 DDL에서 이 분산 가용성 그룹을 만듭니다. 

```sql  
CREATE AVAILABILITY GROUP [SQLFCIDAG]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
  'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-1.contoso.com:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      ),   
  'SQLAG-DR' WITH    
       (   
         LISTENER_URL = 'tcp://SQLAG-DR.contoso.com:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      );   
```  

수신기 URL은 주 FCI 인스턴스의 VNN입니다.

## <a name="manually-fail-over-fci-in-distributed-availability-group"></a>분산 가용성 그룹에서 FCI 수동 장애 조치

FCI 가용성 그룹을 수동으로 장애 조치하려면 수신기 URL의 변경 내용을 반영하도록 분산 가용성 그룹을 업데이트합니다. 예를 들어 SQLFCIAG의 기본 AG와 보조 AG에서 다음 DDL을 실행합니다.

```sql  
ALTER AVAILABILITY GROUP [SQLFCIDAG]  
   MODIFY AVAILABILITY GROUP ON  
 'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-2.contoso.com:5022'
    )
```  
  
## <a name="next-steps"></a>다음 단계

 [CREATE AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  
