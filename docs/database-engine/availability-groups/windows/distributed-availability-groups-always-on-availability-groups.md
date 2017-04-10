---
title: "분산된 가용성 그룹(Always On 가용성 그룹) | Microsoft Docs"
ms.custom: ""
ms.date: "08/30/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f7c7acc5-a350-4a17-95e1-e689c78a0900
caps.latest.revision: 28
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 28
---
# 분산된 가용성 그룹(Always On 가용성 그룹)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  분산된 가용성 그룹을 사용하면 서로 다른 Windows Server 장애 조치 클러스터(WSFC)에 있는 두 가용성 그룹을 연결할 수 있습니다. 분산된 가용성 그룹 배포의 주요 용도 중 하나는 기본 사이트가 DR 사이트로부터 지리적으로 분산된 곳의 문제 해결를 위한 것입니다. 원하는 데이터를 지속적으로 DR 사이트에 복제 하지 않으려는 잠재적인 네트워크 문제 또는 기본 사이트에 종료 DR 사이트에서 문제입니다.  
  
 다음 다이어그램에서는 분산형 가용성 그룹의 아키텍처를 보여줍니다.  
  
 ![AlwaysOn Distributed Availability Groups](../../../database-engine/availability-groups/windows/media/alwayson-distributed-availability-groups.png "AlwaysOn Distributed Availability Groups")  
  
 이전 다이어그램에는 두 개의 별도 Windows Server 장애 조치 클러스터(WFSC 1 및 2 WFSC)가 있습니다. 각 클러스터에는 데이터베이스 구성과 일치하는 자체 가용성 그룹이 있습니다. 분산형 가용성 그룹은 “가용성 그룹의 가용성 그룹”으로 간주될 수 있습니다. AG 1은 이 예제의 주 가용성 그룹입니다. 삽입 및 업데이트는 주 복제본인 AG1에서 모두 수행된 후 보조 복제본으로 복제됩니다. 그러나 WSFC 2의 보조 가용성 그룹 네트워크로도 변경 내용이 복제됩니다. AG 2 가용성 그룹은 그러한 변경 내용을 보조 복제본(들)으로 복제합니다.  
  
> [!IMPORTANT]  
>  두 가용성 그룹 사이에서 분산형 가용성 그룹 관계가 설정되면 보조 가용성 그룹은 자동으로 읽기 전용이 됩니다. 업데이트 및 삽입은 주 가용성 그룹의 주 복제본에서만 수행됩니다(이 예에서는 주 복제본 AG 1).  
  
 분산형 가용성 그룹은 다음의 측면에서 단일 Windows Server 장애 조치(Failover) 클러스터의 가용성 그룹과 다릅니다.  
  
-   각 WSFC는 자체 쿼럼 모드 및 노드 투표 구성을 유지 관리합니다. 즉, 보조 WSFC의 상태는 기본 WSFC에 영향을 주지않습니다.  
  
-   데이터는 네트워크를 통해 보조 WSFC로 한 번 전송된 후 해당 클러스터 내에서 복제됩니다. 단일 WSFC에서 데이터는 각 복제본에 개별적으로 전송됩니다. 지리적으로 분산된 보조 사이트의 경우 분산형 가용성 그룹이 더 효율적입니다.  
  
-   기본 및 보조 클러스터에서 사용되는 운영 체제 버전은 다를 수 있습니다. 단일 WSFC에서 모든 서버는 동일한 버전의 운영 체제를 사용해야 합니다. 이로 인해 운영 체제를 롤링 업데이트/업그레이드하는 분산형 가용성 그룹을 사용할 수 있습니다.  
  
-   주 및 보조 가용성 그룹은 데이터베이스의 구성이 동일해야 합니다.  
  
-   보조 가용성 그룹에 대한 자동 장애 조치(failover)는 지원되지 않습니다.  
  
