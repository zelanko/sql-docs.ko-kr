---
title: SQL Server에서 확장 이벤트에 대한 대상 | Microsoft 문서
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
ms.assetid: 47c64144-4432-4778-93b5-00496749665b
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||=azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 6f5eeb47852da17222c8c749bf7c83c1435ccf5c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47680261"
---
# <a name="targets-for-extended-events-in-sql-server"></a>SQL Server에서 확장 이벤트에 대한 대상
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


이 문서에서는 SQL Server에서 확장 이벤트에 대한 패키지0 대상을 사용하는 시기와 방법에 대해 설명합니다. 각 대상에 대해 현재 문서에서 설명하는 항목은 다음과 같습니다.

- 이벤트에서 보내는 데이터를 수집하고 보고할 수 있는 기능
- 매개 변수(쉽게 이해되는 매개 변수는 제외)


#### <a name="xquery-example"></a>XQuery 예제


[ring_buffer 섹션](#h2_target_ring_buffer) 에는 XML 문자열을 관계형 행 집합에 복사할 수 있는 [Transact-SQL의 XQuery](../../xquery/xquery-language-reference-sql-server.md) 를 사용하는 예제가 포함되어 있습니다.


### <a name="prerequisites"></a>사전 요구 사항


- [빠른 시작: SQL Server에서 확장 이벤트](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md)에서 설명한 대로 확장 이벤트의 기본 사항에 대해 일반적으로 잘 알고 있어야 합니다.


- 자주 업데이트되는 유틸리티 SQL Server Management Studio(SSMS.exe)의 최신 버전이 설치되어 있어야 합니다. 자세한 내용은 다음을 참조하세요.
    - [SSMS(SQL Server Management Studio) 다운로드](../../ssms/download-sql-server-management-studio-ssms.md)


- **출력 데이터를 간편하게 볼 수 있도록** SSMS.exe에서 [개체 탐색기](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)를 사용하여 이벤트 세션에서 대상 노드를 마우스 오른쪽 단추로 클릭하는 방법을 알고 있어야 합니다.
    - 이벤트 데이터는 XML 문자열로 캡처됩니다. 하지만 이 문서에서 데이터는 관계형 행으로 표시됩니다. 데이터 확인을 위해 SSMS가 사용되었고 복사되어 이 문서에 붙여 넣었습니다.
    - XML에서 행 집합을 생성하는 데 필요한 다른 T-SQL 기술에 대해서는 [ring_buffer 섹션](#h2_target_ring_buffer)에서 설명합니다. XQuery도 포함됩니다.



## <a name="parameters-actions-and-fields"></a>매개 변수, 작업 및 필드


Transact-SQL에서 [CREATE EVENT SESSION](~/t-sql/statements/create-event-session-transact-sql.md) 문은 확장 이벤트의 핵심입니다. 문을 작성하려면 다음 목록과 설명이 필요합니다.

- 선택한 이벤트와 연결된 필드.
- 선택한 대상과 연결된 매개 변수.

시스템 뷰에서 이러한 목록을 반환하는 SELECT 문은 다음 문서의 C 섹션에서 복사하여 사용할 수 있습니다.

- [SQL Server 확장 이벤트에 대한 시스템 뷰의 SELECT 및 JOIN](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md)
    - [C.4](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_4_data_fields) SELECT 이벤트에 대한 필드.
    - [C.6](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_6_parameters_targets) SELECT 대상에 대한 매개 변수.
    - [C.3](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_3_select_all_available_objects) SELECT 작업.


실제 CREATE EVENT SESSION 문의 컨텍스트에서 사용되는 매개 변수, 필드 및 작업은 [이 링크](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_B_2_TSQL_perspective)에서 볼 수 있습니다.



<a name="h2_target_etw_classic_sync_target"></a>

## <a name="etwclassicsynctarget-target"></a>etw_classic_sync_target 대상


SQL Server 확장 이벤트는 ETW(Windows용 이벤트 추적)와 함께 작동하여 시스템 작업을 모니터링할 수 있습니다. 참조 항목:

- [Windows용 이벤트 추적 대상](../../relational-databases/extended-events/event-tracing-for-windows-target.md)
- [확장 이벤트를 사용하여 시스템 작업 모니터링](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)


이 ETW 대상은 수신되는 데이터를 *동기적으로* 처리하는 반면 대부분 대상은 *비동기적으로*처리합니다.

> [!NOTE]
> Azure SQL Database는 `etw_classic_sync_target target`을 지원하지 않습니다.

<!-- After OPS Versioning is live, the above !NOTE could be converted into a "3colon ZONE".  GeneMi = MightyPen. -->

<a name="h2_target_event_counter"></a>

## <a name="eventcounter-target"></a>event_counter 대상


event_counter 대상은 단순히 지정된 각 이벤트 발생 횟수를 계산합니다.


대부분의 다른 대상과 달리,

- event_counter에 매개 변수가 없습니다.


- 대부분의 대상과 달리 event_counter 대상은 수신되는 데이터를 *동기적으로* 처리합니다.
    - event_counter는 처리와 거의 연관되지 않기 때문에 단순 event_counter에 대해 동기 처리가 허용됩니다.
    - 데이터베이스 엔진은 속도가 너무 느리고 그로 인해 데이터베이스 엔진의 성능을 저하시키는 대상으로부터 연결이 끊어집니다. 이러한 이유로 대부분의 대상은 *비동기적으로*처리합니다.


#### <a name="example-output-captured-by-eventcounter"></a>event_counter에서 캡처된 출력 예제


```
package_name   event_name         count
------------   ----------         -----
sqlserver      checkpoint_begin   4
```


다음은 이전 결과를 발생시킨 CREATE EVENT SESSION입니다. EVENT...WHERE 절에서는 이 테스트에서 카운트가 4로 올라간 후 계산을 멈추기 위해 **package0.counter** 필드가 사용되었습니다.


```sql
CREATE EVENT SESSION [event_counter_1]
    ON SERVER 
    ADD EVENT sqlserver.checkpoint_begin   -- Test by issuing CHECKPOINT; statements.
    (
        WHERE ([package0].[counter] <= (4))   -- A predicate filter.
    )
    ADD TARGET package0.event_counter
    WITH
    (
        MAX_MEMORY = 4096 KB,
        MAX_DISPATCH_LATENCY = 3 SECONDS
    );
```



<a name="h2_target_event_file"></a>

## <a name="eventfile-target"></a>event_file 대상


**event_file** 대상은 버퍼에서 디스크 파일로 이벤트 세션 출력을 작성합니다.


- *filename=* 매개 변수는 ADD TARGET 절에 지정합니다.
    - **.xel** 은 파일의 확장명이어야 합니다.


- 선택한 파일 이름은 시스템에서 date-time 기반 긴 정수가 추가되는 접두사로 사용되며, 이어서 .xel 확장이 나타납니다.

::: moniker range="= azuresqldb-current || = azuresqldb-mi-current || = sqlallproducts-allversions"

> [!NOTE]
> Azure SQL Database는 Azure Blob Storage에 `xel` 파일 저장만 지원합니다. 
>
> SQL Database(및 SQL Database Managed Instance)에 대한 **event_file** 코드 예제의 경우 [SQL Database의 확장된 이벤트에 대한 이벤트 파일 대상 코드](https://docs.microsoft.com/azure/sql-database/sql-database-xevent-code-event-file)를 참조하세요.

::: moniker-end


#### <a name="create-event-session-with-eventfile-target"></a>**event_file** 대상을 사용하는 CREATE EVENT SESSION


다음은 테스트에 사용된 CREATE EVENT SESSION입니다. ADD TARGET 절 중 하나는 event_file를 지정합니다.


```sql
CREATE EVENT SESSION [locks_acq_rel_eventfile_22]
    ON SERVER 
    ADD EVENT sqlserver.lock_acquired
    (
        SET
            collect_database_name=(1),
            collect_resource_description=(1)

        ACTION (sqlserver.sql_text,sqlserver.transaction_id)

        WHERE
        (
            [database_name]=N'InMemTest2'
            AND
            [object_id]=(370100359)
        )
    ),
    ADD EVENT sqlserver.lock_released
    (
        SET
            collect_database_name=(1),
            collect_resource_description=(1)

        ACTION(sqlserver.sql_text,sqlserver.transaction_id)

        WHERE
        (
            [database_name]=N'InMemTest2'
            AND
            [object_id]=(370100359)
        )
    )
    ADD TARGET package0.event_counter,
    ADD TARGET package0.event_file
    (
        SET     filename=N'C:\Junk\locks_acq_rel_eventfile_22-.xel'
    )
    WITH
    (
        MAX_MEMORY=4096 KB,
        MAX_DISPATCH_LATENCY=10 SECONDS
    );
```


#### <a name="sysfnxefiletargetreadfile-function"></a>sys.fn_xe_file_target_read_file 함수


event_file 대상은 수신되는 데이터를 사람이 읽을 수 없는 이진 형식으로 저장합니다. Transact-SQL에서는 [**sys.fn_xe_file_target_read_file**](../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md) 기능에서 선택하여 .xel 파일의 내용을 보고할 수 있습니다.


SQL Server **2016** 이상의 경우 다음 T-SQL SELECT에서 데이터를 보고합니다. *.xel 접미사는 다음과 같습니다. 


```
SELECT f.*
        --,CAST(f.event_data AS XML)  AS [Event-Data-Cast-To-XML]  -- Optional
    FROM
        sys.fn_xe_file_target_read_file(
            'C:\junk\locks_acq_rel_eventfile_22-*.xel',
            null, null, null)  AS f;
```


SQL Server **2014**이상의 경우 다음과 유사한 SELECT에서 데이터를 보고합니다. SQL Server 2014 이후부터 .xem 파일이 더 이상 사용되지 않습니다.


```
SELECT f.*
        --,CAST(f.event_data AS XML)  AS [Event-Data-Cast-To-XML]  -- Optional
    FROM
        sys.fn_xe_file_target_read_file(
            'C:\junk\locks_acq_rel_eventfile_22-*.xel',
            'C:\junk\metafile.xem',
            null, null)  AS f;
```


물론 .xel 데이터를 보려면 SSMS UI를 수동으로 사용할 수도 있습니다.


#### <a name="data-stored-in-the-eventfile-target"></a>event_file 대상에 저장된 데이터


다음은 SQL Server 2016의 **sys.fn_xe_file_target_read_file**에서 선택한 보고서입니다.


```
module_guid                            package_guid                           object_name     event_data                                                                                                                                                                                                                                                                                          file_name                                                      file_offset
-----------                            ------------                           -----------     ----------                                                                                                                                                                                                                                                                                          ---------                                                      -----------
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   lock_acquired   <event name="lock_acquired" package="sqlserver" timestamp="2016-08-07T20:13:35.827Z"><action name="transaction_id" package="sqlserver"><value>39194</value></action><action name="sql_text" package="sqlserver"><value><![CDATA[  select top 1 * from dbo.T_Target;  ]]></value></action></event>   C:\junk\locks_acq_rel_eventfile_22-_0_131150744126230000.xel   11776
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   lock_released   <event name="lock_released" package="sqlserver" timestamp="2016-08-07T20:13:35.832Z"><action name="transaction_id" package="sqlserver"><value>39194</value></action><action name="sql_text" package="sqlserver"><value><![CDATA[  select top 1 * from dbo.T_Target;  ]]></value></action></event>   C:\junk\locks_acq_rel_eventfile_22-_0_131150744126230000.xel   11776
```



<a name="h2_target_histogram"></a>

## <a name="histogram-target"></a>히스토그램 대상


**히스토그램** 대상은 event_counter 대상을 보다 더 세분화됩니다. 히스토그램에서는 다음을 수행할 수 있습니다.

- 여러 항목에 대한 발생을 개별적으로 계산합니다.
- 다양한 유형의 항목 발생을 계산합니다.
    - 이벤트 필드.
    - 동작.


**source_type** 매개 변수는 히스토그램 대상을 조정하는 중요 항목입니다.

- **source_type = 0** - *이벤트 필드*에 대한 데이터 수집을 의미합니다.
- **source_type = 1** - *작업*에 대한 데이터 수집을 의미합니다.
    - 1은 기본값입니다.


'slots' 매개 변수 기본값은 256입니다. 다른 값을 할당하면 값이 2의 거듭 제곱으로 반올림됩니다.

- 예를 들어 slots= 59이면 반올림되어 최대 64가 됩니다.


### <a name="action-example-for-histogram"></a>히스토그램에 대한*작업* 예제


TARGET...SET 절에서 다음 Transact-SQL CREATE EVENT SESSION 문은 **source_type = 1**의 대상 매개 변수 할당을 지정합니다. 1은 히스토그램 대상에서 작업을 추적했음을 의미합니다.

현재 예에서 EVENT...ACTION 절이 제공되면 선택하는 대상( **sqlos.system_thread_id**)에 대한 작업 하나만 제공됩니다. TARGET...SET 절에는 **source=N'sqlos.system_thread_id'** 할당이 표시됩니다.

- 원본 작업을 하나 이상 추적할 수 있도록 CREATE EVENT SESSION 문에 두 번째 히스토그램 대상을 추가할 수 있습니다.


```sql
CREATE EVENT SESSION [histogram_lockacquired]
    ON SERVER 
    ADD EVENT sqlserver.lock_acquired
        (
        ACTION
            (
            sqlos.system_thread_id
            )
        )
    ADD TARGET package0.histogram
        (
        SET
            filtering_event_name=N'sqlserver.lock_acquired',
            slots=(16),
            source=N'sqlos.system_thread_id',
            source_type=1
        )
    WITH
        (
        <.... (For brevity, numerous parameter assignments generated by SSMS.exe are not shown here.) ....>
        );
```


 다음 데이터는 캡처되었습니다. **값** 열 아래의 값은 system_thread_id 값입니다. 예를 들어 총 236 잠금 수는 스레드 6540에서 가져왔습니다.


```
value   count
-----   -----
 6540     236
 9308      91
 9668      74
10144      49
 5244      44
 2396      28
```


#### <a name="select-to-discover-available-actions"></a>사용 가능한 작업을 검색하는 SELECT


[C.3](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_3_select_all_available_objects) SELECT 문에서는 CREATE EVENT SESSION 문에서 지정하는 데 시스템에서 사용할 수 있는 작업을 찾을 수 있습니다. WHERE 절에서 먼저 **o.name LIKE** 필터를 관심 있는 작업과 일치하도록 편집합니다.


다음은 C.3 SELECT에서 반환된 샘플 행 집합입니다. **system_thread_id** 작업은 두 번째 행에 표시됩니다.


```
Package-Name   Action-Name                 Action-Description
------------   -----------                 ------------------
package0       collect_current_thread_id   Collect the current Windows thread ID
sqlos          system_thread_id            Collect current system thread ID
sqlserver      create_dump_all_threads     Create mini dump including all threads
sqlserver      create_dump_single_thread   Create mini dump for the current thread
```


### <a name="event-field-example-for-histogram"></a>히스토그램에 대한 이벤트 *필드* 예제


다음 예제에서는 **source_type = 0**을 설정합니다. **source=** 에 할당된 값은 이벤트 필드(작업 아님)입니다.



```sql
CREATE EVENT SESSION [histogram_checkpoint_dbid]
    ON SERVER 
    ADD EVENT  sqlserver.checkpoint_begin
    ADD TARGET package0.histogram
    (
    SET
        filtering_event_name = N'sqlserver.checkpoint_begin',
        source               = N'database_id',
        source_type          = (0)
    )
    WITH
    ( <....> );
```


다음 데이터는 히스토그램 대상에서 캡처한 것입니다. 데이터는 ID = 5 숙련됨 7 checkpoint_begin 이벤트인 데이터베이스를 보여 줍니다.


```
value   count
-----   -----
5       7
7       4
6       3
```


#### <a name="select-to-discover-available-fields-on-your-chosen-event"></a>선택한 이벤트에 사용 가능한 필드를 검색하는 SELECT


[C.4](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_4_data_fields) SELECT 문은 선택할 수 있는 이벤트 필드를 보여 줍니다. 먼저 **o.name LIKE** 필터를 선택한 이벤트 이름으로 편집합니다.


다음은 C.4 SELECT에서 반환된 행 집합니다. 행 집합에서는 database_id가 히스토그램 대상에 대한 값을 제공할 수 있는 checkpoint_begin 이벤트의 유일한 필드임을 보여 줍니다.


```
Package-Name   Event-Name         Field-Name   Field-Description
------------   ----------         ----------   -----------------
sqlserver      checkpoint_begin   database_id  NULL
sqlserver      checkpoint_end     database_id  NULL
```


<a name="h2_target_pair_matching"></a>

## <a name="pairmatching-target"></a>pair_matching 대상


pair_matching 대상에서는 해당 종료 이벤트없이 발생하는 시작 이벤트를 검색할 수 있습니다. 예를 들어, lock_acquired 이벤트가 발생하지만 이와 일치하는 lock_released 이벤트가 그다음에 적절히 수행되지 않으면 문제일 수 있습니다.


시스템은 자동으로 시작 및 종료 이벤트를 일치시키지 않습니다. 대신 CREATE EVENT SESSION 문에서 시스템 일치에 대해 설명합니다. 시작 및 종료 이벤트가 일치하면 일치 하지 않는 시작 이벤트에 집중할 수 있도록 해당 쌍은 삭제됩니다.


#### <a name="finding-matchable-fields-for-the-start-and-end-event-pair"></a>시작 및 종료 이벤트 쌍에 대해 일치 가능한 필드 찾기


[C.4 SELECT](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_4_data_fields)를 사용하여 lock_acquired 이벤트에 대한 약 16개 필드가 다음 행 집합으로 표시합니다. 여기에 표시되는 행 집합은 예제에서 일치시킨 필드를 보여주도록 수동으로 분리되었습니다. 일부 필드는 두 이벤트의 **기간** 의 경우와 같이 의미없이 일치를 시도했습니다.


```
Package-Name   Event-Name   Field-Name               Field-Description
------------   ----------   ----------               -----------------
sqlserver   lock_acquired   database_name            NULL
sqlserver   lock_acquired   mode                     NULL
sqlserver   lock_acquired   resource_0               The ID of the locked object, when lock_resource_type is OBJECT.
sqlserver   lock_acquired   resource_1               NULL
sqlserver   lock_acquired   resource_2               The ID of the lock partition, when lock_resource_type is OBJECT, and resource_1 is 0.
sqlserver   lock_acquired   transaction_id           NULL

sqlserver   lock_acquired   associated_object_id     The ID of the object that requested the lock that was acquired.
sqlserver   lock_acquired   database_id              NULL
sqlserver   lock_acquired   duration                 The time (in microseconds) between when the lock was requested and when it was canceled.
sqlserver   lock_acquired   lockspace_nest_id        NULL
sqlserver   lock_acquired   lockspace_sub_id         NULL
sqlserver   lock_acquired   lockspace_workspace_id   NULL
sqlserver   lock_acquired   object_id                The ID of the locked object, when lock_resource_type is OBJECT. For other lock resource types it will be 0
sqlserver   lock_acquired   owner_type               NULL
sqlserver   lock_acquired   resource_description     The description of the lock resource. The description depends on the type of lock. This is the same value as the resource_description column in the sys.dm_tran_locks view.
sqlserver   lock_acquired   resource_type            NULL
```


### <a name="example-of-pairmatching"></a>pair_matching 예


다음 CREATE EVENT SESSION 문을 두 이벤트와 두 대상을 지정합니다. pair_matching 대상에서는 이벤트가 일치하는 두 필드 집합을 쌍으로 지정합니다. **begin_matching_columns=** 및 **end_matching_columns=** 에 할당된 쉼표로 구분된 필드 순서는 동일해야 합니다. 쉼표로 구분된 값에서 언급된 필드 사이에는 탭이나 줄 바꿈이 허용되지 않습니다. 공백은 허용됩니다.

결과 범위를 좁히기 위해 먼저 테스트 테이블의 object_id를 찾을 수 있도록 sys.objects에서 선택했습니다. EVENT...WHERE 절에 해당하는 ID 하나에 대한 필터를 추가했습니다.


```sql
CREATE EVENT SESSION [pair_matching_lock_a_r_33]
    ON SERVER 
    ADD EVENT sqlserver.lock_acquired
    (
        SET
            collect_database_name = (1),
            collect_resource_description = (1)

        ACTION (sqlserver.transaction_id)

        WHERE
        (
            [database_name] = 'InMemTest2'
            AND
            [object_id] = 370100359
        )
    ),
    ADD EVENT sqlserver.lock_released
    (
        SET
            collect_database_name = (1),
            collect_resource_description = (1)

        ACTION (sqlserver.transaction_id)

        WHERE
        (
            [database_name] = 'InMemTest2'
            AND
            [object_id] = 370100359
        )
    )
    ADD TARGET package0.event_counter,
    ADD TARGET package0.pair_matching
    (
        SET
            begin_event = N'sqlserver.lock_acquired',
            begin_matching_columns =
                N'resource_0, resource_1, resource_2, transaction_id, database_id',

            end_event = N'sqlserver.lock_released',
            end_matching_columns =
                N'resource_0, resource_1, resource_2, transaction_id, database_id',

            respond_to_memory_pressure = (1)
    )
    WITH
    (
        MAX_MEMORY = 8192 KB,
        MAX_DISPATCH_LATENCY = 15 SECONDS
    );
```


이벤트 세션을 테스트하기 위해 취득한 잠금이 해제되지 않도록 설정했습니다. 다음 T-SQL 단계에서 수행한 작업입니다.

1. BEGIN TRANSACTION.
2. UPDATE MyTable....
3. 대상을 검사할 때까지 일부러 COMMIT TRANSACTION을 실행하지 않습니다.
4. 테스트한 후 나중에 COMMIT TRANSACTION을 실행했습니다.


단순 **event_counter** 대상은 다음 출력 행을 제공합니다. 52-50=2이므로, 출력을 통해 pair-matching 대상에서 출력을 검사할 때 2개의 쌍을 이루지 않는 lock_acquired 이벤트가 있음을 알려 줍니다.


```
package_name   event_name      count
------------   ----------      -----
sqlserver      lock_acquired   52
sqlserver      lock_released   50
```


**pair_matching** 대상은 다음과 같은 출력을 제공합니다. event_counter 출력에서 제안된 것처럼 2개의 lock_acquired 행이 실제로 확인됩니다. 이 행을 통해 2개의 lock_acquired 이벤트가 쌍을 이루고 있지 않음을 알 수 있습니다.


```
package_name   event_name      timestamp                     database_name   duration   mode   object_id   owner_type   resource_0   resource_1   resource_2   resource_description   resource_type   transaction_id
------------   ----------      ---------                     -------------   --------   ----   ---------   ----------   ----------   ----------   ----------   --------------------   -------------   --------------
sqlserver      lock_acquired   2016-08-05 12:45:47.9980000   InMemTest2      0          S      370100359   Transaction  370100359    3            0            [INDEX_OPERATION]      OBJECT          34126
sqlserver      lock_acquired   2016-08-05 12:45:47.9980000   InMemTest2      0          IX     370100359   Transaction  370100359    0            0                                   OBJECT          34126
```


쌍을 이루지 않는 lock_acquired 이벤트에 대한 행에는 잠금이 발생한 T-SQL 텍스트 또는 **sqlserver.sql_text**이 포함될 수 있습니다. 하지만 표시를 블로트하지는 않았습니다.


<a name="h2_target_ring_buffer"></a>

## <a name="ringbuffer-target"></a>ring_buffer 대상


ring_buffer 대상은 빠르고 간단한 이벤트 테스트에 유용합니다. 이벤트 세션을 중지하면 저장된 출력이 삭제됩니다.

이 ring_buffer 섹션에서는 XQuery의 Transact-SQL 구현을 사용하여 ring_buffer의 XML 콘텐츠를 보다 읽기 쉬운 관계형 행 집합에 복사하는 방법도 알 수 있습니다.


#### <a name="create-event-session-with-ringbuffer"></a>ring_buffer를 사용하는 CREATE EVENT SESSION


이 CREATE EVENT SESSION 문에서 특별한 것은 없습니다. ring_buffer 대상이 사용됩니다.


```sql
CREATE EVENT SESSION [ring_buffer_lock_acquired_4]
    ON SERVER 
    ADD EVENT sqlserver.lock_acquired
    (
        SET collect_resource_description=(1)

        ACTION(sqlserver.database_name)

        WHERE
        (
            [object_id]=(370100359)  -- ID of MyTable
            AND
            sqlserver.database_name='InMemTest2'
        )
    )
    ADD TARGET package0.ring_buffer
    (
        SET max_events_limit=(98)
    )
    WITH
    (
        MAX_MEMORY=4096 KB,
        MAX_DISPATCH_LATENCY=3 SECONDS
    );
```


### <a name="xml-output-received-for-lockacquired-by-ringbuffer"></a>ring_buffer에서 lock_acquired에 대해 수신한 XML 출력


SELECT 문에서 검색할 때 콘텐츠는 XML 문자열 형식으로 표시됩니다. 이 테스트의 경우 ring_buffer 대상에서 저장한 XML 문자열은 다음과 같이 나타납니다. 그러나 다음 XML을 간략하게 표현하기 위해 2개의 &#x3c;event&#x3e; 요소를 제외하고는 모두 지웠습니다. 또한 각 &#x3c;event&#x3e;에서 불필요한 &#x3c;data&#x3e; 요소도 삭제되었습니다.


```xml
<RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="6" eventCount="6" droppedCount="0" memoryUsed="1032">
  <event name="lock_acquired" package="sqlserver" timestamp="2016-08-05T23:59:53.987Z">
    <data name="mode">
      <type name="lock_mode" package="sqlserver"></type>
      <value>1</value>
      <text><![CDATA[SCH_S]]></text>
    </data>
    <data name="transaction_id">
      <type name="int64" package="package0"></type>
      <value>111030</value>
    </data>
    <data name="database_id">
      <type name="uint32" package="package0"></type>
      <value>5</value>
    </data>
    <data name="resource_0">
      <type name="uint32" package="package0"></type>
      <value>370100359</value>
    </data>
    <data name="resource_1">
      <type name="uint32" package="package0"></type>
      <value>0</value>
    </data>
    <data name="resource_2">
      <type name="uint32" package="package0"></type>
      <value>0</value>
    </data>
    <data name="database_name">
      <type name="unicode_string" package="package0"></type>
      <value><![CDATA[]]></value>
    </data>
    <action name="database_name" package="sqlserver">
      <type name="unicode_string" package="package0"></type>
      <value><![CDATA[InMemTest2]]></value>
    </action>
  </event>
  <event name="lock_acquired" package="sqlserver" timestamp="2016-08-05T23:59:56.012Z">
    <data name="mode">
      <type name="lock_mode" package="sqlserver"></type>
      <value>1</value>
      <text><![CDATA[SCH_S]]></text>
    </data>
    <data name="transaction_id">
      <type name="int64" package="package0"></type>
      <value>111039</value>
    </data>
    <data name="database_id">
      <type name="uint32" package="package0"></type>
      <value>5</value>
    </data>
    <data name="resource_0">
      <type name="uint32" package="package0"></type>
      <value>370100359</value>
    </data>
    <data name="resource_1">
      <type name="uint32" package="package0"></type>
      <value>0</value>
    </data>
    <data name="resource_2">
      <type name="uint32" package="package0"></type>
      <value>0</value>
    </data>
    <data name="database_name">
      <type name="unicode_string" package="package0"></type>
      <value><![CDATA[]]></value>
    </data>
    <action name="database_name" package="sqlserver">
      <type name="unicode_string" package="package0"></type>
      <value><![CDATA[InMemTest2]]></value>
    </action>
  </event>
</RingBufferTarget>
```


이전 XML을 보려면 이벤트 세션이 활성 상태인 동안 다음 SELECT를 실행할 수 있습니다. 시스템 뷰 **sys.dm_xe_session_targets**에서 현재 XML 데이터가 검색됩니다.


```sql
SELECT
        CAST(LocksAcquired.TargetXml AS XML)  AS RBufXml,
    INTO
        #XmlAsTable
    FROM
        (
        SELECT
                CAST(t.target_data AS XML)  AS TargetXml
            FROM
                     sys.dm_xe_session_targets  AS t
                JOIN sys.dm_xe_sessions         AS s

                    ON s.address = t.event_session_address
            WHERE
                t.target_name = 'ring_buffer'
                AND
                s.name        = 'ring_buffer_lock_acquired_4'
        )
            AS LocksAcquired;


SELECT * FROM #XmlAsTable;
```


### <a name="xquery-to-see-the-xml-as-a-rowset"></a>행 집합으로 XML을 표시하는 XQuery


이전 XML을 관계형 행 집합으로 보려면 다음 T-SQL을 실행하여 위의 SELECT 문에서 계속 진행합니다. 주석 처리된 줄은 각각 XQuery 사용에 대해 설명합니다.


```sql
SELECT
         -- (A)
         ObjectLocks.value('(@timestamp)[1]',
            'datetime'     )  AS [OccurredDtTm]

        -- (B)
        ,ObjectLocks.value('(data[@name="mode"]/text)[1]',
            'nvarchar(32)' )  AS [Mode]

        -- (C)
        ,ObjectLocks.value('(data[@name="transaction_id"]/value)[1]',
            'bigint' )  AS [TxnId]

        -- (D)
        ,ObjectLocks.value('(action[@name="database_name" and @package="sqlserver"]/value)[1]',
            'nvarchar(128)')  AS [DatabaseName]
    FROM
        #TableXmlCell
    CROSS APPLY
        -- (E)
        TargetDateAsXml.nodes('/RingBufferTarget/event[@name="lock_acquired"]')  AS T(ObjectLocks);
```


#### <a name="xquery-notes-from-preceding-select"></a>이전 SELECT의 XQuery 메모


(A)
- 타임스탬프 = 특성 값, &#x3c;event&#x3e; 요소에 있음
- '(...)[1]' 구문을 사용하면 반복 당 값이 하나만 반환됩니다. XML 데이터 형식 변수 및 열에서 .value() XQuery 메서드에 대한 필수 제한입니다.


(B)
- &#x3c;text&#x3e; 요소의 내부 값, "mode"와 동일한 특성이 이름인 &#x3c;data&#x3e; 요소 내에 있음


(C)
- &#x3c;value&#x3e; 요소의 내부 값, "transaction_id"와 동일한 특성이 이름인 &#x3c;data&#x3e; 요소 내에 있음


(D)
- &#x3c;event&#x3e;에 &#x3c;action&#x3e;이 포함되어 있음
- 이름은 "database_name"과 동일한 특성이고, 패키지는 "sqlserver"("package0" 아님)와 동일한 특성인 &#x3c;action&#x3e;, &#x3c;value&#x3e; 요소의 내부 값을 가져옴.


(E)
- C.A. 로 인해 이름이 "lock_acquired"와 동일한 특성인 모든 개별 &#x3c;event&#x3e; 요소에 대해 반복 처리가 실행됩니다.
- 이전 FROM 절에서 반환된 XML에 적용됩니다.


#### <a name="output-from-xquery-select"></a>XQuery SELECT 출력


다음은 XQuery가 포함된 이전 T-SQL에서 생성된 행 집합입니다.


```
OccurredDtTm              Mode    DatabaseName
------------              ----    ------------
2016-08-05 23:59:53.987   SCH_S   InMemTest2
2016-08-05 23:59:56.013   SCH_S   InMemTest2
```



## <a name="xevent-net-namespaces-and-cx23"></a>XEvent.NET 네임스페이스 및 C&#x23;


Package0에는 대상이 2개이지만 Transact-SQL에서 사용할 수 없습니다.

- compressed_history
- event_stream


T-SQL에서 이러한 두 대상을 사용할 수 없다고 알게 되는 방법 중 한 가지는 열 *sys.dm_xe_objects.capabilities* 에서 null이 아닌 값에 비트 0x1이 포함되지 않았다는 것입니다.


event_stream 대상은 C#과 같은 언어로 작성 된.NET 프로그램에서 사용할 수 있습니다. C# 및 다른.NET 개발자들은 .NET Framework 클래스(예: 네임스페이스 Microsoft.SqlServer.XEvents.Linq)를 통해 이벤트 스트림에 액세스할 수 있습니다.

오류가 발생하는 경우 **25726** 은 이벤트 스트림이 클라이언트에서 데이터를 사용하는 것보다 빨리 데이터를 채웠음을 의미합니다. 이로 인해 데이터베이스 엔진은 서버 성능 속도 방지를 위해 이벤트 스트림에서 연결을 끊습니다.


### <a name="xevent-namespaces"></a>XEvent 네임스페이스


- [Microsoft.SqlServer.Management.XEvent 네임스페이스](https://msdn.microsoft.com/library/microsoft.sqlserver.management.xevent.aspx)

- [Microsoft.SqlServer.XEvent.Linq 네임스페이스](https://msdn.microsoft.com/library/microsoft.sqlserver.xevent.linq.aspx)



