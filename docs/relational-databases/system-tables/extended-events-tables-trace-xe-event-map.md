---
title: trace_xe_event_map (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- trace_xe_event_map_TSQL
- trace_xe_event_map
dev_langs:
- TSQL
helpviewer_keywords:
- trace_xe_event_map
- extended events [SQL Server], tables
ms.assetid: 537aa292-3540-47e8-be28-56dc01abc343
author: stevestein
ms.author: sstein
ms.openlocfilehash: 07810bcd1f43bd3fd2428361e5f429edb9c7c3d5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68056244"
---
# <a name="extended-events-tables---trace_xe_event_map"></a>확장 이벤트 테이블 - trace_xe_event_map
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  SQL 추적 이벤트 클래스에 매핑된 Extended Events 이벤트마다 하나의 행을 포함합니다. 이 테이블은 sys 스키마의 master 데이터베이스에 저장 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|trace_event_id|**smallint**|매핑될 SQL 추적 이벤트 클래스의 ID입니다.|  
|package_name|**nvarchar(60)**|매핑된 이벤트가 있는 Extended Events 패키지의 이름입니다.|  
|xe_event_name|**nvarchar(60)**|SQL 추적 이벤트 클래스에 매핑된 Extended Events 이벤트의 이름입니다.|  
  
## <a name="remarks"></a>설명  
 다음 쿼리를 사용하여 SQL 추적 이벤트 클래스에 해당하는 Extended Events 이벤트를 식별할 수 있습니다.  
  
```  
SELECT te.name, xe.package_name, xe.xe_event_name  
FROM sys.trace_events AS te  
LEFT JOIN sys.trace_xe_event_map AS xe  
   ON te.trace_event_id = xe.trace_event_id  
WHERE xe.trace_event_id IS NOT NULL  
```  
  
 모든 이벤트 클래스에 해당하는 Extended Events 이벤트가 있는 것은 아닙니다. 다음 쿼리를 사용하여 해당하는 Extended Events 이벤트가 없는 이벤트 클래스를 나열할 수 있습니다.  
  
```  
SELECT te.trace_event_id, te.name  
FROM sys.trace_events AS te  
LEFT JOIN sys.trace_xe_event_map AS xe  
   ON te.trace_event_id = xe.trace_event_id  
WHERE xe.trace_event_id IS NULL  
```  
  
 이전 쿼리에서 반환된 이벤트 클래스 대부분은 감사와 관련이 있습니다. 감사를 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit를 사용하는 것이 좋습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit는 감사를 만들기 위해 Extended Events를 사용합니다. 자세한 내용은 [SQL Server Audit&#40;데이터베이스 엔진&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [trace_xe_action_map&#40;Transact-SQL&#41;](../../relational-databases/system-tables/extended-events-tables-trace-xe-action-map.md)  
  
  