## 분산형 가용성 그룹 만들기  
 분산형 가용성 그룹을 만들려면 각 WSFC에서 가용성 그룹 및 수신기를 만들어야 합니다. 그런 다음 이러한 분산형 가용성 그룹으로 결합해야 합니다. 다음 단계는 TRANSACT-SQL에서의 기본 예제를 제공합니다. 이 예제는 가용성 그룹 및 수신기를 만드는 것과 관련한 자세한 내용을 다루는 대신 주요 요구 사항을 집중적으로 다룹니다.  
  
### 첫 번째 클러스터에 주 가용성 그룹 만들기  
 첫 WSFC에 주 가용성 그룹을 만듭니다.   이 예제에서 `ag1` 데이터베이스에 대한 가용성 그룹 이름은 `db1`입니다.  
  
```tsql  
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
  
 이 예제에서는 직접 시드를 사용하고 여기에서 복제본 및 분산형 가용성 그룹 모두에서 **SEEDING_MODE**는 **AUTOMATIC**으로 설정됩니다. 즉, 설정되면 수동으로 백업하고 주 데이터베이스를 복구할 필요 없이 보조 복제본과 보조 가용성 그룹이 자동으로 채워집니다.  
  
### 보조 복제본을 주 가용성 그룹에 조인  
 모든 보조 복제본은 **JOIN** 옵션으로 **ALTER AVAILABILITY GROUP** 이(가) 있는 가용성 그룹에 조인되어야 합니다. 이 예제에서는 직접 시딩이 사용되었지 때문에  **GRANT CREATE ANY DATABASE** 옵션으로 **ALTER AVAILABILITY GROUP** 도 호출해야 합니다. 이를 통해 가용성 그룹이 데이터베이스를 만들고 주 복제본에서 자동으로 시딩을 시작할 수 있습니다.  
  
 이 예제에서는 보조 복제본 `server2`에서 다음 명령이 실행되어 가용성 그룹 `ag1` 에 조인됩니다. 그런 다음 가용성 그룹이 보조 가용성 그룹에 데이터베이스를 만들 수 있습니다.  
  
```tsql  
ALTER AVAILABILITY GROUP [ag1] JOIN   
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE  
GO  
```  
  
### 주 가용성 그룹에 대한 수신기 만들기  
 그런 다음 첫 번째 WSFC에 주 가용성 그룹에 대한 수신기를 추가합니다. 이 예제에서 수신기 이름은 `ag1-listener`입니다. 수신기를 만드는 방법은 [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)을 참조하세요.  
  
```  
ALTER AVAILABILITY GROUP [ag1]    
    ADD LISTENER 'ag1-listener' ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173);    
GO  
```  
  
### 두 번째 클러스터에 보조 가용성 그룹 만들기  
 그런 다음 두 번째 WSFC에서 두 번째 가용성 그룹인 `ag2`을(를) 만듭니다. 이 경우 주 가용성 그룹에서 자동으로 시딩되므로 데이터베이스를 지정하지 않습니다.  
  
```tsql  
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
>  보조 가용성 그룹은 동일한 데이터베이스 미러링 끝점(이 예제에서는 5022 포트)을 사용해야 합니다. 그렇지 않으면 로컬 장애 조치(failover) 후 복제가 중지됩니다.  
  
### 보조 복제본을 보조 가용성 그룹에 조인  
 이 예제에서는 보조 복제본 `server4`에서 다음 명령이 실행되어 가용성 그룹 `ag2` 에 조인됩니다. 그런 다음 가용성 그룹은 보조 가용성 그룹에 데이터베이스를 만들어 직접 시딩을 지원할 수 있습니다.  
  
```tsql  
ALTER AVAILABILITY GROUP [ag2] JOIN   
ALTER AVAILABILITY GROUP [ag2] GRANT CREATE ANY DATABASE  
GO  
```  
  
