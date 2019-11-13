---
title: sys. dm_os_memory_cache_counters (Transact-sql) | Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 755e0cdbf5bff5bcd9c048a2f77918dc9a6eb2a3
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982532"
---
# <a name="sysdm_os_memory_cache_counters-transact-sql"></a>sys.dm_os_memory_cache_counters(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 캐시의 상태에 대한 스냅샷을 반환합니다. **dm_os_memory_cache_counters** 할당 된 캐시 항목에 대 한 런타임 정보를 제공 하 고, 사용 하 고, 캐시 엔트리에 대 한 메모리의 소스를 제공 합니다.  
  
> **참고:** [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서이를 호출 하려면 **dm_pdw_nodes_os_memory_cache_counters**이름을 사용 합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|특정 캐시와 연결된 카운터의 주소(기본 키)를 나타냅니다. Null을 허용하지 않습니다.|  
|**name**|**nvarchar(256)**|캐시 이름을 지정합니다. Null을 허용하지 않습니다.|  
|**유형**|**nvarchar(60)**|이 항목과 연결된 캐시의 유형을 나타냅니다. Null을 허용하지 않습니다.|  
|**single_pages_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]까지<br /><br /> 할당된 단일 페이지 메모리의 양(KB)입니다. 이것은 단일 페이지 할당자를 사용하여 할당된 메모리의 양이며 이 캐시의 버퍼 풀에서 직접 가져온 8KB 페이지를 참조합니다. Null을 허용하지 않습니다.|  
|**pages_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> 캐시에 할당된 메모리의 양(KB)을 지정합니다. Null을 허용하지 않습니다.|  
|**multi_pages_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]까지<br /><br /> 할당된 다중 페이지 메모리의 양(KB)입니다. 이것은 메모리 노드의 다중 페이지 할당자를 사용하여 할당된 메모리 양입니다. 이 메모리는 버퍼 풀 외부에 할당되며 메모리 노드의 가상 할당자를 사용합니다. Null을 허용하지 않습니다.|  
|**pages_in_use_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> 캐시에 할당되어 사용 중인 메모리의 양(KB)을 지정합니다. Null을 허용합니다.  `USERSTORE_<*>` 유형의 개체에 대한 값은 추적되지 않습니다.  개체 값에 대해 NULL이 보고됩니다.|  
|**single_pages_in_use_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]까지<br /><br /> 사용 중인 단일 페이지 메모리의 양(KB)입니다. Null을 허용합니다. 이 정보는 USERSTORE_\<* > 형식의 개체에 대해 추적 되지 않으며, 이러한 값은 NULL입니다.|  
|**multi_pages_in_use_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]까지<br /><br /> 사용 중인 다중 페이지 메모리의 양(KB)입니다. NULL을 허용합니다. 이 정보는 USERSTORE_\<* > 형식의 개체에 대해 추적 되지 않으며, 이러한 값은 NULL입니다.|  
|**entries_count**|**bigint**|캐시에 있는 항목의 개수를 나타냅니다. Null을 허용하지 않습니다.|  
|**entries_in_use_count**|**bigint**|캐시에 있는 사용 중인 항목의 개수를 나타냅니다. Null을 허용하지 않습니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
## <a name="permissions"></a>사용 권한 

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에서 `VIEW SERVER STATE` 권한이 필요 합니다.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 프리미엄 계층에는 데이터베이스에 대 한 `VIEW DATABASE STATE` 권한이 필요 합니다. [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard 및 Basic 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   

## <a name="see-also"></a>참고 항목  
  [운영 체제 관련 동적 관리 뷰 &#40;transact-sql SQL Server&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


