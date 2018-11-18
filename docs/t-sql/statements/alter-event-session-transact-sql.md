---
title: ALTER EVENT SESSION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/07/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER EVENT SESSION
- ALTER_EVENT_SESSION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- event sessions [SQL Server]
- extended events [SQL Server], Transact-SQL
- ALTER EVENT SESSION statement
ms.assetid: da006ac9-f914-4995-a2fb-25b5d971cd90
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 6fb0c0e35b2350bf3b1753434425389eb8f3503d
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51696799"
---
# <a name="alter-event-session-transact-sql"></a>ALTER EVENT SESSION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이벤트 세션을 시작 또는 중지하거나 이벤트 세션 구성을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
ALTER EVENT SESSION event_session_name  
ON SERVER  
{  
    [ [ {  <add_drop_event> [ ,...n] }     
       | { <add_drop_event_target> [ ,...n ] } ]   
    [ WITH ( <event_session_options> [ ,...n ] ) ]  
    ]  
    | [ STATE = { START | STOP } ]  
}  
  
<add_drop_event>::=  
{  
    [ ADD EVENT <event_specifier>   
         [ ( {   
                 [ SET { event_customizable_attribute = <value> [ ,...n ] } ]  
                 [ ACTION ( { [event_module_guid].event_package_name.action_name [ ,...n ] } ) ]  
                 [ WHERE <predicate_expression> ]  
        } ) ]  
   ]   
   | DROP EVENT <event_specifier> }  
  
<event_specifier> ::=  
{  
[event_module_guid].event_package_name.event_name  
}  
  
<predicate_expression> ::=   
{  
    [ NOT ] <predicate_factor> | {( <predicate_expression> ) }   
    [ { AND | OR } [ NOT ] { <predicate_factor> | ( <predicate_expression> ) } ]   
    [ ,...n ]  
}  
  
<predicate_factor>::=   
{  
    <predicate_leaf> | ( <predicate_expression> )  
}  
  
<predicate_leaf>::=  
{  
      <predicate_source_declaration> { = | < > | ! = | > | > = | < | < = } <value>   
    | [event_module_guid].event_package_name.predicate_compare_name ( <predicate_source_declaration>, <value> )   
}  
  
<predicate_source_declaration>::=   
{  
    event_field_name | ( [event_module_guid].event_package_name.predicate_source_name )  
}  
  
<value>::=   
{  
    number | 'string'  
}  
  
<add_drop_event_target>::=  
{  
    ADD TARGET <event_target_specifier>  
        [ ( SET { target_parameter_name = <value> [ ,...n] } ) ]  
    | DROP TARGET <event_target_specifier>  
}  
  
<event_target_specifier>::=  
{  
    [event_module_guid].event_package_name.target_name  
}  
  