### 보조 가용성 그룹에 대한 수신기 만들기  
 그런 다음 두 번째 WSFC에 보조 가용성 그룹에 대한 수신기를 추가합니다. 이 예제에서 수신기 이름은 `ag2-listener`입니다. 수신기를 만드는 방법은 [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)을 참조하세요.  
  
```  
ALTER AVAILABILITY GROUP [ag2]    
    ADD LISTENER 'ag2-listener' ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173);    
GO  
```  
  
### 첫 번째 클러스터에 분산형 가용성 그룹 만들기  
 첫 번째 WSFC에서 분산형 가용성 그룹(이 예제에서의 이름은 `distributedag`)을 만듭니다. **DISTRIBUTED** 옵션으로 **CREATE AVAILABILITY GROUP** 명령을 사용합니다. **AVAILABILITY GROUP ON** 매개 변수는 멤버 가용성 그룹인 `ag1` 및 `ag2`를 지정합니다.  
  
```tsql  
CREATE AVAILABILITY GROUP [distributedag]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO   
```  
  
> [!NOTE]  
>  **LISTENER_URL**은 가용성 그룹의 데이터베이스 미러링 끝점과 함께 각 가용성 그룹에 대한 수신기를 지정합니다. 이 예제에서 수신기는 `5022` 포트(수신기를 만드는 데 사용된 `60173` 포트 아님)입니다.  
  
### 두 번째 클러스터에 분산형 가용성 그룹 조인  
 그런 다음 두 번째 WSFC에 분산형 가용성 그룹을 조인합니다.  
  
```tsql  
ALTER AVAILABILITY GROUP [distributedag]   
   JOIN   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO  
```  

  
## 보조 가용성 그룹에 대한 장애 조치(failover)  
 이 경우에는 수동 장애 조치(failover)만 지원됩니다. 다음 Transact-SQL 문은 `distributedag`라는 이름의 분산형 가용성 그룹에 장애 조치(failover)를 강제로 적용합니다.  


1. 보조 가용성 그룹에 대해 가용성 모드를 동기 커밋으로 설정합니다. 
    
      ```tsql  
      ALTER AVAILABILITY GROUP [distributedag] 
      MODIFY 
      AVAILABILITY GROUP ON
      'ag1' WITH  
         ( 
          LISTENER_URL = 'tcp://ag1-listener:5022',  
          AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = MANUAL, 
          SEEDING_MODE = MANUAL 
          ), 
      'ag2' WITH  
        ( 
        LISTENER_URL = 'tcp://ag2-listener:5022', 
        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
        FAILOVER_MODE = MANUAL, 
        SEEDING_MODE = MANUAL 
        );  
       
      ```  
  
1. 분산 가용성 그룹의 상태가 `SYNCHRONIZED`으로 변경될 때까지 대기합니다. 기본 가용성 그룹의 주 복제본을 호스트하는 SQL Server에서 다음 쿼리를 실행합니다. 
    
      ```tsql  
      SELECT ag.name
             , drs.database_id
             , drs.group_id
             , drs.replica_id
             , drs.synchronization_state_desc
             , drs.end_of_log_lsn 
        FROM sys.dm_hadr_database_replica_states drs,
        sys.availability_groups ag
          WHERE drs.group_id = ag.group_id;      
      ```  

    가용성 그룹 **synchronization_state_desc**가 `SYNCHRONIZED`가 되면 계속합니다. **synchronization_state_desc**가 `SYNCHRONIZED`가 아니면 변경될 때까지 5초 마다 명령을 실행합니다. **synchronization_state_desc** = `SYNCHRONIZED`가 될 때까지 진행하지 마세요. 

1. 기본 가용성 그룹의 주 복제본을 호스트하는 SQL Server에서 분산 가용성 그룹 역할을 `SECONDARY`로 설정합니다. 

      ```tsql
      ALTER AVAILABILITY GROUP distributedag SET (ROLE = SECONDARY); 
      ```  

    참고: 이 시점에서 분산 가용성 그룹은 사용할 수 없습니다.

