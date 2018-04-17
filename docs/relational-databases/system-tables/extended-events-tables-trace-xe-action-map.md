---
title: trace_xe_action_map (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- trace_xe_action_map_TSQL
- trace_xe_action_map
dev_langs:
- TSQL
helpviewer_keywords:
- extended events [SQL Server], tables
- trace_xe_action_map
ms.assetid: 208a1413-ce7f-4521-b765-d74723627302
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d75ed8bd81491e7095f13a794a818d4b2532f176
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="extended-events-tables---tracexeactionmap"></a>확장 이벤트 테이블-trace_xe_action_map
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  SQL 추적 열 ID에 매핑된 Extended Events 동작마다 하나의 행을 포함합니다. 이 테이블에 master 데이터베이스의 sys 스키마에 저장 됩니다.  
  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|trace_column_id|**smallint**|매핑될 SQL 추적 열의 ID입니다.|  
|package_name|**nvarchar(60)**|매핑된 동작이 있는 Extended Events 패키지의 이름입니다.|  
|xe_action_name|**nvarchar(60)**|SQL 추적 열에 매핑된 Extended Events 동작의 이름입니다.|  
  
## <a name="remarks"></a>주의  
 다음 쿼리를 사용하여 SQL 추적 열에 해당하는 Extended Events 동작을 식별할 수 있습니다.  
  
```  
SELECT tc.name AS trace_column, am.package_name, am.xe_action_name  
FROM sys.trace_columns AS tc  
INNER JOIN sys.trace_xe_action_map AS am  
   ON tc.trace_column_id = am.trace_column_id  
```  
  
 동작에 매핑되지 않은 SQL 추적 열은 테이블에 포함되지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [trace_xe_event_map&#40;Transact-SQL&#41;](../../relational-databases/system-tables/extended-events-tables-trace-xe-event-map.md)  
  
  
