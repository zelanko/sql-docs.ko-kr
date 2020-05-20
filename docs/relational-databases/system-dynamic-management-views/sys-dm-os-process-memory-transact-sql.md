---
title: sys. dm_os_process_memory (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_process_memory_TSQL
- dm_os_process_memory_TSQL
- dm_os_process_memory
- sys.dm_os_process_memory
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_process_memory dynamic management view
ms.assetid: e838130c-95d4-4605-9e3b-eb0ab71cd250
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dc8eb11f3b77814ba9cd296cce15bba920f0373a
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82821034"
---
# <a name="sysdm_os_process_memory-transact-sql"></a>sys.dm_os_process_memory(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스 공간에 소요되는 대부분의 메모리 할당은 이러한 할당을 추적 및 계산하도록 허용된 인터페이스를 통해 제어됩니다. 그러나 메모리 할당은 내부 메모리 관리 루틴을 거치지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 주소 공간에서 수행될 수도 있습니다. 값은 기본 운영 체제 호출을 통해 얻습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이 클래스는 잠긴 또는 대량 페이지 할당에 대해 조정 하는 경우를 제외 하 고 내부 메서드를 통해 조작 되지 않습니다.  
  
 메모리 크기를 나타내는 모든 반환 값은 킬로바이트(KB) 단위로 표시됩니다. 열 **total_virtual_address_space_reserved_kb** 은 (는) **dm_os_sys_info**의 **virtual_memory_in_bytes** 와 중복 됩니다.  
  
 다음 표에서는 프로세스 주소 공간의 전체적인 구조를 보여 줍니다.  
  
> [!NOTE]  
>  또는에서이를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 이름 **sys. dm_pdw_nodes_os_process_memory**을 사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**physical_memory_in_use_kb**|**bigint**|운영 체제에서 보고한 내용에 대용량 페이지 API를 사용하여 수행된 추적된 할당을 더한 프로세스 작업 집합(KB)을 나타냅니다. Null을 허용하지 않습니다.|  
|**large_page_allocations_kb**|**bigint**|대용량 페이지 API를 사용하여 할당된 물리적 메모리를 지정합니다. Null을 허용하지 않습니다.|  
|**locked_page_allocations_kb**|**bigint**|메모리에서 잠긴 메모리 페이지를 지정합니다. Null을 허용하지 않습니다.|  
|**total_virtual_address_space_kb**|**bigint**|가상 주소 공간의 사용자 모드 부분의 총 크기를 나타냅니다. Null을 허용하지 않습니다.|  
|**virtual_address_space_reserved_kb**|**bigint**|프로세스에 예약된 가상 주소 공간의 총 크기를 나타냅니다. Null을 허용하지 않습니다.|  
|**virtual_address_space_committed_kb**|**bigint**|물리적 페이지에 커밋되거나 매핑된 예약된 가상 주소 공간의 크기를 나타냅니다. Null을 허용하지 않습니다.|  
|**virtual_address_space_available_kb**|**bigint**|현재 사용 가능한 가상 주소 공간의 크기를 나타냅니다. Null을 허용하지 않습니다.<br /><br /> **참고:** 할당 세분성 보다 작은 무료 지역이 있을 수 있습니다. 이러한 영역은 할당에 사용할 수 없습니다.|  
|**page_fault_count**|**bigint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스에서 발생한 페이지 폴트 수를 나타냅니다. Null을 허용하지 않습니다.|  
|**memory_utilization_percentage**|**int**|작업 집합에 있는 커밋된 메모리의 비율을 지정합니다. Null을 허용하지 않습니다.|  
|**available_commit_limit_kb**|**bigint**|프로세스에서 커밋할 수 있는 메모리의 양을 나타냅니다. Null을 허용하지 않습니다.|  
|**process_physical_memory_low**|**bit**|프로세스가 물리적 메모리 부족 알림에 응답함을 나타냅니다. Null을 허용하지 않습니다.|  
|**process_virtual_memory_low**|**bit**|가상 메모리 공간이 부족한 것으로 감지되었음을 나타냅니다. Null을 허용하지 않습니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 서버에 대한 VIEW SERVER STATE 권한이 필요합니다.  
  
에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium 계층에서는 데이터베이스에 대 한 권한이 필요 합니다 `VIEW DATABASE STATE` . [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;동적 관리 뷰 및 함수](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;운영 체제 관련 동적 관리 뷰 SQL Server](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


