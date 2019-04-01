---
title: 기존 SQL 추적 스크립트를 확장 이벤트 세션으로 변환 | Microsoft 문서
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
helpviewer_keywords:
- SQL Trace, convert script to extended events
- extended events [SQL Server], convert SQL Trace script
ms.assetid: 4c8f29e6-0a37-490f-88b3-33493871b3f9
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c95169a1be08b04be9b7cdb1b90fea243e99cf10
ms.sourcegitcommit: 715683b5fc7a8e28a86be8949a194226b72ac915
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2019
ms.locfileid: "58478198"
---
# <a name="convert-an-existing-sql-trace-script-to-an-extended-events-session"></a>기존 SQL 추적 스크립트를 확장 이벤트 세션으로 변환

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  확장 이벤트 세션으로 변환할 기존 SQL 추적 스크립트가 있는 경우 이 항목의 절차를 따라 해당하는 확장 이벤트 세션을 만들 수 있습니다. trace_xe_action_map 및 trace_xe_event_map 시스템 테이블의 정보를 사용하여 변환을 수행하는 데 필요한 정보를 수집할 수 있습니다.  
  
 단계는 다음과 같습니다.  
  
1.  기존 스크립트를 실행하여 SQL 추적 세션을 만든 다음 추적 ID를 확인합니다.  
  
2.  fn_trace_geteventinfo 함수를 사용하는 쿼리를 실행하여 각 SQL 추적 이벤트 클래스와 관련 열에 해당하는 확장 이벤트의 이벤트 및 동작을 찾습니다.  
  
3.  fn_trace_getfilterinfo 함수를 사용하여 사용할 필터와 해당하는 확장 이벤트 동작을 나열합니다.  
  
4.  해당하는 확장 이벤트의 이벤트, 동작 및 조건자(필터)를 사용하여 확장 이벤트 세션을 수동으로 만듭니다.  
  
## <a name="to-obtain-the-trace-id"></a>추적 ID를 확인하려면  
  
1.  쿼리 편집기에서 SQL 추적 스크립트를 연 다음 실행하여 추적 세션을 만듭니다. 이 절차를 완료하기 위해 추적 세션을 실행하고 있을 필요는 없습니다.  
  
2.  추적 ID를 확인합니다. 이렇게 하려면 다음 쿼리를 사용합니다.  
  
    ```sql
    SELECT * FROM sys.traces;  
    GO  
    ```  
  
    > [!NOTE]  
    >  추적 ID 1은 일반적으로 기본 추적을 나타냅니다.  
  
## <a name="to-determine-the-extended-events-equivalents"></a>확장 이벤트의 해당 항목을 확인하려면  
  
