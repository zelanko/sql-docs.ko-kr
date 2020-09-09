---
description: sys. dm_pdw_os_event_logs (Transact-sql)
title: sys. dm_pdw_os_event_logs (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a0daa8cf-72e2-4349-8be1-d3cc0f9b1e02
author: markingmyname
ms.author: maghan
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: fb4194b866595009b46aea888f600488b6a1cc3b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89530795"
---
# <a name="sysdm_pdw_os_event_logs-transact-sql"></a>sys. dm_pdw_os_event_logs (Transact-sql)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  다른 노드에 있는 다른 Windows 이벤트 로그에 대 한 정보를 저장 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|이 로그를 가져온 어플라이언스 노드입니다.<br /><br /> pdw_node_id 및 log_name이 보기의 키를 구성 합니다.||  
|log_name|**nvarchar(255)**|Windows 이벤트 로그 이름입니다.<br /><br /> pdw_node_id 및 log_name이 보기의 키를 구성 합니다.||  
|log_source|**nvarchar(255)**|Windows 이벤트 로그 원본 이름입니다.||  
|event_id|**int**|이벤트의 ID입니다. 고유 하지 않습니다.||  
|event_type|**nvarchar(255)**|심각도를 식별 하는 이벤트의 유형입니다.|' 정보 ', ' 경고 ', ' 오류 '|  
|event_message|**nvarchar(4000)**|이벤트에 대 한 세부 정보입니다.||  
|generate_time|**datetime**|이벤트가 생성 된 시간입니다.||  
|write_time|**datetime**|이벤트가 실제로 로그에 기록 된 시간입니다.||  
  
 이 보기에 의해 유지 되는 최대 행에 대 한 자세한 내용은 [용량 제한](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) 항목에서 메타 데이터 섹션을 참조 하세요. 
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
