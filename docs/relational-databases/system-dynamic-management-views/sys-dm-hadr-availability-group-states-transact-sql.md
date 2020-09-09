---
description: sys.dm_hadr_availability_group_states(Transact-SQL)
title: sys. dm_hadr_availability_group_states (Transact-sql) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0ca065be60cbe6514d1da606501ff90f72ac1c69
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543909"
---
# <a name="sysdm_hadr_availability_group_states-transact-sql"></a>sys.dm_hadr_availability_group_states(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  의 로컬 인스턴스에서 가용성 복제본을 소유 하는 각 Always On 가용성 그룹에 대해 하나의 행을 반환 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 각 행에는 지정된 가용성 그룹의 상태를 정의하는 상태가 표시됩니다.  
  
> [!NOTE]  
>  의 전체 목록을 얻으려면 [sys. availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) 카탈로그 뷰를 쿼리 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|가용성 그룹의 고유한 식별자입니다.|  
|**primary_replica**|**varchar(128)**|현재 주 복제본을 호스팅하는 서버 인스턴스의 이름입니다.<br /><br /> NULL = 주 복제본이 아니거나 WSFC 장애 조치(Failover) 클러스터와 통신할 수 없습니다.|  
|**primary_recovery_health**|**tinyint**|주 복제본의 복구 상태를 나타내며 다음 중 하나입니다.<br /><br /> 0 = 진행 중<br /><br /> 1 = 온라인<br /><br /> NULL<br /><br /> 보조 복제본에서 **primary_recovery_health** 열은 NULL입니다.|  
|**primary_recovery_health_desc**|**nvarchar(60)**|**Primary_replica_health**에 대 한 설명 이며 다음 중 하나입니다.<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**secondary_recovery_health**|**tinyint**|보조 복제본 복제본의 복구 상태를 나타내며 다음 중 하나입니다.<br /><br /> 0 = 진행 중<br /><br /> 1 = 온라인<br /><br /> NULL<br /><br /> 주 복제본에서 **secondary_recovery_health** 열은 NULL입니다.|  
|**secondary_recovery_health_desc**|**nvarchar(60)**|**Secondary_recovery_health**에 대 한 설명 이며 다음 중 하나입니다.<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**synchronization_health**|**tinyint**|가용성 그룹에 있는 모든 가용성 복제본의 **synchronization_health** 에 대 한 롤업을 반영 합니다. 다음은 가능한 값과 그에 대 한 설명입니다.<br /><br /> 0: 정상이 아닙니다. 정상 상태의 **synchronization_health** 있는 가용성 복제본이 없습니다 (2 = 정상).<br /><br /> 1: 부분 정상 가용성 복제본의 전체가 아닌 일부의 동기화 상태가 정상입니다.<br /><br /> 2: 정상. 모든 가용성 복제본의 동기화 상태가 정상입니다.<br /><br /> 복제본 동기화 상태에 대 한 자세한 내용은 [dm_hadr_availability_replica_states &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md)에서 **synchronization_health** 열을 참조 하세요.|  
|**synchronization_health_desc**|**nvarchar(60)**|**Synchronization_health**에 대 한 설명 이며 다음 중 하나입니다.<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;가용성 그룹 모니터링 ](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Always On 가용성 그룹&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Always On 가용성 그룹 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)  
  
  
