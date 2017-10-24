---
title: CREATE AVAILABILITY GROUP (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AVAILABILITY GROUP
- CREATE_AVAILABILITY_TSQL
- CREATE_AVAILABILITY_GROUP_TSQL
- CREATE AVAILABILITY GROUP
- CREATE AVAILABILITY
- AVAILABILITY_GROUP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- CREATE AVAILABILITY GROUP statement
- Availability Groups [SQL Server], creating
- Availability Groups [SQL Server], Transact-SQL statements
ms.assetid: a3d55df7-b4e4-43f3-a14b-056cba36ab98
caps.latest.revision: 196
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cebeb43402be1762021738096b9a0e959082d986
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-availability-group-transact-sql"></a>CREATE AVAILABILITY GROUP(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 기능을 사용하도록 설정된 경우 새 가용성 그룹을 만듭니다.  
  
> [!IMPORTANT]  
>  새 가용성 그룹의 초기 주 복제본으로 사용할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 CREATE AVAILABILITY GROUP을 실행합니다. 이 서버 인스턴스는 WSFC(Windows Server 장애 조치(failover) 클러스터링) 노드에 있어야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE AVAILABILITY GROUP group_name  
   WITH (<with_option_spec> [ ,...n ] )  
   FOR [ DATABASE database_name [ ,...n ] ]  
   REPLICA ON <add_replica_spec> [ ,...n ]  
   AVAILABILITY GROUP ON <add_availability_group_spec> [ ,...2 ]  
   [ LISTENER ‘dns_name’ ( <listener_option> ) ]  
[ ; ]  
  
<with_option_spec>::=   
    AUTOMATED_BACKUP_PREFERENCE = { PRIMARY | SECONDARY_ONLY| SECONDARY | NONE }  
  | FAILURE_CONDITION_LEVEL  = { 1 | 2 | 3 | 4 | 5 }   
  | HEALTH_CHECK_TIMEOUT = milliseconds  
  | DB_FAILOVER  = { ON | OFF }   
  | DTC_SUPPORT  = { PER_DB | NONE }  
  | BASIC  
  | DISTRIBUTED
  | REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = { integer }
  | CLUSTER_TYPE = { WSFC | EXTERNAL | NONE } 
  
<add_replica_spec>::=  
  <server_instance> WITH  
    (  
       ENDPOINT_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT },  
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
        [,] [ READ_ONLY_ROUTING_LIST = { ( ‘<server_instance>’ [ ,...n ] ) | NONE } ]  
     } )  
     | SESSION_TIMEOUT = integer  
  
<add_availability_group_spec>::=  
 <ag_name> WITH  
    (  
       LISTENER_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT },  
       FAILOVER_MODE = MANUAL,  
       SEEDING_MODE = { AUTOMATIC | MANUAL }  
    )  
  
<listener_option> ::=  
   {  
      WITH DHCP [ ON ( <network_subnet_option> ) ]  
    | WITH IP ( { ( <ip_address_option> ) } [ , ...n ] ) [ , PORT = listener_port ]  
   }  
  
  <network_subnet_option> ::=  
     ‘four_part_ipv4_address’, ‘four_part_ipv4_mask’    
  
  <ip_address_option> ::=  
     {   
        ‘four_part_ipv4_address’, ‘four_part_ipv4_mask’  
      | ‘ipv6_address’  
     }  
  
