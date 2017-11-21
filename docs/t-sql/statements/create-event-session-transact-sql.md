---
title: "(Transact SQL) 이벤트 세션 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE EVENT SESSION
- SESSION
- EVENT SESSION
- SESSION_TSQL
- EVENT_SESSION_TSQL
- CREATE_EVENT_SESSION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- event sessions [SQL Server]
- CREATE EVENT SESSION statement
ms.assetid: 67683027-2b0f-47aa-b223-604731af8b4d
caps.latest.revision: 65
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: aaee13bce387e36c1dcb7d26f2dd983b8d36a661
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-event-session-transact-sql"></a>CREATE EVENT SESSION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  이벤트 원본, 이벤트 세션 대상 및 이벤트 세션 옵션을 식별하는 확장 이벤트 세션을 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [TRANSACT-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE EVENT SESSION event_session_name  
ON SERVER  
{  
    <event_definition> [ ,...n]  
    [ <event_target_definition> [ ,...n] ]  
    [ WITH ( <event_session_options> [ ,...n] ) ]  
}  
;  
  
<event_definition>::=  
{  
    ADD EVENT [event_module_guid].event_package_name.event_name   
         [ ( {   
                 [ SET { event_customizable_attribute = <value> [ ,...n] } ]  
                 [ ACTION ( { [event_module_guid].event_package_name.action_name [ ,...n] } ) ]  
                 [ WHERE <predicate_expression> ]  
        } ) ]  
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
  
<event_target_definition>::=  
{  
    ADD TARGET [event_module_guid].event_package_name.target_name  
        [ ( SET { target_parameter_name = <value> [ ,...n] } ) ]  
}  
  
<event_session_options>::=  
{  
    [    MAX_MEMORY = size [ KB | MB ] ]  
    [ [,] EVENT_RETENTION_MODE = { ALLOW_SINGLE_EVENT_LOSS | ALLOW_MULTIPLE_EVENT_LOSS | NO_EVENT_LOSS } ]  
    [ [,] MAX_DISPATCH_LATENCY = { seconds SECONDS | INFINITE } ]  
    [ [,] MAX_EVENT_SIZE = size [ KB | MB ] ]  
    [ [,] MEMORY_PARTITION_MODE = { NONE | PER_NODE | PER_CPU } ]  
    [ [,] TRACK_CAUSALITY = { ON | OFF } ]  
    [ [,] STARTUP_STATE = { ON | OFF } ]  
}  
```  
  
## <a name="arguments"></a>인수  
 *event_session_name*  
 이벤트 세션에 대한 사용자 정의 이름입니다. *event_session_name* 은 영숫자로 최대 128 자를 사용할 수의 인스턴스 내에서 고유 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대 한 규칙을 준수 해야 [식별자](../../relational-databases/databases/database-identifiers.md)합니다.  
  
 이벤트 추가 [ *event_module_guid* ]. *event_package_name*. *e n t _*  
 이벤트 세션과 연결할 이벤트입니다. 여기서 각 매개 변수의 의미는 다음과 같습니다.  
  
-   *event_module_guid* 이벤트를 포함 하는 모듈에 대 한 GUID입니다.  
  
-   *event_package_name* 작업 개체가 포함 된 패키지입니다.  
  
-   *e n t _* 이벤트 개체입니다.  
  
 이벤트는 sys.dm_xe_objects 뷰에 object_type 'event'로 표시됩니다.  
  
 설정 { *event_customizable_attribute*= \<값 > [,... *n*] }  
 이벤트의 사용자 지정 가능한 특성을 설정합니다. 사용자 지정 가능한 특성 표시는 sys.dm_xe_object_columns 뷰에 column_type 'customizable' 및 object_name = *e n t _*합니다.  
  
 작업 ({[*event_module_guid*]. *event_package_name*. *action_name* [ **,**... *n*] })  
 이벤트 세션과 연결할 동작입니다. 여기서 각 매개 변수의 의미는 다음과 같습니다.  
  
-   *event_module_guid* 이벤트를 포함 하는 모듈에 대 한 GUID입니다.  
  
-   *event_package_name* 작업 개체가 포함 된 패키지입니다.  
  
-   *action_name* 작업 개체입니다.  
  
 동작은 sys.dm_xe_objects 뷰에 object_type 'action'으로 표시됩니다.  
  
 여기서 \<_ e x p > 이벤트를 처리 해야 하는 경우를 확인 하는 데 사용 되는 조건자 식을 지정 합니다. 경우 \<_ e x p >이 true 이면 이벤트 처리 동작과 세션에 대 한 대상에 의해 더 이상. 경우 \<_ e x p >이 false 이면 이벤트는 세션에 대 한 동작과 대상에서 처리 되기 전에 세션에 의해 삭제 됩니다. 조건자 식은 3000자로 제한되며 문자열 인수를 제한합니다. 
  
 *event_field_name*  
 조건자 원본을 식별하는 이벤트 필드의 이름입니다.  
  
 [*event_module_guid*]. *event_package_name*. *predicate_source_name*  
 전역 조건자 원본의 이름입니다. 여기서 각 매개 변수의 의미는 다음과 같습니다.  
  
-   *event_module_guid* 이벤트를 포함 하는 모듈에 대 한 GUID입니다.  
  
-   *event_package_name* 조건자 개체가 포함 된 패키지입니다.  
  
-   *predicate_source_name* sys.dm_xe_objects 뷰에서 object_type 'pred_source'로 정의 됩니다.  
  
 [*event_module_guid*]. *event_package_name*. *predicate_compare_name*  
 이벤트와 연결할 조건자 개체의 이름입니다. 여기서 각 매개 변수의 의미는 다음과 같습니다.  
  
-   *event_module_guid* 이벤트를 포함 하는 모듈에 대 한 GUID입니다.  
  
-   *event_package_name* 조건자 개체가 포함 된 패키지입니다.  
  
-   *predicate_compare_name* 은 sys.dm_xe_objects 뷰에서 object_type 'pred_compare'로 정의 된 전역 원본입니다.  
  
 *number*  
 임의의 숫자 형식을 포함 한 **10 진수**합니다. 단, 사용 가능한 실제 메모리가 부족한 경우나 값이 너무 커서 64비트 정수로 표현할 수 없는 숫자는 제외됩니다.  
  
 '*문자열*'  
 조건자 비교에 필요한 ANSI 또는 유니코드 문자열입니다. 조건자 비교 함수에 대해서는 암시적 문자열 유형 변환이 수행되지 않습니다. 잘못된 유형을 전달하면 오류가 발생합니다.  
  
 대상 추가 [*event_module_guid*]. *event_package_name*. *target_name*  
 이벤트 세션과 연결할 대상입니다. 여기서 각 매개 변수의 의미는 다음과 같습니다.  
  
-   *event_module_guid* 이벤트를 포함 하는 모듈에 대 한 GUID입니다.  
  
-   *event_package_name* 작업 개체가 포함 된 패키지입니다.  
  
-   *target_name* 대상입니다. 대상은 sys.dm_xe_objects 뷰에 object_type 'target'으로 표시됩니다.  
  
 설정 { *target_parameter_name*= \<값 > [,... *n*] }  
 대상 매개 변수를 설정합니다. 대상 매개 변수 표시는 sys.dm_xe_object_columns 뷰에 column_type 'customizable' 및 object_name = *target_name*합니다.  
  
> [!IMPORTANT]  
>  링 버퍼 대상을 사용하는 경우 XML 출력의 데이터 잘림을 피하려면 max_memory 대상 매개 변수를 2048KB로 설정하는 것이 좋습니다. 다양 한 대상 유형에 사용 하는 경우에 대 한 자세한 내용은 참조 [SQL Server Extended Events Targets](http://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384)합니다.  
  
 와 ( \<event_session_options > [,...  *n* ]) 이벤트 세션에 사용할 옵션을 지정 합니다.  
  
 MAX_MEMORY =*크기* [KB | **MB** ]  
 이벤트 버퍼링을 위해 세션에 할당할 최대 메모리 양을 지정하며 기본값은 4MB입니다. *크기* 정수 이며 킬로바이트 (KB) 이나 메가바이트 (MB) 값이 될 수 있습니다.  
  
 EVENT_RETENTION_MODE = { **ALLOW_SINGLE_EVENT_LOSS** | ALLOW_MULTIPLE_EVENT_LOSS | NO_EVENT_LOSS}  
 이벤트 소실을 처리하는 데 사용할 이벤트 보존 모드를 지정합니다.  
  
 **ALLOW_SINGLE_EVENT_LOSS**  
 한 개의 이벤트가 세션에서 손실될 수 있습니다. 모든 이벤트 버퍼가 가득 찬 경우 한 개의 이벤트만 삭제됩니다. 이벤트 버퍼가 가득 찬 경우 이벤트 하나가 소실될 수 있도록 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 성능에 미치는 영향을 허용 범위 내로 유지하면서도 처리된 이벤트 스트림에서 데이터가 소실되는 것을 최소화할 수 있습니다.  
  
 ALLOW_MULTIPLE_EVENT_LOSS  
 여러 개의 이벤트를 포함하는 가득 찬 이벤트 버퍼가 세션에서 손실될 수 있습니다. 손실되는 이벤트 수는 세션에 할당된 메모리 크기, 메모리 분할 및 버퍼에 있는 이벤트의 크기에 따라 달라집니다. 이 옵션은 이벤트 버퍼가 빠른 속도로 채워질 때 서버에 미치는 성능 영향을 최소화하지만 많은 수의 이벤트가 세션에서 손실될 수 있습니다.  
  
 NO_EVENT_LOSS  
 이벤트 손실이 허용되지 않습니다. 이 옵션을 사용하면 발생한 모든 이벤트가 보존되며, 이벤트 버퍼에 사용 가능한 공간이 생길 때까지 이벤트를 발생시키는 모든 태스크가 대기합니다. 따라서 이벤트 세션이 활성 상태인 동안에는 성능이 저하될 수 있습니다. 버퍼에서 이벤트가 플러시되기를 기다리는 동안 사용자 연결이 교착 상태에 빠질 수 있습니다.  
  
 MAX_DISPATCH_LATENCY = { *초* 초 | **무한** }  
 이벤트가 이벤트 세션 대상에 디스패치되기 전에 메모리에 버퍼링될 시간을 지정합니다. 기본적으로 이 값은 30초로 설정됩니다.  
  
 *초* 초  
 버퍼를 대상에 플러시하기 시작할 때까지 대기하는 초 단위 시간입니다. *초* 정수입니다. 최소 대기 시간 값은 1초입니다. 값으로 0을 사용하면 INFINITE 대기를 지정할 수 있습니다.  
  
 **무한**  
 버퍼가 가득 차거나 이벤트 세션이 종료된 경우에만 버퍼를 대상에 플러시합니다.  
  
> [!NOTE]  
>  MAX_DISPATCH_LATENCY = 0 SECONDS는 MAX_DISPATCH_LATENCY = INFINITE와 같습니다.  
  
 MAX_EVENT_SIZE =*크기* [KB | **MB** ]  
 이벤트에 허용되는 최대 크기를 지정합니다. MAX_EVENT_SIZE는 단일 이벤트가 MAX_MEMORY보다 크도록 설정해야만 합니다. 단일 이벤트가 MAX_MEMORY보다 작을 경우 오류가 발생합니다. *크기* 정수 이며 킬로바이트 (KB) 이나 메가바이트 (MB) 값이 될 수 있습니다. 경우 *크기* 허용 되는 최소 크기는 64KB (킬로바이트)에 지정 됩니다. MAX_EVENT_SIZE가 설정 된 경우,의 두 버퍼가 *크기* MAX_MEMORY 외에도 생성 됩니다. 이는 이벤트 버퍼링에 사용되는 총 메모리가 MAX_MEMORY + 2 * MAX_EVENT_SIZE임을 의미합니다.  
  
 MEMORY_PARTITION_MODE = { **NONE** | PER_NODE | PER_CPU}  
 이벤트 버퍼가 만들어지는 위치를 지정합니다.  
  
 **NONE**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내에 한 개의 버퍼 집합이 만들어집니다.  
  
 PER_NODE  
 NUMA 노드당 한 개의 버퍼 집합이 만들어집니다.  
  
 PER_CPU  
 CPU당 한 개의 버퍼 집합이 만들어집니다.  
  
 TRACK_CAUSALITY = {ON | **OFF** }  
 인과 관계를 추적할지 여부를 지정합니다. 이를 ON으로 설정하면 인과 관계에 따라 다른 서버 연결에 있는 관련 이벤트의 상호 연결이 허용됩니다.  
  
 STARTUP_STATE = {ON | **OFF** }  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 시작될 때 해당 이벤트 세션을 자동으로 시작할지 여부를 지정합니다.  
  
> [!NOTE]  
>  STARTUP_STATE = ON이면 SQL Server를 중지했다가 다시 시작한 경우에만 이벤트 세션이 시작됩니다.  
  
 ON  
 시작 시 이벤트 세션이 시작됩니다.  
  
 **OFF**  
 시작 시 이벤트 세션이 시작되지 않습니다.  
  
## <a name="remarks"></a>주의  
 논리 연산자의 우선 순위는 NOT(가장 높음), AND, OR 순입니다.  
  
## <a name="permissions"></a>Permissions  
 ALTER ANY EVENT SESSION 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `test_session`이라는 이벤트 세션을 만드는 방법을 보여 줍니다. 두 개의 이벤트를 추가하며 Windows용 이벤트 추적 대상을 사용합니다.  
  
```  
IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='test_session')  
    DROP EVENT session test_session ON SERVER;  
GO  
CREATE EVENT SESSION test_session  
ON SERVER  
    ADD EVENT sqlos.async_io_requested,  
    ADD EVENT sqlserver.lock_acquired  
    ADD TARGET package0.etw_classic_sync_target   
        (SET default_etw_session_logfile_path = N'C:\demo\traces\sqletw.etl' )  
    WITH (MAX_MEMORY=4MB, MAX_EVENT_SIZE=4MB);  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER EVENT SESSION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)   
 [DROP EVENT SESSION&#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-session-transact-sql.md)   
 [sys.server_event_sessions&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)   
 [sys.dm_xe_objects&#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql.md)   
 [sys.dm_xe_object_columns&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-object-columns-transact-sql.md)  
  
  