<event_session_options>::=  
{  
    [    MAX_MEMORY = size [ KB | MB] ]  
    [ [,] EVENT_RETENTION_MODE = { ALLOW_SINGLE_EVENT_LOSS | ALLOW_MULTIPLE_EVENT_LOSS | NO_EVENT_LOSS } ]  
    [ [,] MAX_DISPATCH_LATENCY = { seconds SECONDS | INFINITE } ]  
    [ [,] MAX_EVENT_SIZE = size [ KB | MB ] ]  
    [ [,] MEMORY_PARTITION_MODE = { NONE | PER_NODE | PER_CPU } ]  
    [ [,] TRACK_CAUSALITY = { ON | OFF } ]  
    [ [,] STARTUP_STATE = { ON | OFF } ]  
}  
```  
  
## <a name="arguments"></a>인수  
  
|||  
|-|-|  
|용어|정의|  
|*event_session_name*|기존 이벤트 세션의 이름입니다.|  
|STATE = START &#124; STOP|이벤트 세션을 시작 또는 중지합니다. 이 인수는 ALTER EVENT SESSION이 이벤트 세션 개체에 적용되는 경우에만 사용할 수 있습니다.|  
|ADD EVENT \<event_specifier>|\<event_specifier>로 식별되는 이벤트를 이벤트 세션과 연결합니다.|
|[*event_module_guid*]*.event_package_name.event_name*|이벤트 패키지에 있는 이벤트의 이름입니다. 여기서 각 매개 변수의 의미는 다음과 같습니다.<br /><br /> -   *event_module_guid*는 이벤트가 포함된 모듈의 GUID입니다.<br />-   *event_package_name*은 동작 개체가 포함된 패키지입니다.<br />-   *event_name*은 이벤트 개체입니다.<br /><br /> 이벤트는 sys.dm_xe_objects 뷰에 object_type 'event'로 표시됩니다.|  
|SET { *event_customizable_attribute*= \<value> [ ,...*n*] }|이벤트의 사용자 지정 가능한 특성을 지정합니다. 사용자 지정 가능한 특성은 sys.dm_xe_object_columns 뷰에 column_type 'customizable' 및 object_name = *event_name*으로 표시됩니다.|  
|ACTION ( { [*event_module_guid*]*.event_package_name.action_name* [ **,**...*n*] } )|이벤트 세션과 연결할 동작입니다. 여기서 각 매개 변수의 의미는 다음과 같습니다.<br /><br /> -   *event_module_guid*는 이벤트가 포함된 모듈의 GUID입니다.<br />-   *event_package_name*은 동작 개체가 포함된 패키지입니다.<br />-   *action_name*은 동작 개체입니다.<br /><br /> 동작은 sys.dm_xe_objects 뷰에 object_type 'action'으로 표시됩니다.|  
|WHERE \<predicate_expression>|이벤트 처리 여부를 확인하는 데 사용할 조건자 식을 지정합니다. \<predicate_expression>이 true일 경우 이벤트가 세션에 대한 동작과 대상에 의해 추가로 처리됩니다. \<predicate_expression>이 false일 경우 세션에 대한 동작과 대상에 의해 이벤트가 처리되기 전에 세션을 통해 이벤트가 삭제됩니다. 조건자 식은 3000자로 제한되며 문자열 인수를 제한합니다.|
|*event_field_name*|조건자 원본을 식별하는 이벤트 필드의 이름입니다.|  
|[event_module_guid].event_package_name.predicate_source_name|전역 조건자 원본의 이름입니다. 여기서 각 매개 변수의 의미는 다음과 같습니다.<br /><br /> -   *event_module_guid*는 이벤트가 포함된 모듈의 GUID입니다.<br />-   *event_package_name*은 조건자 개체가 포함된 패키지입니다.<br />-   *predicate_source_name*은 sys.dm_xe_objects 뷰에서 object_type 'pred_source'로 정의됩니다.|  
|[*event_module_guid*].*event_package_name*.*predicate_compare_name*|이벤트와 연결할 조건자 개체의 이름입니다. 여기서 각 매개 변수의 의미는 다음과 같습니다.<br /><br /> -   *event_module_guid*는 이벤트가 포함된 모듈의 GUID입니다.<br />-   *event_package_name*은 조건자 개체가 포함된 패키지입니다.<br />-   *predicate_compare_name*은 sys.dm_xe_objects 뷰에서 object_type 'pred_compare'로 정의된 전역 원본입니다.|  
|DROP EVENT \<event_specifier>|*\<event_specifier>* 로 식별되는 이벤트를 삭제합니다. \<event_specifier>는 이벤트 세션에서 유효해야 합니다.|  
|ADD TARGET \<event_target_specifier>|\<event_target_specifier>로 식별되는 대상을 이벤트 세션과 연결합니다.|
|[*event_module_guid*].*event_package_name*.*target_name*|이벤트 세션에 있는 대상의 이름입니다. 여기서 각 매개 변수의 의미는 다음과 같습니다.<br /><br /> -   *event_module_guid*는 이벤트가 포함된 모듈의 GUID입니다.<br />-   *event_package_name*은 동작 개체가 포함된 패키지입니다.<br />-   *target_name*은 동작입니다. 동작은 sys.dm_xe_objects 뷰에 object_type 'target'으로 표시됩니다.|  
|SET { *target_parameter_name*= \<value> [, ...*n*] }|대상 매개 변수를 설정합니다. 대상 매개 변수는 sys.dm_xe_object_columns 뷰에 column_type 'customizable' 및 object_name = *target_name*으로 표시됩니다.<br /><br /> **참고!** 링 버퍼 대상을 사용하는 경우 XML 출력의 데이터 잘림을 피하려면 max_memory 대상 매개 변수를 2048KB로 설정하는 것이 좋습니다. 다양한 대상 유형을 사용할 경우에 대한 자세한 내용은 [SQL Server 확장 이벤트 대상](https://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384)을 참조하세요.|  
|DROP TARGET \<event_target_specifier>|\<event_target_specifier>로 식별되는 대상을 삭제합니다. \<event_target_specifier>는 이벤트 세션에서 유효해야 합니다.|  
|EVENT_RETENTION_MODE = { **ALLOW_SINGLE_EVENT_LOSS** &#124; ALLOW_MULTIPLE_EVENT_LOSS &#124; NO_EVENT_LOSS }|이벤트 소실을 처리하는 데 사용할 이벤트 보존 모드를 지정합니다.<br /><br /> **ALLOW_SINGLE_EVENT_LOSS**<br /> 한 개의 이벤트가 세션에서 손실될 수 있습니다. 모든 이벤트 버퍼가 가득 찬 경우 한 개의 이벤트만 삭제됩니다. 이벤트 버퍼가 가득 찬 경우 이벤트 하나가 소실될 수 있도록 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 성능에 미치는 영향을 허용 범위 내로 유지하면서도 처리된 이벤트 스트림에서 데이터가 소실되는 것을 최소화할 수 있습니다.<br /><br /> ALLOW_MULTIPLE_EVENT_LOSS<br /> 여러 개의 이벤트를 포함하는 가득 찬 이벤트 버퍼가 세션에서 손실될 수 있습니다. 손실되는 이벤트 수는 세션에 할당된 메모리 크기, 메모리 분할 및 버퍼에 있는 이벤트의 크기에 따라 달라집니다. 이 옵션은 이벤트 버퍼가 빠른 속도로 채워질 때 서버에 미치는 성능 영향을 최소화하지만 많은 수의 이벤트가 세션에서 손실될 수 있습니다.<br /><br /> NO_EVENT_LOSS<br /> 이벤트 손실이 허용되지 않습니다. 이 옵션을 사용하면 발생한 모든 이벤트가 보존되며, 이벤트 버퍼에 사용 가능한 공간이 생길 때까지 이벤트를 발생시키는 모든 태스크가 대기합니다. 따라서 이벤트 세션이 활성 상태인 동안에는 성능이 저하될 수 있습니다. 버퍼에서 이벤트가 플러시되기를 기다리는 동안 사용자 연결이 교착 상태에 빠질 수 있습니다.|  
|MAX_DISPATCH_LATENCY = { *seconds* SECONDS &#124; **INFINITE** }|이벤트가 이벤트 세션 대상에 디스패치되기 전에 메모리에 버퍼링되는 시간을 지정합니다. 최소 대기 시간 값은 1초입니다. 값으로 0을 사용하면 INFINITE 대기를 지정할 수 있습니다. 기본적으로 이 값은 30초로 설정됩니다.<br /><br /> *초* SECONDS<br /> 버퍼를 대상에 플러시하기 시작할 때까지 대기하는 초 단위 시간입니다. *초*는 정수입니다.<br /><br /> **INFINITE**<br /> 버퍼가 가득 차거나 이벤트 세션이 종료된 경우에만 버퍼를 대상에 플러시합니다.<br /><br /> **참고!** MAX_DISPATCH_LATENCY = 0 SECONDS는 MAX_DISPATCH_LATENCY = INFINITE와 같습니다.|  
|MAX_EVENT_SIZE =*size* [ KB &#124; **MB** ]|이벤트에 허용되는 최대 크기를 지정합니다. MAX_EVENT_SIZE는 단일 이벤트가 MAX_MEMORY보다 크도록 설정해야만 합니다. 단일 이벤트가 MAX_MEMORY보다 작을 경우 오류가 발생합니다. *크기*는 정수이며 KB 또는 MB 값일 수 있습니다. *크기*가 KB로 지정되는 경우 최소 허용 크기는 64KB입니다. MAX_EVENT_SIZE가 설정된 경우 MAX_MEMORY 외에 *크기*의 두 버퍼가 생깁니다. 이는 이벤트 버퍼링에 사용되는 총 메모리가 MAX_MEMORY + 2 * MAX_EVENT_SIZE임을 의미합니다.|  
|MEMORY_PARTITION_MODE = { **NONE** &#124; PER_NODE &#124; PER_CPU }|이벤트 버퍼가 만들어지는 위치를 지정합니다.<br /><br /> **NONE**<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내에 한 개의 버퍼 집합이 만들어집니다.<br /><br /> PER NODE - NUMA 노드당 한 개의 버퍼 집합이 만들어집니다.<br /><br /> PER NODE - CPU당 한 개의 버퍼 집합이 만들어집니다.|  
|TRACK_CAUSALITY = { ON &#124; **OFF** }|인과 관계를 추적할지 여부를 지정합니다. 이를 ON으로 설정하면 인과 관계에 따라 다른 서버 연결에 있는 관련 이벤트의 상호 연결이 허용됩니다.|  
|STARTUP_STATE = { ON &#124; **OFF** }|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 시작될 때 해당 이벤트 세션을 자동으로 시작할지 여부를 지정합니다.<br /><br /> STARTUP_STATE = ON이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 중지했다가 다시 시작한 경우에만 이벤트 세션이 시작됩니다.<br /><br /> ON= 시작 시 이벤트 세션이 시작됩니다.<br /><br /> **OFF** = 시작 시 이벤트 세션이 시작되지 않습니다.|  
  
## <a name="remarks"></a>Remarks  
 ADD 및 DROP 인수는 같은 문에 동시에 사용할 수 없습니다.  
  
## <a name="permissions"></a>Permissions  
 ALTER ANY EVENT SESSION 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 이벤트 세션을 시작하고 몇 가지 사용 중인 세션 통계를 확인한 다음 기존 세션에 두 개의 이벤트를 추가합니다.  
  
```  
-- Start the event session  
ALTER EVENT SESSION test_session  
ON SERVER  
STATE = start;  
GO  
-- Obtain live session statistics   
SELECT * FROM sys.dm_xe_sessions;  
SELECT * FROM sys.dm_xe_session_events;  
GO  
  
-- Add new events to the session  
ALTER EVENT SESSION test_session ON SERVER  
ADD EVENT sqlserver.database_transaction_begin,  
ADD EVENT sqlserver.database_transaction_end;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE EVENT SESSION&#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)   
 [DROP EVENT SESSION&#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-session-transact-sql.md)   
 [SQL Server 확장 이벤트 대상](https://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384)   
 [sys.server_event_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)   
 [sys.dm_xe_objects &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql.md)   
 [sys.dm_xe_object_columns&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-object-columns-transact-sql.md)  
  
  
