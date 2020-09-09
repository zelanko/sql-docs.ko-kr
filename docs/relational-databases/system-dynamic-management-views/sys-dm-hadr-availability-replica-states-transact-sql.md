---
description: sys.dm_hadr_availability_replica_states(Transact-SQL)
title: sys. dm_hadr_availability_replica_states (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 10/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 347d05c0bfc37b1c14fddb728df5508e062cb13d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546564"
---
# <a name="sysdm_hadr_availability_replica_states-transact-sql"></a>sys.dm_hadr_availability_replica_states(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  각 로컬 복제본에 대해 하나의 행을 반환하고 로컬 복제본과 동일한 Always On 가용성 그룹의 각 원격 복제본에 대해 하나의 행을 반환합니다. 각 행에는 지정된 복제본의 상태에 대한 정보가 들어 있습니다.  
  
> [!IMPORTANT]  
>  지정 된 가용성 그룹의 모든 복제본에 대 한 정보를 얻으려면 주 복제본을 호스트 하는 서버 인스턴스에서 **dm_hadr_availability_replica_states** 를 쿼리 합니다. 가용성 그룹의 보조 복제본을 호스팅 중인 서버 인스턴스에 대해 쿼리한 경우 이 동적 관리 뷰에는 가용성 그룹에 대한 로컬 정보만 반환됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|복제본의 고유 식별자입니다.|  
|**group_id**|**uniqueidentifier**|가용성 그룹의 고유한 식별자입니다.|  
|**is_local**|**bit**|복제본이 로컬 인지 여부를 지정 합니다. 다음 중 하나입니다.<br /><br /> 0 = 주 복제본이 로컬 서버 인스턴스에 의해 호스팅되는 가용성 그룹의 원격 보조 복제본을 나타냅니다. 이 값은 주 복제본 위치에서만 발생합니다.<br /><br /> 1 = 로컬 복제본을 나타냅니다. 보조 복제본에서는 복제본이 속하는 가용성 그룹에 대해 이 값만 사용할 수 있습니다.|  
|**role**|**tinyint**|[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]로컬 복제본 또는 연결 된 원격 복제본의 현재 역할 이며 다음 중 하나입니다.<br /><br /> 0 = 확인 중<br /><br /> 1 = 주<br /><br /> 2 = 보조<br /><br /> [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 역할에 대한 자세한 내용은 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)를 참조하세요.|  
|**role_desc**|**nvarchar(60)**|**역할**에 대 한 설명 이며 다음 중 하나입니다.<br /><br /> RESOLVING<br /><br /> PRIMARY<br /><br /> SECONDARY|  
|**operational_state**|**tinyint**|복제본의 현재 작동 상태 이며 다음 중 하나입니다.<br /><br /> 0 = 장애 조치(Failover) 보류 중<br /><br /> 1 = 보류 중<br /><br /> 2 = 온라인<br /><br /> 3 = 오프 라인<br /><br /> 4 = 실패<br /><br /> 5 = 실패, 쿼럼 없음<br /><br /> NULL = 복제본이 로컬이 아닙니다.<br /><br /> 자세한 내용은이 항목의 뒷부분에 나오는 [역할 및 작동 상태](#RolesAndOperationalStates)를 참조 하세요.|  
|**작동 \_ 상태 \_ desc**|**nvarchar(60)**|**작동 \_ 상태**에 대 한 설명 이며 다음 중 하나입니다.<br /><br /> PENDING_FAILOVER<br /><br /> PENDING<br /><br /> ONLINE<br /><br /> OFFLINE<br /><br /> FAILED<br /><br /> FAILED_NO_QUORUM<br /><br /> NULL|  
|**복구 \_ 상태**|**tinyint**|[Sys. dm_hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) 동적 관리 뷰의 **데이터베이스 \_ 상태** 열에 대 한 롤업 다음은 가능한 값과 그에 대 한 설명입니다.<br /><br /> 0: 진행 중  하나 이상의 조인 된 데이터베이스의 데이터베이스 상태가 온라인이 아닙니다 (**데이터베이스 \_ 상태가** 0이 아님).<br /><br /> 1: 온라인. 조인 된 모든 데이터베이스의 데이터베이스 상태는 온라인 (**database_state** 0)입니다.<br /><br /> NULL: **is_local** = 0|  
|**recovery_health_desc**|**nvarchar(60)**|**Recovery_health**에 대 한 설명 이며 다음 중 하나입니다.<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**동기화 \_ 상태**|**tinyint**|조인 된 모든 가용성 데이터베이스 ( *복제본*이 라고도 함) 및 복제본의 가용성 모드 (동기 커밋 또는 비동기 커밋 모드)의 데이터베이스 동기화 상태 (**synchronization_state**) 롤업을 반영 합니다. Rollup은 복제본의 데이터베이스에 대 한 최소 정상 누적 상태를 반영 합니다. 다음은 가능한 값과 그에 대 한 설명입니다.<br /><br /> 0: 정상이 아닙니다.   하나 이상의 조인된 데이터베이스가 NOT SYNCHRONIZING 상태입니다.<br /><br /> 1: 부분 정상 일부 복제본이 대상 동기화 상태에 있지 않습니다. 동기-커밋 복제본을 동기화 하 고 비동기-커밋 복제본을 동기화 해야 합니다.<br /><br /> 2: 정상. 모든 복제본이 대상 동기화 상태입니다. 동기-커밋 복제본이 동기화 되 고 비동기-커밋 복제본이 동기화 됩니다.|  
|**synchronization_health_desc**|**nvarchar(60)**|**Synchronization_health**에 대 한 설명 이며 다음 중 하나입니다.<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
|**connected_state**|**tinyint**|보조 복제본이 주 복제본에 현재 연결 되어 있는지 여부를 나타냅니다. 가능한 값은 아래와 같이 설명 합니다.<br /><br /> 0: 연결 끊김 연결 끊김 상태의 가용성 복제본에 대 한 응답은 해당 역할에 따라 다릅니다. 주 복제본에서 보조 복제본의 연결이 끊어지면 보조 데이터베이스는 주 복제본에 동기화 되지 않음으로 표시 되 고 보조 복제본은 보조 복제본이 다시 연결 될 때까지 대기 합니다. 보조 복제본의 연결이 끊어지면 보조 복제본은 주 복제본에 다시 연결 하려고 시도 합니다.<br /><br /> 1: 연결 됨<br /><br /> 각 주 복제본이 동일한 가용성 그룹의 모든 보조 복제본에 대한 연결 상태를 추적합니다. 보조 복제본은 주 복제본에 대해서만 연결 상태를 추적합니다.|  
|**connected_state_desc**|**nvarchar(60)**|**Connection_state**에 대 한 설명 이며 다음 중 하나입니다.<br /><br /> DISCONNECTED<br /><br /> CONNECTED|  
|**last_connect_error_number**|**int**|마지막 연결 오류의 번호입니다.|  
|**last_connect_error_description**|**nvarchar(1024)**|**Last_connect_error_number** 메시지의 텍스트입니다.|  
|**last_connect_error_timestamp**|**datetime**|**Last_connect_error_number** 오류가 발생 한 시간을 나타내는 날짜 및 시간 타임 스탬프입니다.|  
  
##  <a name="roles-and-operational-states"></a><a name="RolesAndOperationalStates"></a> 역할 및 작동 상태  
 Role **역할은**지정 된 가용성 복제본의 상태를 반영 하 고 작동 상태 **operational_state**는 복제본이 가용성 복제본의 모든 데이터베이스에 대 한 클라이언트 요청을 처리할 준비가 되었는지 여부를 설명 합니다. 다음은 각 역할에 대해 가능한 작동 상태를 요약 한 것입니다. 각 역할은 해결, 기본 및 보조입니다.  
  
 **해결 방법:** 가용성 복제본이 확인 역할에 있는 경우 가능한 작동 상태는 다음 표에 나와 있는 것과 같습니다.  
  
|작동 상태|Description|  
|-----------------------|-----------------|  
|PENDING_FAILOVER|장애 조치(failover) 명령이 가용성 그룹에 대해 처리되고 있습니다.|  
|OFFLINE|가용성 복제본에 대한 모든 구성 데이터가 WSFC 클러스터와 로컬 메타데이터에서 업데이트되었지만 가용성 그룹에 현재 주 복제본이 부족합니다.|  
|FAILED|WSFC 클러스터에서 정보를 검색하려고 시도하는 동안 읽기 오류가 발생 했습니다.|  
|FAILED_NO_QUORUM|로컬 WSFC 노드에 쿼럼이 없습니다. 유추된 상태입니다.|  
  
 **기본:** 가용성 복제본이 주 역할을 수행 하는 경우 현재 주 복제본입니다. 가능한 작동 상태는 다음 표에 나와 있습니다.  
  
|작동 상태|Description|  
|-----------------------|-----------------|  
|PENDING|임시 상태이지만, 작업자가 요청을 처리할 수 없는 경우 주 복제본이 이 상태에서 멈출 수 있습니다.|  
|ONLINE|가용성 그룹 리소스가 온라인 상태이고 모든 데이터베이스 작업자 스레드가 선택되었습니다.|  
|FAILED|가용성 복제본이 WSFC 클러스터에서 읽거나 쓸 수 없습니다.|  
  
 **보조:** 가용성 복제본이 보조 역할을 수행 하는 경우 현재 보조 복제본입니다. 가능한 작동 상태는 아래 표에 표시 된 것과 같습니다.  
  
|작동 상태|Description|  
|-----------------------|-----------------|  
|ONLINE|로컬 보조 복제본이 주 복제본에 연결되어 있습니다.|  
|FAILED|로컬 보조 복제본이 WSFC 클러스터에서 읽거나 쓸 수 없습니다.|  
|NULL|주 복제본에서 행이 보조 복제본과 관련이 있는 경우 이 값이 반환됩니다.|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 그룹 모니터링&#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
