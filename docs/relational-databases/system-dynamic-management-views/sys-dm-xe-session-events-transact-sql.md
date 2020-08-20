---
description: sys.dm_xe_session_events(Transact-SQL)
title: sys. dm_xe_session_events (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_xe_session_events
- sys.dm_xe_session_events_TSQL
- dm_xe_session_events
- dm_xe_session_events_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_session_events dynamic management view
- extended events [SQL Server], views
ms.assetid: 4f027b31-4e03-43a6-849d-1ba9d8d34ae8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: cf341fc33337e0205544ce8fbd56b3ead705f894
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498288"
---
# <a name="sysdm_xe_session_events-transact-sql"></a>sys.dm_xe_session_events(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  세션 이벤트에 대한 정보를 반환합니다. 이벤트는 불연속 실행 지점입니다. 조건자를 이벤트에 적용하여 이벤트가 필요한 정보를 포함하지 않을 경우 발생하지 않도록 할 수 있습니다.  
   
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|이벤트 세션의 메모리 주소입니다. Null을 허용하지 않습니다.|  
|event_name|**nvarchar(256)**|동작이 바인딩된 이벤트의 이름입니다. Null을 허용하지 않습니다.|  
|event_package_guid|**uniqueidentifier**|이벤트가 포함된 패키지의 GUID입니다. Null을 허용하지 않습니다.|  
|event_predicate|**nvarchar (3072)**|이벤트에 적용되는 조건자 트리의 XML 표현입니다. Null을 허용합니다.|  
  
## <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
### <a name="relationship-cardinalities"></a>관계 카디널리티  
  
|보낸 사람|대상|관계|  
|----------|--------|------------------|  
|sys.dm_xe_session_events.event_session_address|sys.dm_xe_sessions.address|다 대 일|  
|dm_xe_session_events. event_package_guid,<br /><br /> dm_xe_session_events. event_name|sys.dm_xe_objects.name,<br /><br /> sys.dm_xe_objects.package_guid|다 대 일|  
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

