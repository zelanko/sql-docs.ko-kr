---
title: 등록 된 패키지에 대 한 이벤트 보기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- viewing events
- extended events [SQL Server], viewing events
ms.assetid: 9a90b1a2-aa69-43f6-bdeb-cc5f57a26c6f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1156a7272edc8ad1ecfb8e173f81bc678800c855
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66089626"
---
# <a name="view-the-events-for-registered-packages"></a>등록된 패키지에 대한 이벤트 보기
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 확장 이벤트 세션을 만들기 전에 등록된 패키지에서 사용할 수 있는 이벤트를 확인하는 것이 좋습니다. 자세한 내용은 [SQL Server Extended Events Packages](../relational-databases/extended-events/sql-server-extended-events-packages.md)을 참조하세요.  
  
 이 태스크를 수행하려면 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 에서 쿼리 편집기를 사용하여 다음 절차를 수행해야 합니다.  
  
 이 프로시저의 문이 끝나면 쿼리 편집기의 **결과** 탭에 다음 열이 표시됩니다.  
  
-   name. 패키지 이름.  
  
-   event. 이벤트 이름입니다.  
  
-   keyword. 내부 숫자 매핑 테이블에서 파생된 키워드입니다.  
  
-   channel. 이벤트의 대상입니다.  
  
-   description. 이벤트 설명입니다.  
  
## <a name="to-view-the-events-for-registered-packages-using-query-editor"></a>쿼리 편집기를 사용하여 등록된 패키지에 대한 이벤트를 보려면  
  
-   쿼리 편집기에서 다음 문을 실행합니다.  
  
    ```  
    USE msdb  
    SELECT p.name, c.event, k.keyword, c.channel, c.description FROM  
    (  
    SELECT event_package=o.package_guid, o.description,   
    event=c.object_name, channel=v.map_value  
    FROM sys.dm_xe_objects o  
    LEFT JOIN sys.dm_xe_object_columns c ON o.name=c.object_name  
    INNER JOIN sys.dm_xe_map_values v ON c.type_name=v.name   
    AND c.column_value=cast(v.map_key AS nvarchar)  
    WHERE object_type='event' AND (c.name='CHANNEL' or c.name IS NULL)  
  
    ) c LEFT JOIN   
    (  
    SELECT event_package=c.object_package_guid, event=c.object_name,   
    keyword=v.map_value  
    FROM sys.dm_xe_object_columns c INNER JOIN sys.dm_xe_map_values v   
    ON c.type_name=v.name AND c.column_value=v.map_key   
    AND c.type_package_guid=v.object_package_guid  
    INNER JOIN sys.dm_xe_objects o ON o.name=c.object_name   
    AND o.package_guid=c.object_package_guid  
    WHERE object_type='event' AND c.name='KEYWORD'   
    ) k  
    ON  
    k.event_package=c.event_package AND (k.event=c.event or k.event IS NULL)  
    INNER JOIN sys.dm_xe_packages p ON p.guid=c.event_package  
    ORDER BY keyword desc, channel, event  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [확장 이벤트 패키지 SQL Server](../relational-databases/extended-events/sql-server-extended-events-packages.md)   
 [dm_xe_objects &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql)   
 [sys.dm_xe_packages&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql)  
  
  
