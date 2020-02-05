---
title: 확장 이벤트에 대한 시스템 뷰의 SELECT 및 JOIN
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
ms.assetid: 04521d7f-588c-4259-abc2-1a2857eb05ec
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d3bcb7e272c1a5120b65018aab781546ba8d0f2b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75242895"
---
# <a name="selects-and-joins-from-system-views-for-extended-events-in-sql-server"></a>SQL Server 확장 이벤트에 대한 시스템 뷰의 SELECT 및 JOIN

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


이 문서에서는 SQL Server 및 Azure SQL Database의 확장 이벤트와 관련된 두 가지 시스템 뷰 집합에 대해 설명합니다. 문서 내용은 다음과 같습니다.

- 다양한 시스템 뷰를 조인(JOIN)하는 방법
- 시스템 뷰에서 특정 종류의 정보를 선택(SELECT)하는 방법
- 각 관점의 이해에 도움이 되도록 동일한 이벤트 세션 정보를 다양한 기술적 관점에서 표현하는 방법


대부분의 예제는 SQL Server용으로 작성되었습니다. 하지만 약간만 편집하면 SQL 데이터베이스에서도 실행됩니다.



## <a name="a-foundational-information"></a>A. 기본 정보


확장 이벤트에 대한 다음 두 가지 시스템 뷰 집합이 있습니다.


#### <a name="catalog-views"></a>카탈로그 뷰:

- 이러한 뷰는 *CREATE EVENT SESSION* 또는 동등한 SSMS UI에 의해 생성된 각 이벤트 세션의 [정의](../../t-sql/statements/create-event-session-transact-sql.md)에 대한 정보를 저장합니다. 그러나 세션 실행이 시작된 적이 있는지 여부에 대한 정보는 없습니다.
    - 예를 들어 SSMS **개체 탐색기** 에 정의된 이벤트 세션이 없다고 표시되는 경우 *sys.server_event_session_targets* 뷰에서 SELECT를 실행하면 0개 행이 반환됩니다.


- 이름 접두사는 다음과 같습니다.
    - SQL Server의 이름 접두사는 *sys.server\_event\_session\** 입니다.
    - SQL 데이터베이스의 이름 접두사는 *sys.database\_event\_session\** 입니다.


#### <a name="dynamic-management-views-dmvs"></a>DMV(동적 관리 뷰)

- 실행 중인 이벤트 세션의 *현재 활동* 에 대한 정보를 저장합니다. 그러나 이러한 DMV에는 세션의 정의에 대한 정보가 거의 없습니다.
    - 모든 이벤트 세션이 현재 중지된 경우에도 *sys.dm_xe_packages* 뷰에서 SELECT를 실행하면 다양한 패키지가 서버 시작 시 활성 메모리에 로드되기 때문에 여전히 행이 반환됩니다.
    - 동일한 이유로 *sys.dm_xe_objects* *sys.dm_xe_object_columns*도 여전히 행을 반환합니다.


- 확장 이벤트 DMV에 대한 이름 접두사는 다음과 같습니다.
    - SQL Server의 이름 접두사는 *sys.dm\_xe\_\** 입니다.
    - 일반적으로 SQL Database의 이름 접두사는 *sys.dm\_xe\_database\_\** 입니다.


#### <a name="permissions"></a>사용 권한:


시스템 뷰에서 SELECT를 실행하려면 다음과 같은 사용 권한이 필요합니다.

- VIEW SERVER STATE - Microsoft SQL Server에 있는 경우
- VIEW DATABASE STATE - Azure SQL 데이터베이스에 있는 경우


<a name="section_B_catalog_views"></a>

## <a name="b-catalog-views"></a>B. 카탈로그 뷰


이 섹션에서는 동일하게 정의된 이벤트 세션에 대한 세 가지 기술적 관점을 일치 및 상호 연결합니다. 세션이 정의되었으며 SQL Server Management Studio(SSMS.exe)의 **개체 탐색기** 에 표시되지만 세션이 현재 실행되고 있지 않습니다.