1.  해당하는 확장 이벤트의 이벤트 및 동작을 확인하려면 다음 쿼리를 실행합니다. 여기서 *trace_id* 는 이전 절차에서 확인한 추적 ID 값으로 설정합니다.  
  
    > [!NOTE]  
    >  이 예에서는 기본 추적의 추적 ID(1)가 사용됩니다.  
  
    ```sql
    USE MASTER;  
    GO  
    DECLARE @trace_id int;  
    SET @trace_id = 1;  
    SELECT DISTINCT el.eventid, em.package_name, em.xe_event_name AS 'event'  
       , el.columnid, ec.xe_action_name AS 'action'  
    FROM (sys.fn_trace_geteventinfo(@trace_id) AS el  
       LEFT OUTER JOIN sys.trace_xe_event_map AS em  
          ON el.eventid = em.trace_event_id)  
    LEFT OUTER JOIN sys.trace_xe_action_map AS ec  
       ON el.columnid = ec.trace_column_id  
    WHERE em.xe_event_name IS NOT NULL AND ec.xe_action_name IS NOT NULL;  
    ```  
  
     해당하는 확장 이벤트의 이벤트 ID, 패키지 이름, 이벤트 이름, 열 ID 및 동작 이름이 반환됩니다. 이 출력은 이 항목 뒷부분의 "확장 이벤트 세션을 만들려면" 절차에서 사용합니다.  
  
     필터링된 열이 확장 이벤트의 이벤트에 기본적으로 포함되는 이벤트 데이터 필드에 매핑되는 경우도 있습니다. 따라서 "Extended_Events_action_name" 열은 NULL이 됩니다. 이 경우 다음을 수행하여 필터링된 열에 해당하는 데이터 필드를 확인해야 합니다.  
  
    1.  NULL을 반환하는 동작의 경우 스크립트에서 필터링되는 열을 포함하는 SQL 추적 이벤트 클래스를 확인합니다.  
  
         예를 들어 SP:StmtCompleted 이벤트 클래스를 사용하고 Duration 추적 열 이름(SQL 추적 이벤트 클래스 ID 45 및 SQL 추적 열 ID 13)에 필터를 지정했을 수 있습니다. 이 경우 동작 이름이 쿼리 결과에 NULL로 나타납니다.  
  
    2.  이전 단계에서 확인한 각 SQL 추적 이벤트 클래스에 대해 해당하는 확장 이벤트의 이벤트 이름을 찾습니다. 해당하는 이벤트 이름을 모르면 [SQL 추적 이벤트 클래스에 해당하는 확장 이벤트 항목 확인](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md)항목에 나오는 쿼리를 사용합니다.  
  
    3.  다음 쿼리를 사용하여 이전 단계에서 확인한 이벤트에 사용할 올바른 데이터 필드를 확인합니다. 이 쿼리는 확장 이벤트 데이터 필드를 "event_field" 열에 표시합니다. 쿼리에서 *<event_name>* 을 이전 단계에서 지정한 이벤트의 이름으로 바꿉니다.  
  
        ```sql
        SELECT xp.name package_name, xe.name event_name  
           ,xc.name event_field, xc.description  
        FROM sys.trace_xe_event_map AS em  
        INNER JOIN sys.dm_xe_objects AS xe  
           ON em.xe_event_name = xe.name  
        INNER JOIN sys.dm_xe_packages AS xp  
           ON xe.package_guid = xp.guid AND em.package_name = xp.name  
        INNER JOIN sys.dm_xe_object_columns AS xc  
           ON xe.name = xc.object_name  
        WHERE xe.object_type = 'event' AND xc.column_type <> 'readonly'  
           AND em.xe_event_name = '<event_name>';  
        ```  
  
         예를 들어 SP:StmtCompleted 이벤트 클래스는 확장 이벤트의 sp_statement_completed 이벤트에 매핑됩니다. 쿼리에서 sp_statement_completed를 이벤트 이름으로 지정하면 "event_field" 열에는 기본적으로 이벤트와 함께 포함되는 필드가 표시됩니다. 이러한 필드를 보고 "duration" 필드가 있는지 확인할 수 있습니다. 해당하는 확장 이벤트 세션에 필터를 만들려면 "WHERE duration > 0"과 같은 조건자를 추가합니다. 예를 보려면 이 항목의 "확장 이벤트 세션을 만들려면" 절차를 참조하십시오.  
  
## <a name="to-create-the-extended-events-session"></a>확장 이벤트 세션을 만들려면  
 쿼리 편집기를 사용하여 확장 이벤트 세션을 만들고 출력을 파일 대상에 씁니다. 다음 단계에서는 단일 쿼리를 설명하고 쿼리 작성 방법을 보여 줍니다. 전체 쿼리 예를 보려면 이 항목의 "예" 섹션을 참조하십시오.  
  
1.  다음과 같이 이벤트 세션을 만드는 문을 추가합니다. *session_name*을 확장 이벤트 세션에 사용할 이름으로 바꿉니다.  
  
    ```sql
    IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='session_name')  
       DROP EVENT SESSION [Session_Name] ON SERVER;  
    CREATE EVENT SESSION [Session_Name]  
    ON SERVER;  
    ```  
  
2.  "확장 이벤트의 해당 항목을 확인하려면" 절차에서 출력으로 반환된 확장 이벤트의 이벤트 및 동작을 추가하고 "스크립트에 사용된 필터를 확인하려면" 절차에서 확인한 조건자(필터)를 추가합니다.  
  
     다음 예제에서는 SQL:StmtStarting 및 SP:StmtCompleted 이벤트 클래스와 세션 ID 및 기간에 대한 필터를 포함하는 SQL 추적 스크립트를 사용합니다. "확장 이벤트의 해당 항목을 확인하려면" 절차의 쿼리를 통해 반환되는 결과 집합의 예제 출력은 다음과 같습니다.  
  
    ```  
    Eventid  package_name  event                   columnid  action  
    44       sqlserver     sp_statement_starting   6         nt_username  
    44       sqlserver     sp_statement_starting   9         client_pid  
    44       sqlserver     sp_statement_starting   10        client_app_name  
    44       sqlserver     sp_statement_starting   11        server_principal_name  
    44       sqlserver     sp_statement_starting   12        session_id  
    45       sqlserver     sp_statement_completed  6         nt_username  
    45       sqlserver     sp_statement_completed  9         client_pid  
    45       sqlserver     sp_statement_completed  10        client_app_name  
    45       sqlserver     sp_statement_completed  11        server_principal_name  
    45       sqlserver     sp_statement_completed  12        session_id  
    ```  
  
     이 결과 집합을 확장 이벤트의 해당 항목으로 변환하기 위해 동작 목록과 함께 sqlserver.sp_statement_starting 및 sqlserver.sp_statement_completed 이벤트가 추가됩니다. 조건자 문은 WHERE 절로 포함되어 있습니다.  
  
    ```sql
    ADD EVENT sqlserver.sp_statement_starting  
       (ACTION  
          (  
          sqlserver.nt_username,  
          sqlserver.client_pid,  
          sqlserver.client_app_name,  
          sqlserver.server_principal_name,  
          sqlserver.session_id  
          )  
       WHERE sqlserver.session_id = 59   
       ),  
  
    ADD EVENT sqlserver.sp_statement_completed  
       (ACTION  
          (  
          sqlserver.nt_username,  
          sqlserver.client_pid,  
          sqlserver.client_app_name,  
          sqlserver.server_principal_name,  
          sqlserver.session_id  
          )  
       WHERE sqlserver.session_id = 59 AND duration > 0  
       )  
    ```  
  
