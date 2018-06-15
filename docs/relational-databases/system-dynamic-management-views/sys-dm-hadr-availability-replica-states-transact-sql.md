---
title: sys.dm_hadr_availability_replica_states (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/16/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_hadr_availability_replica_states
- sys.dm_hadr_availability_replica_states_TSQL
- sys.dm_hadr_availability_replica_states
- dm_hadr_availability_replica_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_availability_replica_states dynamic management view
ms.assetid: d2e678bb-51e8-4a61-b223-5c0b8d08b8b1
caps.latest.revision: 65
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e04fa466f018e114fe66686b81c5e5899dd2371e
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34466469"
---
# <a name="sysdmhadravailabilityreplicastates-transact-sql"></a>sys.dm_hadr_availability_replica_states(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  동일한 Always On 가용성 그룹의 로컬 복제본으로 각 로컬 복제본에 대 한 행과 각 원격 복제본에 대 한 행을 반환합니다. 각 행에 지정된 된 복제본의 상태에 대 한 정보가 포함 되어 있습니다.  
  
> [!IMPORTANT]  
>  지정된 된 가용성 그룹에 있는 모든 복제본에 대 한 정보, 쿼리 **sys.dm_hadr_availability_replica_states** 주 복제본을 호스팅하는 서버 인스턴스에서 합니다. 가용성 그룹의 보조 복제본을 호스팅 중인 서버 인스턴스에 대해 쿼리한 경우 이 동적 관리 뷰에는 가용성 그룹에 대한 로컬 정보만 반환됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|복제본의 고유 식별자입니다.|  
|**group_id**|**uniqueidentifier**|가용성 그룹의 고유한 식별자입니다.|  
|**is_local**|**bit**|복제본이 로컬 인지 중 하나:<br /><br /> 0 = 주 복제본이 로컬 서버 인스턴스에 의해 호스팅되는 가용성 그룹의 원격 보조 복제본을 나타냅니다. 이 값은 주 복제본 위치에서만 발생합니다.<br /><br /> 1 = 로컬 복제본을 나타냅니다. 보조 복제본에서는 복제본이 속하는 가용성 그룹에 대해 이 값만 사용할 수 있습니다.|  
|**role**|**tinyint**|현재 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 로컬 복제 또는 중 하나는 연결 된 원격 복제본의 역할:<br /><br /> 0 = 확인 중<br /><br /> 1 = 주<br /><br /> 2 = 보조<br /><br /> [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 역할에 대한 자세한 내용은 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)를 참조하세요.|  
|**role_desc**|**nvarchar(60)**|에 대 한 설명 **역할**이며 다음 중 하나입니다.<br /><br /> RESOLVING<br /><br /> PRIMARY<br /><br /> SECONDARY|  
|**operational_state**|**tinyint**|중 하나는 복제본의 현재 작동 상태:<br /><br /> 0 = 장애 조치(Failover) 보류 중<br /><br /> 1 = 보류 중<br /><br /> 2 = 온라인<br /><br /> 3 = 오프 라인<br /><br /> 4 = 실패<br /><br /> 5 = 실패, 쿼럼 없음<br /><br /> NULL = 복제본이 로컬이 아닙니다.<br /><br /> 자세한 내용은 참조 [역할 및 작동 상태](#RolesAndOperationalStates)이 항목의 뒷부분에 나오는 합니다.|  
|**operational\_state\_desc**|**nvarchar(60)**|에 대 한 설명 **operational\_상태**이며 다음 중 하나입니다.<br /><br /> PENDING_FAILOVER<br /><br /> PENDING<br /><br /> ONLINE<br /><br /> OFFLINE<br /><br /> FAILED<br /><br /> FAILED_NO_QUORUM<br /><br /> NULL|  
|**recovery\_health**|**tinyint**|롤업을 **데이터베이스\_상태** 의 열은 [sys.dm_hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) 동적 관리 뷰. 가능한 값 및 해당 설명을 보려면은 다음과 같습니다.<br /><br /> 0: 진행 중에서입니다.  하나 이상의 조인 된 데이터베이스의 데이터베이스 상태가 online (**데이터베이스\_상태** 는 0이 아닌).<br /><br /> 1: 온라인입니다. 모든 조인 된 데이터베이스의 온라인 데이터베이스 상태에 있는 (**database_state** 은 0).<br /><br /> NULL : **is_local** = 0|  
|**recovery_health_desc**|**nvarchar(60)**|에 대 한 설명 **recovery_health**이며 다음 중 하나입니다.<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**synchronization\_health**|**tinyint**|데이터베이스 동기화 상태에 대 한 롤업을 반영 (**synchronization_state**)의 모든 가용성 데이터베이스 조인 (라고도 *복제본*) 및 복제본 (의 가용성 모드 동기-커밋 또는 비동기-커밋 모드). 롤업을 복제 데이터베이스에 최소 정상 누적된 상태는 데이터베이스를 반영 합니다. 다음은 가능한 값 및 해당 설명을 보려면입니다.<br /><br /> 0: 정상 상태가 아닙니다.   하나 이상의 조인된 데이터베이스가 NOT SYNCHRONIZING 상태입니다.<br /><br /> 1: 부분적으로 정상입니다. 일부 복제본 대상 동기화 상태에 있지 않은: 동기-커밋 복제본을 동기화 해야 하 고 비동기-커밋 복제본을 동기화 해야 합니다.<br /><br /> 2: 정상입니다. 모든 복제본이 대상 동기화 상태: 동기-커밋 복제본이 동기화 되 고 비동기-커밋 복제본은 동기화가 수행 합니다.|  
|**synchronization_health_desc**|**nvarchar(60)**|에 대 한 설명 **synchronization_health**이며 다음 중 하나입니다.<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
|**connected_state**|**tinyint**|여부는 보조 복제본이 현재 주 복제본에 연결 됩니다. 해당 설명이 포함 된 가능한 값은 다음과 같습니다.<br /><br /> 0: 끊어졌습니다. 연결이 끊긴된 상태에 대 한 가용성 복제본의 응답의 역할에 따라 달라 집니다: 주 복제본에서 보조 복제본의 연결이 끊어질 경우 해당 보조 데이터베이스는 표시 되지 않는 것으로 SYNCHRONIZED 보조 될 때까지 대기 하는 주 복제본에서 다시 연결 합니다. 연결이 끊어져 있는지를 감지 되 면 보조 복제본에서 보조 복제본은 주 복제본에 다시 연결을 시도 합니다.<br /><br /> 1: 연결 합니다.<br /><br /> 각 주 복제본이 동일한 가용성 그룹의 모든 보조 복제본에 대한 연결 상태를 추적합니다. 보조 복제본은 주 복제본에 대해서만 연결 상태를 추적합니다.|  
|**connected_state_desc**|**nvarchar(60)**|에 대 한 설명 **connection_state**이며 다음 중 하나입니다.<br /><br /> DISCONNECTED<br /><br /> CONNECTED|  
|**last_connect_error_number**|**int**|마지막 연결 오류의 번호입니다.|  
|**last_connect_error_description**|**nvarchar(1024)**|텍스트는 **last_connect_error_number** 메시지입니다.|  
|**last_connect_error_timestamp**|**datetime**|시간을 나타내는 날짜 및 시간 타임 스탬프는 **last_connect_error_number** 오류가 발생 했습니다.|  
  
##  <a name="RolesAndOperationalStates"></a> 역할 및 작동 상태  
 역할, **역할**, 지정된 된 가용성 복제본의 상태와 작동 상태를 반영 **operational_state**, 복제본이 모두에 대 한 클라이언트 요청을 처리할 준비가 되었는지 여부를 설명 합니다.는 가용성 복제본의 데이터베이스입니다. 다음은 각 역할에 대해 가능한 작동 상태에 대 한 요약: 확인 하 고, 기본 및 보조 합니다.  
  
 **RESOLVING:** 가능한 작동 상태는 다음 표에 나와 있는 것 처럼 가용성 복제본이 RESOLVING 역할인 경우.  
  
|작동 상태|Description|  
|-----------------------|-----------------|  
|PENDING_FAILOVER|장애 조치(failover) 명령이 가용성 그룹에 대해 처리되고 있습니다.|  
|OFFLINE|가용성 복제본에 대한 모든 구성 데이터가 WSFC 클러스터와 로컬 메타데이터에서 업데이트되었지만 가용성 그룹에 현재 주 복제본이 부족합니다.|  
|FAILED|WSFC 클러스터에서 정보를 검색하려고 시도하는 동안 읽기 오류가 발생 했습니다.|  
|FAILED_NO_QUORUM|로컬 WSFC 노드에 쿼럼이 없습니다. 유추된 상태입니다.|  
  
 **기본 사이트:** 가용성 복제본은 주 역할을 수행 하는 것이 현재 주 복제본입니다. 가능한 작동 상태는 다음 표에 나와 있는 것 처럼 됩니다.  
  
|작동 상태|Description|  
|-----------------------|-----------------|  
|PENDING|임시 상태이지만, 작업자가 요청을 처리할 수 없는 경우 주 복제본이 이 상태에서 멈출 수 있습니다.|  
|ONLINE|가용성 그룹 리소스가 온라인 상태이고 모든 데이터베이스 작업자 스레드가 선택되었습니다.|  
|FAILED|가용성 복제본이 WSFC 클러스터에서 읽거나 쓸 수 없습니다.|  
  
 **보조 복제본:** 가용성 복제본은 보조 역할을 수행 하는 경우에 현재 보조 복제본입니다. 가능한 작동 상태는 아래 표에 나와 있는 것 처럼 됩니다.  
  
|작동 상태|Description|  
|-----------------------|-----------------|  
|ONLINE|로컬 보조 복제본이 주 복제본에 연결되어 있습니다.|  
|FAILED|로컬 보조 복제본이 WSFC 클러스터에서 읽거나 쓸 수 없습니다.|  
|NULL|주 복제본에서 행이 보조 복제본과 관련이 있는 경우 이 값이 반환됩니다.|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 그룹 모니터링&#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
