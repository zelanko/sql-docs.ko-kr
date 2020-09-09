---
description: 확장 이벤트 테이블 - trace_xe_action_map
title: trace_xe_action_map (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5f3b742741d3add5b54c07d3cec4f47bbd919e2d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540424"
---
# <a name="extended-events-tables---trace_xe_action_map"></a>확장 이벤트 테이블 - trace_xe_action_map
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  SQL 추적 열 ID에 매핑된 Extended Events 동작마다 하나의 행을 포함합니다. 이 테이블은 sys 스키마의 master 데이터베이스에 저장 됩니다.  
  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|trace_column_id|**smallint**|매핑될 SQL 추적 열의 ID입니다.|  
|package_name|**nvarchar(60)**|매핑된 동작이 있는 Extended Events 패키지의 이름입니다.|  
|xe_action_name|**nvarchar(60)**|SQL 추적 열에 매핑된 Extended Events 동작의 이름입니다.|  
  
## <a name="remarks"></a>설명  
 다음 쿼리를 사용하여 SQL 추적 열에 해당하는 Extended Events 동작을 식별할 수 있습니다.  
  
```  
SELECT tc.name AS trace_column, am.package_name, am.xe_action_name  
FROM sys.trace_columns AS tc  
INNER JOIN sys.trace_xe_action_map AS am  
   ON tc.trace_column_id = am.trace_column_id  
```  
  
 동작에 매핑되지 않은 SQL 추적 열은 테이블에 포함되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [trace_xe_event_map&#40;Transact-SQL&#41;](../../relational-databases/system-tables/extended-events-tables-trace-xe-event-map.md)  
  
  
