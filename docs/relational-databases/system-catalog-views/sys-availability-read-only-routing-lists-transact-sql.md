---
description: sys.availability_read_only_routing_lists(Transact-SQL)
title: sys. availability_read_only_routing_lists (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- availability_read_only_routing_lists_TSQL
- availability_read_only_routing_lists
- sys.availability_read_only_routing_lists
- sys.availability_read_only_routing_lists_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- read-only routing
- Availability Groups [SQL Server], readable secondary replicas
- Availability Groups [SQL Server], read-only routing
- readable secondary replicas
- sys.availability_read_only_routing_lists dynamic management view
ms.assetid: 0686bc5a-c206-41ef-b40a-79a8259d51d2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 88d9f7757489e929f9e7981600f66a34ef79e920
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537486"
---
# <a name="sysavailability_read_only_routing_lists-transact-sql"></a>sys.availability_read_only_routing_lists(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  WSFC 장애 조치(Failover) 클러스터의 Always On 가용성 그룹에서 각각의 가용성 복제본의 읽기 전용 라우팅 목록에 대한 행을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|라우팅 목록을 소유하는 가용성 복제본의 고유 ID입니다.|  
|**routing_priority**|**int**|라우팅 우선 순위입니다(1이 우선 순위가 가장 높고 2가 그 다음으로 높음).|  
|**read_only_replica_id**|**uniqueidentifier**|읽기 전용 작업이 라우팅될 가용성 복제본의 고유한 ID입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 동적 관리 뷰 및 함수 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 가용성 그룹 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;가용성 그룹 모니터링 ](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Always On 가용성 그룹&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
