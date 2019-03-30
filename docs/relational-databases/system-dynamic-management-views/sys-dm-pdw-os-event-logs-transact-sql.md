---
title: sys.dm_pdw_os_event_logs (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a0daa8cf-72e2-4349-8be1-d3cc0f9b1e02
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 44a24b12c284cf253838bc1c2252e4081b8efe98
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58657238"
---
# <a name="sysdmpdwoseventlogs-transact-sql"></a>sys.dm_pdw_os_event_logs (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  다른 노드에서 다른 Windows 이벤트에 대 한 정보 로그를 보유 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|이 로그는 어플라이언스 노드입니다.<br /><br /> pdw_node_id 및 log_name이이 보기에 대 한 키를 구성합니다.||  
|log_name|**nvarchar(255)**|Windows 이벤트 로그 이름입니다.<br /><br /> pdw_node_id 및 log_name이이 보기에 대 한 키를 구성합니다.||  
|log_source|**nvarchar(255)**|Windows 이벤트 로그 원본 이름입니다.||  
|event_id|**int**|이벤트의 ID입니다. 고유 하지 않습니다.||  
|event_type|**nvarchar(255)**|심각도 식별 하는 이벤트의 유형입니다.|' 정보 ', 'Warning', 'Error'|  
|event_message|**nvarchar(4000)**|이벤트의 세부 정보입니다.||  
|generate_time|**datetime**|이벤트가 만들어진 시간입니다.||  
|write_time|**datetime**|이벤트 로그에 실제로 기록 된 시간입니다.||  
  
 이 보기에 의해 보존 된 최대 행에 대 한 내용은에서 메타 데이터 섹션을 참조 합니다 [용량 제한](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) 항목입니다. 
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