3.  다음과 같이 비동기 파일 대상을 추가합니다. 파일 경로는 출력을 저장할 위치로 바꿉니다. 파일 대상을 지정할 때는 로그 파일 및 메타데이터 파일 경로를 포함해야 합니다.  
  
    ```sql
    ADD TARGET package0.asynchronous_file_target(  
       SET filename='c:\temp\ExtendedEventsStoredProcs.xel', metadatafile='c:\temp\ExtendedEventsStoredProcs.xem');  
    ```  
  
## <a name="to-view-the-results"></a>결과를 보려면  
  
1.  sys.fn_xe_file_target_read_file 함수를 사용하여 출력을 볼 수 있습니다. 이렇게 하려면 다음 쿼리를 실행합니다. 파일 경로는 지정한 경로로 바꿉니다.  
  
    ```sql
    SELECT *, CAST(event_data as XML) AS 'event_data_XML'  
    FROM sys.fn_xe_file_target_read_file('c:\temp\ExtendedEventsStoredProcs*.xel', 'c:\temp\ExtendedEventsStoredProcs*.xem', NULL, NULL);  
  
    ```  
  
    > [!NOTE]  
    >  이벤트 데이터를 XML로 캐스팅하는 것은 선택 사항입니다.  
  
     sys.fn_xe_file_target_read_file 함수에 대한 자세한 내용은 [sys.fn_xe_file_target_read_file&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md)을 참조하세요.  
  
    ```sql
    IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='session_name')  
       DROP EVENT SESSION [session_name] ON SERVER;  
    CREATE EVENT SESSION [session_name]  
    ON SERVER  
  
    ADD EVENT sqlserver.sp_statement_starting  
       (ACTION  
       (  
          sqlserver.nt_username,  
          sqlserver.client_pid,  
          sqlserver.client_app_name,  
          sqlserver.server_principal_name,  
          sqlserver.session_id  
       )  
       WHERE sqlserver.session_id = 59   
       ),  
  
    ADD EVENT sqlserver.sp_statement_completed  
       (ACTION  
       (  
          sqlserver.nt_username,  
          sqlserver.client_pid,  
          sqlserver.client_app_name,  
          sqlserver.server_principal_name,  
          sqlserver.session_id  
       )  
       WHERE sqlserver.session_id = 59 AND duration > 0  
       );  
  
    ADD TARGET package0.asynchronous_file_target  
       (SET filename='c:\temp\ExtendedEventsStoredProcs.xel', metadatafile='c:\temp\ExtendedEventsStoredProcs.xem');  
    ```  
  
## <a name="example"></a>예제  
  
```sql
IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='session_name')  
   DROP EVENT SESSION [session_name] ON SERVER;  
CREATE EVENT SESSION [session_name]  
ON SERVER  
  
ADD EVENT sqlserver.sp_statement_starting  
   (ACTION  
   (  
      sqlserver.nt_username,  
      sqlserver.client_pid,  
      sqlserver.client_app_name,  
      sqlserver.server_principal_name,  
      sqlserver.session_id  
   )  
   WHERE sqlserver.session_id = 59   
   ),  
  
ADD EVENT sqlserver.sp_statement_completed  
   (ACTION  
   (  
      sqlserver.nt_username,  
      sqlserver.client_pid,  
      sqlserver.client_app_name,  
      sqlserver.server_principal_name,  
      sqlserver.session_id  
   )  
   WHERE sqlserver.session_id = 59 AND duration > 0  
   )  
  
ADD TARGET package0.asynchronous_file_target  
   (SET filename='c:\temp\ExtendedEventsStoredProcs.xel', metadatafile='c:\temp\ExtendedEventsStoredProcs.xem');  
```  
  
## <a name="see-also"></a>참고 항목  
 [SQL 추적 이벤트 클래스에 해당하는 확장 이벤트 항목 확인](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md)  
  
  
