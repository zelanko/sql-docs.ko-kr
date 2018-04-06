---
title: sys.dm_os_memory_objects (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql-non-specified
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
- dm_os_memory_objects
- sys.dm_os_memory_objects
- sys.dm_os_memory_objects_TSQL
- dm_os_memory_objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_objects dynamic management view
ms.assetid: 5688bcf8-5da9-4ff9-960b-742b671d7096
caps.latest.revision: 40
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d348f0c9cf748228e9eb3a55ebf6bc04c329a19a
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/05/2018
---
# <a name="sysdmosmemoryobjects-transact-sql"></a>sys.dm_os_memory_objects(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 의해 현재 할당된 메모리 개체를 반환합니다. 사용할 수 있습니다 **sys.dm_os_memory_objects** 누수 메모리 사용을 분석 하 고 가능한 메모리를 확인 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**memory_object_address**|**varbinary(8)**|메모리 개체의 주소입니다. Null을 허용하지 않습니다.|  
|**parent_address**|**varbinary(8)**|상위 메모리 개체의 주소입니다. Null을 허용합니다.|  
|**pages_allocated_count**|**int**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]까지<br /><br /> 이 개체에서 할당한 페이지 수입니다. Null을 허용하지 않습니다.|  
|**pages_in_bytes**|**bigint**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 메모리 개체의 이 인스턴스에서 할당하는 메모리의 양(바이트)입니다. Null을 허용하지 않습니다.|  
|**creation_options**|**int**|내부적으로만 사용됩니다. Null을 허용합니다.|  
|**bytes_used**|**bigint**|내부적으로만 사용됩니다. Null을 허용합니다.|  
|**type**|**nvarchar(60)**|메모리 개체의 유형입니다.<br /><br /> 이 메모리 개체가 속한 구성 요소 또는 메모리 개체의 기능을 나타냅니다. Null을 허용합니다.|  
|**name**|**varchar(128)**|내부적으로만 사용됩니다. Null을 허용합니다.|  
|**memory_node_id**|**smallint**|이 메모리 개체에서 사용하고 있는 메모리 노드의 ID입니다. Null을 허용하지 않습니다.|  
|**creation_time**|**datetime**|내부적으로만 사용됩니다. Null을 허용합니다.|  
|**max_pages_allocated_count**|**int**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]까지<br /><br /> 이 메모리 개체에서 할당한 최대 페이지 수입니다. Null을 허용하지 않습니다.|  
|**page_size_in_bytes**|**int**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 이 개체에서 할당한 페이지의 크기(바이트)입니다. Null을 허용하지 않습니다.|  
|**max_pages_in_bytes**|**bigint**|이 메모리 개체에서 사용한 최대 메모리 양입니다. Null을 허용하지 않습니다.|  
|**page_allocator_address**|**varbinary(8)**|페이지 할당자의 메모리 주소입니다. Null을 허용하지 않습니다. 자세한 내용은 참조 [sys.dm_os_memory_clerks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)합니다.|  
|**creation_stack_address**|**varbinary(8)**|내부적으로만 사용됩니다. Null을 허용합니다.|  
|**sequence_num**|**int**|내부적으로만 사용됩니다. Null을 허용합니다.|  
|**partition_type**|**int**|파티션 유형:<br /><br /> 0-시스템이 메모리 내 개체<br /><br /> 1-이러한 시스템이 메모리 개체를 현재 분할 되지<br /><br /> 2-NUMA 노드에 의해 분할 이러한 시스템이 메모리 개체입니다. 단일 NUMA 노드에 있는 환경에서 1로 같습니다.<br /><br /> 3-CPU에 의해 분할 되는 이러한 시스템이 메모리 개체입니다.|  
|**contention_factor**|**real**|이 메모리 개체에서 발생 하지 0 경합을 지정 하는 값입니다. 값은 지정된 된 수의 메모리 할당에는 기간 동안 반사 경합 적용 된 될 때마다 업데이트 됩니다. 스레드로부터 안전한 메모리 개체에만 적용 됩니다.|  
|**waiting_tasks_count**|**bigint**|이 메모리 개체에 대 한 대기 수입니다. 이 메모리 개체에서 할당 된 메모리 될 때마다이 카운터가 증가 합니다. 증가값이 현재이 메모리 개체에 대 한 액세스를 기다리는 태스크 수입니다. 스레드로부터 안전한 메모리 개체에만 적용 됩니다. 정확성을 보장 하지 않고 최선의 노력 값입니다.|  
|**exclusive_access_count**|**bigint**|이 메모리 개체가 독점적으로 액세스 빈도 지정 합니다. 스레드로부터 안전한 메모리 개체에만 적용 됩니다.  정확성을 보장 하지 않고 최선의 노력 값입니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
 **partition_type**, **contention_factor**, **waiting_tasks_count**, 및 **exclusive_access_count** 에서 아직 구현 되지 않은 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]합니다.  
  
## <a name="permissions"></a>Permissions

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다.   

## <a name="remarks"></a>주의  
 메모리 개체는 힙으로, 메모리 클럭보다 세분화된 할당 기능을 제공합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소는 메모리 클럭 대신 메모리 개체를 사용합니다. 메모리 개체는 메모리 클럭의 페이지 할당자 인터페이스를 사용하여 페이지를 할당합니다. 메모리 개체는 가상 또는 공유 메모리 인터페이스를 사용하지 않습니다. 구성 요소는 할당 패턴에 따라 여러 다른 유형의 메모리 개체를 만들어 임의의 크기를 가진 영역을 할당할 수 있습니다.  
  
 메모리 개체의 일반적인 페이지 크기는 8KB입니다. 하지만 증분 메모리 개체의 페이지 크기의 범위는 512바이트에서 8KB 사이가 될 수 있습니다.  
  
> [!NOTE]  
>  페이지 크기는 최대 할당이 아닙니다. 대신에 페이지 크기는 페이지 할당자에서 지원하고 메모리 클럭에서 구현하는 할당 세분성을 지원합니다. 메모리 개체에서 8KB보다 큰 할당을 요청할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 각 메모리 개체 유형에서 할당한 메모리를 반환합니다.  
  
```  
SELECT SUM (pages_in_bytes) as 'Bytes Used', type   
FROM sys.dm_os_memory_objects  
GROUP BY type   
ORDER BY 'Bytes Used' DESC;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
  [SQL Server 운영 체제 관련 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_os_memory_clerks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)  
  
  


