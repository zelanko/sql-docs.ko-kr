---
title: 쿼리 편집기를 사용 하 여 확장된 이벤트 세션 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- create extended events session
- extended events [SQL Server], create session
ms.assetid: cba0e02b-b201-4863-bf1b-9164e68e5fa8
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ef0dfbb1c0e62bbe5301f769ee0f3e4d585b06b6
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52521265"
---
# <a name="create-an-extended-events-session-using-query-editor"></a>쿼리 편집기를 사용하여 확장 이벤트 세션 만들기
  쿼리 편집기를 사용하거나 개체 탐색기에서 확장 이벤트 세션을 만들 수 있습니다. 개체 탐색기에서 확장 이벤트 만들기, 수정 및 이벤트 세션 데이터-이벤트 세션 생성 프로세스를 안내 하는 마법사 및 고급 구성 옵션을 제공 하는 새 세션 UI를 확인 하 여 두 개의 사용자 인터페이스를 제공 합니다. 확장 이벤트 세션을 만들어 SQL Server 추적을 진단하면 다음과 같은 문제를 해결할 수 있습니다.  
  
-   가장 비용이 많이 드는 쿼리 찾기  
  
-   래치 경합의 근본 원인 찾기  
  
-   다른 쿼리를 차단하는 쿼리 찾기  
  
-   쿼리 재컴파일에 의해 발생하는 과도한 CPU 사용 문제 해결  
  
