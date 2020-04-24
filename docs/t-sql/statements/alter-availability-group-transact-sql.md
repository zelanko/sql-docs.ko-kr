---
title: ALTER AVAILABILITY GROUP(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/02/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_AVAILABILITY_GROUP_TSQL
- ALTER_AVAILABILITY_TSQL
- ALTER AVAILABILITY GROUP
- ALTER AVAILABILITY
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- ALTER AVAILABILITY GROUP statement
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], Transact-SQL statements
ms.assetid: f039d0de-ade7-4aaf-8b7b-d207deb3371a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 36920dce9c6539d64097b2051494c90cf88b6a1f
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81634795"
---
# <a name="alter-availability-group-transact-sql"></a>ALTER AVAILABILITY GROUP(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 기존 Always On 가용성 그룹을 변경합니다. 대부분의 ALTER AVAILABILITY GROUP 인수는 현재 주 복제본에서만 지원됩니다. 그러나 JOIN, FAILOVER 및 FORCE_FAILOVER_ALLOW_DATA_LOSS 인수는 보조 복제본에서만 지원됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
ALTER AVAILABILITY GROUP group_name   
  {  
     SET ( <set_option_spec> )   
   | ADD DATABASE database_name   
   | REMOVE DATABASE database_name  
   | ADD REPLICA ON <add_replica_spec>   
   | MODIFY REPLICA ON <modify_replica_spec>  
   | REMOVE REPLICA ON <server_instance>  
   | JOIN  
   | JOIN AVAILABILITY GROUP ON <add_availability_group_spec> [ ,...2 ]  
   | MODIFY AVAILABILITY GROUP ON <modify_availability_group_spec> [ ,...2 ]  
   | GRANT CREATE ANY DATABASE  
   | DENY CREATE ANY DATABASE  
   | FAILOVER  
   | FORCE_FAILOVER_ALLOW_DATA_LOSS   
   | ADD LISTENER 'dns_name' ( <add_listener_option> )  
   | MODIFY LISTENER 'dns_name' ( <modify_listener_option> )  
   | RESTART LISTENER 'dns_name'  
   | REMOVE LISTENER 'dns_name'  
   | OFFLINE  
  }  
[ ; ]  
  
<set_option_spec> ::=   
    AUTOMATED_BACKUP_PREFERENCE = { PRIMARY | SECONDARY_ONLY| SECONDARY | NONE }  
  | FAILURE_CONDITION_LEVEL  = { 1 | 2 | 3 | 4 | 5 }   
  | HEALTH_CHECK_TIMEOUT = milliseconds  
  | DB_FAILOVER  = { ON | OFF }   
  | DTC_SUPPORT  = { PER_DB | NONE }  
  | REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = { integer }
  
<server_instance> ::=   
 { 'system_name[\instance_name]' | 'FCI_network_name[\instance_name]' }  
  
<add_replica_spec>::=  
  <server_instance> WITH  
    (  
       ENDPOINT_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT | CONFIGURATION_ONLY },  
       FAILOVER_MODE = { AUTOMATIC | MANUAL }   
       [ , <add_replica_option> [ ,...n ] ]  
    )   
  
  <add_replica_option>::=  
       SEEDING_MODE = { AUTOMATIC | MANUAL }  
     | BACKUP_PRIORITY = n  
     | SECONDARY_ROLE ( {   
            [ ALLOW_CONNECTIONS = { NO | READ_ONLY | ALL } ]   
        [,] [ READ_ONLY_ROUTING_URL = 'TCP://system-address:port' ]  
     } )  
     | PRIMARY_ROLE ( {   
            [ ALLOW_CONNECTIONS = { READ_WRITE | ALL } ]   
        [,] [ READ_ONLY_ROUTING_LIST = { ( '<server_instance>' [ ,...n ] ) | NONE } ]  
        [,] [ READ_WRITE_ROUTING_URL = { ( '<server_instance>' ) ] 
     } )  
     | SESSION_TIMEOUT = integer
  
<modify_replica_spec>::=  
  <server_instance> WITH  
    (    
       ENDPOINT_URL = 'TCP://system-address:port'   
     | AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }   
     | FAILOVER_MODE = { AUTOMATIC | MANUAL }   
     | SEEDING_MODE = { AUTOMATIC | MANUAL }   
     | BACKUP_PRIORITY = n  
     | SECONDARY_ROLE ( {   
          ALLOW_CONNECTIONS = { NO | READ_ONLY | ALL }   
        | READ_ONLY_ROUTING_URL = 'TCP://system-address:port'   
          } )  
     | PRIMARY_ROLE ( {   
          ALLOW_CONNECTIONS = { READ_WRITE | ALL }   
        | READ_ONLY_ROUTING_LIST = { ( '<server_instance>' [ ,...n ] ) | NONE }   
          } )  
     | SESSION_TIMEOUT = seconds  
    )   
  
<add_availability_group_spec>::=  
 <ag_name> WITH  
    (  
       LISTENER_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT },  
       FAILOVER_MODE = MANUAL,  
       SEEDING_MODE = { AUTOMATIC | MANUAL }  
    )  
  
<modify_availability_group_spec>::=  
 <ag_name> WITH  
    (  
       LISTENER = 'TCP://system-address:port'  
       | AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }  
       | SEEDING_MODE = { AUTOMATIC | MANUAL }  
    )  
  
<add_listener_option> ::=  
   {  
      WITH DHCP [ ON ( <network_subnet_option> ) ]  
    | WITH IP ( { ( <ip_address_option> ) } [ , ...n ] ) [ , PORT = listener_port ]  
   }  
  
  <network_subnet_option> ::=  
     'ipv4_address', 'ipv4_mask'    
  
  <ip_address_option> ::=  
     {   
        'four_part_ipv4_address', 'four_part_ipv4_mask'  
      | 'ipv6_address'  
     }  
  
<modify_listener_option>::=  
    {  
       ADD IP ( <ip_address_option> )   
     | PORT = listener_port  
    }  
  