예기치 않은 오류를 방지하려면 매달 [SSMS의 최신 업데이트를 설치](https://msdn.microsoft.com/library/mt238290.aspx)하는 것이 좋습니다.


확장 이벤트 카탈로그 뷰에 대한 참조 설명서는 [확장 이벤트 카탈로그 뷰(TRANSACT-SQL)](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)에 있습니다.


&nbsp;



#### <a name="the-sequence-in-this-section-b"></a>이 섹션 B의 순서


- [B.1 SSMS UI 관점](#section_B_1_SSMS_UI_perspective)
    - SSMS UI를 사용하여 이벤트 세션의 정의를 만듭니다. 단계별 스크린샷이 나와 있습니다.


- [B.2 TRANSACT-SQL 관점](#section_B_2_TSQL_perspective)
    - SSMS 상황에 맞는 메뉴를 사용하여 정의된 이벤트 세션을 동등한 Transact-SQL **CREATE EVENT SESSION** 문으로 리버스 엔지니어링할 수 있습니다. T-SQL은 SSMS 스크린샷 선택 항목에 완벽한 일치를 보여 줍니다.


- [B.3 카탈로그 뷰 SELECT JOIN UNION 관점](#section_B_3_Catalog_view_S_J_UNION)
    - 이벤트 세션에 대한 시스템 카탈로그 뷰에서 T-SQL SELECT 문을 실행합니다. 결과는 **CREATE EVENT SESSION** 문 사양과 일치합니다.


&nbsp;



<a name="section_B_1_SSMS_UI_perspective"></a>

### <a name="b1-ssms-ui-perspective"></a>B.1 SSMS UI 관점


SSMS의 **개체 탐색기**에서 **관리** 확장 이벤트 **를 확장한 다음** > **세션**새 세션 **을 마우스 오른쪽 단추로 클릭하면** > **새 세션**대화 상자를 시작할 수 있습니다.

큰 **새 세션** 대화 상자의 첫 번째 섹션인 **일반**레이블이 지정된 섹션에서 옵션이 **서버 시작 시 이벤트 세션 시작**으로 선택된 것을 확인할 수 있습니다.

![새 세션 > 일반, 서버 시작 시 이벤트 세션 시작](../../relational-databases/extended-events/media/xevents-ssms-ac105-eventname-startup.png)


**이벤트** 섹션에서는 **lock_deadlock** 이벤트가 선택되어 있습니다. 해당 이벤트에 대해 세 가지 **작업** 이 선택되었습니다. 즉, **구성** 단추가 클릭되었으며, 클릭 후 회색으로 표시됩니다.

![새 세션 > 이벤트, 전역 필드(동작)](../../relational-databases/extended-events/media/xevents-ssms-ac110-actions-global.png)


<a name="resource_type_PAGE_cat_view"></a>

계속 **이벤트** > **구성** 섹션에서 [**resource_type** 이 **페이지**](#resource_type_dmv_actual_row)로 설정된 것을 확인할 수 있습니다. 즉, **resource_type** 값이 **페이지**가 아니면 이벤트 데이터가 이벤트 엔진에서 대상으로 전송되지 않습니다.

데이터베이스 이름 및 카운터에 대한 추가 조건자 필터가 표시됩니다.

![새 세션 > 이벤트, 필터 조건자 필드(동작)](../../relational-databases/extended-events/media/xevents-ssms-ac115-predicate-db.png)


**데이터 스토리지** 섹션에서는 **event_file** 이 대상으로 선택되어 있습니다. 또한 **파일 롤오버 사용** 옵션이 선택되었습니다.

![새 세션 &gt; 데이터 스토리지, eventfile_enablefileroleover](../../relational-databases/extended-events/media/xevents-ssms-ac120-target-eventfile.png)


마지막으로, **고급** 섹션에서는 **최대 디스패치 대기 시간** 값이 4초까지 감소되었습니다.

![새 세션 > 고급, 최대 디스패치 대기 시간](../../relational-databases/extended-events/media/xevents-ssms-ac125-latency4.png)


이상으로 이벤트 세션 정의에 대한 SSMS UI 관점을 마쳤습니다.


<a name="section_B_2_TSQL_perspective"></a>

### <a name="b2-transact-sql-perspective"></a>B.2 TRANSACT-SQL 관점


이벤트 세션 정의가 생성된 방식에 관계없이 SSMS UI에서 세션을 완벽하게 일치하는 TRANSACT-SQL 스크립트로 리버스 엔지니어링할 수 있습니다. 앞의 새 세션 스크린샷을 검사하고 해당 표시 사양을 다음 생성된 T-SQL **CREATE EVENT SESSION** 스크립트의 절과 비교할 수 있습니다.

이벤트 세션을 리버스 엔지니어링하려면 **개체 탐색기** 에서 사용자 세션 노드를 마우스 오른쪽 단추로 클릭한 다음 **세션 스크립팅** > **CREATE** > **클립보드**를 선택합니다.

다음 T-SQL 스크립트는 SSMS로 리버스 엔지니어링하여 생성되었습니다. 그런 다음 공백만 전략적으로 조작하여 스크립트를 수동으로 수정했습니다.


```sql
CREATE EVENT SESSION [event_session_test3]
    ON SERVER  -- Or, if on Azure SQL Database, ON DATABASE.

    ADD EVENT sqlserver.lock_deadlock
    (
        SET
            collect_database_name = (1)
        ACTION
        (
            package0  .collect_system_time,
            package0  .event_sequence,
            sqlserver .client_hostname
        )
        WHERE
        (
            [database_name]           = N'InMemTest2'
            AND [package0].[counter] <= (16)
            AND [resource_type]       = (6)
        )
    )

    ADD TARGET package0.event_file
    (
        SET
            filename           = N'C:\Junk\event_session_test3_EF.xel',
            max_file_size      = (20),
            max_rollover_files = (2)
    )

    WITH
    (
        MAX_MEMORY            = 4096 KB,
        EVENT_RETENTION_MODE  = ALLOW_SINGLE_EVENT_LOSS,
        MAX_DISPATCH_LATENCY  = 4 SECONDS,
        MAX_EVENT_SIZE        = 0 KB,
        MEMORY_PARTITION_MODE = NONE,
        TRACK_CAUSALITY       = OFF,
        STARTUP_STATE         = ON
    );
```


이상으로 T-SQL 관점을 마쳤습니다.


<a name="section_B_3_Catalog_view_S_J_UNION"></a>

### <a name="b3-catalog-view-select-join-union-perspective"></a>B.3 카탈로그 뷰 SELECT JOIN UNION 관점


염려하지 마세요. 다음 T-SQL SELECT 문은 여러 개의 작은 SELECT를 UNION하기 때문에 긴 것뿐입니다. 작은 SELECT를 모두 개별적으로 실행할 수 있습니다. 작은 SELECT는 다양한 시스템 카탈로그 뷰를 JOIN하는 방법을 보여 줍니다.


```sql
SELECT
        s.name        AS [Session-Name],
        '1_EVENT'     AS [Clause-Type],
        'Event-Name'  AS [Parameter-Name],
        e.name        AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_events   AS e

            ON  e.event_session_id = s.event_session_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name         AS [Session-Name],
        '2_EVENT_SET'  AS [Clause-Type],
        f.name         AS [Parameter-Name],
        f.value        AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_events   AS e

            ON  e.event_session_id = s.event_session_id

        JOIN  sys.server_event_session_fields   As f

            ON  f.event_session_id = s.event_session_id
            AND f.object_id        = e.event_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name              AS [Session-Name],
        '3_EVENT_ACTION'    AS [Clause-Type],

        a.package + '.' + a.name
                            AS [Parameter-Name],

        '(Not_Applicable)'  AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_events   AS e

            ON  e.event_session_id = s.event_session_id

        JOIN  sys.server_event_session_actions  As a

            ON  a.event_session_id = s.event_session_id
            AND a.event_id         = e.event_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name                AS [Session-Name],
        '4_EVENT_PREDICATES'  AS [Clause-Type],
        e.predicate           AS [Parameter-Name],
        '(Not_Applicable)'    AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_events   AS e

            ON  e.event_session_id = s.event_session_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name              AS [Session-Name],
        '5_TARGET'          AS [Clause-Type],
        t.name              AS [Parameter-Name],
        '(Not_Applicable)'  AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_targets  AS t

            ON  t.event_session_id = s.event_session_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name          AS [Session-Name],
        '6_TARGET_SET'  AS [Clause-Type],
        f.name          AS [Parameter-Name],
        f.value         AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_targets  AS t

            ON  t.event_session_id = s.event_session_id

        JOIN  sys.server_event_session_fields   As f

            ON  f.event_session_id = s.event_session_id
            AND f.object_id        = t.target_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name               AS [Session-Name],
        '7_WITH_MAX_MEMORY'  AS [Clause-Type],
        'max_memory'         AS [Parameter-Name],
        s.max_memory         AS [Parameter-Value]
    FROM
              sys.server_event_sessions  AS s
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name                  AS [Session-Name],
        '7_WITH_STARTUP_STATE'  AS [Clause-Type],
        'startup_state'         AS [Parameter-Name],
        s.startup_state         AS [Parameter-Value]
    FROM
              sys.server_event_sessions  AS s
    WHERE
        s.name = 'event_session_test3'

ORDER BY
    [Session-Name],
    [Clause-Type],
    [Parameter-Name]
;
```


#### <a name="output"></a>출력


다음은 앞의 SELECT JOIN UNION을 실행하여 얻은 실제 출력입니다. 출력 매개 변수 이름과 값은 앞의 CREATE EVENT SESSION 문에서 명확하게 표시되는 항목에 매핑됩니다.


```
Session-Name          Clause-Type            Parameter-Name                  Parameter-Value
------------          -----------            --------------                  ---------------
event_session_test3   1_EVENT                Event-Name                      lock_deadlock
event_session_test3   2_EVENT_SET            collect_database_name           1
event_session_test3   3_EVENT_ACTION         sqlserver.client_hostname       (Not_Applicable)
event_session_test3   3_EVENT_ACTION         sqlserver.collect_system_time   (Not_Applicable)
event_session_test3   3_EVENT_ACTION         sqlserver.event_sequence        (Not_Applicable)
event_session_test3   4_EVENT_PREDICATES     ([sqlserver].[equal_i_sql_unicode_string]([database_name],N'InMemTest2') AND [package0].[counter]<=(16))   (Not_Applicable)
event_session_test3   5_TARGET               event_file                      (Not_Applicable)
event_session_test3   6_TARGET_SET           filename                        C:\Junk\event_session_test3_EF.xel
event_session_test3   6_TARGET_SET           max_file_size                   20
event_session_test3   6_TARGET_SET           max_rollover_files              2
event_session_test3   7_WITH_MAX_MEMORY      max_memory                      4096
event_session_test3   7_WITH_STARTUP_STATE   startup_state                   1
```


이상으로 카탈로그 뷰 섹션을 마쳤습니다.



<a name="section_C_DMVs"></a>

## <a name="c-dynamic-management-views-dmvs"></a>C. DMV(동적 관리 뷰)


이제 DMV로 넘어가겠습니다. 이 섹션에서는 각각 유용한 특정 비즈니스 용도로 맞는 여러 개의 TRANSACT-SQL SELECT 문을 제공합니다. 또한 SELECT는 원하는 새 사용을 위해 DMV를 JOIN할 수 있는 방법을 보여 줍니다.


DMV 참조 설명서는 [확장 이벤트 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)에서 확인할 수 있습니다.


이 문서에서 다음 SELECT의 실제 출력 행은 달리 지정되지 않은 경우 SQL Server 2016에서 얻은 것입니다.


이 DMV 섹션 C의 SELECT 목록은 다음과 같습니다.

- [C.1 모든 패키지 목록](#section_C_1_list_packages)
- [C.2 각 개체 유형 개수](#section_C_2_count_object_type)
- [C.3 유형별로 정렬된 사용 가능한 모든 항목 SELECT](#section_C_3_select_all_available_objects)
- [C.4 이벤트에 사용 가능한 데이터 필드](#section_C_4_data_fields)
- [C.5 *sys.dm_xe_map_values* 및 이벤트 필드](#section_C_5_map_values_fields)
- [C.6 대상에 대한 매개 변수](#section_C_6_parameters_targets)
- [C.7 target_data 열을 XML로 캐스팅하는 DMV SELECT](#section_C_7_dmv_select_target_data_column)
- [C.8 디스크 드라이브에서 event_file 데이터를 검색하기 위해 함수에서 SELECT](#section_C_8_select_function_disk)



<a name="section_C_1_list_packages"></a>

### <a name="c1-list-of-all-packages"></a>C.1 모든 패키지 목록


확장 이벤트 영역에서 사용할 수 있는 모든 개체는 시스템에 로드된 패키지에서 제공됩니다. 이 섹션에서는 모든 패키지와 해당 설명을 보여 줍니다.


```sql
SELECT  --C.1
        p.name         AS [Package],
        p.description  AS [Package-Description]
    FROM
        sys.dm_xe_packages  AS p
    ORDER BY
        p.name;
```


#### <a name="output"></a>출력

패키지 목록은 다음과 같습니다.


```
/***  (The unique p.guid values are not shown.)
Package        Package-Description
-------        -------------------
filestream     Extended events for SQL Server FILESTREAM and FileTable
package0       Default package. Contains all standard types, maps, compare operators, actions and targets
qds            Extended events for Query Store
SecAudit       Security Audit Events
sqlclr         Extended events for SQL CLR
sqlos          Extended events for SQL Operating System
SQLSatellite   Extended events for SQL Satellite
sqlserver      Extended events for Microsoft SQL Server
sqlserver      Extended events for Microsoft SQL Server
sqlserver      Extended events for Microsoft SQL Server
sqlsni         Extended events for Microsoft SQL Server
ucs            Extended events for Unified Communications Stack
XtpCompile     Extended events for the XTP Compile
XtpEngine      Extended events for the XTP Engine
XtpRuntime     Extended events for the XTP Runtime
***/
```


*앞의 두문자어 정의:*

- clr = .NET의 공용 언어 런타임
- qds = 쿼리 데이터 저장소
- sni = 서버 네트워크 인터페이스
- ucs = 통합 통신 스택
- xtp = 고성능 트랜잭션 처리


<a name="section_C_2_count_object_type"></a>

### <a name="c2-count-of-every-object-type"></a>C.2 각 개체 유형 개수


이 섹션에서는 이벤트 패키지에 포함된 개체 유형에 대해 설명합니다. *sys.dm\_xe\_objects*에 있는 모든 개체 유형의 전체 목록이 각 유형의 개수와 함께 표시됩니다.


```sql
SELECT  --C.2
        Count(*)  AS [Count-of-Type],
        o.object_type
    FROM
        sys.dm_xe_objects  AS o
    GROUP BY
        o.object_type
    ORDER BY
        1  DESC;
```


#### <a name="output"></a>출력

개체 유형별 개체 개수는 다음과 같습니다. 약 1915개의 개체가 있습니다.


```
/***  Actual output, sum is about 1915:

Count-of-Type   object_type
-------------   -----------
1303            event
351             map
84              message
77              pred_compare
53              action
46              pred_source
28              type
17              target
***/
```


<a name="section_C_3_select_all_available_objects"></a>

### <a name="c3-select-all-available-items-sorted-by-type"></a>C.3 유형별로 정렬된 사용 가능한 모든 항목 SELECT


다음 SELECT는 각 개체에 대해 하나씩, 약 1915개 행을 반환합니다.



```sql
SELECT  --C.3
        o.object_type  AS [Type-of-Item],
        p.name         AS [Package],
        o.name         AS [Item],
        o.description  AS [Item-Description]
    FROM
             sys.dm_xe_objects  AS o
        JOIN sys.dm_xe_packages AS p  ON o.package_guid = p.guid
    WHERE
        o.object_type IN ('action' , 'target' , 'pred_source')
        AND
        (
            (o.capabilities & 1) = 0
            OR
            o.capabilities IS NULL
        )
    ORDER BY
        [Type-of-Item],
        [Package],
        [Item];
```


#### <a name="output"></a>출력

앞의 SELECT에서 반환된 개체의 임의 샘플링은 다음과 같습니다.


```
/***
Type-of-Item   Package        Item                          Item-Description
------------   -------        ----                          ----------------
action         package0       callstack                     Collect the current call stack
action         package0       debug_break                   Break the process in the default debugger
action         sqlos          task_time                     Collect current task execution time
action         sqlserver      sql_text                      Collect SQL text
event          qds            query_store_aprc_regression   Fired when Query Store detects regression in query plan performance
event          SQLSatellite   connection_accept             Occurs when a new connection is accepted. This event serves to log all connection attempts.
event          XtpCompile     cgen                          Occurs at start of C code generation.
map            qds            aprc_state                    Query Store Automatic Plan Regression Correction state
message        package0       histogram_event_required      A value is required for the parameter 'filtering_event_name' when source type is 0.
pred_compare   package0       equal_ansi_string             Equality operator between two ANSI string values
pred_compare   sqlserver      equal_i_sql_ansi_string       Equality operator between two SQL ANSI string values
pred_source    sqlos          task_execution_time           Get current task execution time
pred_source    sqlserver      client_app_name               Get the current client application name
target         package0       etw_classic_sync_target       Event Tracing for Windows (ETW) Synchronous Target
target         package0       event_counter                 Use the event_counter target to count the number of occurrences of each event in the event session.
target         package0       event_file                    Use the event_file target to save the event data to an XEL file, which can be archived and used for later analysis and review. You can merge multiple XEL files to view the combined data from separate event sessions.
target         package0       histogram                     Use the histogram target to aggregate event data based on a specific event data field or action associated with the event. The histogram allows you to analyze distribution of the event data over the period of the event session.
target         package0       pair_matching                 Pairing target
target         package0       ring_buffer                   Asynchronous ring buffer target.
type           package0       xml                           Well formed XML fragment
***/
```



<a name="section_C_4_data_fields"></a>

### <a name="c4-data-fields-available-for-your-event"></a>C.4 이벤트에 사용 가능한 데이터 필드


다음 SELECT는 해당 이벤트 유형과 관련된 모든 데이터 필드를 반환합니다.

- WHERE 절 항목: *column_type = 'data'* 를 확인합니다.
- 또한 *o.name =* 에 대한 WHERE 절 값을 편집해야 합니다.


```sql
SELECT  -- C.4
        p.name         AS [Package],
        c.object_name  AS [Event],
        c.name         AS [Column-for-Predicate-Data],
        c.description  AS [Column-Description]
    FROM
              sys.dm_xe_object_columns  AS c
        JOIN  sys.dm_xe_objects         AS o

            ON  o.name = c.object_name

        JOIN  sys.dm_xe_packages        AS p

            ON  p.guid = o.package_guid
    WHERE
        c.column_type = 'data'
        AND
        o.object_type = 'event'
        AND
        o.name        = '\<EVENT-NAME-HERE!>'  --'lock_deadlock'
    ORDER BY
        [Package],
        [Event],
        [Column-for-Predicate-Data];
```


#### <a name="output"></a>출력

앞의 SELECT, WHERE `o.name = 'lock_deadlock'`에서 반환된 행은 다음과 같습니다.

- 각 행은 *sqlserver.lock_deadlock* 이벤트에 대한 선택적 필터를 나타냅니다.
- *\[열 설명\]* 열은 다음 표시에서 생략되었습니다. 값이 NULL인 경우가 많습니다.


```
/***
Actual output, except for the omitted Description column which is often NULL.
These rows are where object_type = 'lock_deadlock'.

Package     Event           Column-for-Predicate-Data
-------     -----           -------------------------
sqlserver   lock_deadlock   associated_object_id
sqlserver   lock_deadlock   database_id
sqlserver   lock_deadlock   database_name
sqlserver   lock_deadlock   deadlock_id
sqlserver   lock_deadlock   duration
sqlserver   lock_deadlock   lockspace_nest_id
sqlserver   lock_deadlock   lockspace_sub_id
sqlserver   lock_deadlock   lockspace_workspace_id
sqlserver   lock_deadlock   mode
sqlserver   lock_deadlock   object_id
sqlserver   lock_deadlock   owner_type
sqlserver   lock_deadlock   resource_0
sqlserver   lock_deadlock   resource_1
sqlserver   lock_deadlock   resource_2
sqlserver   lock_deadlock   resource_description
sqlserver   lock_deadlock   resource_type
sqlserver   lock_deadlock   transaction_id
***/
```



<a name="section_C_5_map_values_fields"></a>

### <a name="c5-sysdm_xe_map_values-and-event-fields"></a>C.5 *sys.dm_xe_map_values* 및 이벤트 필드


다음 SELECT는 *sys.dm_xe_map_values*라는 까다로운 뷰에 대한 JOIN을 포함합니다.

SELECT의 목적은 이벤트 세션에 대해 선택할 수 있는 다양한 필드를 표시하는 것입니다. 이벤트 필드는 다음 두 가지 방법으로 사용할 수 있습니다.

- 각 이벤트 발생에 대해 대상에 기록할 필드 값을 선택하기 위해
- 대상에 전송할 이벤트 발생 및 대상에서 유지할 이벤트 발생을 필터링하기 위해


```sql
SELECT  --C.5
        dp.name         AS [Package],
        do.name         AS [Object],
        do.object_type  AS [Object-Type],
        'o--c'     AS [O--C],
        dc.name         AS [Column],
        dc.type_name    AS [Column-Type-Name],
        dc.column_type  AS [Column-Type],
        dc.column_value AS [Column-Value],
        'c--m'     AS [C--M],
        dm.map_value    AS [Map-Value],
        dm.map_key      AS [Map-Key]
    FROM
              sys.dm_xe_objects         AS do
        JOIN  sys.dm_xe_object_columns  AS dc

            ON  dc.object_name = do.name

        JOIN  sys.dm_xe_map_values      AS dm

            ON  dm.name = dc.type_name

        JOIN  sys.dm_xe_packages        AS dp

            ON  dp.guid = do.package_guid
    WHERE
        do.object_type = 'event'
        AND
        do.name        = '\<YOUR-EVENT-NAME-HERE!>'  --'lock_deadlock'
    ORDER BY
        [Package],
        [Object],
        [Column],
        [Map-Value];
```


#### <a name="output"></a>출력

<a name="resource_type_dmv_actual_row"></a>

앞의 T-SQL SELECT에서 얻은 출력 중 실제 153개 행의 샘플링은 다음과 같습니다. **resource_type** 행은 이 문서의 [event_session_test3](#resource_type_PAGE_cat_view) 예제에서 사용된 조건자 필터링과 **관련** 이 있습니다.


```
/***  5 sampled rows from the actual 153 rows returned.
    NOTE:  'resource_type' under 'Column'.

Package     Object          Object-Type   O--C   Column          Column-Type-Name     Column-Type   Column-Value   C--M   Map-Value        Map-Key
-------     ------          -----------   ----   ------          ----------------     -----------   ------------   ----   ---------        -------
sqlserver   lock_deadlock   event         o--c   CHANNEL         etw_channel          readonly      2              c--m   Operational      4
sqlserver   lock_deadlock   event         o--c   KEYWORD         keyword_map          readonly      16             c--m   access_methods   1024
sqlserver   lock_deadlock   event         o--c   mode            lock_mode            data          NULL           c--m   IX               8
sqlserver   lock_deadlock   event         o--c   owner_type      lock_owner_type      data          NULL           c--m   Cursor           2
sqlserver   lock_deadlock   event         o--c   resource_type   lock_resource_type   data          NULL           c--m   PAGE             6

Therefore, on your CREATE EVENT SESSION statement, in its ADD EVENT WHERE clause,
you could put:
    WHERE( ... resource_type = 6 ...)  -- Meaning:  6 = PAGE.
***/
```


<a name="section_C_6_parameters_targets"></a>

### <a name="c6-parameters-for-targets"></a>C.6 대상에 대한 매개 변수


다음 SELECT는 대상에 대한 모든 매개 변수를 반환합니다. 각 매개 변수에는 필수 여부를 나타내는 태그가 지정되어 있습니다. 매개 변수에 할당한 값은 대상의 동작에 영향을 줍니다.

- WHERE 절 항목: *object_type = 'customizable'* 을 확인합니다.
- 또한 *o.name =* 에 대한 WHERE 절 값을 편집해야 합니다.


```sql
SELECT  --C.6
        p.name        AS [Package],
        o.name        AS [Target],
        c.name        AS [Parameter],
        c.type_name   AS [Parameter-Type],

        CASE c.capabilities_desc
            WHEN 'mandatory' THEN 'YES_Mandatory'
            ELSE 'Not_mandatory'
        END  AS [IsMandatoryYN],

        c.description AS [Parameter-Description]
    FROM
              sys.dm_xe_objects   AS o
        JOIN  sys.dm_xe_packages  AS p

            ON  o.package_guid = p.guid

        LEFT OUTER JOIN  sys.dm_xe_object_columns  AS c

            ON  o.name        = c.object_name
            AND c.column_type = 'customizable'  -- !
    WHERE
        o.object_type = 'target'
        AND
        o.name     LIKE '%'    -- Or '\<YOUR-TARGET-NAME-HERE!>'.
    ORDER BY
        [Package],
        [Target],
        [IsMandatoryYN]  DESC,
        [Parameter];
```


#### <a name="output"></a>출력

다음 매개 변수 행은 SQL Server 2016에서 앞의 SELECT에서 반환된 매개 변수 하위 집합입니다.


```
/***  Actual output, all rows, where target name = 'event_file'.
Package    Target       Parameter            Parameter-Type       IsMandatoryYN   Parameter-Description
-------    ------       ---------            --------------       -------------   ---------------------
package0   event_file   filename             unicode_string_ptr   YES_Mandatory   Specifies the location and file name of the log
package0   event_file   increment            uint64               Not_mandatory   Size in MB to grow the file
package0   event_file   lazy_create_blob     boolean              Not_mandatory   Create blob upon publishing of first event buffer, not before.
package0   event_file   max_file_size        uint64               Not_mandatory   Maximum file size in MB
package0   event_file   max_rollover_files   uint32               Not_mandatory   Maximum number of files to retain
package0   event_file   metadatafile         unicode_string_ptr   Not_mandatory   Not used
***/
```


<a name="section_C_7_dmv_select_target_data_column"></a>

### <a name="c7-dmv-select-casting-target_data-column-to-xml"></a>C.7 target_data 열을 XML로 캐스팅하는 DMV SELECT


이 DMV SELECT는 활성 이벤트 세션의 대상에서 데이터 행을 반환합니다. 데이터는 XML로 캐스팅되어 SSMS에서 표시하기 쉽도록 반환된 셀을 클릭 가능하게 합니다.

- 이벤트 세션이 중지된 경우 이 SELECT는 0개 행을 반환합니다.
- *s.name =* 에 대한 WHERE 절 값을 편집해야 합니다.


```sql
SELECT  --C.7
        s.name,
        t.target_name,
        CAST(t.target_data AS XML)  AS [XML-Cast]
    FROM
              sys.dm_xe_session_targets  AS t
        JOIN  sys.dm_xe_sessions         AS s

            ON s.address = t.event_session_address
    WHERE
        s.name = '\<Your-Session-Name-Here!>';
```


#### <a name="output-the-only-row-including-its-xml-cell"></a>출력, 유일한 행, 해당 XML 셀 포함

앞의 SELECT에서 얻은 출력인 유일한 행은 다음과 같습니다. *XML-Cast* 열에는 SSMS에서 XML로 인식하는 XML 문자열이 포함되어 있습니다. 따라서 SSMS에서 XML-Cast를 클릭 가능하게 해야 함을 확인합니다.


이 실행의 경우

- *s.name =* 값이 *checkpoint_begin* 이벤트에 대한 이벤트 세션으로 설정되었습니다.
- 대상은 *ring_buffer*였습니다.


```XML
name                              target_name   XML-Cast
----                              -----------   --------
checkpoint_session_ring_buffer2   ring_buffer   <RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="2" eventCount="2" droppedCount="0" memoryUsed="104"><event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T01:28:23.508Z"><data name="database_id"><type name="uint32" package="package0" /><value>5</value></data></event><event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T01:28:26.975Z"><data name="database_id"><type name="uint32" package="package0" /><value>5</value></data></event></RingBufferTarget>
```


#### <a name="output-xml-displayed-pretty-when-cell-is-clicked"></a>출력, 셀을 클릭할 때 멋지게 표시되는 XML


XML-Cast 셀을 클릭하면 다음과 같은 멋진 표시가 나타납니다.


```xml
<RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="2" eventCount="2" droppedCount="0" memoryUsed="104">
  <event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T01:28:23.508Z">
    <data name="database_id">
      <type name="uint32" package="package0" />
      <value>5</value>
    </data>
  </event>
  <event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T01:28:26.975Z">
    <data name="database_id">
      <type name="uint32" package="package0" />
      <value>5</value>
    </data>
  </event>
</RingBufferTarget>
```


<a name="section_C_8_select_function_disk"></a>

### <a name="c8-select-from-a-function-to-retrieve-event_file-data-from-disk-drive"></a>C.8 디스크 드라이브에서 event_file 데이터를 검색하기 위해 함수에서 SELECT


이벤트 세션이 일부 데이터를 수집하고 나중에 중지되었다고 가정합니다. 세션이 event_file 대상을 사용하도록 정의된 경우에도 *sys.fn_xe_target_read_file*함수를 호출하여 데이터를 검색할 수 있습니다.

- 이 SELECT를 실행하기 전에 함수 호출의 매개 변수에 사용자 경로와 파일 이름을 편집해야 합니다.
    - 세션을 다시 시작할 때마다 SQL 시스템이 실제 .XEL 파일 이름에 포함하는 추가 자릿수는 무시하고, 기본 루트 이름과 확장명만 지정합니다.


```sql
SELECT  --C.8
        f.module_guid,
        f.package_guid,
        f.object_name,
        f.file_name,
        f.file_offset,
        CAST(f.event_data AS XML)  AS [Event-Data-As-XML]
    FROM
        sys.fn_xe_file_target_read_file(

            '\<YOUR-PATH-FILE-NAME-ROOT-HERE!>*.xel',
            --'C:\Junk\Checkpoint_Begins_ES*.xel',  -- Example.

            NULL, NULL, NULL
        )  AS f;
```


#### <a name="output-rows-returned-by-select-from-the-function"></a>출력, SELECT FROM 함수에서 반환된 행


앞의 SELECT FROM 함수에서 반환된 행은 다음과 같습니다. 맨 오른쪽 XML 열에는 이벤트 발생과 관련된 데이터가 포함되어 있습니다.


```
module_guid                            package_guid                           object_name        file_name                                                           file_offset   Event-Data-As-XML
-----------                            ------------                           -----------        ---------                                                           -----------   -----------------
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   checkpoint_begin   C:\Junk\Checkpoint_Begins_ES_20160615bb-_0_131125086091700000.xel   5120          <event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T03:30:14.023Z"><data name="database_id"><value>5</value></data><action name="session_id" package="sqlserver"><value>60</value></action><action name="database_id" package="sqlserver"><value>5</value></action></event>
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   checkpoint_end     C:\Junk\Checkpoint_Begins_ES_20160615bb-_0_131125086091700000.xel   5120          <event name="checkpoint_end" package="sqlserver" timestamp="2016-07-09T03:30:14.025Z"><data name="database_id"><value>5</value></data></event>
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   checkpoint_begin   C:\Junk\Checkpoint_Begins_ES_20160615bb-_0_131125086091700000.xel   5632          <event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T03:30:17.704Z"><data name="database_id"><value>5</value></data><action name="session_id" package="sqlserver"><value>60</value></action><action name="database_id" package="sqlserver"><value>5</value></action></event>
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   checkpoint_end     C:\Junk\Checkpoint_Begins_ES_20160615bb-_0_131125086091700000.xel   5632          <event name="checkpoint_end" package="sqlserver" timestamp="2016-07-09T03:30:17.709Z"><data name="database_id"><value>5</value></data></event>
```


#### <a name="output-one-xml-cell"></a>출력, 하나의 XML 셀


앞의 반환된 행 집합에서 첫 번째 XML 셀의 내용은 다음과 같습니다.


```xml
<event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T03:30:14.023Z">
  <data name="database_id">
    <value>5</value>
  </data>
  <action name="session_id" package="sqlserver">
    <value>60</value>
  </action>
  <action name="database_id" package="sqlserver">
    <value>5</value>
  </action>
</event>
```


