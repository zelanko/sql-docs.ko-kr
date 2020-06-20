---
title: 히스토그램 대상 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- bucketing target [SQL Server extended events]
- event bucketing target
- targets [SQL Server extended events], bucketing
ms.assetid: 2ea39141-7eb0-4c74-abf8-114c2c106a19
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: acb124ef949849561a6bca0ba4016b40c1343384
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84932844"
---
# <a name="histogram-target"></a>히스토그램 대상
  히스토그램 대상은 이벤트 데이터를 기준으로 특정 이벤트 유형의 항목을 그룹화합니다. 이벤트 그룹화는 지정된 이벤트 열 또는 동작을 기준으로 계산됩니다. 히스토그램 대상을 사용하여 성능 문제를 해결할 수 있습니다. 가장 자주 발생하는 이벤트가 무엇인지 확인하면 성능 문제의 원인이 될 수 있는 "핫스폿"을 찾아낼 수 있습니다.  
  
 다음 표에서는 히스토그램 대상을 구성하는 데 사용할 수 있는 옵션을 설명합니다.  
  
|옵션|허용되는 값|Description|  
|------------|--------------------|-----------------|  
|slots|임의의 정수 값을 사용할 수 있습니다. 이 값은 선택 사항입니다.|유지할 최대 그룹화 수를 나타내는 사용자 지정 값입니다. 이 값에 도달하면 기존 그룹에 속하지 않는 새 이벤트는 무시됩니다.<br /><br /> 성능 향상을 위해 슬롯 번호는 2의 다음 거듭제곱으로 반올림됩니다.|  
|filtering_event_name|확장 이벤트 세션에 있는 이벤트입니다. 이 값은 선택 사항입니다.|이벤트의 클래스를 식별하는 데 사용되는 사용자 지정 값입니다. 지정된 이벤트의 인스턴스만 버킷팅되고 다른 이벤트는 모두 무시됩니다.<br /><br /> 이 값을 지정하는 경우 *package_name*.*event_name*형식을 사용해야 합니다(예: `'sqlserver.checkpoint_end'`). 다음 쿼리를 사용하여 패키지 이름을 확인할 수 있습니다.<br /><br /> P.name, se event_name를 선택 합니다.<br />Sys. dm_xe_session_events se<br />Dm_xe_packages p를 조인 합니다.<br />ON se_event_package_guid = p. guid<br />ORDER BY p.name, se. event_name<br /><br /> <br /><br /> filtering_event_name 값을 지정하지 않는 경우 source_type을 기본값인 1로 설정해야 합니다.|  
|source_type|버킷의 기반이 되는 개체의 유형입니다. 이 값은 선택 사항이고 지정되지 않은 경우 기본값이 1입니다.|다음 값 중 하나가 될 수 있습니다.<br /><br /> 0 = 이벤트<br /><br /> 1 = 동작|  
|source|이벤트 열 또는 동작의 이름입니다.|데이터 원본으로 사용되는 이벤트 열 또는 동작 이름입니다.<br /><br /> 원본에 대한 이벤트 열을 지정하는 경우 filtering_event_name 값에 사용되는 이벤트의 열을 지정해야 합니다. 다음 쿼리를 사용하여 후보 열을 확인할 수 있습니다.<br /><br /> Sys. dm_xe_object_columns에서 이름을 선택 합니다.<br />WHERE object_name = ' \<eventname> '<br />및 column_type! = ' readonly '<br /><br /> 원본에 대한 이벤트 열을 지정할 때는 원본 값에 패키지 이름을 포함할 필요가 없습니다.<br /><br /> 원본에 대한 동작 이름을 지정하는 경우 이 대상이 사용되고 있는 이벤트 세션의 컬렉션을 위해 구성된 동작 중 하나를 사용해야 합니다. sys.dm_xe_sesssion_event_actions view의 action_name 열을 쿼리하면 동작 이름의 후보 값을 찾을 수 있습니다.<br /><br /> 동작 이름을 데이터 원본으로 사용하고 있는 경우 *package_name*.*action_name*형식을 사용하여 원본 값을 지정해야 합니다.|  
  
 다음 예에서는 히스토그램 대상이 데이터를 수집하는 방식을 높은 수준에서 보여 줍니다. 이 예에서 히스토그램 대상을 사용하여 각 대기 유형의 대기 횟수가 몇 번인지 계산할 수 있습니다. 이를 계산하려면 히스토그램 대상을 정의할 때 다음 옵션을 지정하면 됩니다.  
  
