---
title: sys.dm_hadr_availability_group_states (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_availability_group_states
- sys.dm_hadr_availability_group_states_TSQL
- dm_hadr_availability_group_states_TSQL
- dm_hadr_availability_group_states
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_availability_group_states dynamic management view
ms.assetid: d18019dd-f8dc-4492-b035-b1a639369b65
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b06ffc7a8400d3b02698009b2452282658cf959e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47745361"
---
# <a name="sysdmhadravailabilitygroupstates-transact-sql"></a>sys.dm_hadr_availability_group_states(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  로컬 인스턴스에서 가용성 복제본이 있는 각 Always On 가용성 그룹에 대 한 행을 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 각 행에는 지정된 가용성 그룹의 상태를 정의하는 상태가 표시됩니다.  
  
> [!NOTE]  
>  전체 목록은 쿼리 합니다 [sys.availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) 카탈로그 뷰.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|가용성 그룹의 고유한 식별자입니다.|  
|**primary_replica**|**varchar(128)**|현재 주 복제본을 호스팅하는 서버 인스턴스의 이름입니다.<br /><br /> NULL = 주 복제본이 아니거나 WSFC 장애 조치(Failover) 클러스터와 통신할 수 없습니다.|  
|**primary_recovery_health**|**tinyint**|주 복제본의 복구 상태를 나타내며 다음 중 하나입니다.<br /><br /> 0 = 진행 중<br /><br /> 1 = 온라인<br /><br /> NULL<br /><br /> 보조 복제본에는 **primary_recovery_health** 열은 NULL입니다.|  
|**primary_recovery_health_desc**|**nvarchar(60)**|에 대 한 설명을 **primary_replica_health**하나씩입니다.<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**secondary_recovery_health**|**tinyint**|복구 상태를 보조 복제본 중 하나를 나타냅니다.<br /><br /> 0 = 진행 중<br /><br /> 1 = 온라인<br /><br /> NULL<br /><br /> 주 복제본에는 **secondary_recovery_health** 열은 NULL입니다.|  
|**secondary_recovery_health_desc**|**nvarchar(60)**|에 대 한 설명을 **secondary_recovery_health**하나씩입니다.<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**synchronization_health**|**tinyint**|에 대 한 롤업을 반영 합니다 **synchronization_health** 가용성 그룹의 모든 가용성 복제본의 합니다. 가능한 값 및 해당 설명이 같습니다.<br /><br /> 0: 올바른 상태가 아닙니다. 가용성 복제본이 하나도 정상 상태인 **synchronization_health** (2 = 정상).<br /><br /> 1: 부분적으로 정상. 가용성 복제본의 전체가 아닌 일부의 동기화 상태가 정상입니다.<br /><br /> 2: 정상 상태입니다. 모든 가용성 복제본의 동기화 상태가 정상입니다.<br /><br /> 복제본 동기화 상태에 대 한 자세한 참조를 **synchronization_health** 열에 [sys.dm_hadr_availability_replica_states &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md).|  
|**synchronization_health_desc**|**nvarchar(60)**|에 대 한 설명을 **synchronization_health**하나씩입니다.<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목  
 [가용성 그룹 모니터링&#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Always On 가용성 그룹&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Always On 가용성 그룹 동적 관리 뷰 및 함수 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)  
  
  
