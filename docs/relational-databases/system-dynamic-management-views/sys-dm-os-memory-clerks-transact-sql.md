---
description: sys.dm_os_memory_clerks(Transact-SQL)
title: sys.dm_os_memory_clerks (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_memory_clerks
- sys.dm_os_memory_clerks
- dm_os_memory_clerks_TSQL
- sys.dm_os_memory_clerks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_clerks dynamic management view
ms.assetid: 1d556c67-5c12-46d5-aa8c-7ec1bb858df7
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 256d01bcd3b33e96adb576a59ad917df4b04585b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477274"
---
# <a name="sysdm_os_memory_clerks-transact-sql"></a>sys.dm_os_memory_clerks(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 현재 활성 상태인 모든 메모리 클럭 집합을 반환합니다.  
  
> [!NOTE]  
>  또는에서이를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] **sys.dm_pdw_nodes_os_memory_clerks** 이름을 사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**memory_clerk_address**|**varbinary(8)**|메모리 클럭의 고유 메모리 주소를 지정합니다. 이것은 기본 키 열입니다. Null을 허용하지 않습니다.|  
|**type**|**nvarchar(60)**|메모리 클럭의 유형을 지정합니다. 모든 클럭은 CLR 클럭 MEMORYCLERK_SQLCLR와 같은 특정한 유형을 가지고 있습니다. Null을 허용하지 않습니다.|  
|**name**|**nvarchar(256)**|이 메모리 클럭의 내부적으로 할당된 이름을 지정합니다. 구성 요소에는 특정 유형의 여러 메모리 클럭이 있을 수 있습니다. 따라서 구성 요소에서 이름을 지정하여 같은 유형의 메모리 클럭을 구분하도록 선택할 수 있습니다. Null을 허용하지 않습니다.|  
|**memory_node_id**|**smallint**|메모리 노드의 ID를 지정합니다. Null을 허용하지 않습니다.|  
|**single_pages_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]까지|  
|**pages_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> 이 메모리 클럭에 할당되는 페이지 메모리의 양(KB)를 지정합니다. Null을 허용하지 않습니다.|  
|**multi_pages_kb**|**bigint**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]까지<br /><br /> 할당된 다중 페이지 메모리(KB)입니다. 이것은 메모리 노드의 다중 페이지 할당자를 사용하여 할당된 메모리입니다. 이 메모리는 버퍼 풀 외부에 할당되며 메모리 노드의 가상 할당자를 사용합니다. Null을 허용하지 않습니다.|  
|**virtual_memory_reserved_kb**|**bigint**|메모리 클럭이 예약한 가상 메모리의 양을 지정합니다. Null을 허용하지 않습니다.|  
|**virtual_memory_committed_kb**|**bigint**|메모리 클럭이 커밋한 가상 메모리의 양을 지정합니다. 커밋된 메모리의 양은 항상 예약된 메모리보다 적어야 합니다. Null을 허용하지 않습니다.|  
|**awe_allocated_kb**|**bigint**|물리적 메모리에서 잠기고 운영 체제에서 페이지 아웃되지 않은 메모리의 양(KB)을 지정합니다. Null을 허용하지 않습니다.|  
|**shared_memory_reserved_kb**|**bigint**|메모리 클럭이 예약한 공유 메모리의 양을 지정합니다. 공유 메모리와 파일 매핑에 사용하도록 예약된 메모리입니다. Null을 허용하지 않습니다.|  
|**shared_memory_committed_kb**|**bigint**|메모리 클럭이 커밋한 공유 메모리의 양을 지정합니다. Null을 허용하지 않습니다.|  
|**page_size_in_bytes**|**bigint**|이 메모리 클럭에 대한 페이지 할당의 세분성을 지정합니다. Null을 허용하지 않습니다.|  
|**page_allocator_address**|**varbinary(8)**|페이지 할당자의 주소를 지정합니다. 이 주소는 메모리 클럭에 대해 고유 하며 **sys.dm_os_memory_objects** 에 사용 하 여이 클럭에 바인딩된 메모리 개체를 찾을 수 있습니다. Null을 허용하지 않습니다.|  
|**host_address**|**varbinary(8)**|이 메모리 클럭에 대한 호스트의 메모리 주소를 지정합니다. 자세한 내용은 [sys.dm_os_hosts &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-hosts-transact-sql.md)를 참조 하세요. Native Client와 같은 구성 요소 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 호스트 인터페이스를 통해 메모리 리소스에 액세스 합니다.<br /><br /> 0x00000000 = 메모리 클럭이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 속합니다.<br /><br /> Null을 허용하지 않습니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
## <a name="permissions"></a>사용 권한 

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
SQL Database Basic, S0 및 S1 서비스 목적과 탄력적 풀의 데이터베이스에 대해서는 `Server admin` 또는 `Azure Active Directory admin` 계정이 필요 합니다. 다른 모든 SQL Database 서비스 목표에서 `VIEW DATABASE STATE` 사용 권한은 데이터베이스에서 필요 합니다.   
  
## <a name="remarks"></a>설명  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 관리자의 계층 구조는 세 계층으로 이루어져 있습니다. 계층 구조의 맨 아래에는 메모리 노드가 있습니다. 중간 수준은 메모리 클럭, 메모리 캐시 및 메모리 풀로 구성됩니다. 맨 위 계층은 메모리 개체로 구성됩니다. 이러한 개체는 일반적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 메모리를 할당하는 데 사용됩니다.  
  
 메모리 노드는 하위 수준 할당자에 대한 인터페이스와 구현을 제공합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내에서는 메모리 클럭만 메모리 노드에 액세스할 수 있습니다. 메모리 클럭은 메모리 노드 인터페이스에 액세스하여 메모리를 할당합니다. 또한 진단을 위해 메모리 노드는 클럭을 사용하여 할당된 메모리를 추적합니다. 상당량의 메모리를 할당하는 모든 구성 요소는 자체 메모리 클럭을 만들고 클럭 인터페이스를 사용하여 메모리를 모두 할당해야 합니다. 대개 구성 요소는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 시작될 때 해당 클럭을 만듭니다.  
  
## <a name="see-also"></a>참고 항목  

 [Transact-sql&#41;&#40;운영 체제 관련 동적 관리 뷰 SQL Server ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_os_sys_info&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [Transact-sql&#41;sys.dm_exec_query_memory_grants &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [Transact-sql&#41;sys.dm_exec_query_plan &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)   
 [Transact-sql&#41;sys.dm_exec_sql_text &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)  
  
  


