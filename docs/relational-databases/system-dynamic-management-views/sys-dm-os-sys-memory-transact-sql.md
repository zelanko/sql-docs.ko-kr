---
title: sys. dm_os_sys_memory (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_sys_memory
- sys.dm_os_sys_memory_TSQL
- sys.dm_os_sys_memory
- dm_os_sys_memory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_sys_memory dynamic management view
ms.assetid: 1ca58814-1caa-44c1-b307-ff0bdcbbef62
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2304a0afc16c99934f6f77c640c60cb2ade52acf
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827890"
---
# <a name="sysdm_os_sys_memory-transact-sql"></a>sys.dm_os_sys_memory(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  운영 체제의 메모리 정보를 반환합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 운영 체제 수준의 외부 메모리 상태 및 기본 하드웨어의 물리적 제한에 제약을 받고 이에 따라 반응합니다. 전체 시스템 상태 파악은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 사용량 평가에서 중요한 부분입니다.  
  
> [!NOTE]  
>  또는에서이를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 이름 **sys. dm_pdw_nodes_os_sys_memory**을 사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**total_physical_memory_kb**|**bigint**|운영 체제에서 사용할 수 있는 실제 메모리의 총 크기(KB)입니다.|  
|**available_physical_memory_kb**|**bigint**|사용할 수 있는 실제 메모리의 크기(KB)입니다.|  
|**total_page_file_kb**|**bigint**|운영 체제에서 보고한 커밋 제한 크기(KB)입니다.|  
|**available_page_file_kb**|**bigint**|사용 되지 않는 페이지 파일의 총 크기 (KB)입니다.|  
|**system_cache_kb**|**bigint**|시스템 캐시 메모리의 총 공간(KB)입니다.|  
|**kernel_paged_pool_kb**|**bigint**|페이징된 커널 풀의 총 공간(KB)입니다.|  
|**kernel_nonpaged_pool_kb**|**bigint**|페이징되지 않은 커널 풀의 총 공간(KB)입니다.|  
|**system_high_memory_signal_state**|**bit**|시스템 고용량 메모리 리소스 상태 알림입니다. 값이 1이면 Windows에서 고용량 메모리 신호가 설정된 것입니다. 자세한 내용은 MSDN library에서 [CreateMemoryResourceNotification](https://go.microsoft.com/fwlink/?LinkId=82427) 을 참조 하세요.|  
|**system_low_memory_signal_state**|**bit**|시스템 저용량 메모리 리소스 상태 알림입니다. 값이 1이면 Windows에서 저용량 메모리 신호가 설정된 것입니다. 자세한 내용은 MSDN library에서 [CreateMemoryResourceNotification](https://go.microsoft.com/fwlink/?LinkId=82427) 을 참조 하세요.|  
|**system_memory_state_desc**|**nvarchar(256)**|메모리 상태에 대한 설명입니다. 아래 표를 참조하세요.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
|조건|값|  
|---------------|-----------|  
|system_high_memory_signal_state = 1<br /><br /> 및<br /><br /> system_low_memory_signal_state = 0|사용 가능한 실제 메모리가 높은 수준입니다.|  
|system_high_memory_signal_state = 0<br /><br /> 및<br /><br /> system_low_memory_signal_state = 1|사용 가능한 실제 메모리가 낮은 수준입니다.|  
|system_high_memory_signal_state = 0<br /><br /> 및<br /><br /> system_low_memory_signal_state = 0|실제 메모리 사용률이 안정적입니다.|  
|system_high_memory_signal_state = 1<br /><br /> 및<br /><br /> system_low_memory_signal_state = 1|실제 메모리 상태가 전환되는 중입니다.<br /><br /> 높음 신호와 낮음 신호는 동시에 설정될 수 없습니다. 하지만 운영 체제 수준에서 상태가 빠르게 변경되면 사용자 모드 애플리케이션에 두 값이 동시에 나타날 수 있습니다. 두 신호가 동시에 설정된 것으로 나타나면 전환 상태로 해석됩니다.|  
  
## <a name="permissions"></a>권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;동적 관리 뷰 및 함수](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;운영 체제 관련 동적 관리 뷰 SQL Server](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