1. 장애 조치(failover) 준비를 테스트합니다. 다음 쿼리를 실행합니다.

      ```tsql
      SELECT ag.name, 
             drs.database_id, 
             drs.group_id, 
             drs.replica_id, 
             drs.synchronization_state_desc, 
             drs.end_of_log_lsn 
      FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
      WHERE drs.group_id = ag.group_id; 
      ```  
    **synchronization_state_desc**가 `SYNCHRONIZED`이고, **end_of_log_lsn**이 두 가용성 그룹에 대해 동일할 경우 가용성 그룹은 장애 조치(failover)할 준비가 됩니다. 

1. 주 가용성 그룹에서 보조 가용성 그룹으로 장애 조치(failover)합니다. 보조 가용성 그룹의 주 복제본을 호스트하는 SQL Server에서 다음 명령을 실행합니다. 

      ```tsql
      ALTER AVAILABILITY GROUP distributedag FORCE_FAILOVER_ALLOW_DATA_LOSS; 
      ```  
      참고: 이 단계를 마치면 분산 가용성 그룹을 사용할 수 있게 됩니다.
      
위의 단계를 완료한 후 분산 가용성 그룹은 데이터 손실없이 장애 조치(failover)됩니다. 가용성 그룹이 지연이 발생하는 지리적 거리 위치에 있는 경우에는 가용성 모드를 다시 ASYNCHRONOUS_COMMIT으로 변경하는 것이 좋습니다. 
  
## 분산형 가용성 그룹 제거  
 다음 Transact-SQL 문은 `distributedag`라는 이름의 분산형 가용성 그룹을 삭제합니다.  
  
```tsql  
DROP AVAILABILITY GROUP [distributedag]  
```  

## 장애 조치(failover) 클러스터 인스턴스에서 분산 가용성 그룹 만들기

FCI(장애 조치 클러스터 인스턴스)에서 가용성 그룹을 사용하여 분산 가용성 그룹을 만들 수 있습니다. 이 경우 가용성 그룹 수신기가 필요 없습니다. FCI 인스턴스의 주 복제본에 VNN(가상 네트워크 이름)을 사용합니다. 다음 예제에서는 SQLFCIDAG 라는 분산 가용성 그룹을 보여 줍니다. 가용성 그룹으로 SQLFCIAG가 하나 있으며, SQLFCIAG에는 FCI 복제본이 2개 있습니다. 주 FCI 복제본의 VNN은 SQLFCIAG-1이며 보조 FCI 복제본의 VNN은 SQLFCIAG-2입니다. 재해 복구를 위해 분산 가용성 그룹에는 재해 복구를 위해 SQLAG-DR도 포함됩니다.

![배포되는 Always On 가용성 그룹](../../../database-engine/availability-groups/windows/media/always-on-availability-group-distributed.png)

 
 
 다음 DDL에서 이 분산 가용성 그룹을 만듭니다. 

```tsql  
CREATE AVAILABILITY GROUP [SQLFCIDAG]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
  'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-1:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      ),   
  'SQLAG-DR' WITH    
       (   
         LISTENER_URL = 'tcp://SQLAG-DR:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      );   
```  

수신기 URL은 주 FCI 인스턴스의 VNN입니다.

## 분산 가용성 그룹에서 FCI 수동 장애 조치(failover)

FCI 가용성 그룹을 수동으로 장애 조치하려면 수신기 URL의 변경 내용을 반영하도록 분산 가용성 그룹을 업데이트합니다. 예를 들어 SQLFCIAG의 기본 AG와 보조 AG에서 다음 DDL을 실행합니다.

```tsql  
ALTER AVAILABILITY GROUP [SQLFCIDAG]  
   MODIFY AVAILABILITY GROUP ON  
 'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-2:5022'
    )
```  
  
## 관련 항목:  
 [CREATE AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  