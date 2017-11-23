---
title: trace_xe_event_map (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- trace_xe_event_map_TSQL
- trace_xe_event_map
dev_langs: TSQL
helpviewer_keywords:
- trace_xe_event_map
- extended events [SQL Server], tables
ms.assetid: 537aa292-3540-47e8-be28-56dc01abc343
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 194c5ac43bc24361b608b85b9aa68cc8f64b2461
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="extended-events-tables---tracexeeventmap"></a>확장 이벤트 테이블-trace_xe_event_map
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  SQL 추적 이벤트 클래스에 매핑된 Extended Events 이벤트마다 하나의 행을 포함합니다. 이 테이블에 master 데이터베이스의 sys 스키마에 저장 됩니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|trace_event_id|**smallint**|매핑될 SQL 추적 이벤트 클래스의 ID입니다.|  
|package_name|**nvarchar (60)**|매핑된 이벤트가 있는 Extended Events 패키지의 이름입니다.|  
|xe_event_name|**nvarchar (60)**|SQL 추적 이벤트 클래스에 매핑된 Extended Events 이벤트의 이름입니다.|  
  
## <a name="remarks"></a>주의  
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
  
## <a name="see-also"></a>관련 항목:  
 [trace_xe_action_map&#40;Transact-SQL&#41;](../../relational-databases/system-tables/extended-events-tables-trace-xe-action-map.md)  
  
  
