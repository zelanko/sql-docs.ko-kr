---
title: sys.dm_os_memory_nodes (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_memory_nodes_TSQL
- sys.dm_os_memory_nodes
- sys.dm_os_memory_nodes_TSQL
- dm_os_memory_nodes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_nodes dynamic management view
ms.assetid: bf4032fe-7db1-40e9-a62e-d69cebff4b44
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 91f30ee2c8a11c936480658af3c8ee0a4ddbf973
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmosmemorynodes-transact-sql"></a>sys.dm_os_memory_nodes(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부의 할당은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 관리자를 사용합니다. 프로세스 메모리 카운터 간의 차이 추적 **sys.dm_os_process_memory** 내부 카운터의 외부 구성 요소에서 메모리 사용을 나타낼 수 있습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 공간입니다.  
  
 노드는 물리적 NUMA 메모리 노드별로 생성됩니다. CPU 노드와 다를 수 있습니다 이러한 **sys.dm_os_nodes**합니다.  
  
 Windows 메모리 할당 루틴을 통한 직접적인 할당은 추적되지 않습니다. 다음 표에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 관리자 인터페이스를 통해서만 이루어진 메모리 할당에 대한 정보가 나와 있습니다.  
  
> [!NOTE]  
>  이 메서드를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_os_memory_nodes**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**memory_node_id**|**smallint**|메모리 노드의 ID를 지정합니다. 관련 된 **되어** 의 **sys.dm_os_memory_clerks**합니다. Null을 허용하지 않습니다.|  
|**virtual_address_space_reserved_kb**|**bigint**|물리적 페이지에 커밋 또는 매핑되지 않은 가상 주소 예약의 크기(KB)를 나타냅니다. Null을 허용하지 않습니다.|  
|**virtual_address_space_committed_kb**|**bigint**|물리적 페이지에 커밋 또는 매핑된 가상 주소 크기(KB)를 지정합니다. Null을 허용하지 않습니다.|  
|**locked_page_allocations_kb**|**bigint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 의해 잠긴 물리적 메모리 크기(KB)를 지정합니다. Null을 허용하지 않습니다.|  
|**single_pages_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]까지<br /><br /> 이 노드에서 실행 중인 스레드별로 단일 페이지 할당자를 사용하여 할당된 커밋된 메모리 크기(KB)입니다. 이 메모리는 버퍼 풀에서 할당됩니다. 이 값은 할당 요청이 충족된 물리적 위치가 아닌 할당 요청이 발생한 지점의 노드를 나타냅니다.|  
|**pages_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> Memory Manager 페이지 할당자에 의해 이 NUMA 노드에서 할당되는 커밋된 메모리 크기(KB)를 지정합니다. Null을 허용하지 않습니다.|  
|**multi_pages_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]까지<br /><br /> 이 노드에서 실행 중인 스레드별로 다중 페이지 할당자를 사용하여 할당된 커밋된 메모리의 크기(KB)입니다. 이 메모리는 버퍼 풀 외부에 있습니다. 이 값은 할당 요청이 충족된 물리적 위치가 아닌 할당 요청이 발생한 지점의 노드를 나타냅니다.|  
|**shared_memory_reserved_kb**|**bigint**|이 노드에서 예약된 공유 메모리 크기(KB)를 지정합니다. Null을 허용하지 않습니다.|  
|**shared_memory_committed_kb**|**bigint**|이 노드에서 커밋된 공유 메모리 크기(KB)를 지정합니다. Null을 허용하지 않습니다.|  
|**cpu_affinity_mask**|**bigint**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 내부적으로만 사용됩니다. Null을 허용하지 않습니다.|  
|**online_scheduler_mask**|**bigint**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 내부적으로만 사용됩니다. Null을 허용하지 않습니다.|  
|**processor_group**|**smallint**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 내부적으로만 사용됩니다. Null을 허용하지 않습니다.|  
|**foreign_committed_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 다른 메모리 노드에서 커밋된 메모리 크기(KB)를 지정합니다. Null을 허용하지 않습니다.|  
|**target_kb** |**bigint** |**적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]까지<br /><br /> KB 단위로 메모리 노드에 대 한 메모리 목표를 지정 합니다. |   
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="permissions"></a>Permissions

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다.   

## <a name="see-also"></a>관련 항목:  
  [SQL Server 운영 체제 관련 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


