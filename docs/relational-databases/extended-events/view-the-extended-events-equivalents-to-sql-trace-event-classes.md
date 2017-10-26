---
title: "SQL 추적 이벤트 클래스에 해당하는 확장 이벤트 항목 확인(Transact-SQL) | Microsoft 문서"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
- xevents
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Trace, extended events equivalents
- extended events [SQL Server], SQL Trace equivalents
- extended events [SQL Server], user configurable events
ms.assetid: 7f24104c-201d-4361-9759-f78a27936011
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 54e4c8309c290255cb2885fab04bb394bc453046
ms.openlocfilehash: 008cdb3fc158b36793f7d4b42ee4b24fd2b56ea5
ms.contentlocale: ko-kr
ms.lasthandoff: 10/16/2017

---
# <a name="view-the-extended-events-equivalents-to-sql-trace-event-classes"></a>SQL 추적 이벤트 클래스에 해당하는 확장 이벤트 항목 확인
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  확장 이벤트를 사용하여 SQL 추적 이벤트 클래스 및 열에 해당하는 이벤트 데이터를 수집하려는 경우 SQL 추적 이벤트가 확장 이벤트의 이벤트 및 동작에 매핑되는 방식을 이해하고 있으면 유용합니다.  
  
 다음 절차에 따라 각 SQL 추적 이벤트 및 관련 열에 해당하는 확장 이벤트의 이벤트 및 동작을 확인할 수 있습니다.  
  
## <a name="to-view-the-extended-events-equivalents-to-sql-trace-events-using-query-editor"></a>쿼리 편집기를 사용하여 SQL 추적 이벤트에 해당하는 확장 이벤트를 보려면  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 쿼리 편집기에서 다음 쿼리를 실행합니다.  
  
    ```  
    USE MASTER;  
    GO  
    SELECT DISTINCT  
       tb.trace_event_id,  
       te.name AS 'Event Class',  
       em.package_name AS 'Package',  
       em.xe_event_name AS 'XEvent Name',  
       tb.trace_column_id,  
       tc.name AS 'SQL Trace Column',  
       am.xe_action_name as 'Extended Events action'  
    FROM (sys.trace_events te LEFT OUTER JOIN sys.trace_xe_event_map em  
       ON te.trace_event_id = em.trace_event_id) LEFT OUTER JOIN sys.trace_event_bindings tb  
       ON em.trace_event_id = tb.trace_event_id LEFT OUTER JOIN sys.trace_columns tc  
       ON tb.trace_column_id = tc.trace_column_id LEFT OUTER JOIN sys.trace_xe_action_map am  
       ON tc.trace_column_id = am.trace_column_id  
    ORDER BY te.name, tc.name  
    ```  
  
 결과를 확인할 때는 다음에 유의하십시오.  
  
-   이벤트 클래스 열을 제외한 모든 열에서 NULL이 반환되었으면 이벤트 클래스가 SQL 추적에서 마이그레이션되지 않았음을 나타냅니다.  
  
-   확장 이벤트 동작 열의 값만 NULL이면 다음 경우 중 하나에 해당함을 나타냅니다.  
  
    -   SQL 추적 열이 확장 이벤트의 이벤트와 관련된 데이터 필드 중 하나에 매핑되어 있습니다.  
  
        > [!NOTE]  
        >  확장 이벤트의 각 이벤트에는 결과 집합에 자동으로 포함되는 기본 데이터 필드 집합이 있습니다.  
  
    -   동작 열에 의미 있는 확장 이벤트 해당 항목이 없습니다. 예를 들어 SQL 추적의 EventClass 열이 이러한 경우에 해당합니다. 이벤트 이름이 동일한 용도로 사용되므로 이 열은 확장 이벤트에 필요하지 않습니다.  
  
-   사용자가 구성할 수 있는 SQL 추적 이벤트 클래스(UserConfigurable:1 ~ UserConfigurable:9)의 경우 확장 이벤트에서는 단일 이벤트를 사용하여 이러한 이벤트 클래스를 대체합니다. 이 이벤트의 이름은 user_event입니다. 이 이벤트는 SQL 추적에서 사용되는 것과 동일한 sp_trace_generateevent 저장 프로시저를 사용하여 발생합니다. user_event 이벤트는 저장 프로시저에 전달된 이벤트 ID에 관계없이 반환됩니다. 그러나 event_id 필드는 이벤트 데이터의 일부로 반환됩니다. 이 필드를 사용하여 이벤트 ID를 기반으로 하는 조건자를 만들 수 있습니다. 예를 들어 코드에 UserConfigurable:0(event ID = 82)을 사용하는 경우 세션에 user_event 이벤트를 추가하고 'event_id = 82'라는 조건자를 지정할 수 있습니다. 그에 따라 sp_trace_generateevent 저장 프로시저에서 확장 이벤트의 user_event 이벤트와 해당하는 SQL 추적 이벤트 클래스를 생성하므로 코드를 변경할 필요가 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [sp_trace_generateevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)  
  
  

