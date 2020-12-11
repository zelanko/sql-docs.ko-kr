---
description: sys.dm_os_memory_cache_counters(Transact-SQL)
title: sys.dm_os_memory_cache_counters (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6d5a10ea51c39aea00e73c74169c4acd4a94d615
ms.sourcegitcommit: 2991ad5324601c8618739915aec9b184a8a49c74
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97331905"
---
# <a name="sysdm_os_memory_cache_counters-transact-sql"></a>sys.dm_os_memory_cache_counters(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 캐시의 상태에 대한 스냅샷을 반환합니다. **sys.dm_os_memory_cache_counters** 할당 된 캐시 항목에 대 한 런타임 정보를 제공 하 고, 사용 하 고, 캐시 엔트리에 대 한 메모리 소스를 제공 합니다.  
  
> **참고:** 또는에서이를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] **sys.dm_pdw_nodes_os_memory_cache_counters** 이름을 사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|특정 캐시와 연결된 카운터의 주소(기본 키)를 나타냅니다. Null을 허용하지 않습니다.|  
|**name**|**nvarchar(256)**|캐시 이름을 지정합니다. Null을 허용하지 않습니다.|  
|**type**|**nvarchar(60)**|이 항목과 연결된 캐시의 유형을 나타냅니다. Null을 허용하지 않습니다.|  
|**single_pages_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]까지<br /><br /> 할당된 단일 페이지 메모리의 양(KB)입니다. 이것은 단일 페이지 할당자를 사용하여 할당된 메모리의 양이며 이 캐시의 버퍼 풀에서 직접 가져온 8KB 페이지를 참조합니다. Null을 허용하지 않습니다.|  
|**pages_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> 캐시에 할당된 메모리의 양(KB)을 지정합니다. Null을 허용하지 않습니다.|  
|**multi_pages_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]까지<br /><br /> 할당된 다중 페이지 메모리의 양(KB)입니다. 이것은 메모리 노드의 다중 페이지 할당자를 사용하여 할당된 메모리 양입니다. 이 메모리는 버퍼 풀 외부에 할당되며 메모리 노드의 가상 할당자를 사용합니다. Null을 허용하지 않습니다.|  
|**pages_in_use_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> 캐시에 할당되어 사용 중인 메모리의 양(KB)을 지정합니다. Null을 허용합니다.  `USERSTORE_<*>` 유형의 개체에 대한 값은 추적되지 않습니다.  개체 값에 대해 NULL이 보고됩니다.|  
|**single_pages_in_use_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]까지<br /><br /> 사용 중인 단일 페이지 메모리의 양(KB)입니다. Null을 허용합니다. USERSTORE_ 형식의 개체에 대해서는이 정보가 추적 되지 않으며 \<*> , 이러한 값은 NULL입니다.|  
|**multi_pages_in_use_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]까지<br /><br /> 사용 중인 다중 페이지 메모리의 양(KB)입니다. NULL을 허용합니다. USERSTORE_ 형식의 개체에 대해서는이 정보가 추적 되지 않으며 \<*> , 이러한 값은 NULL입니다.|  
|**entries_count**|**bigint**|캐시에 있는 항목의 개수를 나타냅니다. Null을 허용하지 않습니다.|  
|**entries_in_use_count**|**bigint**|캐시에 있는 사용 중인 항목의 개수를 나타냅니다. Null을 허용하지 않습니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
## <a name="permissions"></a>사용 권한 

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
SQL Database Basic, S0 및 S1 서비스 목적과 탄력적 풀의 데이터베이스에 대해서는 `Server admin` 또는 `Azure Active Directory admin` 계정이 필요 합니다. 다른 모든 SQL Database 서비스 목표에서 `VIEW DATABASE STATE` 사용 권한은 데이터베이스에서 필요 합니다.   

## <a name="see-also"></a>참고 항목  
  [Transact-sql&#41;&#40;운영 체제 관련 동적 관리 뷰 SQL Server ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