```  
  
## <a name="arguments"></a>인수  
 *o u p _*  
 새 가용성 그룹의 이름을 지정합니다. *group_name* 은 유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [식별자](../../relational-databases/databases/database-identifiers.md), WSFC 클러스터의 모든 가용성 그룹에서 고유 해야 합니다. 가용성 그룹 이름의 최대 길이는 128자입니다.  
  
 AUTOMATED_BACKUP_PREFERENCE  **=**  {기본 | SECONDARY_ONLY | 보조 | NONE}  
 백업을 수행할 위치를 선택할 때 백업 작업에서 주 복제본을 평가하는 방식에 관한 기본 설정을 지정합니다. 자동화된 백업 기본 설정을 고려하도록 지정한 백업 작업을 스크립팅할 수 있습니다. 기본 설정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 적용하는 것이 아니므로 임시 백업에 영향을 미치지 않는다는 것을 이해해야 합니다.  
  
 지원되는 값은 다음과 같습니다.  
  
 PRIMARY  
 백업이 항상 주 복제본에서 수행되도록 지정합니다. 이 옵션은 백업이 보조 복제본에서 실행될 때 지원되지 않는 차등 백업 만들기와 같은 백업 기능이 필요한 경우에 유용합니다.  
  
> [!IMPORTANT]  
>  로그 전달을 사용하여 가용성 그룹의 보조 데이터베이스를 준비하려는 경우 모든 보조 데이터베이스가 준비되고 가용성 그룹에 조인될 때까지 자동화된 백업 기본 설정을 **주** 로 설정합니다.  
  
 SECONDARY_ONLY  
 백업이 주 복제본에서 수행되지 않도록 지정합니다. 주 복제본이 유일한 온라인 복제본인 경우에는 백업이 수행되지 않아야 합니다.  
  
 SECONDARY  
 백업이 보조 복제본에서 수행되도록 지정합니다. 주 복제본이 유일한 온라인 복제본인 경우는 예외로, 이 경우에는 백업이 주 복제본에서 수행되어야 합니다. 이것이 기본 동작입니다.  
  
 없음  
 백업을 수행할 복제본을 선택할 때 백업 작업에서 가용성 복제본의 역할을 무시하도록 지정합니다. 백업 작업에서는 각 가용성 복제본의 작동 상태 및 연결 상태와 함께 백업 우선 순위 등의 기타 요인을 평가할 수 있습니다.  
  
> [!IMPORTANT]  
>  AUTOMATED_BACKUP_PREFERENCE 설정은 적용되지 않습니다. 이 기본 설정의 해석은 지정된 가용성 그룹의 데이터베이스에 대한 백업 작업으로 스크립팅하는 논리(있는 경우)에 따라 달라집니다. 자동화된 백업 기본 설정은 임시 백업에는 영향을 미치지 않습니다. 자세한 내용은 참조 [에 가용성 복제본 &#40; 백업 구성 SQL Server &#41; ](../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md).  
  
> [!NOTE]  
>  기존 가용성 그룹의 자동화 된 백업 기본 설정을 보려면를 선택는 **automated_backup_preference** 또는 **automated_backup_preference_desc** 의 열은 [ sys.availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) 카탈로그 뷰에 있습니다. 또한 [sys.fn_hadr_backup_is_preferred_replica&#40; Transact SQL &#41; ](../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md) 기본 백업 복제본을 확인 하기 위해 사용할 수 있습니다.  이 함수는 복제본 중 하나 이상에 대 한 1을 반환 합니다. 경우에 `AUTOMATED_BACKUP_PREFERENCE = NONE`합니다.  
  
 FAILURE_CONDITION_LEVEL  **=**  {1 | 2 | **3** | 4 | 5}  
 이 가용성 그룹에 대 한 자동 장애 조치 트리거하는 오류 상태를 지정 합니다. FAILURE_CONDITION_LEVEL은 그룹 수준에서 설정 되지만 동기-커밋 가용성 모드에 대해 구성 된 가용성 복제본에만 해당 됩니다 (AVAILIBILITY_MODE  **=**  SYNCHRONOUS_COMMIT). 또한 통해 실패 조건 에서도 기본 및 보조 복제본이 자동 장애 조치 모드에 대 한 구성 된 경우에 자동 장애 조치를 트리거할 수 있습니다 (FAILOVER_MODE  **=**  자동) 보조 복제본이 고 현재 주 복제본과 동기화 합니다.  
  
 오류 상태 수준(1–5)의 범위는 가장 낮은 제한 수준 1에서 가장 높은 제한 수준 5까지입니다. 특정 상태 수준은 그보다 낮은 모든 제한 수준을 포함합니다. 따라서 가장 엄격한 상태 수준 5에는 그보다 낮은 네 개의 제한 상태 수준(1~4)이 포함되고, 수준 4에는 수준 1~3이 포함됩니다. 다음 표에서는 각 수준에 해당하는 오류 상태를 설명합니다.  
  
|Level|오류 상태|  
|-----------|-----------------------|  
|1.|다음과 같은 경우 자동 장애 조치(failover)를 시작하도록 지정합니다.<br /><br /> - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 중지 되었습니다.<br /><br /> -WSFC 클러스터에 연결 하기 위한 가용성 그룹의 임대가 서버 인스턴스로부터 ACK를 받지 못해 만료 됩니다. 자세한 내용은 [작동 방법: SQL Server Always On 임대 시간 제한](http://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-AlwaysOn-lease-timeout.aspx)을 참조하세요.|  
|2|다음과 같은 경우 자동 장애 조치(failover)를 시작하도록 지정합니다.<br /><br /> -인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클러스터에 연결 되어 있지 않고 가용성 그룹의 사용자 지정 HEALTH_CHECK_TIMEOUT 임계값을 초과 하 고 합니다.<br /><br /> -가용성 복제본이 실패 상태입니다.|  
|3|분리된 spinlock, 중대한 쓰기 액세스 위반 또는 과도한 덤프와 같이 심각한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부 오류가 발생할 경우 자동 장애 조치(failover)를 시작하도록 지정합니다.<br /><br /> 이것이 기본 동작입니다.|  
|4|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부 리소스 풀에서 지속적인 메모리 부족 상태와 같은 일반적인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부 오류가 발생할 경우 자동 장애 조치(failover)를 시작하도록 지정합니다.|  
|5|다음과 같은 오류 상태가 발생할 경우 자동 장애 조치(failover)를 시작하도록 지정합니다.<br /><br /> -SQL 엔진 작업자 스레드가 소진 된 경우<br /><br /> -해결할 수 없는 교착 상태가 발견 된 합니다.|  
  
> [!NOTE]  
>  클라이언트 요청에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 응답이 없는 것은 가용성 그룹과 관련이 없습니다.  
  
 FAILURE_CONDITION_LEVEL 및 HEALTH_CHECK_TIMEOUT 값이 정의 *유연한 장애 조치 정책* 지정된 된 그룹에 대 한 합니다. 유연한 장애 조치(failover) 정책을 통해 자동 장애 조치(failover)를 수행해야 하는 상태를 세부적으로 제어할 수 있습니다. 자세한 내용은 참조 [가용성 그룹 &#40; 자동 장애 조치에 대 한 유연한 장애 조치 정책 SQL Server &#41; ](../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md).  
  
 HEALTH_CHECK_TIMEOUT  **=**  *시간 (밀리초)*  
 대기 시간 (밀리초)을 지정 된 [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) 시스템 저장 프로시저를 WSFC 클러스터 서버 인스턴스가 느리거나 중지 하기 전에 서버 상태 정보를 반환 합니다. HEALTH_CHECK_TIMEOUT은 그룹 수준에서 설정 되지만 자동 장애 조치를 사용 하 여 동기-커밋 가용성 모드에 대해 구성 된 가용성 복제본에만 해당 됩니다 (AVAILIBILITY_MODE  **=**  동기 _COMMIT)입니다.  또한 통해 상태 확인 제한 시간 주 및 보조 복제본이 자동 장애 조치 모드에 대 한 구성 된 경우에 자동 장애 조치를 트리거할 수 있습니다 (FAILOVER_MODE  **=**  자동)와 보조 데이터베이스 복제본이 주 복제본과 현재 동기화 됩니다.  
  
 기본 HEALTH_CHECK_TIMEOUT 값은 30,000밀리초(30초)입니다. 최소값은 15,000밀리초(15초)이고 최대값은 4,294,967,295밀리초입니다.  
  
> [!IMPORTANT]  
>  **sp_server_diagnostics** 는 데이터베이스 수준에서 상태 확인을 수행하지 않습니다.  
  
 DB_FAILOVER  **=**  {ON | OFF}  
 주 복제본에서 데이터베이스가 오프 라인 상태일 때 수행할에 대 한 응답을 지정 합니다. 가용성 그룹에 데이터베이스에 대 한 온라인 이외의 모든 상태를 ON으로 설정 된 경우 자동 장애 조치를 트리거합니다. 이 옵션을 OFF로 설정 하는 경우 자동 장애 조치를 트리거하는 인스턴스 상태에만 사용 됩니다.  
  
  이 설정에 대 한 자세한 내용은 참조 [데이터베이스 수준 상태 검색 옵션](../../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md) 
  
 DTC_SUPPORT  **=**  {PER_DB | NONE}  
 Distributed transaction coordinator (DTC)를 통해 데이터베이스 간 트랜잭션이 지원 되는지 여부를 지정 합니다. 데이터베이스 간 트랜잭션부터만 지원 됩니다 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]합니다. PER_DB 이러한 트랜잭션 지원 하 여 가용성 그룹을 만듭니다. 자세한 내용은 [Always On 가용성 그룹 및 데이터베이스 미러링에 대한 데이터베이스 간 트랜잭션 및 분산 트랜잭션&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)를 참조하세요.  
  
 BASIC  
 기본 가용성 그룹을 만들려면 사용 합니다. 기본 가용성 그룹 데이터베이스 하나 및 두 개의 복제본으로 제한 됩니다: 주 복제본과 하나의 보조 복제본입니다. 이 옵션은 사용 되지 않는 데이터베이스 미러링 기능에 SQL Server Standard Edition에 대 한 대체 합니다. 자세한 내용은 참조 [기본 가용성 그룹 &#40; Always On 가용성 그룹 &#41; ](../../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md). 기본 가용성 그룹은부터 지원 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]합니다.  

 DISTRIBUTED  
 분산형된 가용성 그룹을 만드는 데 사용 합니다. 이 옵션은 별도 Windows Server 장애 조치 클러스터에 두 개의 가용성 그룹을 연결 하려면 가용성 그룹에 매개 변수와 함께 사용 됩니다.  자세한 내용은 [분산된 가용성 그룹&#40;Always On 가용성 그룹&#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)을 참조하세요. 분산된 된 가용성 그룹에서 시작 하 고 사용할 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]합니다. 

 REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT   
 SQL Server 2017 CTP 2.2에서에서 도입 되었습니다. 기본 트랜잭션을 커밋합니다 하기 전에 커밋하는 데 필요한 동기 보조 복제본의 최소 수를 설정 하는 데 사용 합니다. SQL Server 트랜잭션이 트랜잭션 로그는 보조 복제본의 최소 수에서 업데이트 될 때까지 대기 하는 것을 보장 합니다. 기본값은 0으로 SQL Server 2016으로 동일한 동작을 제공 합니다. 최소값은 0입니다. 최대값은 1 뺀 값 복제본의 수입니다. 이 옵션은 동기 커밋 모드에 있는 복제본 관련이 있습니다. 복제본이 동기 커밋 모드에 있는 경우 주 복제본에서 쓰기가 복제본 데이터베이스 트랜잭션 로그에 쓰기 동기 보조 복제본에 커밋됩니다 때까지 기다립니다. 동기 보조 복제본을 호스팅하는 SQL Server 응답 하지 않는 경우 주 복제본을 호스팅하는 SQL Server 표시 해당 보조 복제본이 동기화 되지 않은 한 계속 합니다. 응답 하지 않는 데이터베이스를 다시 온라인 상태가 되 면 중인 "동기화 되지 않음" 상태 및 주 수 있도록 동기 다시 될 때까지 복제본 비정상으로 표시 합니다. 이 설정은 주 복제본은 최소한 복제본의 커밋된 각 트랜잭션에 될 때까지 대기 하는 것을 보장 합니다. 복제본의 최소 수를 사용할 수 없는 경우에 주 복제본에서 커밋 실패 합니다. 이 설정은 클러스터 유형 가용성 그룹에 적용 됩니다 `WSFC` 및 `EXTERNAL`합니다. 클러스터 형식에 대 한 `EXTERNAL` 가용성 그룹 클러스터 리소스에 추가 될 때 설정이 변경 됩니다. 참조 [가용성 그룹 구성에 대 한 높은 가용성 및 데이터 보호](../../linux/sql-server-linux-availability-group-ha.md)합니다.

 CLUSTER_TYPE  
 SQL Server 2017 CTP 2.2에서에서 도입 되었습니다. 가용성 그룹은 Windows Server 장애 조치 클러스터 (WSFC)에 있는지 확인 하는 데 사용 합니다.  Windows Server 장애 조치 클러스터에서 장애 조치 클러스터 인스턴스의 가용성 그룹은 WSFC로 설정 합니다. 클러스터 Linux Pacemaker와 같은 Windows Server 장애 조치 클러스터 되지 않은 클러스터 관리자에서 관리 하는 경우 외부로 설정 합니다. 하지 WSFC 클러스터를 조정 하기 위해 사용 하 여 가용성 그룹으로 만들 때 NONE으로 설정 합니다. 예를 들어 포함 되 면 가용성 그룹 Linux 서버입니다. 

 데이터베이스 *database_name*  
 로컬 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스(즉, 가용성 그룹을 만들 서버 인스턴스)에 있는 하나 이상의 사용자 데이터베이스 목록을 지정합니다. 하나의 가용성 그룹에 여러 개의 데이터베이스를 지정할 수 있지만 각 데이터베이스는 하나의 가용성 그룹에만 속할 수 있습니다. 가용성 그룹에서 지원할 수 있는 데이터베이스의 유형에 대 한 정보를 참조 하십시오. [필수 구성 요소, 제한 사항 및 Always On 가용성 그룹 &#40;에 대 한 권장 사항 SQL Server &#41; ](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md). 로컬 데이터베이스를 가용성 그룹에 이미 속해를 확인 하려면 참조는 **replica_id** 열에는 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰.  
  
 DATABASE 절은 선택적입니다. 를 생략 하면 새 가용성 그룹이 비어 있습니다.  
  
 가용성 그룹을 만든 후 보조 복제본을 호스팅하는 각 서버 인스턴스에 연결 하 고 각 보조 데이터베이스를 준비 하 고 가용성 그룹에 조인 합니다. 자세한 내용은 [Always On 보조 데이터베이스에서 데이터 이동 시작&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)을 참조하세요.  
  
> [!NOTE]  
>  나중에 현재 주 복제본을 호스팅하는 서버 인스턴스에서 적합한 데이터베이스를 가용성 그룹에 추가할 수 있습니다. 또한 가용성 그룹에서 데이터베이스를 제거할 수도 있습니다. 자세한 내용은 [ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)또는 PowerShell을 사용하여 기존 Always On 가용성 그룹에 보조 복제본을 추가하는 방법에 대해 설명합니다.  
  
 REPLICA ON  
 새 가용성 그룹의 가용성 복제본을 호스팅하는 1~5개의 SQL Server 인스턴스를 지정합니다.  각 복제본은 서버 인스턴스 주소 다음에 WITH (…) 절을 사용하여 지정합니다. 최소한 초기 주 복제본이 되는 해당 로컬 서버 인스턴스를 지정 해야 합니다. 선택적으로 최대 네 개의 보조 복제본을 지정할 수도 있습니다.  
  
 모든 보조 복제본을 가용성 그룹에 조인해야 합니다. 자세한 내용은 [ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)또는 PowerShell을 사용하여 기존 Always On 가용성 그룹에 보조 복제본을 추가하는 방법에 대해 설명합니다.  
  
> [!NOTE]  
>  사용 하 여 언제 든 지 보조 복제본을 추가할 수 있습니다 보다 작거나 4 개의 보조 복제본을 가용성 그룹을 만들 때 지정 하면는 [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] 문. 이 문을 사용하여 기존 가용성 그룹에서 보조 복제본을 제거할 수도 있습니다.  
  
 \<서버 인스턴스 >의 인스턴스 주소를 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 복제본에 대 한 호스트입니다. 주소 형식은 다음과 같이 인스턴스가 기본 인스턴스이거나 명명된 인스턴스인지 그리고 독립형 인스턴스이거나 FCI(장애 조치(failover) 클러스터 인스턴스)인지에 따라 달라집니다.  
  
 { '*system_name*[\\*instance_name*]' | '*FCI_network_name*[\\*instance_name*]' }  
  
 이 주소의 구성 요소는 다음과 같습니다.  
  
 *system_name*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 대상 인스턴스가 있는 컴퓨터 시스템의 NetBIOS 이름입니다. 이 컴퓨터는 WSFC 노드여야 합니다.  
  
 *FCI_network_name*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터에 액세스하는 데 사용되는 네트워크 이름입니다. 서버 인스턴스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]장애 조치(failover) 파트너로 참여하는 경우 이 인수를 사용합니다. 선택 실행 [@@SERVERNAME ](../../t-sql/functions/servername-transact-sql.md) FCI에서 서버 인스턴스는 전체가 반환 '*FCI_network_name*[\\*instance_name*]' 문자열 (되는 전체 복제 데이터베이스 이름)입니다.  
  
 *instance_name*  
 인스턴스의 이름입니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 으로 호스팅되고 *system_name* 또는 *FCI_network_name* 올려진 HADR 서비스를 사용할 수 있습니다. 기본 서버 인스턴스의 경우 *instance_name* 은 선택 사항입니다. 인스턴스 이름은 대/소문자를 구분하지 않습니다. 독립 실행형 서버 인스턴스에서이 값 이름은 SELECT를 실행 하 여 반환 된 값과 동일한 [@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md)합니다.  
  
 \  
 구분 기호를 지정 하는 경우에 사용할 *instance_name*에서 구분 하기 위해서 *system_name* 또는 *FCI_network_name*합니다.  
  
 WSFC 노드 및 서버 인스턴스에 대 한 필수 구성 요소에 대 한 정보를 참조 하십시오. [필수 구성 요소, 제한 사항 및 Always On 가용성 그룹 &#40;에 대 한 권장 사항 SQL Server &#41; ](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
 ENDPOINT_URL **='**TCP**://***시스템 주소***:***포트***'**  
 URL 경로를 지정 된 [데이터베이스 미러링 끝점이](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md) 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 현재 REPLICA ON 절에서 정의 중인 가용성 복제본을 호스팅하는 합니다.  
  
 ENDPOINT_URL 절은 필수입니다. 자세한 내용은 [가용성 복제본 추가 또는 수정 시 끝점 URL 지정&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)에 대한 서버 인스턴스를 구성하는 것과 관련된 일반적인 문제를 해결하는 데 유용한 정보를 제공합니다.  
  
 **'**TCP**://***시스템 주소***:***포트***'**  
 끝점 URL 또는 읽기 전용 라우팅 URL을 지정하기 위한 URL을 지정합니다. URL 매개 변수는 다음과 같습니다.  
  
 *system-address*  
 대상 컴퓨터 시스템을 명확하게 식별하는 시스템 이름, 정규화된 도메인 이름 또는 IP 주소 등의 문자열입니다.  
  
 *port*  
 파트너 서버 인스턴스(ENDPOINT_URL 옵션의 경우)의 미러링 끝점과 연관된 포트 번호 또는 서버 인스턴스의 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 사용되는 포트 번호(READ_ONLY_ROUTING_URL 옵션의 경우)입니다.  
  
 AVAILABILITY_MODE  **=**  {{SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT}  
 Synchronous_commit을 지정한 또는 ASYNCHRONOUS_COMMIT을 보조 복제본을 주 복제본에는 지정 된 주 복제본에서 트랜잭션을 커밋할 수 전에 디스크에 로그 레코드 확정 (쓰기)를 확인할 때까지 대기 하는 주 복제본에 있는지 여부를 지정합니다 데이터베이스입니다. 동일한 주 복제본의 서로 다른 데이터베이스에 있는 트랜잭션을 개별적으로 커밋할 수 있습니다.
  
 SYNCHRONOUS_COMMIT  
 주 복제본이 보조 복제본 (동기-커밋 모드)에서 확정 될 때까지 트랜잭션을 커밋하기 위해 대기 하는 것을 지정 합니다. 주 복제본을 포함하여 최대 세 개의 복제본에 대해 SYNCHRONOUS_COMMIT을 지정할 수 있습니다.  
  
 ASYNCHRONOUS_COMMIT  
 이 보조 복제본이 로그를 확정할 때까지 기다리지 않고 주 복제본이 트랜잭션을 커밋하도록 지정합니다(동기-커밋 가용성 모드). 주 복제본을 포함하여 최대 다섯 개의 가용성 복제본에 대해 ASYNCHRONOUS_COMMIT을 지정할 수 있습니다.  
  
 AVAILABILITY_MODE 절은 필수적입니다. 자세한 내용은 [가용성 모드&#40;Always On 가용성 그룹&#41;](../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)을 참조하세요.  
  
 FAILOVER_MODE  **=**  {자동 | 수동}  
 정의하는 가용성 복제본의 장애 조치(failover) 모드를 지정합니다.  
  
 AUTOMATIC  
 자동 장애 조치(failover)를 사용하도록 설정합니다. 이 옵션은 AVAILABILITY_MODE = SYNCHRONOUS_COMMIT도 지정한 경우에만 지원됩니다. 주 복제본을 포함하여 두 개의 가용성 복제본에 대해 AUTOMATIC을 지정할 수 있습니다.  
  
> [!NOTE]  
>  SQL Server FCI(장애 조치(Failover) 클러스터 인스턴스)는 가용성 그룹에 따라 AlwaysOn 자동 장애 조치(Failover)를 지원하지 않으므로 FCI에서 호스팅하는 모든 가용성 복제본은 수동 장애 조치(Failover)에 대해서만 구성될 수 있습니다.  
  
 MANUAL  
 사용 하면 계획 된 수동 장애 조치 또는 강제 수동 장애 조치 (일반적으로 호출 *강제 장애 조치*)은 데이터베이스 관리자가 있습니다.  
  
 FAILOVER_MODE 절은 필수적입니다. 두 가지 유형의 수동 장애 조치(failover)인 데이터 손실이 없는 수동 장애 조치(failover)와 데이터가 손실될 수 있는 강제 장애 조치(failover)는 서로 다른 조건에서 지원됩니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [장애 조치(Failover) 및 장애 조치(Failover) 모드&#40;Always On 가용성 그룹&#41;](../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)를 참조하세요.  
  
 SEEDING_MODE  **=**  {자동 | 수동}  
 보조 복제본은 처음 시드 된 방법을 지정 합니다.  
  
 AUTOMATIC  
 직접 시 딩을 사용 하도록 설정 합니다. 이 메서드는 네트워크를 통해 보조 복제본을 시드합니다. 이 메서드 백업 하 고 복제본에서 주 데이터베이스의 복사본을 복원 필요 하지 않습니다.  
  
> [!NOTE]  
>  직접 시드를 위해 허용 해야 데이터베이스를 만들 각 보조 복제본에서 호출 하 여 **ALTER AVAILABILITY GROUP** 와 **GRANT CREATE ANY DATABASE** 옵션입니다.  
  
 MANUAL  
 수동 시드 (기본값)을 지정합니다. 이 메서드를 사용 하면 주 복제본에 데이터베이스의 백업을 만들고 보조 복제본에서 해당 백업을 수동으로 복원 해야 합니다.  
  
 BACKUP_PRIORITY  **=** *n*  
 이 복제본에 대한 백업을 수행하기 위한 우선 순위를 지정하며 동일한 가용성 그룹의 다른 복제본을 기준으로 합니다. 이 값은 0에서 100 사이의 정수입니다. 이러한 값에는 다음과 같은 의미가 있습니다.  
  
-   1..100은 가용성 복제본이 백업 수행을 위해 선택될 수 있음을 나타냅니다. 1은 가장 낮은 우선 순위를 나타내고 100은 가장 높은 우선 순위를 나타냅니다. BACKUP_PRIORITY = 1이면 현재 사용 가능한 더 높은 우선 순위의 가용성 복제본이 없는 경우에만 해당 가용성 복제본이 백업 수행을 위해 선택됩니다.  
  
-   0이 가용성 복제본 백업 수행을 위해 아님을 나타냅니다. 이 값은 예를 들어 백업을 장애 조치할 대상으로 사용하지 않을 원격 가용성 복제본의 경우에 유용합니다.  
  
 자세한 내용은 [활성 보조: 보조 복제본에 백업&#40;Always On 가용성 그룹&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)을 참조하세요.  
  
 SECONDARY_ROLE **(** ... **).**  
 가용성 복제본이 보조 역할을 현재 소유 하는 경우에 적용 되는 역할별 설정을 지정 (즉, 때마다 보조 복제본). 괄호 안에 보조 역할 옵션 중 하나 또는 모두를 지정합니다. 둘 다 지정할 경우 쉼표로 구분된 목록을 사용합니다.  
  
 보조 역할 옵션은 다음과 같습니다.  
  
 ALLOW_CONNECTIONS  **=**  {아니요 | READ_ONLY | 모든}  
 보조 역할, 즉 보조 복제본의 역할을 수행하는 지정된 가용성 복제본의 데이터베이스에서 클라이언트의 연결을 허용할 수 있는지 여부를 다음 중 하나로 지정합니다.  
  
 NO  
 이 복제본의 보조 데이터베이스에 대한 사용자 연결이 허용되지 않습니다. 즉, 읽기 액세스가 가능하지 않습니다. 이것이 기본 동작입니다.  
  
 READ_ONLY  
 연결만 허용 하는 응용 프로그램 의도 속성이 설정 되어 있는 보조 복제본의 데이터베이스에 **ReadOnly**합니다. 이 속성에 대한 자세한 내용은 [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)을 참조하십시오.  
  
 ALL  
 보조 복제본의 데이터베이스에 대해 읽기 전용 액세스를 위한 모든 연결이 허용됩니다.  
  
 자세한 내용은 [활성 보조: 읽기 가능한 보조 복제본&#40;Always On 가용성 그룹&#41;](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)을 참조하세요.  
  
 READ_ONLY_ROUTING_URL **='**TCP**://***시스템 주소***:***포트***'**  
 이 가용성 복제본에 대한 읽기 전용 연결 요청을 라우팅하는 데 사용할 URL을 지정합니다. 이 URL은 SQL Server 데이터베이스 엔진이 수신하는 URL입니다. 일반적으로 SQL Server 데이터베이스 엔진의 기본 인스턴스는 TCP 포트 1433에서 수신합니다.  
  
 명명 된 인스턴스의 포트 번호를 쿼리하여 가져올 수 있습니다는 **포트** 및 **type_desc** 의 열은 [sys.dm_tcp_listener_states](../../relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql.md) 동적 관리 뷰. TRANSACT-SQL 수신기를 사용 하는 서버 인스턴스 (**type_desc = 't s q L'**).  
  
 복제본에 대 한 읽기 전용 라우팅 URL을 계산 하는 방법에 대 한 자세한 내용은 참조 [Always On에 대 한 read_only_routing_url 계산](http://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-AlwaysOn.aspx)합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 명명된 인스턴스의 경우 Transact-SQL 수신기가 특정 포트를 사용하도록 구성되어야 합니다. 자세한 내용은 [특정 TCP 포트로 수신하도록 서버 구성&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)을 참조하세요.  
  
 PRIMARY_ROLE **(** ... **).**  
 가용성 복제본이 현재 주 역할을 소유한 경우에 적용 되는 역할별 설정을 지정 (즉, 때마다 주 복제본). 괄호 안에 주 역할 옵션 중 하나 또는 모두를 지정합니다. 둘 다 지정할 경우 쉼표로 구분된 목록을 사용합니다.  
  
 주 역할 옵션은 다음과 같습니다.  
  
 ALLOW_CONNECTIONS  **=**  {READ_WRITE | 모든}  
 주 역할, 즉 주 복제본의 역할을 수행하는 지정된 가용성 복제본의 데이터베이스에서 허용할 수 있는 클라이언트 연결 유형을 다음 중 하나로 지정합니다.  
  
 READ_WRITE  
 응용 프로그램 의도 연결 속성이 **ReadOnly** 로 설정된 연결은 허용되지 않습니다.  응용 프로그램 의도 속성이 **ReadWrite** 로 설정되었거나 응용 프로그램 의도 연결 속성이 설정되지 않은 경우에는 연결이 허용됩니다. 응용 프로그램 의도 연결 속성에 대한 자세한 내용은 [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)을 참조하십시오.  
  
 ALL  
 주 복제본의 데이터베이스에 대한 모든 연결이 허용됩니다. 이것이 기본 동작입니다.  
  
 READ_ONLY_ROUTING_LIST  **=**  { **('**\<서버 인스턴스 >**'** [ **,**... *n* ] **)** | NONE} 보조 역할에서 실행 하는 경우 다음 요구 사항을 충족 하는이 가용성 그룹에 대 한 가용성 복제본을 호스팅하는 서버 인스턴스의 쉼표로 구분 된 목록 지정:  
  
-   모든 연결 또는 읽기 전용 연결을 허용하도록 구성되어야 합니다(위에서 SECONDARY_ROLE 옵션의 ALLOW_CONNECTIONS 인수 참조).  
  
-   읽기 전용 라우팅 URL을 정의해야 합니다(위에서 SECONDARY_ROLE 옵션의 READ_ONLY_ROUTING_URL 인수 참조).  
  
 READ_ONLY_ROUTING_LIST 값은 다음과 같습니다.  
  
 \<서버 인스턴스 >의 인스턴스 주소를 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보조 역할에서 실행 될 때 읽기 가능한 보조 복제본은 복제본에 대 한 호스트입니다.  
  
 읽기 가능한 보조 복제본을 호스팅할 수도 있는 모든 서버 인스턴스를 지정하려면 쉼표로 구분된 목록을 사용합니다. 서버 인스턴스는 목록에 지정 된 순서에 따라 읽기 전용 라우팅입니다. 복제본의 읽기 전용 라우팅 목록에 복제본의 호스트 서버 인스턴스를 포함한 경우 읽기 전용 연결이 보조 복제본(사용 가능한 경우)으로 이동할 수 있도록 일반적으로 이 서버 인스턴스를 목록 끝에 두는 것이 좋습니다.  
  
 부터는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], 읽기 가능한 보조 복제본에서 읽기 전용 요청 부하 분산할 수 있습니다. 중첩 된 한 쌍의 읽기 전용 라우팅 목록 내에 복제본을 배치 하 여이 지정 합니다. 자세한 내용 및 예제에 대 한 참조 [읽기 전용 복제본에 부하 분산 구성](../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md#loadbalancing)합니다.  
  
 없음  
 주 복제본이 가용성 복제본을 사용 하는 경우 읽기 전용 라우팅을 지원 되지 않음을 지정 합니다. 이것이 기본 동작입니다.  
  
 SESSION_TIMEOUT  **=**  *정수*  
 세션 제한 시간(초)을 지정합니다. 이 옵션을 지정하지 않으면 기본적으로 제한 시간은 10초로 설정됩니다. 최소값은 5초입니다.  
  
> [!IMPORTANT]  
>  제한 시간을 10초 이상으로 유지하는 것이 좋습니다.  
  
 세션 제한 시간에 대 한 자세한 내용은 참조 하십시오. [Always On 가용성 그룹 개요 &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).  
  
 가용성 그룹에  
 구성 하는 두 개의 가용성 그룹을 지정 된 *분산형된 가용성 그룹*합니다. 각 가용성 그룹은 부분의 자체 장애 조치 클러스터 WSFC (Windows Server). 분산형된 가용성 그룹을 만들 때 현재 SQL Server 인스턴스에서 가용성 그룹은 주 가용성 그룹입니다. 두 번째 가용성 그룹은 보조 가용성 그룹입니다.  
  
 분산형된 가용성 그룹에 보조 가용성 그룹에 참가 해야 합니다. 자세한 내용은 [ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)또는 PowerShell을 사용하여 기존 Always On 가용성 그룹에 보조 복제본을 추가하는 방법에 대해 설명합니다.  
  
 \<ag_name > 하나를 구성 하는 가용성 그룹의 이름을 지정 분산형된 가용성 그룹의 절반입니다.  
  
 수신기 **='**TCP**://***시스템 주소***:***포트***'**  
 연결 된 가용성 그룹 수신기에 대 한 URL 경로 지정 합니다.  
  
 수신기 절이 필요 합니다.  
  
 **'**TCP**://***시스템 주소***:***포트***'**  
 연결 된 가용성 그룹 수신기에 대 한 URL을 지정 합니다. URL 매개 변수는 다음과 같습니다.  
  
 *system-address*  
 시스템 이름, 정규화 된 도메인 이름 또는 IP 주소를 수신기를 명확 하 게 식별 하는 등의 문자열이입니다.  
  
 *port*  
 가용성 그룹의 미러링 끝점과 연관 된 포트 번호가입니다. 수신기의 포트 아닌지 note 합니다.  
  
 AVAILABILITY_MODE  **=**  {SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT}  
 주 복제본이 주 복제본에는 지정된 된 주 데이터베이스에서 트랜잭션을 커밋할 수 전에 디스크에 로그 레코드 확정 (쓰기)을 보조 가용성 그룹에 대해 기다려야에 있는지 여부를 지정 합니다.  
  
 SYNCHRONOUS_COMMIT  
 주 복제본이 보조 가용성 그룹에 확정 될 때까지 트랜잭션을 커밋하기 위해 기다리는 지정 합니다. 최대 두 개의 가용성 그룹을 주 가용성 그룹을 포함 하 여 SYNCHRONOUS_COMMIT을 지정할 수 있습니다.  
  
 ASYNCHRONOUS_COMMIT  
 주 복제본이 보조 가용성 그룹 로그를 확정할 때까지 기다리지 않고 트랜잭션을 커밋합니다 있는지를 지정 합니다. 최대 두 개의 가용성 그룹을 주 가용성 그룹을 포함 하 여 ASYNCHRONOUS_COMMIT을 지정할 수 있습니다.  
  
 AVAILABILITY_MODE 절은 필수적입니다.  
  
 FAILOVER_MODE  **=**  {수동}  
 분산형된 가용성 그룹의 장애 조치 모드를 지정합니다.  
  
 MANUAL  
 사용 하면 계획 된 수동 장애 조치 또는 강제 수동 장애 조치 (일반적으로 호출 *강제 장애 조치*)은 데이터베이스 관리자가 있습니다.  
  
 FAILOVER_MODE 절이 필요 하 고 유일한 옵션은 수동입니다. 보조 가용성 그룹에 대한 자동 장애 조치(failover)는 지원되지 않습니다.  
  
 SEEDING_MODE  **=**  {자동 | 수동}  
 보조 가용성 그룹은 처음 시드 된 방법을 지정 합니다.  
  
 AUTOMATIC  
 직접 시 딩을 사용 하도록 설정 합니다. 이 메서드는 네트워크를 통해 보조 가용성 그룹을 시드합니다. 이 메서드 않아도 백업 하 고 보조 가용성 그룹의 복제본에서 주 데이터베이스의 복사본을 복원 합니다.  
  
 MANUAL  
 수동 시드 (기본값)을 지정합니다. 이 메서드를 사용 하면 주 복제본에 데이터베이스의 백업을 만들고 보조 가용성 그룹 복제본에서 해당 백업을 수동으로 복원 해야 합니다.  
  
 수신기 **'***dns_name***' (** \<_ o p > **)** 이 새 가용성 그룹 수신기를 정의 합니다. 가용성 그룹입니다. LISTENER는 선택적 인수입니다.  
  
> [!IMPORTANT]  
>  첫 번째 수신기를 만들기 전에 좋습니다 읽어 [만들기 또는 가용성 그룹 수신기 &#40; 구성 합니다. SQL Server &#41; ](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
>   
>  지정된 가용성 그룹에 대한 수신기를 만든 후에는 다음을 수행하는 것이 좋습니다.  
>   
>  -   네트워크 관리자에게 요청하여 수신기의 IP 주소를 배타적으로 사용할 수 있도록 예약합니다.  
> -   이 가용성 그룹에 대한 클라이언트 연결을 요청할 때 연결 문자열에 사용할 수신기의 DNS 호스트 이름을 응용 프로그램 개발자에게 제공합니다.  
  
 *dns_name*  
 가용성 그룹 수신기의 DNS 호스트 이름을 지정합니다. 수신기의 DNS 이름은 도메인 및 NetBIOS에서 고유해야 합니다.  
  
 *dns_name* 문자열 값입니다. 이 이름은 순서에 관계없이 영숫자 문자, 대시(-) 및 하이픈(_)만 포함할 수 있습니다. DNS 호스트 이름은 대/소문자를 구분하지 않습니다. 최대 길이는 63자입니다.  
  
 의미 있는 문자열을 지정하는 것이 좋습니다. 예를 들어, `AG1`이라는 가용성 그룹의 경우 `ag1-listener`와 같은 의미 있는 DNS 호스트 이름을 지정합니다.  
  
> [!IMPORTANT]  
>  NetBIOS는 dns_name에서 처음 15자만 인식합니다. 두 WSFC 클러스터가 동일한 Active Directory에 의해 제어 되는 경우 이름을 15 자 이상의 및 동일한 15 자 접두사를 사용 하 여 두 클러스터 모두에서 가용성 그룹 수신기 만들기 하면 오류가 발생 되는 가상 네트워크를 보고합니다 이름 리소스를 온라인 상태로 연결할 수 없습니다. DNS 이름의 접두사 명명 규칙에 대한 자세한 내용은 [도메인 이름 할당](http://technet.microsoft.com/library/cc731265\(WS.10\).aspx)을 참조하세요.  
  
 \<r _ o p > LISTENER는 다음 중 하나를 사용 \<_ o p > 옵션: 
  
 DHCP 사용 [ON { **('***four_part_ipv4_address***','***four_part_ipv4_mask***')** }]  
 가용성 그룹 수신기는 DHCP Dynamic Host Configuration Protocol ()을 사용 하도록 지정 합니다.  필요에 따라 ON 절을 사용 하 여이 수신기는 만들어지지 네트워크를 식별 합니다. DHCP는 단일 서브넷으로 모든 서버 인스턴스에 사용 되는 가용성 그룹에 복제본을 호스팅하는 제한 됩니다.  
  
> [!IMPORTANT]  
>  프로덕션 환경에서는 DHCP를 사용하지 않는 것이 좋습니다. 중단 시간이 있고 DHCP IP 임대가 만료되는 경우 수신기 DNS 이름과 연결되고 클라이언트 연결에 영향을 주는 새 DHCP 네트워크 IP 주소를 등록하기 위해 추가 시간이 필요합니다. 그러나 가용성 그룹의 기본 기능을 확인하고 응용 프로그램과 통합하기 위해 DHCP를 개발 및 테스트 환경에 설정하는 것은 좋습니다.  
  
 예를 들어  
  
 `WITH DHCP ON ('10.120.19.0','255.255.254.0')`  
  
 IP **(** { **('***four_part_ipv4_address***','***four_part_ipv4_mask* **')** | **('***ipv6_address***')** } [ **,** ...  *n*  ] **)** [ **,** 포트  **=**  *listener_port* ]  
 즉, DHCP를 사용 하는 대신 가용성 그룹 수신기 사용 하 여 하나 이상의 고정 IP 주소를 지정 합니다. 여러 서브넷에서 가용성 그룹을 만들려면 각 서브넷의 수신기 구성에 하나의 고정 IP 주소가 필요합니다. 지정된 서브넷에 대해 고정 IP 주소는 IPv4 주소이거나 IPv6 주소일 수 있습니다. 새 가용성 그룹에 대 한 복제본을 호스팅하는 각 서브넷에 대 한 고정 IP 주소를 확인 하려면 네트워크 관리자를 게 문의 하십시오.  
  
 예를 들어  
  
 `WITH IP ( ('10.120.19.155','255.255.254.0') )`  
  
 *four_part_ipv4_address*  
 가용성 그룹 수신기에 대해 네 부분으로 된 IPv4 주소를 지정합니다. `10.120.19.155`)을 입력합니다.  
  
 *four_part_ipv4_mask*  
 가용성 그룹 수신기에 대해 네 부분으로 된 IPv4 마스크를 지정합니다. `255.255.254.0`)을 입력합니다.  
  
 *ipv6_address*  
 가용성 그룹 수신기의 IPv6 주소를 지정합니다. `2001::4898:23:1002:20f:1fff:feff:b3a3`)을 입력합니다.  
  
 포트  **=**  *listener_port*  
 포트 번호를 지정-*listener_port*-WITH IP 절에 지정 된 가용성 그룹 수신기가 사용할 수 있습니다. PORT는 선택적입니다.  
  
 기본 포트 번호 1433이 지원됩니다. 그러나 보안이 중요한 경우에는 다른 포트 번호를 사용하는 것이 좋습니다.  
  
 예: `WITH IP ( ('2001::4898:23:1002:20f:1fff:feff:b3a3') ) , PORT = 7777`  
  
## <a name="prerequisites-and-restrictions"></a>사전 요구 사항 및 제한 사항  
 가용성 그룹을 만들기 위한 필수 구성 요소에 대 한 정보를 참조 하십시오. [필수 구성 요소, 제한 사항 및 Always On 가용성 그룹 &#40;에 대 한 권장 사항 SQL Server &#41; ](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
 가용성 그룹 Transact SQL 문 제한에 대 한 정보를 참조 하십시오. [Always On 가용성 그룹 &#40;에 대 한 개요의 TRANSACT-SQL 문 SQL Server &#41; ](../../database-engine/availability-groups/windows/transact-sql-statements-for-always-on-availability-groups.md).  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 CREATE AVAILABILITY GROUP 서버 권한, ALTER ANY AVAILABILITY GROUP 권한, CONTROL SERVER 권한 중 하나와 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-configuring-backup-on-secondary-replicas-flexible-failover-policy-and-connection-access"></a>1. 보조 복제본, 유연한 장애 조치(failover) 정책 및 연결 액세스에 대한 백업 구성  
 다음 예에서는 두 개의 사용자 데이터베이스 `MyAg` 및 `ThisDatabase`에 대해 `ThatDatabase`라는 가용성 그룹을 만듭니다. 다음 표에는 가용성 그룹 전체에 대해 설정되는 옵션에 지정되는 값이 요약되어 있습니다.  
  
|그룹 옵션|설정|Description|  
|------------------|-------------|-----------------|  
|AUTOMATED_BACKUP_PREFERENCE|SECONDARY|이 자동화된 백업 기본 설정은 주 복제본이 유일한 온라인 복제본일 경우(기본 동작)를 제외하고 백업이 보조 복제본에서 수행되도록 지정합니다. 자동화된 백업 기본 설정을 고려하도록 가용성 데이터베이스에서 백업 작업을 스크립팅해야 AUTOMATED_BACKUP_PREFERENCE 설정이 적용됩니다.|  
|FAILURE_CONDITION_LEVEL|3|이 오류 상태 수준 설정은 분리된 spinlock, 중대한 쓰기 액세스 위반 또는 과도한 덤프와 같이 심각한 SQL Server 내부 오류가 발생할 경우 자동 장애 조치(failover)를 시작하도록 지정합니다.|  
|HEALTH_CHECK_TIMEOUT|600000|WSFC 클러스터에 대 한 60000 밀리초를 대기 하는 상태 확인 제한 시간 값이 60 초로 지정는 [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) 시스템 저장 프로시저는 서버 인스턴스에 대 한 서버 상태 정보를 반환 하려면 클러스터 호스트 서버 인스턴스가 느리거나 중지 이라고 가정 하기 전에 자동으로 동기-커밋 복제본을 호스팅. 기본값은 30,000밀리초입니다.|  
  
 세 가지 가용성 복제본은 `COMPUTER01`, `COMPUTER02` 및 `COMPUTER03`이라는 컴퓨터의 기본 서버 인스턴스가 호스팅합니다. 다음 표에는 각 복제본의 복제본 옵션에 지정되는 값이 요약되어 있습니다.  
  
|복제본 옵션|`COMPUTER01`의 설정|`COMPUTER02`의 설정|`COMPUTER03`의 설정|Description|  
|--------------------|-----------------------------|-----------------------------|-----------------------------|-----------------|  
|ENDPOINT_URL|TCP: / /*COMPUTER01:5022*|TCP: / /*COMPUTER02:5022*|TCP: / /*COMPUTER03:5022*|이 예에서는 시스템이 같은 도메인에 있으므로 끝점 URL에서 컴퓨터 시스템의 이름을 시스템 주소로 사용할 수 있습니다.|  
|AVAILABILITY_MODE|SYNCHRONOUS_COMMIT|SYNCHRONOUS_COMMIT|ASYNCHRONOUS_COMMIT|두 복제본이 동기-커밋 모드를 사용합니다. 동기화된 복제본은 데이터 손실 없는 장애 조치(failover)를 지원합니다. 비동기-커밋을 가용성 모드를 사용하는 세 번째 복제본입니다.|  
|FAILOVER_MODE|AUTOMATIC|AUTOMATIC|MANUAL|동기-커밋 복제본은 자동 장애 조치(failover) 및 계획된 수동 장애 조치(failover)를 지원합니다. 동기-커밋 가용성 모드 복제본은 강제 수동 장애 조치(failover)만 지원합니다.|  
|BACKUP_PRIORITY|30|30|90|동기-커밋 복제본보다 높은 우선 순위인 90이 비동기-커밋 복제본에 할당됩니다. 백업을 자주 비동기-커밋 복제본을 호스팅하는 서버 인스턴스에서 발생 하는 것입니다.|  
|SECONDARY_ROLE|( ALLOW_CONNECTIONS = NO,<br /><br /> READ_ONLY_ROUTING_URL = 'TCP://COMPUTER01:1433' )|( ALLOW_CONNECTIONS = NO,<br /><br /> READ_ONLY_ROUTING_URL = 'TCP://COMPUTER02:1433' )|( ALLOW_CONNECTIONS = READ_ONLY, <br />READ_ONLY_ROUTING_URL = 'TCP://COMPUTER03:1433' )|비동기-커밋 복제본만 읽기 가능한 보조 복제본 역할을 합니다.<br /><br /> 컴퓨터 이름 및 기본 데이터베이스 엔진 포트 번호(1433)를 지정합니다.<br /><br /> 이 인수는 선택 사항입니다.|  
|PRIMARY_ROLE|( ALLOW_CONNECTIONS = READ_WRITE, <br />READ_ONLY_ROUTING_LIST = (COMPUTER03) )|( ALLOW_CONNECTIONS = READ_WRITE, <br />READ_ONLY_ROUTING_LIST = (COMPUTER03) )|( ALLOW_CONNECTIONS = READ_WRITE, <br />READ_ONLY_ROUTING_LIST = NONE )|주 역할의 모든 복제본은 읽기 전용 연결 시도 거부합니다.<br /><br /> 로컬 복제본이 보조 역할에서 실행 되는 경우에 읽기 전용 연결 요청은 COMPUTER03으로 라우팅됩니다. 복제본이 주 역할로 실행될 경우 읽기 전용 라우팅이 비활성화됩니다.<br /><br /> 이 인수는 선택 사항입니다.|  
|SESSION_TIMEOUT|10|10|10|이 예제에서는 기본 세션 시간 제한 값(10)을 지정합니다. 이 인수는 선택 사항입니다.|  
  
 마지막으로 예제에서 새 가용성 그룹에 대한 가용성 그룹 수신기를 만들도록 LISTENER 절(옵션)을 지정합니다. 이 수신기에 대해 고유한 DNS 이름인 `MyAgListenerIvP6`이 지정됩니다. 두 복제본이 서로 다른 서브넷에 있으므로 수신기에서 고정 IP 주소를 사용해야 합니다. 두 가용성 복제본 각각에 대해 WITH IP 절이 IPv6 형식을 사용하는 고정 IP 주소인 `2001:4898:f0:f00f::cf3c` 및 `2001:4898:e0:f213::4ce2`를 지정합니다. 또한 이 예제에서 PORT 인수(옵션)를 사용하여 포트 `60173` 을 수신기 포트로 지정합니다.  
  
```  
CREATE AVAILABILITY GROUP MyAg   
   WITH (  
      AUTOMATED_BACKUP_PREFERENCE = SECONDARY,  
      FAILURE_CONDITION_LEVEL  =  3,   
      HEALTH_CHECK_TIMEOUT = 600000  
       )  
  
   FOR   
      DATABASE  ThisDatabase, ThatDatabase   
   REPLICA ON   
      'COMPUTER01' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER01:5022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC,  
         BACKUP_PRIORITY = 30,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = NO,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER01:1433' ),
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = (COMPUTER03) ),  
         SESSION_TIMEOUT = 10  
         ),   
  
      'COMPUTER02' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER02:5022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC,  
         BACKUP_PRIORITY = 30,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = NO,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER02:1433' ),  
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = (COMPUTER03) ),  
         SESSION_TIMEOUT = 10  
         ),   
  
      'COMPUTER03' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER03:5022',  
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,  
         FAILOVER_MODE =  MANUAL,  
         BACKUP_PRIORITY = 90,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER03:1433' ),  
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = NONE ),  
         SESSION_TIMEOUT = 10  
         );
GO  
ALTER AVAILABIIITY GROUP [MyAg]
  ADD LISTENER ‘MyAgListenerIvP6’ ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173 );   
GO  
```  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [가용성 그룹 만들기&#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
-   [가용성 그룹 마법사 사용&#40;SQL Server Management Studio&#41;](../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [새 가용성 그룹 대화 상자 사용&#40;SQL Server Management Studio&#41;](../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [가용성 그룹 마법사 사용&#40;SQL Server Management Studio&#41;](../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [ALTER DATABASE SET HADR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)   
 [가용성 그룹 &#40; Transact SQL &#41;](../../t-sql/statements/drop-availability-group-transact-sql.md)   
 [Always On 가용성 그룹 구성 &#40; 문제 해결 SQL Server &#41;](../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)   
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 그룹 수신기, 클라이언트 연결 및 응용 프로그램 장애 조치&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)  
  
  