-   교착 상태 해결  
  
 새 세션 마법사를 사용하여 확장 이벤트 세션을 만드는 방법은 [마법사를 사용하여 확장 이벤트 세션 만들기&#40;개체 탐색기&#41;](../ssms/object/object-explorer.md)를 참조하세요. 새 세션 UI를 사용하여 확장 이벤트 세션을 만드는 방법은 [새 세션 대화 상자를 사용하여 확장 이벤트 세션 만들기](../../2014/database-engine/create-an-extended-events-session-using-the-new-session-dialog.md)를 참조하세요.  
  
##  <a name="BeforeYouBegin"></a> Permissions  
 확장 이벤트 세션을 만들려면 ALTER ANY EVENT SESSION 권한이 있어야 합니다.  
  
## <a name="creating-an-extended-events-session-using-query-editor"></a>쿼리 편집기를 사용하여 확장 이벤트 세션 만들기  
  
#### <a name="to-create-an-extended-events-session"></a>확장 이벤트 세션을 만들려면  
  
1.  다음 절차에서는 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 쿼리 편집기를 사용하여 확장 이벤트 세션을 만드는 방법을 보여 줍니다.  
  
     세션에 사용할 이벤트를 결정합니다. 사용 가능한 모든 이벤트와 키워드 및 채널을 함께 보려면 다음 쿼리를 사용합니다.  
  
    > [!NOTE]  
    >  키워드 및 채널에 대한 자세한 내용은 [SQL Server 확장 이벤트 패키지](../relational-databases/extended-events/sql-server-extended-events-packages.md)를 참조하세요.  
  
    ```  
    SELECT p.name, c.event, k.keyword, c.channel, c.description FROM  
       (  
       SELECT event_package = o.package_guid, o.description,   
       event=c.object_name, channel = v.map_value  
       FROM sys.dm_xe_objects o  
       LEFT JOIN sys.dm_xe_object_columns c ON o.name = c.object_name  
       INNER JOIN sys.dm_xe_map_values v ON c.type_name = v.name   
       AND c.column_value = cast(v.map_key AS nvarchar)  
       WHERE object_type = 'event' AND (c.name = 'CHANNEL' or c.name IS NULL)  
       ) c LEFT JOIN   
       (  
       SELECT event_package = c.object_package_guid, event = c.object_name,   
       keyword = v.map_value  
       FROM sys.dm_xe_object_columns c INNER JOIN sys.dm_xe_map_values v   
       ON c.type_name = v.name AND c.column_value = v.map_key   
       AND c.type_package_guid = v.object_package_guid  
       INNER JOIN sys.dm_xe_objects o ON o.name = c.object_name   
       AND o.package_guid = c.object_package_guid  
       WHERE object_type = 'event' AND c.name = 'KEYWORD'   
       ) k  
       ON  
       k.event_package = c.event_package AND (k.event=c.event or k.event IS NULL)  
       INNER JOIN sys.dm_xe_packages p ON p.guid = c.event_package  
    ORDER BY keyword desc, channel, event  
    ```  
  
2.  새 쿼리 창에서 다음 문을 추가하여 이벤트 세션을 만듭니다. *session_name* 은 사용할 세션 이름으로 바꿉니다.  
  
    > [!IMPORTANT]  
    >  이 절차의 2~6단계에서는 이벤트 세션 정의의 각 섹션에 대해 설명합니다. 모든 문은 단일 쿼리 창에 추가한 후에 실행합니다. 전체 예를 보려면 이 항목의 "예" 섹션을 참조하십시오.  
  
    ```  
    CREATE EVENT SESSION session_name   
    ON SERVER  
    ```  
  
3.  모니터링할 이벤트를 *package_name*.*event_name*형식으로 추가합니다. 각 이벤트에 대해 다음과 같은 줄을 추가합니다.  
  
    ```  
    ADD EVENT package_name.event_name  
    ```  
  
     이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
    ```  
    ADD EVENT sqlserver.file_read_completed,  
    ADD EVENT sqlserver.file_write_completed  
    ```  
  
4.  (선택 사항) 이벤트를 추가한 후 필요한 동작을 추가할 수 있습니다. 조건자를 추가할 수도 있습니다. 조건자는 대상에서 이벤트 정보를 사용해야 하는 경우에 대한 조건을 설정하는 데 사용됩니다. 동작은 ACTION 절을 사용하여 추가하고 조건자는 WHERE 절을 사용하여 추가합니다. 예를 들어 파일 ID가 1인 경우 이벤트에 대해 [!INCLUDE[tsql](../includes/tsql-md.md)] 텍스트를 캡처하는 동작 및 조건자를 추가하려면 다음 문을 포함합니다.  
  
    ```  
    ADD EVENT sqlserver.file_read_completed  
       (ACTION (sqlserver.sql_text)  
       WHERE file_id = 1),  
    ```  
  
    -   사용할 수 있는 동작을 보려면 다음 쿼리를 사용합니다.  
  
        ```  
        SELECT p.name AS 'package_name', xo.name AS 'action_name', xo.description, xo.object_type  
        FROM sys.dm_xe_objects AS xo  
        JOIN sys.dm_xe_packages AS p  
           ON xo.package_guid = p.guid  
        WHERE xo.object_type = 'action'  
        AND (xo.capabilities & 1 = 0   
        OR xo.capabilities IS NULL)  
        ORDER BY p.name, xo.name  
        ```  
  
    -   이벤트에 사용할 수 있는 조건자를 보려면 다음 쿼리를 사용합니다. *event_name* 은 조건자를 추가할 이벤트의 이름으로 바꿉니다.  
  
        ```  
        SELECT *  
        FROM sys.dm_xe_object_columns  
        WHERE object_name = 'event_name'  
        AND column_type = 'data'  
        ```  
  
         이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
        ```  
        SELECT *   
        FROM sys.dm_xe_object_columns   
        WHERE object_name = 'file_read_completed'  
        AND column_type = 'data'  
        ```  
  
         전역 조건자 원본을 추가할 수도 있습니다. 모든 조건자 식에 전역 조건자 원본을 사용할 수 있습니다. 사용할 수 있는 전역 조건자 원본을 보려면 다음 쿼리를 사용합니다.  
  
        ```  
        SELECT p.name AS package_name, xo.name AS predicate_name  
           , xo.description, xo.object_type  
        FROM sys.dm_xe_objects AS xo  
        JOIN sys.dm_xe_packages AS p  
           ON xo.package_guid = p.guid  
        WHERE xo.object_type = 'pred_source'  
        ORDER BY p.name, xo.name  
        ```  
  
         예를 들어 다음 조건자 식을 사용하여 이벤트가 발생하는 처음 다섯 번만 이벤트에 대한 데이터를 수집하도록 지정할 수 있습니다.  
  
        ```  
        WHERE package0.counter <= 5  
        ```  
  
5.  이벤트 데이터가 처리되고 사용될 원하는 대상을 추가합니다. 다음 형식을 사용합니다.  
  
    ```  
    ADD TARGET package_name.target_name  
    ```  
  
     다음 예에서는 비동기 파일 대상을 추가합니다.  
  
    ```  
    ADD TARGET package0.asynchronous_file_target  
       (SET filename = 'c:\temp\xelog.xel', metadatafile = 'c:\temp\xelog.xem')  
    ```  
  
     사용 가능한 대상 목록을 보려면 다음 쿼리를 사용합니다.  
  
    ```  
    SELECT p.name AS 'package_name', xo.name AS 'target_name'  
       , xo.description, xo.object_type   
    FROM sys.dm_xe_objects AS xo  
    JOIN sys.dm_xe_packages AS p  
       ON xo.package_guid = p.guid  
    WHERE xo.object_type = 'target'  
    AND (xo.capabilities & 1 = 0  
    OR xo.capabilities IS NULL)  
    ORDER BY p.name, xo.name  
    ```  
  
    > [!NOTE]  
    >  다양한 대상 유형에 대한 자세한 내용은 [SQL Server 확장 이벤트 대상](../../2014/database-engine/sql-server-extended-events-targets.md)을 참조하세요.  
  
6.  추가 구성 옵션을 검토하고 추가합니다. 예를 들어 이벤트 보존 모드, 이벤트가 메모리에 버퍼링되는 시간, 또는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 시작 시 이벤트 세션을 자동으로 시작할지 여부 등의 옵션을 구성할 수 있습니다. 이 옵션은 [ALTER EVENT SESSION&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql) 항목에서 설명합니다. 이러한 옵션을 지정하지 않은 경우 기본값이 할당됩니다.  
  
7.  세션을 시작합니다.  
  
    > [!NOTE]  
    >  세션 결과를 보는 방법은 온라인 설명서의 [SQL Server 확장 이벤트 대상](../../2014/database-engine/sql-server-extended-events-targets.md) 노드에서 사용한 대상 유형에 해당하는 항목을 참조하세요.  
  
 아래 예에서는 다음 정보를 캡처하는 IOActivity라는 확장 이벤트 세션을 만듭니다.  
  
-   완료된 파일 읽기에 대한 이벤트 데이터(파일 ID가 1인 경우 파일 읽기를 위한 관련 [!INCLUDE[tsql](../includes/tsql-md.md)] 텍스트 포함)  
  
-   완료된 파일 쓰기에 대한 이벤트 데이터  
  
-   로그 캐시의 데이터가 물리적 로그 파일에 기록될 때의 이벤트 데이터  
  
 이 세션에서는 출력을 파일 대상으로 보냅니다.  
  
```  
CREATE EVENT SESSION IOActivity  
ON SERVER  
  
ADD EVENT sqlserver.file_read_completed  
   (  
   ACTION (sqlserver.sql_text)  
   WHERE file_id = 1),  
ADD EVENT sqlserver.file_write_completed,  
ADD EVENT sqlserver.databases_log_flush  
  
ADD TARGET package0.asynchronous_file_target   
   (SET filename = 'c:\temp\xelog.xel', metadatafile = 'c:\temp\xelog.xem')  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE EVENT SESSION&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [SQL Server 확장 이벤트 대상](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [SQL Server 확장 이벤트 패키지](../relational-databases/extended-events/sql-server-extended-events-packages.md)  
  
  
