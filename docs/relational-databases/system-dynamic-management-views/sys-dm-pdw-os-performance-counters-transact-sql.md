---
description: sys.dm_pdw_os_performance_counters (Transact-sql)
title: sys.dm_pdw_os_performance_counters (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0673a8f8-8bed-41eb-8959-a9e3e9e03a65
author: markingmyname
ms.author: maghan
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d2a5715df9f95f6f2090ba4a25ddc22329bb4160
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035259"
---
# <a name="sysdm_pdw_os_performance_counters-transact-sql"></a>sys.dm_pdw_os_performance_counters (Transact-sql)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  의 노드에 대 한 Windows 성능 카운터에 대 한 정보를 포함 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|카운터를 포함 하는 노드의 ID입니다.<br /><br /> pdw_node_id 및 counter_name이 보기의 키를 구성 합니다.|[Sys.dm_pdw_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)에서 node_id를 참조 하세요.|  
|counter_name|**nvarchar(255)**|Windows 성능 카운터의 이름입니다.||  
|counter_category|**nvarchar(255)**|Windows 성능 카운터 범주의 이름입니다.||  
|instance_name|**nvarchar(255)**|카운터의 특정 항목 이름입니다.||  
|counter_value|**Decimal (38, 10)**|카운터의 현재 값입니다.||  
|last_update_time|**Datetime2 (3)**|값이 마지막으로 업데이트 된 시간의 타임 스탬프입니다.||  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;Azure Synapse 분석 및 병렬 데이터 웨어하우스 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