```  
  
## <a name="arguments"></a>인수  
 *group_name*  
 새 가용성 그룹의 이름을 지정합니다. *group_name*은 유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자이고 WSFC 클러스터의 모든 가용성 그룹에서 고유해야 합니다.  
  
 AUTOMATED_BACKUP_PREFERENCE **=** { PRIMARY | SECONDARY_ONLY| SECONDARY | NONE }  
 백업을 수행할 위치를 선택할 때 백업 작업에서 주 복제본을 평가하는 방식에 관한 기본 설정을 지정합니다. 자동화된 백업 기본 설정을 고려하도록 지정한 백업 작업을 스크립팅할 수 있습니다. 기본 설정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 적용하는 것이 아니므로 임시 백업에 영향을 미치지 않는다는 것을 이해해야 합니다.  
  
 주 복제본에서만 지원되며,  
  
 값은 다음과 같습니다.  
  
 PRIMARY  
 백업이 항상 주 복제본에서 수행되도록 지정합니다. 이 옵션은 백업이 보조 복제본에서 실행될 때 지원되지 않는 차등 백업 만들기와 같은 백업 기능이 필요한 경우에 유용합니다.  
  
> [!IMPORTANT]  
>  로그 전달을 사용하여 가용성 그룹의 보조 데이터베이스를 준비하려는 경우 모든 보조 데이터베이스가 준비되고 가용성 그룹에 조인될 때까지 자동화된 백업 기본 설정을 **주** 로 설정합니다.  
  
 SECONDARY_ONLY  
 백업이 주 복제본에서 수행되지 않도록 지정합니다. 주 복제본이 유일한 온라인 복제본인 경우에는 백업이 수행되지 않아야 합니다.  
  
 SECONDARY  
 백업이 보조 복제본에서 수행되도록 지정합니다. 주 복제본이 유일한 온라인 복제본인 경우는 예외로, 이 경우에는 백업이 주 복제본에서 수행되어야 합니다. 기본 동작입니다.  
  
 없음  
 백업을 수행할 복제본을 선택할 때 백업 작업에서 가용성 복제본의 역할을 무시하도록 지정합니다. 백업 작업에서는 각 가용성 복제본의 작동 상태 및 연결 상태와 함께 백업 우선 순위 등의 기타 요인을 평가할 수 있습니다.  
  
> [!IMPORTANT]  
>  AUTOMATED_BACKUP_PREFERENCE 설정은 적용되지 않습니다. 이 기본 설정의 해석은 지정된 가용성 그룹의 데이터베이스에 대한 백업 작업으로 스크립팅하는 논리(있는 경우)에 따라 달라집니다. 자동화된 백업 기본 설정은 임시 백업에는 영향을 미치지 않습니다. 자세한 내용은 [가용성 복제본에 백업 구성&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)을 참조하세요.  
  
> [!NOTE]  
>  기존 가용성 그룹의 자동화된 백업 기본 설정을 보려면 [sys.availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) 카탈로그 뷰의 **automated_backup_preference** 또는 **automated_backup_preference_desc** 열을 선택합니다. 또한 [sys.fn_hadr_backup_is_preferred_replica&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md)를 사용하여 기본 백업 복제본을 확인할 수 있습니다.  이 함수는 `AUTOMATED_BACKUP_PREFERENCE = NONE`인 경우에도 복제본 하나 이상에 대해 항상 1을 반환합니다.  
  
 FAILURE_CONDITION_LEVEL **=** { 1 | 2 | **3** | 4 | 5 }  
 이 가용성 그룹에 대한 자동 장애 조치(failover)를 트리거할 오류 상태를 지정합니다. FAILURE_CONDITION_LEVEL은 그룹 수준에서 설정되지만 동기-커밋 가용성 모드(AVAILABILITY_MODE **=** SYNCHRONOUS_COMMIT)에 대해 구성된 가용성 복제본에서만 적절합니다. 또한 오류 상태는 주 복제본과 보조 복제본 모두 자동 장애 조치 모드(FAILOVER_MODE **=** AUTOMATIC)에 대해 구성되고 보조 복제본이 현재 주 복제본과 동기화된 경우에만 자동 장애 조치(failover)를 트리거할 수 있습니다.  
  
 주 복제본에서만 지원되며,  
  
 오류 상태 수준(1–5)의 범위는 가장 낮은 제한 수준 1에서 가장 높은 제한 수준 5까지입니다. 특정 상태 수준은 그보다 낮은 모든 제한 수준을 포함합니다. 따라서 가장 엄격한 상태 수준 5에는 그보다 낮은 네 개의 제한 상태 수준(1~4)이 포함되고, 수준 4에는 수준 1~3이 포함됩니다. 다음 표에서는 각 수준에 해당하는 오류 상태를 설명합니다.  
  
|Level|오류 상태|  
|-----------|-----------------------|  
|1|다음과 같은 경우 자동 장애 조치(failover)를 시작하도록 지정합니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 다운된 경우<br /><br /> 서버 인스턴스로부터 ACK를 받지 못해 WSFC 클러스터에 연결할 가용성 그룹의 임대가 만료된 경우. 자세한 내용은 [작동 방법: SQL Server Always On 임대 시간 제한](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx)을 참조하세요.|  
|2|다음과 같은 경우 자동 장애 조치(failover)를 시작하도록 지정합니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 클러스터에 연결되어 있지 않고 가용성 그룹의 사용자 지정 HEALTH_CHECK_TIMEOUT 임계값이 초과된 경우<br /><br /> 가용성 복제본이 오류 상태에 있는 경우|  
|3|분리된 spinlock, 중대한 쓰기 액세스 위반 또는 과도한 덤프와 같이 심각한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부 오류가 발생할 경우 자동 장애 조치(failover)를 시작하도록 지정합니다.<br /><br /> 기본 동작입니다.|  
|4|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부 리소스 풀에서 지속적인 메모리 부족 상태와 같은 일반적인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부 오류가 발생할 경우 자동 장애 조치(failover)를 시작하도록 지정합니다.|  
|5|다음과 같은 오류 상태가 발생할 경우 자동 장애 조치(failover)를 시작하도록 지정합니다.<br /><br /> SQL 엔진 작업자 스레드가 소진된 경우<br /><br /> 해결할 수 없는 교착 상태가 발견된 경우|  
  
> [!NOTE]  
>  클라이언트 요청에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 응답이 없는 것은 가용성 그룹과 관련이 없습니다.  
  
 FAILURE_CONDITION_LEVEL 및 HEALTH_CHECK_TIMEOUT 값은 지정된 그룹에 대한 *유연한 장애 조치(failover) 정책*을 정의합니다. 유연한 장애 조치(failover) 정책을 통해 자동 장애 조치(failover)를 수행해야 하는 상태를 세부적으로 제어할 수 있습니다. 자세한 내용은 [가용성 그룹 자동 장애 조치에 대한 유연한 장애 조치 정책&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md)을 참조하세요.  
  
 HEALTH_CHECK_TIMEOUT **=** *milliseconds*  
 [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) 시스템 저장 프로시저에서 서버 상태 정보를 반환할 때까지 허용되는 대기 시간(밀리초)을 지정합니다. 이 시간이 경과하면 WSFC 클러스터에서는 서버 인스턴스가 느리거나 응답하지 않는 것으로 간주합니다. HEALTH_CHECK_TIMEOUT은 그룹 수준에서 설정되지만 자동 장애 조치(failover)를 지원하는 동기-커밋 가용성 모드(AVAILABILITY_MODE **=** SYNCHRONOUS_COMMIT)에 대해 구성된 가용성 복제본에서만 적절합니다.  또한 상태 확인 시간 제한은 복제본과 보조 복제본 모두 자동 장애 조치 모드(FAILOVER_MODE **=** AUTOMATIC)에 대해 구성되고 보조 복제본이 현재 주 복제본과 동기화된 경우에만 자동 장애 조치(failover)를 트리거할 수 있습니다.  
  
 기본 HEALTH_CHECK_TIMEOUT 값은 30,000밀리초(30초)입니다. 최소값은 15,000밀리초(15초)이고 최대값은 4,294,967,295밀리초입니다.  
  
 주 복제본에서만 지원되며,  
  
> [!IMPORTANT]  
>  **sp_server_diagnostics** 는 데이터베이스 수준에서 상태 확인을 수행하지 않습니다.  
  
 DB_FAILOVER  **=** { ON | OFF }  
 주 복제본의 데이터베이스가 오프라인 상태일 때 수행할 응답을 지정합니다. 가용성 그룹의 데이터베이스에 대한 ONLINE 이외의 모든 상태가 ON으로 설정되는 경우 자동 장애 조치(failover)를 트리거합니다. 이 옵션이 OFF로 설정되는 경우 인스턴스의 상태만 자동 장애 조치(failover)를 트리거하는 데 사용됩니다.  
 
 이 설정에 대한 자세한 내용은 [데이터베이스 수준 상태 검색 옵션](../../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md)을 참조하세요. 

DTC_SUPPORT  **=** { PER_DB | NONE }  
이 가용성 그룹에 대한 분산 트랜잭션을 사용할 수 있는지 여부를 지정합니다. 분산 트랜잭션은 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서 시작하는 가용성 그룹 데이터베이스에 대해서만 지원되고 데이터베이스 간 트랜잭션은 [!INCLUDE[ssSQL16](../../includes/sssql15-md.md)] SP2에서 시작하는 경우에만 지원됩니다. `PER_DB`는 이러한 트랜잭션을 지원하는 가용성 그룹을 만들고 가용성 그룹의 데이터베이스와 관련된 데이터베이스 간 트랜잭션을 분산 트랜잭션으로 자동 승격합니다. `NONE`은 분산 트랜잭션에 대한 데이터베이스 간 트랜잭션의 자동 승격을 방지하고 DTC에서 안정적인 RMID로 데이터베이스를 등록하지 않습니다. `NONE` 설정을 사용하면 분산 트랜잭션을 방지하지 않지만 일부 상황에서는 데이터베이스 장애 조치(failover) 및 자동 복구가 성공하지 못할 수 있습니다. 자세한 내용은 [Always On 가용성 그룹 및 데이터베이스 미러링에 대한 데이터베이스 간 트랜잭션 및 분산 트랜잭션&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)를 참조하세요. 
 
> [!NOTE]
> 가용성 그룹의 DTC_SUPPORT 설정 변경에 대한 지원은 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 서비스 팩 2에서 도입되었습니다. 이 옵션은 이전 버전과 함께 사용할 수 없습니다. 이전 버전의 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]에서 이 설정을 변경하려면 가용성 그룹을 다시 드롭하고 만들어야 합니다.
 
 REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT   
 SQL Server 2017에서 도입되었습니다. 주 복제본이 트랜잭션을 커밋하기 전에 커밋하는 데 필요한 최소 동기 보조 복제본 수를 설정하는 데 사용됩니다. SQL Server 트랜잭션이 트랜잭션 로그가 보조 복제본의 최소 수에서 업데이트될 때까지 대기함을 보장합니다. 기본값은 0으로 SQL Server 2016과 동일한 동작을 제공합니다. 최솟값은 0입니다. 최댓값은 복제본 수에서 1을 뺀 수입니다. 이 옵션은 동기 커밋 모드의 복제본과 관련이 있습니다. 복제본이 동기 커밋 모드에 있는 경우 주 복제본의 쓰기는 보조 동기 복제본의 쓰기가 복제본 데이터베이스 트랜잭션 로그에 커밋될 때까지 기다립니다. 보조 동기 복제본을 호스팅하는 SQL Server가 응답을 중지하는 경우 주 복제본을 호스팅하는 SQL Server는 보조 복제본을 NOT SYNCHRONIZED로 표시하고 진행합니다. 응답하지 않는 데이터베이스가 다시 온라인 상태가 되면 "동기화 되지 않음" 상태에 되고 복제본은 주 복제본이 다시 동기화할 수 있을 때까지 비정상으로 표시됩니다. 이 설정은 주 복제본이 최소 복제본 수가 각 트랜잭션을 커밋할 때까지 진행되지 않음을 보장합니다. 최소 복제본 수를 사용할 수 없는 경우 주 복제본에서 커밋에 실패합니다. 클러스터 형식 `EXTERNAL`의 경우 가용성 그룹이 클러스터 리소스에 추가될 때 설정이 변경됩니다. [가용성 그룹 구성을 위한 고가용성 및 데이터 보호](../../linux/sql-server-linux-availability-group-ha.md)를 참조하세요.
  
 ADD DATABASE *database_name*  
 가용성 그룹에 추가할 하나 이상의 사용자 데이터베이스 목록을 지정합니다. 이러한 데이터베이스는 현재 주 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 있어야 합니다. 하나의 가용성 그룹에 여러 개의 데이터베이스를 지정할 수 있지만 각 데이터베이스는 하나의 가용성 그룹에만 속할 수 있습니다. 가용성 그룹에서 지원할 수 있는 데이터베이스 형식에 대한 자세한 내용은 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)을 참조하세요. 가용성 그룹에 이미 속해 있는 로컬 데이터베이스를 확인하려면 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 **replica_id** 열을 확인합니다.  
  
 주 복제본에서만 지원되며,  
  
> [!NOTE]  
>  가용성 그룹을 만든 다음에는 보조 복제본을 호스팅하는 각 서버 인스턴스에 연결하여 각각의 보조 데이터베이스를 준비하고 이를 가용성 그룹에 조인해야 합니다. 자세한 내용은 [Always On 보조 데이터베이스에서 데이터 이동 시작&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)를 참조하세요.  
  
 REMOVE DATABASE *database_name*  
 지정된 주 데이터베이스 및 해당 보조 데이터베이스를 가용성 그룹에서 제거합니다. 주 복제본에서만 지원되며,  
  
 가용성 그룹에서 가용성 데이터베이스를 제거한 후에 권장되는 후속 작업에 대한 자세한 내용은 [가용성 그룹에서 주 데이터베이스 제거&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md)를 참조하세요.  
  
 ADD REPLICA ON  
 가용성 그룹의 보조 복제본을 호스트하는 1~8개의 SQL Server 인스턴스를 지정합니다.  각 복제본은 서버 인스턴스 주소 다음에 WITH(...) 절을 사용하여 지정합니다.  
  
 주 복제본에서만 지원되며,  
  
 모든 새 보조 복제본을 가용성 그룹에 조인해야 합니다. 자세한 내용은 이 섹션의 뒷부분에 나오는 JOIN 옵션에 대한 설명을 참조하십시오.  
  
 \<server_instance>  
 복제본의 호스트인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스 주소를 지정합니다. 주소 형식은 인스턴스가 기본 인스턴스이거나 명명된 인스턴스인지 그리고 독립형 인스턴스이거나 FCI(장애 조치(failover) 클러스터 인스턴스)인지에 따라 달라집니다. 구문은 다음과 같습니다.  
  
 { '*system_name*[\\*instance_name*]' | '*FCI_network_name*[\\*instance_name*]' }  
  
 이 주소의 구성 요소는 다음과 같습니다.  
  
 *system_name*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 대상 인스턴스가 있는 컴퓨터 시스템의 NetBIOS 이름입니다. 이 컴퓨터는 WSFC 노드여야 합니다.  
  
 *FCI_network_name*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터에 액세스하는 데 사용되는 네트워크 이름입니다. 서버 인스턴스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]장애 조치(failover) 파트너로 참여하는 경우 이 인수를 사용합니다. FCI 서버 인스턴스에서 SELECT [@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md)을 실행하면 전체 복제본 이름인 '*FCI_network_name*[\\*instance_name*]' 문자열 전체가 반환됩니다.  
  
 *instance_name*  
 *system_name* 또는 *FCI_network_name*으로 호스팅되고 Always On을 사용하도록 설정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다. 기본 서버 인스턴스의 경우 *instance_name* 은 선택 사항입니다. 인스턴스 이름은 대/소문자를 구분하지 않습니다. 독립 실행형 서버 인스턴스에서 이 값 이름은 SELECT [@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md)을 실행할 때 반환되는 값과 동일합니다.  
  
 \  
 *system_name* 또는 *FCI_network_name*에서 구분하기 위해 *instance_name*을 지정하는 경우에만 사용되는 구분 기호입니다.  
  
 WSFC 노드 및 서버 인스턴스의 필수 조건에 대한 자세한 내용은 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)을 참조하세요.  
  
 ENDPOINT_URL ='TCP://*system-address*:*port*'  
 추가 또는 수정 중인 가용성 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 [데이터베이스 미러링 엔드포인트](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)에 대한 URL 경로를 지정합니다.  
  
 ENDPOINT_URL은 ADD REPLICA ON 절에서는 필수적이고 MODIFY REPLICA ON 절에서는 선택적입니다.  자세한 내용은 [가용성 복제본 추가 또는 수정 시 엔드포인트 URL 지정&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)을 참조하세요.  
  
 **'** TCP **://** _system-address_ **:** _port_ **'**  
 엔드포인트 URL 또는 읽기 전용 라우팅 URL을 지정하기 위한 URL을 지정합니다. URL 매개 변수는 다음과 같습니다.  
  
 *system-address*  
 대상 컴퓨터 시스템을 명확하게 식별하는 시스템 이름, 정규화된 도메인 이름 또는 IP 주소 등의 문자열입니다.  
  
 *port*  
 서버 인스턴스(ENDPOINT_URL 옵션의 경우)의 미러링 엔드포인트와 연관된 포트 번호 또는 서버 인스턴스의 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 사용되는 포트 번호(READ_ONLY_ROUTING_URL 옵션의 경우)입니다.  
  
 AVAILABILITY_MODE **=** { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT | CONFIGURATION_ONLY }  
 주 복제본이 지정된 주 데이터베이스의 트랜잭션을 커밋하기 전에 보조 복제본이 디스크에 로그 레코드 확정(쓰기)을 확인할 때까지 주 복제본이 기다려야 하는지 여부를 지정합니다. 동일한 주 복제본의 서로 다른 데이터베이스에 있는 트랜잭션을 개별적으로 커밋할 수 있습니다.  
  
 SYNCHRONOUS_COMMIT  
 트랜잭션이 이 보조 복제본에서 확정될 때까지 주 복제본이 트랜잭션을 커밋하지 않고 기다리도록 지정합니다(동기-커밋 모드). 주 복제본을 포함하여 최대 세 개의 복제본에 대해 SYNCHRONOUS_COMMIT을 지정할 수 있습니다.  
  
 ASYNCHRONOUS_COMMIT  
 이 보조 복제본이 로그를 확정할 때까지 기다리지 않고 주 복제본이 트랜잭션을 커밋하도록 지정합니다(동기-커밋 가용성 모드). 주 복제본을 포함하여 최대 다섯 개의 가용성 복제본에 대해 ASYNCHRONOUS_COMMIT을 지정할 수 있습니다.  

 CONFIGURATION_ONLY는 주 복제본이 가용성 그룹 구성 메타데이터를 이 복제본의 master 데이터베이스로 동기적으로 커밋하도록 지정합니다. 복제본에는 사용자 데이터가 포함되지 않습니다. 이 옵션:

- Express Edition을 포함하여 SQL Server의 모든 버전에서 호스팅할 수 있습니다.
- CONFIGURATION_ONLY 복제본의 데이터 미러링 엔드포인트는 `WITNESS` 형식이 되어야 합니다.
- 변경될 수 없습니다.
- `CLUSTER_TYPE = WSFC`인 경우 유효하지 않습니다. 

   자세한 내용은 [구성 복제본](../../linux/sql-server-linux-availability-group-ha.md)을 참조하세요.
    
 AVAILABILITY_MODE는 ADD REPLICA ON 절에서는 필수적이고 MODIFY REPLICA ON 절에서는 선택적입니다. 자세한 내용은 [가용성 모드&#40;Always On 가용성 그룹&#41;](../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)라는 프로세스에서 서로 바꿀 수 있습니다.  
  
 FAILOVER_MODE **=** { AUTOMATIC | MANUAL }  
 정의하는 가용성 복제본의 장애 조치(failover) 모드를 지정합니다.  
  
 AUTOMATIC  
 자동 장애 조치(failover)를 사용하도록 설정합니다. AUTOMATIC은 AVAILABILITY_MODE = SYNCHRONOUS_COMMIT을 지정한 경우에만 지원됩니다. 주 복제본을 포함하여 세 개의 가용성 복제본에 대해 AUTOMATIC을 지정할 수 있습니다.  
  
> [!NOTE]  
>  SQL Server 2016 이전에는 주 복제본을 포함하여 두 개의 자동 장애 조치(failover) 복제본으로 제한되었습니다.
  
> [!NOTE]  
>  SQL Server FCI(장애 조치(Failover) 클러스터 인스턴스)는 가용성 그룹에 따라 AlwaysOn 자동 장애 조치(Failover)를 지원하지 않으므로 FCI에서 호스팅하는 모든 가용성 복제본은 수동 장애 조치(Failover)에 대해서만 구성될 수 있습니다.  
  
 MANUAL  
 데이터베이스 관리자에 의한 수동 장애 조치(failover) 또는 강제 수동 장애 조치(failover)(*강제 장애 조치(failover)* )를 사용하도록 설정합니다.  
  
 FAILOVER_MODE는 ADD REPLICA ON 절에서는 필수적이고 MODIFY REPLICA ON 절에서는 선택적입니다. 수동 장애 조치(failover)에는 데이터 손실이 없는 수동 장애 조치(failover)와 데이터가 손실될 수 있는 강제 장애 조치(failover)의 두 가지 유형이 있으며 이 두 유형은 서로 다른 조건에서 지원됩니다.  자세한 내용은 이 항목의 뒷부분에 나오는 [장애 조치(Failover) 및 장애 조치(Failover) 모드&#40;Always On 가용성 그룹&#41;](../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)를 참조하세요.  
  
 SEEDING_MODE **=** { AUTOMATIC | MANUAL }  
 보조 복제본을 처음에 시드하는 방법을 지정합니다.  
  
 AUTOMATIC  
 직접 시드를 활성화합니다. 이 메서드는 네트워크를 통해 보조 복제본을 시드합니다. 이 메서드를 사용하면 복제본에서 주 데이터베이스의 복사본을 백업 및 복원할 필요가 없습니다.  
  
> [!NOTE]  
>  직접 시드를 위해 **GRANT CREATE ANY DATABASE** 옵션으로 **ALTER AVAILABILITY GROUP**을 호출하여 각 보조 복제본에서 데이터베이스 생성을 허용해야 합니다.  
  
 MANUAL  
 수동 시드(기본값)를 지정합니다. 이 메서드를 사용하면 주 복제본에서 데이터베이스의 백업을 만들고 보조 복제본에서 해당 백업을 수동으로 복원해야 합니다.  
  
 BACKUP_PRIORITY **=** _n_  
 이 복제본에 대한 백업을 수행하기 위한 우선 순위를 지정하며 동일한 가용성 그룹의 다른 복제본을 기준으로 합니다. 이 값은 0에서 100  사이의 정수입니다. 이러한 값에는 다음과 같은 의미가 있습니다.  
  
-   1..100은 가용성 복제본이 백업 수행을 위해 선택될 수 있음을 나타냅니다. 1은 가장 낮은 우선 순위를 나타내고 100은 가장 높은 우선 순위를 나타냅니다. BACKUP_PRIORITY = 1이면 현재 사용 가능한 더 높은 우선 순위의 가용성 복제본이 없는 경우에만 해당 가용성 복제본이 백업 수행을 위해 선택됩니다.  
  
-   0은 이 가용성 복제본이 백업 수행을 위해 선택될 수 없음을 나타냅니다. 이 값은 예를 들어 백업을 장애 조치할 대상으로 사용하지 않을 원격 가용성 복제본의 경우에 유용합니다.  
  
 자세한 내용은 [활성 보조 복제본: 보조 복제본에 백업&#40;Always On 가용성 그룹&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)을 참조하세요.  
  
 SECONDARY_ROLE **(** ... **)**  
 이 가용성 복제본이 현재 보조 역할을 소유하는 경우(즉, 보조 복제본일 때마다) 적용되는 역할별 설정을 지정합니다. 괄호 안에 보조 역할 옵션 중 하나 또는 모두를 지정합니다. 둘 다 지정할 경우 쉼표로 구분된 목록을 사용합니다.  
  
 보조 역할 옵션은 다음과 같습니다.  
  
 ALLOW_CONNECTIONS **=** { NO | READ_ONLY | ALL }  
 보조 역할, 즉 보조 복제본의 역할을 수행하는 지정된 가용성 복제본의 데이터베이스에서 클라이언트의 연결을 허용할 수 있는지 여부를 다음 중 하나로 지정합니다.  
  
 아니요  
 이 복제본의 보조 데이터베이스에 대한 사용자 연결이 허용되지 않습니다. 즉, 읽기 액세스가 가능하지 않습니다. 기본 동작입니다.  
  
 READ_ONLY  
 애플리케이션 의도 속성이 **ReadOnly**로 설정된 경우에만 보조 복제본의 데이터베이스에 연결할 수 있습니다. 이 속성에 대한 자세한 내용은 [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)을 참조하십시오.  
  
 ALL  
 보조 복제본의 데이터베이스에 대해 읽기 전용 액세스를 위한 모든 연결이 허용됩니다.  
  
 자세한 내용은 [활성 보조 복제본: 읽기 가능한 보조 복제본&#40;Always On 가용성 그룹&#41;](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)을 참조하세요.  
  
 READ_ONLY_ROUTING_URL **='** TCP **://** _system-address_ **:** _port_ **'**  
 이 가용성 복제본에 대한 읽기 전용 연결 요청을 라우팅하는 데 사용할 URL을 지정합니다. 이 URL은 SQL Server 데이터베이스 엔진이 수신하는 URL입니다. 일반적으로 SQL Server 데이터베이스 엔진의 기본 인스턴스는 TCP 포트 1433에서 수신합니다.  
  
 명명된 인스턴스의 경우 [sys.dm_tcp_listener_states](../../relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql.md) 동적 관리 뷰의 **port** 및 **type_desc** 열을 쿼리하여 포트 번호를 가져올 수 있습니다. 서버 인스턴스는 Transact-SQL 수신기를 사용합니다(**type_desc='TSQL'** ).  
  
 가용성 복제본에 대한 읽기 전용 라우팅 URL을 계산하는 방법에 대한 자세한 내용은 [Always On에 대한 read_only_routing_url 계산](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-Always%20On.aspx)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 명명된 인스턴스의 경우 Transact-SQL 수신기가 특정 포트를 사용하도록 구성되어야 합니다. 자세한 내용은 [특정 TCP 포트로 수신하도록 서버 구성&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)을 참조하세요.  
  
 PRIMARY_ROLE **(** ... **)**  
 이 가용성 복제본이 현재 주 역할을 소유하는 경우(즉, 주 복제본일 때마다) 적용되는 역할별 설정을 지정합니다. 괄호 안에 주 역할 옵션 중 하나 또는 모두를 지정합니다. 둘 다 지정할 경우 쉼표로 구분된 목록을 사용합니다.  
  
 주 역할 옵션은 다음과 같습니다.  
  
 ALLOW_CONNECTIONS **=** { READ_WRITE | ALL }  
 주 역할, 즉 주 복제본의 역할을 수행하는 지정된 가용성 복제본의 데이터베이스에서 허용할 수 있는 클라이언트 연결 유형을 다음 중 하나로 지정합니다.  
  
 READ_WRITE  
 애플리케이션 의도 연결 속성이 **ReadOnly** 로 설정된 연결은 허용되지 않습니다.  애플리케이션 의도 속성이 **ReadWrite** 로 설정되었거나 애플리케이션 의도 연결 속성이 설정되지 않은 경우에는 연결이 허용됩니다. 애플리케이션 의도 연결 속성에 대한 자세한 내용은 [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)을 참조하십시오.  
  
 ALL  
 주 복제본의 데이터베이스에 대한 모든 연결이 허용됩니다. 기본 동작입니다.  
  
 READ_ONLY_ROUTING_LIST **=** { **('** \<server_instance> **'** [ **,** ...*n* ] **)** | NONE }  
 보조 역할로 실행 중일 때 다음과 같은 요구 사항을 충족하는 이 가용성 그룹에 대한 가용성 복제본을 호스팅하는 서버 인스턴스의 쉼표로 구분된 목록을 지정합니다.  
  
-   모든 연결 또는 읽기 전용 연결을 허용하도록 구성되어야 합니다(위에서 SECONDARY_ROLE 옵션의 ALLOW_CONNECTIONS 인수 참조).  
  
-   읽기 전용 라우팅 URL을 정의해야 합니다(위에서 SECONDARY_ROLE 옵션의 READ_ONLY_ROUTING_URL 인수 참조).  
  
 READ_ONLY_ROUTING_LIST 값은 다음과 같습니다.  
  
 \<server_instance>  
 보조 역할로 실행 중일 때 읽기 가능한 보조 복제본인 가용성 그룹에 대한 호스트인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 주소를 지정합니다.  
  
 읽기 가능한 보조 복제본을 호스팅할 수도 있는 모든 서버 인스턴스를 지정하려면 쉼표로 구분된 목록을 사용합니다. 읽기 전용 라우팅은 서버 인스턴스가 목록에 지정된 순서에 따릅니다. 복제본의 읽기 전용 라우팅 목록에 복제본의 호스트 서버 인스턴스를 포함한 경우 읽기 전용 연결이 보조 복제본(사용 가능한 경우)으로 이동할 수 있도록 일반적으로 이 서버 인스턴스를 목록 끝에 두는 것이 좋습니다.  
  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 읽기 가능한 보조 복제본에서 읽기 전용 요청을 부하 분산할 수 있습니다. 복제본을 읽기 전용 라우팅 목록 내의 중첩된 괄호 쌍에 배치하여 이를 지정합니다. 자세한 내용 및 예제는 [읽기 전용 복제본에 대한 부하 분산 구성](../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md#loadbalancing)을 참조하세요.  
  
 없음  
 이 가용성 복제본이 주 복제본인 경우 읽기 전용 라우팅이 지원되지 않도록 지정합니다. 기본 동작입니다. 이 값에 MODIFY REPLICA ON을 사용하면 기존 목록(있는 경우)이 비활성화됩니다.  
  
 SESSION_TIMEOUT **=** _seconds_  
 세션 제한 시간(초)을 지정합니다. 이 옵션을 지정하지 않으면 기본적으로 제한 시간은 10초로 설정됩니다. 최소값은 5초입니다.  
  
> [!IMPORTANT]  
>  제한 시간을 10초 이상으로 유지하는 것이 좋습니다.  
  
 세션 제한 시간에 대한 자세한 내용은 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)를 참조하세요.  
  
 MODIFY REPLICA ON  
 가용성 그룹의 복제본을 수정합니다. 수정할 복제본 목록에는 각 복제본에 대한 서버 인스턴스 주소와 WITH(...) 절이 포함됩니다.  
  
 주 복제본에서만 지원되며,  
  
 REMOVE REPLICA ON  
 지정한 보조 복제본을 가용성 그룹에서 제거합니다. 현재 주 복제본은 가용성 그룹에서 제거할 수 없습니다. 제거하면 해당 복제본이 더 이상 데이터를 받지 못합니다. 보조 데이터베이스는 가용성 그룹에서 제거되고 RESTORING 상태로 전환됩니다.  
  
 주 복제본에서만 지원되며,  
  
> [!NOTE]  
>  사용할 수 없거나 오류가 발생한 복제본을 제거할 경우 이 복제본은 다시 온라인 상태가 되어도 더 이상 가용성 그룹에 속하지 않습니다.  
  
 JOIN  
 로컬 서버 인스턴스에서 지정된 가용성 그룹의 보조 복제본을 호스팅하도록 합니다.  
  
 가용성 그룹에 아직 조인되지 않은 보조 복제본에서만 지원됩니다.  
  
 자세한 내용은 [가용성 그룹에 보조 복제본 조인&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)또는 PowerShell을 사용하여 Always On 가용성 그룹에 보조 데이터베이스를 조인하는 방법에 대해 설명합니다.  
  
 FAILOVER  
데이터 손실 없이 연결된 보조 복제본으로 가용성 그룹의 수동 장애 조치(failover)를 시작합니다. 주 복제본을 호스팅하는 복제본은 *장애 조치(failover) 대상*입니다.  장애 조치(failover) 대상이 주 역할을 맡고 각 데이터베이스의 복사본을 복구하여 이를 온라인 상태의 새 주 데이터베이스로 만듭니다. 이전 주 복제본은 동시에 보조 역할로 전환되고 해당 데이터베이스는 보조 데이터베이스가 되고 즉시 일시 정지됩니다. 잠재적으로 이러한 역할은 일련의 오류로 인해 상태가 앞뒤로 전환될 수 있습니다.  
  
 현재 주 복제본과 동기화된 동기-커밋 보조 복제본에서만 지원됩니다. 보조 복제본을 동기화하기 위해서는 주 복제본도 동기-커밋 모드로 실행되어야 합니다.  
  
> [!NOTE]  
>  장애 조치(failover) 명령은 장애 조치(failover) 대상에서 해당 명령을 수락하는 즉시 반환하지만 데이터베이스 복구는 가용성 그룹의 장애 조치가 끝난 후 비동기로 수행됩니다.  
  
 예정된 수동 장애 조치(failover) 수행에 대한 제한 사항, 사전 요구 사항 및 권장 사항에 대한 자세한 내용은 [가용성 그룹의 계획된 수동 장애 조치(failover) 수행&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)을 참조하세요.  
  
 FORCE_FAILOVER_ALLOW_DATA_LOSS  
 > [!CAUTION]  
>  강제 장애 조치(failover)를 수행하면 일부 데이터가 손실될 수 있으므로 재해 복구 방법으로만 사용해야 합니다. 따라서 주 복제본이 더 이상 실행되지 않고 데이터 손실 위험을 감수할 수 있는 경우에만 강제 장애 조치(failover)를 수행하는 것이 좋으며, 서비스를 즉시 가용성 그룹으로 복원해야 합니다.  
  
 역할이 SECONDARY 또는 RESOLVING 상태인 복제본에만 지원됩니다. 사용자가 장애 조치(failover) 명령을 입력하는 복제본을 *장애 조치(failover) 대상*이라고 합니다.  
  
 장애 조치(failover) 대상에 대해 가용성 그룹의 장애 조치(failover)를 적용하며, 데이터 손실이 발생할 가능성이 있습니다. 장애 조치(failover) 대상이 주 역할을 맡고 각 데이터베이스의 복사본을 복구하여 이를 온라인 상태의 새 주 데이터베이스로 만듭니다. 남은 보조 복제본에서 모든 보조 데이터베이스는 수동으로 다시 시작할 때까지 일시 중지됩니다. 이전 주 복제본을 사용할 수 있게 되면 보조 역할로 전환되고 해당 데이터베이스는 일시 중지된 보조 데이터베이스가 됩니다.  
  
> [!NOTE]  
>  장애 조치(failover) 명령은 장애 조치(failover) 대상에서 해당 명령을 수락하는 즉시 반환하지만 데이터베이스 복구는 가용성 그룹의 장애 조치가 끝난 후 비동기로 수행됩니다.  
  
 강제 장애 조치(failover)에 대한 제한 사항, 사전 요구 사항 및 권장 사항과 강제 장애 조치(failover) 시 가용성 그룹의 이전 주 데이터베이스에 미치는 영향에 대한 자세한 내용은 [가용성 그룹의 강제 수동 장애 조치(failover) 수행&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)을 참조하세요.  
  
 ADD LISTENER **‘** _dns\_name_ **’(** \<add_listener_option> **)**  
 이 가용성 그룹의 새 가용성 그룹 수신기를 정의합니다. 주 복제본에서만 지원되며,  
  
> [!IMPORTANT]
>  첫 번째 수신기를 만들기 전에 [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)을 읽는 것이 좋습니다.  
> 
>  지정된 가용성 그룹에 대한 수신기를 만든 후에는 다음을 수행하는 것이 좋습니다.  
> 
>  -   네트워크 관리자에게 요청하여 수신기의 IP 주소를 배타적으로 사용할 수 있도록 예약합니다.  
> -   이 가용성 그룹에 대한 클라이언트 연결을 요청할 때 연결 문자열에 사용할 수신기의 DNS 호스트 이름을 애플리케이션 개발자에게 제공합니다.  
  
 *dns_name*  
 가용성 그룹 수신기의 DNS 호스트 이름을 지정합니다. 수신기의 DNS 이름은 도메인 및 NetBIOS에서 고유해야 합니다.  
  
 *dns_name*은 문자열 값입니다. 이 이름은 순서에 관계없이 영숫자 문자, 대시(-) 및 하이픈(_)만 포함할 수 있습니다. DNS 호스트 이름은 대/소문자를 구분하지 않습니다. 최대 길이는 63자입니다.  
  
 의미 있는 문자열을 지정하는 것이 좋습니다. 예를 들어, `AG1`이라는 가용성 그룹의 경우 `ag1-listener`와 같은 의미 있는 DNS 호스트 이름을 지정합니다.  
  
> [!IMPORTANT]  
>  NetBIOS는 dns_name에서 처음 15자만 인식합니다. 두 WSFC 클러스터가 동일한 Active Directory에 의해 제어될 때 15자 이상의 이름과 동일한 15자 접두사를 사용하여 두 클러스터 모두에서 가용성 그룹 수신기를 만들려고 하면Virtual Network 이름 리소스를 온라인으로 전환할 수 없다는 오류 메시지가 표시됩니다. DNS 이름의 접두사 명명 규칙에 대한 자세한 내용은 [도메인 이름 할당](https://technet.microsoft.com/library/cc731265\(WS.10\).aspx)을 참조하세요.  
  
 JOIN AVAILABILITY GROUP ON  
 *분산 가용성 그룹*에 조인합니다. 분산 가용성 그룹을 만들 때 만들어지는 클러스터의 가용성 그룹은 주 가용성 그룹입니다. 분산 가용성 그룹에 조인하는 가용성 그룹은 보조 가용성 그룹입니다.  
  
 \<ag_name>  
 분산 가용성 그룹의 절반을 구성하는 가용성 그룹의 이름을 지정합니다.  
  
 LISTENER **='** TCP **://** _system-address_ **:** _port_ **'**  
 가용성 그룹과 연결된 수신기에 대한 URL 경로를 지정합니다.  
  
 LISTENER 절은 필수입니다.  
  
 **'** TCP **://** _system-address_ **:** _port_ **'**  
 가용성 그룹과 연결된 수신기에 대한 URL을 지정합니다. URL 매개 변수는 다음과 같습니다.  
  
 *system-address*  
 수신기를 명확하게 식별하는 시스템 이름, 정규화된 도메인 이름 또는 IP 주소 등의 문자열입니다.  
  
 *port*  
 가용성 그룹의 미러링 엔드포인트와 연결된 포트 번호입니다. 수신기의 포트가 아닙니다.  
  
 AVAILABILITY_MODE **=** { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }  
 주 복제본이 지정된 주 데이터베이스의 트랜잭션을 커밋하기 전에 보조 가용성 그룹이 디스크에 로그 레코드 확정(쓰기)을 확인할 때까지 주 복제본이 기다려야 하는지 여부를 지정합니다.  
  
 SYNCHRONOUS_COMMIT  
 트랜잭션이 보조 가용성 그룹에서 확정될 때까지 주 복제본이 트랜잭션을 커밋하지 않고 기다리도록 지정합니다. 주 가용성 그룹을 포함하여 최대 두 개의 가용성 그룹에 대해 SYNCHRONOUS_COMMIT를 지정할 수 있습니다.  
  
 ASYNCHRONOUS_COMMIT  
 이 보조 가용성 그룹이 로그를 확정할 때까지 기다리지 않고 주 복제본이 트랜잭션을 커밋하도록 지정합니다. 주 가용성 그룹을 포함하여 최대 두 개의 가용성 그룹에 대해 ASYNCHRONOUS_COMMIT를 지정할 수 있습니다.  
  
 AVAILABILITY_MODE 절은 필수적입니다.  
  
 FAILOVER_MODE **=** { MANUAL }  
 분산형 가용성 그룹의 장애 조치(failover) 모드를 지정합니다.  
  
 MANUAL  
 데이터베이스 관리자에 의한 예정된 수동 장애 조치(failover) 또는 강제 수동 장애 조치(failover)(일반적으로 *강제 장애 조치(failover)* 라고 함)를 사용하도록 설정합니다.  
  
 보조 가용성 그룹에 대한 자동 장애 조치(failover)는 지원되지 않습니다.  
  
 SEEDING_MODE **=** { AUTOMATIC | MANUAL }  
 보조 가용성 그룹을 처음에 시드하는 방법을 지정합니다.  
  
 AUTOMATIC  
 자동 시드를 활성화합니다. 이 메서드는 네트워크를 통해 보조 가용성 그룹을 시드합니다. 이 메서드를 사용하면 보조 가용성 그룹의 복제본에서 주 데이터베이스의 복사본을 백업 및 복원할 필요가 없습니다.  
  
 MANUAL  
 수동 시드를 지정합니다. 이 메서드를 사용하면 주 복제본에서 데이터베이스의 백업을 만들고 보조 가용성 그룹의 복제본에서 해당 백업을 수동으로 복원해야 합니다.  
  
 MODIFY AVAILABILITY GROUP ON  
 분산 가용성 그룹의 가용성 그룹 설정을 수정합니다. 수정할 가용성 그룹의 목록은 각 가용성 그룹에 대한 가용성 그룹 이름 및 WITH(…) 절을 포함합니다.  
  
> [!IMPORTANT]  
>  이 명령은 주 가용성 그룹 및 보조 가용성 그룹 인스턴스 모두에서 반복되어야 합니다.  
  
 GRANT CREATE ANY DATABASE  
 직접 시드를 지원하는 주 복제본을 대신하여 가용성 그룹에서 데이터베이스를 만들도록 허용합니다(SEEDING_MODE = AUTOMATIC). 이 매개 변수는 해당 보조가 가용성 그룹에 조인한 후 직접 시드를 지원하는 모든 보조 복제본에서 실행되어야 합니다.  CREATE ANY DATABASE 권한이 필요합니다.  
  
 DENY CREATE ANY DATABASE  
 주 복제본을 대신하여 데이터베이스를 만들 수 있는 가용성 그룹의 기능을 제거합니다.  
  
 \<add_listener_option>  
 ADD LISTENER는 다음 옵션 중 하나를 사용합니다.  
  
 WITH DHCP [ ON { **('** _four\_part\_ipv4\_address_ **','** _four\_part\_ipv4\_mask_ **')** } ]  
 가용성 그룹 수신기가 DHCP(동적 호스트 구성 프로토콜)를 사용할지 여부를 지정합니다.  필요할 경우 ON 절을 사용하여 이 수신기를 만들 네트워크를 식별합니다. DHCP는 가용성 그룹의 가용성 복제본을 호스팅하는 모든 서버 인스턴스에 사용되는 단일 서브넷으로 제한됩니다.  
  
> [!IMPORTANT]  
>  프로덕션 환경에서는 DHCP를 사용하지 않는 것이 좋습니다. 중단 시간이 있고 DHCP IP 임대가 만료되는 경우 수신기 DNS 이름과 연결되고 클라이언트 연결에 영향을 주는 새 DHCP 네트워크 IP 주소를 등록하기 위해 추가 시간이 필요합니다. 그러나 가용성 그룹의 기본 기능을 확인하고 애플리케이션과 통합하기 위해 DHCP를 개발 및 테스트 환경에 설정하는 것은 좋습니다.  
  
 다음은 그 예입니다.  
  
 `WITH DHCP ON ('10.120.19.0','255.255.254.0')`  
  
 WITH IP **(** { **('** _four\_part\_ipv4\_address_ **','** _four\_part\_ipv4\_mask_ **')**  |  **('** _ipv6\_address_ **')** } [ **,** ..._n_ ] **)** [ **,** PORT **=** _listener\_port_ ]  
 DHCP를 사용하는 대신 가용성 그룹 수신기가 하나 이상의 고정 IP 주소를 사용할지 여부를 지정합니다. 여러 서브넷에서 가용성 그룹을 만들려면 각 서브넷의 수신기 구성에 하나의 고정 IP 주소가 필요합니다. 지정된 서브넷에 대해 고정 IP 주소는 IPv4 주소이거나 IPv6 주소일 수 있습니다. 새 가용성 그룹에 대한 가용성 복제본을 호스팅할 각 서브넷의 고정 IP 주소를 얻으려면 네트워크 관리자에게 문의하십시오.  
  
 다음은 그 예입니다.  
  
 `WITH IP ( ('10.120.19.155','255.255.254.0') )`  
  
 *ipv4_address*  
 가용성 그룹 수신기에 대해 네 부분으로 된 IPv4 주소를 지정합니다. `10.120.19.155`)을 입력합니다.  
  
 *ipv4_mask*  
 가용성 그룹 수신기에 대해 네 부분으로 된 IPv4 마스크를 지정합니다. `255.255.254.0`)을 입력합니다.  
  
 *ipv6_address*  
 가용성 그룹 수신기의 IPv6 주소를 지정합니다. `2001::4898:23:1002:20f:1fff:feff:b3a3`)을 입력합니다.  
  
 PORT **=** *listener_port*  
 WITH IP 절에서 지정된 가용성 그룹 수신기에서 사용될 포트 번호(*listener_port*)를 지정합니다. PORT는 선택적입니다.  
  
 기본 포트 번호 1433이 지원됩니다. 그러나 보안이 중요한 경우에는 다른 포트 번호를 사용하는 것이 좋습니다.  
  
 예: `WITH IP ( ('2001::4898:23:1002:20f:1fff:feff:b3a3') ) , PORT = 7777`  
  
 MODIFY LISTENER **’** _dns\_name_ **’(** \<modify\_listener\_option\> **)**  
 이 가용성 그룹의 기존 가용성 수신기를 수정합니다. 주 복제본에서만 지원되며,  
  
 \<modify\_listener\_option\>  
 MODIFY LISTENER는 다음 옵션 중 하나를 사용합니다.  
  
 ADD IP { **(‘** _four\_part\_ipv4\_address_ **’,’** _four\_part\_ipv4_mask_ **)** \| <b>(‘</b>dns\_name*ipv6\_address* __’)__ }  
 *dns\_name*으로 지정된 가용성 그룹 수신기에 지정된 IP 주소를 추가합니다.  
  
 PORT **=** *listener_port*  
 이 섹션 앞에 나온 이 인수에 대한 설명을 참조하십시오.  
  
 RESTART LISTENER **'** _dns\_name_ **'**  
 지정된 DNS 이름과 관련된 수신기를 다시 시작합니다. 주 복제본에서만 지원되며,  
  
 REMOVE LISTENER **'** _dns\_name_ **'**  
 지정된 DNS 이름과 관련된 수신기를 제거합니다. 주 복제본에서만 지원되며,  
  
 OFFLINE  
 온라인 가용성 그룹을 오프라인 상태로 전환합니다. 동기-커밋 데이터베이스의 데이터는 손실되지 않습니다.  
  
 가용성 그룹이 오프라인 상태로 전환된 후에는 클라이언트에서 해당 데이터베이스를 사용할 수 없게 되고 사용자가 가용성 그룹을 다시 온라인 상태로 전환할 수 없습니다. 따라서 가용성 그룹 리소스를 WSFC 클러스터로 마이그레이션할 때 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]의 클러스터 간 마이그레이션을 수행하는 동안에만 OFFLINE 옵션을 사용하십시오.  
  
 자세한 내용은 [가용성 그룹을 오프라인 상태로 만들기&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/take-an-availability-group-offline-sql-server.md)를 참조하세요.  
  
## <a name="prerequisites-and-restrictions"></a>사전 요구 사항 및 제한 사항  
 가용성 복제본, 해당 호스트 서버 인스턴스 및 컴퓨터에 대한 필수 조건 및 제한 사항에 대한 자세한 내용은 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)을 참조하세요.  
  
 AVAILABILITY GROUP Transact SQL 문에 대한 제한 사항에 대한 자세한 내용은 [Always On 가용성 그룹에 대한 Transact-SQL 문 개요&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/transact-sql-statements-for-always-on-availability-groups.md)를 참조하세요.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다.  또한 ALTER ANY DATABASE 권한이 필요합니다.   
  
## <a name="examples"></a>예  
  
###  <a name="a-joining-a-secondary-replica-to-an-availability-group"></a><a name="Join_Secondary_Replica"></a> 1. 가용성 그룹에 보조 복제본 조인  
 다음 예에서는 현재 연결된 보조 복제본을 `AccountsAG` 가용성 그룹에 조인합니다.  
  
```SQL  
ALTER AVAILABILITY GROUP AccountsAG JOIN;  
GO  
```  
  
###  <a name="b-forcing-failover-of-an-availability-group"></a><a name="Force_Failover"></a> 2. 가용성 그룹 강제 장애 조치(failover)  
 다음 예에서는 `AccountsAG` 가용성 그룹을 연결된 보조 복제본으로 강제로 장애 조치(Failover)합니다.  
  
```SQL
ALTER AVAILABILITY GROUP AccountsAG FORCE_FAILOVER_ALLOW_DATA_LOSS;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER DATABASE SET HADR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)   
 [DROP AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/drop-availability-group-transact-sql.md)   
 [sys.availability_replicas&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [sys.availability_groups&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [Always On 가용성 그룹 구성 문제 해결&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)   
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 그룹 수신기, 클라이언트 연결 및 애플리케이션 장애 조치(failover)&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)  
  
  
