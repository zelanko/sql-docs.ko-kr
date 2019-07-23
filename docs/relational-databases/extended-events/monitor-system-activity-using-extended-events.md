---
title: 확장 이벤트를 사용하여 시스템 작업 모니터링 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
helpviewer_keywords:
- xe
- extended events [SQL Server], monitoring system activity
ms.assetid: d83ad88f-818c-49fe-a9a9-299f704fca53
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4ef39b9e8834d83c564e7480e29c927f4aa194fe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140144"
---
# <a name="monitor-system-activity-using-extended-events"></a>확장 이벤트를 사용하여 시스템 작업 모니터링

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  이 절차는 확장 이벤트를 ETW(Windows용 이벤트 추적)와 함께 사용하여 시스템 작업을 모니터링하는 방법을 설명합니다. 또한 CREATE EVENT SESSION, ALTER EVENT SESSION 및 DROP EVENT SESSION 문을 사용하는 방법도 보여 줍니다.  
  
 이 태스크를 수행하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 쿼리 편집기를 사용하여 다음 절차를 수행해야 합니다. 또한 명령 프롬프트를 사용하여 ETW 명령도 실행해야 합니다.  
  
### <a name="to-monitor-system-activity-using-extended-events"></a>확장 이벤트를 사용하여 시스템 작업을 모니터링하려면  
  
1.  쿼리 편집기에서 다음 문을 실행하여 이벤트 세션을 만들고 두 개의 이벤트를 추가합니다. checkpoint_begin 및 checkpoint_end 이벤트는 데이터베이스 검사점이 시작될 때와 끝날 때 실행됩니다.  
  
    ```  
    CREATE EVENT SESSION test0  
    ON SERVER  
    ADD EVENT sqlserver.checkpoint_begin,  
    ADD EVENT sqlserver.checkpoint_end  
    WITH (MAX_DISPATCH_LATENCY = 1 SECONDS)  
    go  
    ```  
  
2.  버킷이 32개인 버킷팅 대상을 추가하여 데이터베이스 ID를 기준으로 검사점 수를 계산합니다.  
  
    ```  
    ALTER EVENT SESSION test0  
    ON SERVER  
    ADD TARGET package0.histogram  
    (  
          SET slots = 32, filtering_event_name = 'sqlserver.checkpoint_end', source_type = 0, source = 'database_id'  
    )  
    go  
    ```  
  
3.  다음 문을 실행하여 ETW 대상을 추가합니다. 그러면 검사점의 소요 시간을 확인하는 데 사용할 수 있는 시작 및 끝 이벤트를 확인할 수 있습니다.  
  
    ```  
    ALTER EVENT SESSION test0  
    ON SERVER  
    ADD TARGET package0.etw_classic_sync_target  
    go  
    ```  
  
4.  다음 문을 실행하여 세션 및 이벤트 수집을 시작합니다.  
  
    ```  
    ALTER EVENT SESSION test0  
    ON SERVER  
    STATE = start  
    go  
    ```  
  
5.  다음 문을 실행하여 세 이벤트를 실행합니다.  
  
    ```  
    USE tempdb  
          checkpoint  
    go  
    USE master  
          checkpoint  
          checkpoint  
    go  
    ```  
  
6.  다음 문을 실행하여 이벤트 수를 확인합니다.  
  
    ```  
    SELECT CAST(xest.target_data AS xml) Bucketizer_Target_Data_in_XML  
    FROM sys.dm_xe_session_targets xest  
    JOIN sys.dm_xe_sessions xes ON xes.address = xest.event_session_address  
    JOIN sys.server_event_sessions ses ON xes.name = ses.name  
    WHERE xest.target_name = 'histogram' AND xes.name = 'test0'  
    go  
    ```  
  
7.  명령 프롬프트에서 다음 명령을 실행하여 ETW 데이터를 확인합니다.  
  
    > [!NOTE]  
    >  **tracerpt** 명령에 대한 도움말을 보려면 명령 프롬프트에서 `tracerpt /?`를 입력하세요.  
  
    ```  
    logman query -ets --- List the ETW sessions. This is optional.  
    logman update XE_DEFAULT_ETW_SESSION -fd -ets --- Flush the ETW log.  
    tracerpt %temp%\xeetw.etl -o xeetw.txt --- Dump the events so they can be seen.  
    ```  
  
8.  다음 문을 실행하여 이벤트 세션을 중지하고 서버에서 제거합니다.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

    ```  
    ALTER EVENT SESSION test0  
    ON SERVER  
    STATE = STOP  
    go  
  
    DROP EVENT SESSION test0  
    ON SERVER  
    go  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE EVENT SESSION&#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)   
 [ALTER EVENT SESSION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)   
 [DROP EVENT SESSION&#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-session-transact-sql.md)   
 [확장 이벤트 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [확장 이벤트 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)   
 [SQL Server 확장 이벤트 대상](https://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384)  
  
  
