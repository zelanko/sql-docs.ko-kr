---
title: sys.dm_os_memory_cache_counters (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_cache_counters_TSQL
- dm_os_memory_cache_counters_TSQL
- sys.dm_os_memory_cache_counters
- dm_os_memory_cache_counters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_counters dynamic management view
ms.assetid: ca7bd036-d661-4c17-b00a-e1a975bd8932
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c5a513e851ed7a521009d39c927d2e5f94335994
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/05/2018
---
# <a name="sysdmosmemorycachecounters-transact-sql"></a>sys.dm_os_memory_cache_counters(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 캐시의 상태에 대한 스냅숏을 반환합니다. **sys.dm_os_memory_cache_counters** 캐시 항목에 대 한 할당 된 캐시 항목에 대 한 런타임 정보, 사용 및 메모리의 소스를 제공 합니다.  
  
> **참고:** 로 표현에서 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_os_memory_cache_counters**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|특정 캐시와 연결된 카운터의 주소(기본 키)를 나타냅니다. Null을 허용하지 않습니다.|  
|**name**|**nvarchar(256)**|캐시 이름을 지정합니다. Null을 허용하지 않습니다.|  
|**type**|**nvarchar(60)**|이 항목과 연결된 캐시의 유형을 나타냅니다. Null을 허용하지 않습니다.|  
|**single_pages_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]까지<br /><br /> 할당된 단일 페이지 메모리의 양(KB)입니다. 이것은 단일 페이지 할당자를 사용하여 할당된 메모리의 양이며 이 캐시의 버퍼 풀에서 직접 가져온 8KB 페이지를 참조합니다. Null을 허용하지 않습니다.|  
|**pages_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 캐시에 할당된 메모리의 양(KB)을 지정합니다. Null을 허용하지 않습니다.|  
|**multi_pages_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]까지<br /><br /> 할당된 다중 페이지 메모리의 양(KB)입니다. 이것은 메모리 노드의 다중 페이지 할당자를 사용하여 할당된 메모리 양입니다. 이 메모리는 버퍼 풀 외부에 할당되며 메모리 노드의 가상 할당자를 사용합니다. Null을 허용하지 않습니다.|  
|**pages_in_use_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 캐시에 할당되어 사용 중인 메모리의 양(KB)을 지정합니다. Null을 허용합니다.  `USERSTORE_<*>` 유형의 개체에 대한 값은 추적되지 않습니다.  개체 값에 대해 NULL이 보고됩니다.|  
|**single_pages_in_use_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]까지<br /><br /> 사용 중인 단일 페이지 메모리의 양(KB)입니다. Null을 허용합니다. USERSTORE_ 유형의 개체에 대 한이 정보가 추적 되지\<* > 않으며 이러한 값은 NULL입니다.|  
|**multi_pages_in_use_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]까지<br /><br /> 사용 중인 다중 페이지 메모리의 양(KB)입니다. NULL을 허용합니다. USERSTORE_ 유형의 개체에 대 한이 정보가 추적 되지\<* >, 않으며 이러한 값은 NULL입니다.|  
|**entries_count**|**bigint**|캐시에 있는 항목의 개수를 나타냅니다. Null을 허용하지 않습니다.|  
|**entries_in_use_count**|**bigint**|캐시에 있는 사용 중인 항목의 개수를 나타냅니다. Null을 허용하지 않습니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="permissions"></a>Permissions 

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다.   

## <a name="see-also"></a>관련 항목:  
  [SQL Server 운영 체제 관련 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


