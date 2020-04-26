---
title: 잠금을 보유한 쿼리 파악 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], extended events
- queries [SQL Server], holding locks
- xe
- extended events [SQL Server], locks
- extended events [SQL Server], holding locks
ms.assetid: bdfce092-3cf1-4b5e-99d5-fd8c6f9ad560
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cf37fbc1b5402e825d38b5f19326484d7b1afd12
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62519360"
---
# <a name="determine-which-queries-are-holding-locks"></a>잠금을 보유한 쿼리 파악
  데이터베이스 관리자는 종종 데이터베이스 성능을 저하시키는 잠금의 원인을 파악해야 합니다.  
  
 예를 들어 서버의 성능 문제가 차단으로 인한 것이라고 의심될 경우 sys.dm_exec_requests를 쿼리하면 대기 중인 리소스가 잠겨 있음을 나타내는 대기 유형을 사용하는 일시 중단 모드의 세션을 여러 개 찾을 수 있습니다.  
  
 sys.dm_tran_locks를 쿼리하면 보류 중인 잠금이 여러 개 있다는 결과가 나타나지만 잠금을 부여한 세션에는 sys.dm_exec_requests에 표시된 활성 요청이 없습니다.  
  
 이 예는 잠금이 수행될 때 어떤 쿼리가 잠금, 쿼리 계획 및 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스택을 가져오는지 확인하는 방법을 보여 줍니다. 이 예에서는 또한 확장 이벤트 세션에서 쌍 대상을 사용하는 방법도 보여 줍니다.  
  
 이 태스크를 수행하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 쿼리 편집기를 사용하여 다음 절차를 수행해야 합니다.  
  
> [!NOTE]  
>  이 예에서는 AdventureWorks 데이터베이스를 사용합니다.  
  
### <a name="to-determine-which-queries-are-holding-locks"></a>잠금을 보유한 쿼리를 파악하려면  
  
1.  쿼리 편집기에서 다음 문을 실행합니다.  
  
    ```  
    -- Perform cleanup.   
    IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='FindBlockers')  
        DROP EVENT SESSION FindBlockers ON SERVER  
    GO  
    -- Use dynamic SQL to create the event session and allow creating a -- predicate on the AdventureWorks database id.  
    --  
    DECLARE @dbid int  
  
    SELECT @dbid = db_id('AdventureWorks')  
  
    IF @dbid IS NULL  
    BEGIN  
        RAISERROR('AdventureWorks is not installed. Install AdventureWorks before proceeding', 17, 1)  
        RETURN  
    END  
  
    DECLARE @sql nvarchar(1024)  
    SET @sql = '  
    CREATE EVENT SESSION FindBlockers ON SERVER  
    ADD EVENT sqlserver.lock_acquired   
        (action   
            ( sqlserver.sql_text, sqlserver.database_id, sqlserver.tsql_stack,  
             sqlserver.plan_handle, sqlserver.session_id)  
        WHERE ( database_id=' + cast(@dbid as nvarchar) + ' AND resource_0!=0)   
        ),  
    ADD EVENT sqlserver.lock_released   
        (WHERE ( database_id=' + cast(@dbid as nvarchar) + ' AND resource_0!=0 ))  
    ADD TARGET package0.pair_matching   
        ( SET begin_event=''sqlserver.lock_acquired'',   
                begin_matching_columns=''database_id, resource_0, resource_1, resource_2, transaction_id, mode'',   
                end_event=''sqlserver.lock_released'',   
                end_matching_columns=''database_id, resource_0, resource_1, resource_2, transaction_id, mode'',  
        respond_to_memory_pressure=1)  
    WITH (max_dispatch_latency = 1 seconds)'  
  
    EXEC (@sql)  
    --   
    -- Create the metadata for the event session  
    -- Start the event session  
    --  
    ALTER EVENT SESSION FindBlockers ON SERVER  
    STATE = START  
  
    ```  
  
2.  서버에서 작업을 실행한 후 쿼리 편집기에서 다음 문을 실행하여 여전히 잠금을 보유하고 있는 쿼리를 찾습니다.  
  
    ```  
    --  
    -- The pair matching targets report current unpaired events using   
    -- the sys.dm_xe_session_targets dynamic management view (DMV)  
    -- in XML format.  
    -- The following query retrieves the data from the DMV and stores  
    -- key data in a temporary table to speed subsequent access and  
    -- retrieval.  
    --  
    SELECT   
    objlocks.value('(action[@name="session_id"]/value)[1]', 'int')  
            AS session_id,  
        objlocks.value('(data[@name="database_id"]/value)[1]', 'int')   
            AS database_id,  
        objlocks.value('(data[@name="resource_type"]/text)[1]', 'nvarchar(50)' )   
            AS resource_type,  
        objlocks.value('(data[@name="resource_0"]/value)[1]', 'bigint')   
            AS resource_0,  
        objlocks.value('(data[@name="resource_1"]/value)[1]', 'bigint')   
            AS resource_1,  
        objlocks.value('(data[@name="resource_2"]/value)[1]', 'bigint')   
            AS resource_2,  
        objlocks.value('(data[@name="mode"]/text)[1]', 'nvarchar(50)')   
            AS mode,  
        objlocks.value('(action[@name="sql_text"]/value)[1]', 'varchar(MAX)')   
            AS sql_text,  
        CAST(objlocks.value('(action[@name="plan_handle"]/value)[1]', 'varchar(MAX)') AS xml)   
            AS plan_handle,      
        CAST(objlocks.value('(action[@name="tsql_stack"]/value)[1]', 'varchar(MAX)') AS xml)   
            AS tsql_stack  
    INTO #unmatched_locks  
    FROM (  
        SELECT CAST(xest.target_data as xml)   
            lockinfo  
        FROM sys.dm_xe_session_targets xest  
        JOIN sys.dm_xe_sessions xes ON xes.address = xest.event_session_address  
        WHERE xest.target_name = 'pair_matching' AND xes.name = 'FindBlockers'  
    ) heldlocks  
    CROSS APPLY lockinfo.nodes('//event[@name="lock_acquired"]') AS T(objlocks)  
  
    --  
    -- Join the data acquired from the pairing target with other   
    -- DMVs to return provide additional information about blockers  
    --  
    SELECT ul.*  
        FROM #unmatched_locks ul  
        INNER JOIN sys.dm_tran_locks tl ON ul.database_id = tl.resource_database_id AND ul.resource_type = tl.resource_type  
        WHERE resource_0 IS NOT NULL  
        AND session_id IN   
            (SELECT blocking_session_id FROM sys.dm_exec_requests WHERE blocking_session_id != 0)  
        AND tl.request_status='wait'  
        AND REPLACE(ul.mode, 'LCK_M_', '' ) = tl.request_mode  
  
    ```  
  
3.  문제를 식별한 후에는 임시 테이블과 이벤트 세션을 삭제합니다.  
  
    ```  
    DROP TABLE #unmatched_locks  
    DROP EVENT SESSION FindBlockers ON SERVER  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;이벤트 세션 만들기](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-sql&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)   
 [DROP EVENT SESSION &#40;Transact-sql&#41;](/sql/t-sql/statements/drop-event-session-transact-sql)   
 [dm_xe_session_targets &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)   
 [sys.dm_xe_sessions&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql)  
  
  
