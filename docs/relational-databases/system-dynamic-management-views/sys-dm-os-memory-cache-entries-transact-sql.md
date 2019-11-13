---
title: sys. dm_os_memory_cache_entries (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_memory_cache_entries
- sys.dm_os_memory_cache_entries
- dm_os_memory_cache_entries_TSQL
- sys.dm_os_memory_cache_entries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_entries dynamic management view
ms.assetid: dd32be6b-10d1-4059-b4fd-0bf817f40d54
author: stevestein
ms.author: sstein
ms.openlocfilehash: 737de971ca39cdf8c164787ff7703b87c38e92e2
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2019
ms.locfileid: "73983117"
---
# <a name="sysdm_os_memory_cache_entries-transact-sql"></a>sys.dm_os_memory_cache_entries(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 캐시에 있는 모든 항목에 대한 정보를 반환합니다. 이 뷰를 사용하여 캐시 항목과 연관된 개체를 추적할 수 있고 캐시 항목에 대한 통계를 얻을 수도 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서이를 호출 하려면 **dm_pdw_nodes_os_memory_cache_entries**이름을 사용 합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|캐시 주소입니다. Null을 허용하지 않습니다.|  
|**name**|**nvarchar(256)**|캐시의 이름입니다. Null을 허용하지 않습니다.|  
|**유형**|**varchar(60)**|캐시 유형입니다. Null을 허용하지 않습니다.|  
|**entry_address**|**varbinary(8)**|캐시 항목의 설명자 주소입니다. Null을 허용하지 않습니다.|  
|**entry_data_address**|**varbinary(8)**|캐시 항목에 있는 사용자 데이터의 주소입니다.<br /><br /> 0x00000000 = 항목 데이터 주소를 사용할 수 없습니다.<br /><br /> Null을 허용하지 않습니다.|  
|**in_use_count**|**int**|이 캐시 항목의 동시 사용자 수입니다. Null을 허용하지 않습니다.|  
|**is_dirty**|**bit**|이 캐시 항목을 제거하도록 표시할지 여부를 나타납니다. 1 = 제거하도록 표시합니다. Null을 허용하지 않습니다.|  
|**disk_ios_count**|**int**|이 항목을 만드는 동안 발생한 I/O 수입니다. Null을 허용하지 않습니다.|  
|**context_switches_count**|**int**|이 항목을 만드는 동안 발생한 컨텍스트 전환 수입니다. Null을 허용하지 않습니다.|  
|**original_cost**|**int**|항목의 원래 비용입니다. 이 값은 발생한 I/O 수, CPU 명령 비용 및 항목에서 사용하는 메모리 양에 대한 근사 값입니다. 비용이 높아질수록 캐시에서 항목이 제거될 가능성은 낮아집니다. Null을 허용하지 않습니다.|  
|**current_cost**|**int**|캐시 항목의 현재 비용입니다. 이 값은 항목 제거 프로세스 중에 업데이트됩니다. 항목을 다시 사용할 경우 현재 비용이 원래 값으로 다시 설정됩니다. Null을 허용하지 않습니다.|  
|**memory_object_address**|**varbinary(8)**|연관된 메모리 개체의 주소입니다. Null을 허용합니다.|  
|**pages_allocated_count**|**bigint**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]까지<br /><br /> 이 캐시 항목을 저장하는 8KB 페이지의 수입니다. Null을 허용하지 않습니다.|  
|**pages_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> 이 캐시 항목에서 사용하는 메모리 양(KB)입니다.  Null을 허용하지 않습니다.|  
|**entry_data**|**nvarchar(2048)**|캐시된 항목의 직렬화된 표현입니다. 이 정보는 캐시 저장소에 따라 달라집니다. Null을 허용합니다.|  
|**pool_id**|**int**|**적용 대상**: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 이상<br /><br /> 항목과 연관된 리소스 풀 ID입니다. Null을 허용합니다.<br /><br /> katmai 아님|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
## <a name="permissions"></a>사용 권한 

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에서 `VIEW SERVER STATE` 권한이 필요 합니다.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 프리미엄 계층에는 데이터베이스에 대 한 `VIEW DATABASE STATE` 권한이 필요 합니다. [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard 및 Basic 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   

## <a name="see-also"></a>참고 항목  
 
  [운영 체제 관련 동적 관리 뷰 &#40;transact-sql SQL Server&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


