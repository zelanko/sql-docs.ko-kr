---
title: sys.dm_pdw_os_performance_counters (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0673a8f8-8bed-41eb-8959-a9e3e9e03a65
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 96f788386a53e4493d0fb52ab33bfe1848527f4f
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmpdwosperformancecounters-transact-sql"></a>sys.dm_pdw_os_performance_counters (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  노드에 대 한 Windows 성능 카운터에 대 한 정보를 포함 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|카운터를 포함 하는 노드의 ID입니다.<br /><br /> pdw_node_id 및 counter_name이이 보기에 대 한 키를 형성합니다.|참조에 대 한 node_id [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)합니다.|  
|counter_name|**nvarchar(255)**|Windows 성능 카운터의 이름입니다.||  
|counter_category|**nvarchar(255)**|Windows 성능 카운터 범주의 이름입니다.||  
|instance_name|**nvarchar(255)**|카운터의 특정 항목 이름입니다.||  
|counter_value|**Decimal(38,10)**|카운터의 현재 값입니다.||  
|last_update_time|**Datetime2(3)**|타임 스탬프 값으로 업데이트 된 시간입니다.||  
  
## <a name="see-also"></a>관련 항목:  
 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
