---
title: sys.dm_os_memory_pools (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_pools_TSQL
- dm_os_memory_pools
- dm_os_memory_pools_TSQL
- sys.dm_os_memory_pools
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_pools dynamic management view
ms.assetid: 1ef053f3-c6f3-456e-82b6-26e4bd630d46
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0de67bd53b568f77a16fd10903a5d0c3fddfce4c
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34466190"
---
# <a name="sysdmosmemorypools-transact-sql"></a>sys.dm_os_memory_pools(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 각 개체 저장소에 대해 하나의 행을 반환합니다. 이 뷰를 사용하여 캐시 메모리 사용을 모니터링하고 잘못된 캐싱 동작을 확인할 수 있습니다.  
  
> [!NOTE]  
>  이 메서드를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_os_memory_pools**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**memory_pool_address**|**varbinary(8)**|메모리 풀을 나타내는 항목의 메모리 주소입니다. Null을 허용하지 않습니다.|  
|**pool_id**|**int**|풀 집합 내에 있는 특정 풀의 ID입니다. Null을 허용하지 않습니다.|  
|**type**|**nvarchar(60)**|개체 풀의 유형입니다. Null을 허용하지 않습니다. 자세한 내용은 참조 [sys.dm_os_memory_clerks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)합니다.|  
|**name**|**nvarchar(256)**|시스템에서 할당된 이 메모리 개체의 이름입니다. Null을 허용하지 않습니다.|  
|**max_free_entries_count**|**bigint**|풀에 포함될 수 있는 사용 가능한 최대 항목 수입니다. Null을 허용하지 않습니다.|  
|**free_entries_count**|**bigint**|풀에서 현재 사용 가능한 항목 수입니다. Null을 허용하지 않습니다.|  
|**removed_in_all_rounds_count**|**bigint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 시작된 이후 풀에서 제거된 항목 수입니다. Null을 허용하지 않습니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="permissions"></a>Permissions

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다.   

## <a name="remarks"></a>주의  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소가 공용 풀 프레임워크를 사용하여 유형이 같은 상태 비저장 유형의 데이터를 캐싱하는 경우가 있습니다. 풀 프레임워크는 캐시 프레임워크보다 간단합니다. 풀의 모든 항목은 동일하게 간주됩니다. 내부적으로 풀은 메모리 클럭이며 메모리 클럭이 사용되는 곳에 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 
  [SQL Server 운영 체제 관련 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