-   filtering_event_name = 'wait_info'  
  
-   source = 'wait_type'  
  
-   source_type = 0(wait_type이 이벤트 열이므로)  
  
 예제 시나리오에서는 wait_type 원본에 대해 다음 데이터가 기록됩니다.  
  
|필터링 이벤트 이름|원본 열 값|  
|--------------------------|-------------------------|  
|wait_info|file_io|  
|wait_info|file_io|  
|wait_info|network|  
|wait_info|network|  
|wait_info|sleep|  
  
 대기 유형 값은 세 개의 슬롯으로 분류되고 각각의 값 및 슬롯 개수는 다음과 같습니다.  
  
|값|슬롯 개수|  
|-----------|----------------|  
|file_io|2|  
|network|2|  
|sleep|1|  
  
 히스토그램 대상은 지정된 원본에 대한 이벤트 데이터만 유지합니다. 이벤트 데이터가 너무 커서 모두 유지할 수 없는 경우에는 데이터가 잘립니다. 이벤트 데이터가 잘리면 바이트 수가 기록되고 XML 출력으로 표시됩니다.  
  
## <a name="adding-the-target-to-a-session"></a>세션에 대상 추가  
 확장 이벤트 세션에 히스토그램 대상을 추가하려면 이벤트 세션을 만들거나 변경할 때 추가할 대상 유형에 따라 다음 문 중 하나를 포함해야 합니다.  
  
```  
ADD TARGET package0.histogram  
```  
  
 SET 문을 사용하여 다양한 옵션을 설정할 수 있습니다. 다음 예제에서는 sqlserver.checkpoint_end 이벤트의 데이터가 수집되는 히스토그램 대상을 추가하는 방법을 보여 줍니다.  
  
```  
ADD TARGET package0.histogram  
(SET slots = 32, filtering_event_name = 'sqlserver.checkpoint_end', source_type = 0, source = 'database_id')  
```  
  
 자세한 내용은 [가장 많은 잠금이 발생한 개체 찾기](../relational-databases/extended-events/find-the-objects-that-have-the-most-locks-taken-on-them.md)및 [확장 이벤트를 사용하여 시스템 작업 모니터링](../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)을 참조하세요.  
  
## <a name="reviewing-the-target-output"></a>대상 출력 검토  
 히스토그램 대상은 데이터를 XML 형식으로 직렬화하여 호출 프로그램 또는 프로시저에 반환합니다. 대상 출력은 어떤 스키마도 따르지 않습니다.  
  
 다음 쿼리를 사용하여 히스토그램 대상의 출력을 검토할 수 있습니다. 쿼리에서 *session_name* 을 이벤트 세션의 이름으로 바꿉니다.  
  
```  
SELECT name, target_name, CAST(xet.target_data AS xml)  
FROM sys.dm_xe_session_targets AS xet  
JOIN sys.dm_xe_sessions AS xe  
   ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'session_name'  
```  
  
 다음 예에서는 히스토그램 대상의 출력 형식을 보여 줍니다.  
  
```  
<Slots truncated = "0" buckets=[count]>  
    <Slot count=[count] trunc=[truncated bytes]>  
        <value>  
        </value>  
    </Slot>  
</Slots>  
```  
  
## <a name="see-also"></a>참고 항목  
 [확장 이벤트 대상 SQL Server](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [dm_xe_session_targets &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)   
 [Transact-sql&#41;&#40;이벤트 세션 만들기](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
