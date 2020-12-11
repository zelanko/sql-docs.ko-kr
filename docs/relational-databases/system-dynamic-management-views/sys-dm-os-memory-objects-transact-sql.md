---
description: sys.dm_os_memory_objects(Transact-SQL)
title: sys.dm_os_memory_objects (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bf5fff49104658af4cf5a5102e538200d0393a1f
ms.sourcegitcommit: 2991ad5324601c8618739915aec9b184a8a49c74
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97326230"
---
# <a name="sysdm_os_memory_objects-transact-sql"></a>sys.dm_os_memory_objects(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 의해 현재 할당된 메모리 개체를 반환합니다. **Sys.dm_os_memory_objects** 를 사용 하 여 메모리 사용을 분석 하 고 가능한 메모리 누수를 식별할 수 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**memory_object_address**|**varbinary(8)**|메모리 개체의 주소입니다. Null을 허용하지 않습니다.|  
|**parent_address**|**varbinary(8)**|상위 메모리 개체의 주소입니다. Null을 허용합니다.|  
|**pages_allocated_count**|**int**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]까지<br /><br /> 이 개체에서 할당한 페이지 수입니다. Null을 허용하지 않습니다.|  
|**pages_in_bytes**|**bigint**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> 메모리 개체의 이 인스턴스에서 할당하는 메모리의 양(바이트)입니다. Null을 허용하지 않습니다.|  
|**creation_options**|**int**|내부 전용입니다. Null을 허용합니다.|  
|**bytes_used**|**bigint**|내부 전용입니다. Null을 허용합니다.|  
|**type**|**nvarchar(60)**|메모리 개체의 유형입니다.<br /><br /> 이 메모리 개체가 속한 구성 요소 또는 메모리 개체의 기능을 나타냅니다. Null을 허용합니다.|  
|**name**|**varchar(128)**|내부 전용입니다. Null을 허용합니다.|  
|**memory_node_id**|**smallint**|이 메모리 개체에서 사용하고 있는 메모리 노드의 ID입니다. Null을 허용하지 않습니다.|  
|**creation_time**|**datetime**|내부 전용입니다. Null을 허용합니다.|  
|**max_pages_allocated_count**|**int**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]까지<br /><br /> 이 메모리 개체에서 할당한 최대 페이지 수입니다. Null을 허용하지 않습니다.|  
|**page_size_in_bytes**|**int**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> 이 개체에서 할당한 페이지의 크기(바이트)입니다. Null을 허용하지 않습니다.|  
|**max_pages_in_bytes**|**bigint**|이 메모리 개체에서 사용한 최대 메모리 양입니다. Null을 허용하지 않습니다.|  
|**page_allocator_address**|**varbinary(8)**|페이지 할당자의 메모리 주소입니다. Null을 허용하지 않습니다. 자세한 내용은 [sys.dm_os_memory_clerks &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)를 참조 하세요.|  
|**creation_stack_address**|**varbinary(8)**|내부 전용입니다. Null을 허용합니다.|  
|**sequence_num**|**int**|내부 전용입니다. Null을 허용합니다.|  
|**partition_type**|**int**|**적용 대상**: [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 이상<br /><br /> 파티션 유형입니다.<br /><br /> 0-분할 되지 않은 메모리 개체<br /><br /> 1-분할 된 메모리 개체 (현재 분할 되지 않음)<br /><br /> 2-NUMA 노드에 의해 분할 된 분할 된 메모리 개체입니다. 단일 NUMA 노드가 있는 환경에서는 1과 같습니다.<br /><br /> 3-CPU로 분할 된 분할 된 메모리 개체입니다.|  
|**contention_factor**|**real**|**적용 대상**: [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 이상<br /><br /> 이 메모리 개체에 대 한 경합을 지정 하는 값으로 0은 경합이 없음을 의미 합니다. 지정 된 수의 메모리 할당이 해당 기간 동안 경합을 반영 하는 경우 값이 업데이트 됩니다. 스레드로부터 안전한 메모리 개체에만 적용 됩니다.|  
|**waiting_tasks_count**|**bigint**|**적용 대상**: [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 이상<br /><br /> 이 메모리 개체의 대기 수입니다. 이 카운터는 메모리가이 메모리 개체에서 할당 될 때마다 증가 합니다. 이 증가값은 현재이 메모리 개체에 대 한 액세스를 대기 중인 작업의 수입니다. 스레드로부터 안전한 메모리 개체에만 적용 됩니다. 이 값은 정확성을 보장 하지 않는 최상의 노력입니다.|  
|**exclusive_access_count**|**bigint**|**적용 대상**: [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 이상<br /><br /> 이 메모리 개체에 단독으로 액세스 한 빈도를 지정 합니다. 스레드로부터 안전한 메모리 개체에만 적용 됩니다.  이 값은 정확성을 보장 하지 않는 최상의 노력입니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
 **partition_type**, **contention_factor**, **waiting_tasks_count** 및 **exclusive_access_count** 은에서 아직 구현 되지 않았습니다 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] .  
  
## <a name="permissions"></a>사용 권한

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
SQL Database Basic, S0 및 S1 서비스 목적과 탄력적 풀의 데이터베이스에 대해서는 `Server admin` 또는 `Azure Active Directory admin` 계정이 필요 합니다. 다른 모든 SQL Database 서비스 목표에서 `VIEW DATABASE STATE` 사용 권한은 데이터베이스에서 필요 합니다.   

## <a name="remarks"></a>설명  
 메모리 개체는 힙으로, 메모리 클럭보다 세분화된 할당 기능을 제공합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소는 메모리 클럭 대신 메모리 개체를 사용합니다. 메모리 개체는 메모리 클럭의 페이지 할당자 인터페이스를 사용하여 페이지를 할당합니다. 메모리 개체는 가상 또는 공유 메모리 인터페이스를 사용하지 않습니다. 구성 요소는 할당 패턴에 따라 여러 다른 유형의 메모리 개체를 만들어 임의의 크기를 가진 영역을 할당할 수 있습니다.  
  
 메모리 개체의 일반적인 페이지 크기는 8KB입니다. 하지만 증분 메모리 개체의 페이지 크기의 범위는 512바이트에서 8KB 사이가 될 수 있습니다.  
  
> [!NOTE]  
>  페이지 크기는 최대 할당이 아닙니다. 대신에 페이지 크기는 페이지 할당자에서 지원하고 메모리 클럭에서 구현하는 할당 세분성을 지원합니다. 메모리 개체에서 8KB보다 큰 할당을 요청할 수 있습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 각 메모리 개체 유형에서 할당한 메모리를 반환합니다.  
  
```  
SELECT SUM (pages_in_bytes) as 'Bytes Used', type   
FROM sys.dm_os_memory_objects  
GROUP BY type   
ORDER BY 'Bytes Used' DESC;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
  [Transact-sql&#41;&#40;운영 체제 관련 동적 관리 뷰 SQL Server ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [Transact-sql&#41;sys.dm_os_memory_clerks &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)  
  
  


