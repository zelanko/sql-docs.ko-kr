---
title: sys.dm_os_virtual_address_dump (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_virtual_address_dump
- sys.dm_os_virtual_address_dump_TSQL
- sys.dm_os_virtual_address_dump
- dm_os_virtual_address_dump_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_virtual_address_dump dynamic management view
ms.assetid: 7b24ea55-3873-42fd-a86c-441c92eb6175
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: de031974b003c09fa033b2faa770e0177039f30f
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmosvirtualaddressdump-transact-sql"></a>sys.dm_os_virtual_address_dump(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  호출 프로세스의 가상 주소 공간에 있는 페이지 범위에 대한 정보를 반환합니다.  
  
> [!NOTE]  
>  이 정보는도에서 반환 되는 **VirtualQuery** Windows API입니다.  
  
> [!NOTE]  
>  이 메서드를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_os_virtual_address_dump**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**region_base_address**|**varbinary(8)**|페이지 영역의 기준 주소에 대한 포인터입니다. Null을 허용하지 않습니다.|  
|**region_allocation_base_address**|**varbinary(8)**|VirtualAlloc Windows API 함수에 의해 할당된 페이지 영역의 기준 주소에 대한 포인터입니다. BaseAddress 멤버가 가리키는 페이지가 이 할당 범위 내에 포함됩니다. Null을 허용하지 않습니다.|  
|**region_allocation_protection**|**varbinary(8)**|영역이 처음 할당되었을 때의 보호 특성입니다. 값은 다음 중 하나입니다.<br /><br /> -PAGE_READONLY<br />-PAGE_READWRITE<br />-PAGE_NOACCESS<br />-PAGE_WRITECOPY<br />-PAGE_EXECUTE<br />-PAGE_EXECUTE_READ<br />-PAGE_EXECUTE_READWRITE<br />-PAGE_EXECUTE_WRITECOPY<br />-PAGE_GUARD<br />-PAGE_NOCACHE<br /><br /> Null을 허용하지 않습니다.|  
|**region_size_in_bytes**|**bigint**|모든 페이지의 특성이 동일한 기준 주소에서 시작하는 영역의 크기(바이트)입니다. Null을 허용하지 않습니다.|  
|**region_state**|**varbinary(8)**|영역의 현재 상태입니다. 다음 중 하나일 수 있습니다.<br /><br /> -   MEM_COMMIT<br />-MEM_RESERVE<br />-   MEM_FREE<br /><br /> Null을 허용하지 않습니다.|  
|**region_current_protection**|**varbinary(8)**|보호 특성입니다. 값은 다음 중 하나입니다.<br /><br /> -PAGE_READONLY<br />-PAGE_READWRITE<br />-PAGE_NOACCESS<br />-PAGE_WRITECOPY<br />-PAGE_EXECUTE<br />-PAGE_EXECUTE_READ<br />-PAGE_EXECUTE_READWRITE<br />-PAGE_EXECUTE_WRITECOPY<br />-PAGE_GUARD<br />-PAGE_NOCACHE<br /><br /> Null을 허용하지 않습니다.|  
|**region_type**|**varbinary(8)**|영역의 페이지 형식을 나타냅니다. 이 값은<br /><br /> -   MEM_PRIVATE<br />-MEM_MAPPED<br />-   MEM_IMAGE<br /><br /> Null을 허용하지 않습니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="permissions"></a>Permissions  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server 운영 체제 관련 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


