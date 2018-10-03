---
title: sys.dm_pdw_os_event_logs (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a0daa8cf-72e2-4349-8be1-d3cc0f9b1e02
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ad9c7b96858c1ded81c2651c389ae63490af6408
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47699201"
---
# <a name="sysdmpdwoseventlogs-transact-sql"></a>sys.dm_pdw_os_event_logs (Transact SQL)
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
  
 이 보기에 의해 보존 된 최대 행에 대 한 내용은에서 최대 시스템 뷰의 값 섹션을 참조 합니다 [최소값 및 최대값 (SQL Server PDW)](http://msdn.microsoft.com/5243f018-2713-45e3-9b61-39b2a57401b9) 항목입니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
