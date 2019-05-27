---
title: 이벤트 쌍 대상 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- pairing target [SQL Server extended events]
- event pairing target
- targets [SQL Server extended events], pairing target
ms.assetid: 3c87dcfb-543a-4bd8-a73d-1390bdf4ffa3
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 39e444077c3dbe27ae243e4292b7a047e21de2b9
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66064844"
---
# <a name="event-pairing-target"></a>이벤트 쌍 대상
  이벤트 쌍 대상은 각 이벤트에 있는 하나 이상의 데이터 열을 사용하여 두 이벤트를 연결합니다. 잠금 획득과 잠금 해제 등 많은 이벤트가 쌍을 이루게 됩니다. 이벤트 시퀀스가 쌍을 이루면 두 이벤트는 삭제됩니다. 일치하는 집합을 삭제하면 해제되지 않은 잠금 획득을 쉽게 찾아낼 수 있습니다.  
  
 이벤트 수준 필터를 사용하여 이벤트 쌍 대상이 사전 설정된 기준에 일치하지 않는 이벤트만 캡처하도록 할 수 있습니다.  
  
 이벤트 쌍 대상을 사용하면 연결 작업을 수행할 열 시퀀스와 연결할 두 이벤트를 선택할 수 있습니다. 이 시퀀스의 모든 열은 같은 유형이어야 합니다.  
  
 다음 표에는 이벤트 쌍을 구성하는 데 사용할 수 있는 옵션이 나와 있습니다.  
  
|옵션|허용된 값|Description|  
|------------|--------------------|-----------------|  
|begin_event|현재 세션에 있는 이벤트 이름입니다.|시퀀스 쌍의 시작 이벤트를 지정하는 이벤트 이름입니다.|  
|end_event|현재 세션에 있는 이벤트 이름입니다.|시퀀스 쌍의 종료 이벤트를 나타내는 이벤트 이름입니다.|  
|begin_matching_columns|쉼표로 구분하여 순서대로 나열된 열 이름 목록입니다.|연결 작업을 수행할 열입니다.|  
|end_matching_columns|쉼표로 구분하여 순서대로 나열된 열 이름 목록입니다.|연결 작업을 수행할 열입니다.|  
|begin_matching_actions|쉼표로 구분하여 순서대로 나열한 동작 목록입니다.|연결 작업을 수행할 동작입니다.|  
|end_matching_actions|쉼표로 구분하여 순서대로 나열한 동작 목록입니다.|연결 작업을 수행할 동작입니다.|  
|respond_to_memory_pressure|다음 값 중 하나입니다.<br /><br /> 0 = 응답하지 않습니다.<br /><br /> 1 = 메모리가 부족하면 목록에 새 고아를 추가하지 않습니다.|대상이 메모리 이벤트에 응답합니다. 1로 설정되어 있고 서버에 메모리가 부족하면 유지되고 있는 짝이 없는 정보가 제거됩니다.|  
|max_orphans||대상에 수집되는 쌍을 이루지 않는 이벤트의 총 개수를 지정합니다. 한도에 도달하면 쌍을 이루지 않는 이벤트가 FIFO(선입선출) 기준에 따라 제거됩니다. 기본값 = 10,000|  
  
 이벤트와 연결된 모든 데이터는 캡처된 후 나중에 쌍을 이루기 위해 저장됩니다. 또한 동작에 의해 추가된 데이터도 수집됩니다. 수집된 이벤트 데이터는 메모리에 저장되므로 일정한 제한이 따릅니다. 이러한 제한은 시스템 용량 및 활동에 따라 달라집니다. 사용 가능한 시스템 리소스의 기준은 매개 변수로 사용 가능한 최대 메모리 양이 아니라 사용된 메모리 양이며 시스템 리소스를 사용할 수 없는 경우 저장된 짝이 없는 이벤트가 삭제됩니다. 이벤트가 짝이 없어 삭제된 경우 연결 이벤트는 짝이 없는 이벤트로 표시됩니다.  
  
 이벤트 쌍 대상은 짝이 없는 이벤트를 XML 형식으로 직렬화합니다. 이 형식은 어떤 스키마도 따르지 않으며 두 요소 유형만 포함합니다. 합니다  **\<쌍을 이루지 않는 >** 요소는 루트에 옵니다. **\<이벤트 >** 현재 추적 중인 각 쌍을 이루지 않는 이벤트에 대 한 요소입니다. 합니다  **\<이벤트 >** 요소 쌍을 이루지 않는 이벤트의 이름이 들어 있는 특성이 포함 되어 있습니다.  
  
## <a name="adding-the-target-to-a-session"></a>세션에 대상 추가  
 확장 이벤트 세션에 쌍 일치 대상을 추가하려면 이벤트 세션을 만들거나 변경할 때 다음 문을 포함해야 합니다.  
  
```  
ADD TARGET package0.pair_matching   
```  
  
 이 문 다음에 시작 이벤트와 종료 이벤트 및 일치시킬 동작이나 열을 정의하는 SET 문을 추가합니다. 다음 예제에서는 sqlserver.lock_acquired 및 sqlserver.lock_released 이벤트의 쌍 일치를 위한 예제 구문을 보여 줍니다.  
  
```  
   ( SET begin_event = 'sqlserver.lock_acquired',  
      begin_matching_columns = 'database_id, resource_0, resource_1, resource_2, transaction_id, mode',  
      end_event = 'sqlserver.lock_released',  
      end_matching_columns = 'database_id, resource_0, resource_1, resource_2, transaction_id, mode',  
   respond_to_memory_pressure = 1)  
```  
  
 자세한 내용은 [잠금을 보유한 쿼리 파악](../relational-databases/extended-events/determine-which-queries-are-holding-locks.md)을 참조하세요.  
  
## <a name="reviewing-the-target-output"></a>대상 출력 검토  
 다음 쿼리를 사용하여 쌍 일치 대상의 출력을 검토할 수 있습니다. 쿼리에서 *session_name* 을 이벤트 세션의 이름으로 바꿉니다.  
  
```  
SELECT name, target_name, CAST(xet.target_data AS xml)  
FROM sys.dm_xe_session_targets AS xet  
JOIN sys.dm_xe_sessions AS xe  
   ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'session_name'  
```  
  
 다음 예에서는 쌍 대상의 출력 형식을 보여 줍니다.  
  
```  
<unpaired truncated = "0" matchedCount = "[matched count]" memoryPressureDroppedCount = " [lost count]">  
    <event name  = "[event name]" package = "[package]" id= "[event ID value]" version = "[event version]">  
    <data name = "[column name]">   
    <type name = "[column type]" package = "[type package]" />   
    <value>[column value]</value>  
    <text value>[text value]</text>>  
        </data>  
    </event>  
</unpaired>  
```  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 확장 이벤트 대상](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [sys.dm_xe_session_targets&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)   
 [CREATE EVENT SESSION&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
