---
title: 링 버퍼 대상 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- targets [SQL Server extended events], ring buffer target
- ring buffer target [SQL Server extended events]
ms.assetid: 54494e11-b56b-43b7-aa5e-c8724e56b251
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d042ef49a82d16eb33cb27d80c8083a68ea69092
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62773681"
---
# <a name="ring-buffer-target"></a>링 버퍼 대상
  간단히 말해 링 버퍼 대상은 메모리에 이벤트 데이터를 보관합니다. 이 대상은 다음 두 모드 중 하나로 이벤트를 관리할 수 있습니다.  
  
-   첫째 모드는 엄격한 FIFO(선입선출) 모드로서 대상에 할당된 모든 메모리가 사용되면 가장 오래된 이벤트가 삭제됩니다. 기본 모드인 이 모드에서는 occurrence_number 옵션이 0으로 설정됩니다.  
  
-   둘째 모드는 이벤트별 FIFO 모드로서 각 유형별로 지정된 이벤트 수가 유지됩니다. 이 모드에서는 대상에 할당 된 모든 메모리가 사용 되 면 각 유형별로 가장 오래 된 이벤트가 삭제 됩니다. occurrence_number 옵션을 구성하여 각 유형별로 보존할 이벤트 수를 지정할 수 있습니다.  
  
 다음 표에서는 링 버퍼 대상을 구성하는 데 사용할 수 있는 옵션에 대해 설명합니다.  
  
|옵션|허용된 값|Description|  
|------------|--------------------|-----------------|  
|max_memory|모든 32 비트 정수입니다. 이 값은 선택 사항입니다.|사용 가능한 최대 메모리 크기(KB)입니다. 기존 이벤트는 처음 도달한 제한인 max_event_limit 또는 max_memory에 따라 삭제됩니다. 최대값은 4194303 (kb)입니다. SQL Server의 다른 메모리 소비자에 게 영향을 줄 수 있으므로 제한 GB 범위의 링 버퍼 크기를 설정 하기 전에 신중 하 게 고려 이루어져야|  
|max_event_limit|모든 32 비트 정수입니다. 이 값은 선택 사항입니다.|ring_buffer에 보관되는 최대 이벤트 수입니다. 기존 이벤트는 처음 도달한 제한인 max_event_limit 또는 max_memory에 따라 삭제됩니다. 기본값 = 1000입니다.|  
|occurrence_number|다음 값 중 하나입니다.<br /><br /> 0(기본값) = 대상에 할당된 모든 메모리가 사용되면 가장 오래된 이벤트가 삭제됩니다.<br /><br /> 32 비트 정수 = 이벤트별 fifo 방식으로 삭제 하기 전까지 유지할 각 유형의 이벤트 개수입니다.<br /><br /> <br /><br /> 이 값은 선택 사항입니다.|사용할 FIFO 모드 및 각 유형별로 버퍼에 기본적으로 보존할 이벤트의 수(0보다 큰 값을 설정한 경우)입니다.|
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="adding-the-target-to-a-session"></a>세션에 대상 추가  
 확장 이벤트 세션에 링 버퍼 대상을 추가하려면 이벤트 세션을 만들거나 변경할 때 다음 문을 포함해야 합니다.  
  
```sql
ADD TARGET package0.ring_buffer  
```  
  
## <a name="reviewing-the-target-output"></a>대상 출력 검토  
 링 버퍼 대상의 출력을 검토하려면 다음 쿼리를 사용합니다. 쿼리에서 *session_name* 을 이벤트 세션의 이름으로 바꿉니다.  
  
```sql
SELECT name, target_name, CAST(xet.target_data AS xml)  
FROM sys.dm_xe_session_targets AS xet  
JOIN sys.dm_xe_sessions AS xe  
   ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'session_name'  
```  
  
 다음 예에서는 링 버퍼 대상의 출력 형식을 보여 줍니다.  
  
```  
<RingBufferTarget eventsPerSec="" processingTime="" totalEventsProcessed="" eventCount="" droppedCount="" memoryUsed="">  
 <event name="" package="" id="" version="" timestamp="">  
    <data name="">  
      <type name="" package="" />  
      <value></value>  
      <text></text>  
    </data>  
    <action name="" package="">  
      <type name="" package="" />  
      <value></value>  
      <text></text>  
    </action>  
  </event>  
</RingBufferTarget>  
```


## <a name="see-also"></a>관련 항목

- [SQL Server Extended Events Targets](../../2014/database-engine/sql-server-extended-events-targets.md)
- [sys.dm_xe_session_targets&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql?view=sql-server-2016)
- [CREATE EVENT SESSION&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql?view=sql-server-2016)
- [ALTER EVENT SESSION&#40;Transact-SQL&#41;](https://docs.microsoft.com/sql/t-sql/statements/alter-event-session-transact-sql?view=sql-server-2016)

