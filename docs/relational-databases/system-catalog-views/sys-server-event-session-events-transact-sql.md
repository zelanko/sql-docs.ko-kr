---
description: sys.server_event_session_events(Transact-SQL)
title: sys. server_event_session_events (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_event_session_events
- server_event_session_events_TSQL
- sys.server_event_session_events
- sys.server_event_session_events_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_session_events catalog view
- xe
ms.assetid: 75986e91-1fc7-4f14-98ac-4e90154a74db
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d7f58a80a3d3d85fd7411d629d9d018a40002641
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551428"
---
# <a name="sysserver_event_session_events-transact-sql"></a>sys.server_event_session_events(Transact-SQL)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  이벤트 세션의 각 이벤트에 대한 행을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|이벤트 세션의 ID입니다. Null을 허용하지 않습니다.|  
|event_id|**int**|이벤트 ID입니다. 이 ID는 이벤트 세션 개체 내에서 고유합니다. Null을 허용하지 않습니다.|  
|name|**sysname**|이벤트의 이름입니다. Null을 허용하지 않습니다.|  
|패키지|**sysname**|이벤트가 포함된 이벤트 패키지의 이름입니다. Null을 허용하지 않습니다.|  
|모듈(module)|**sysname**|이벤트가 포함된 모듈의 이름입니다. Null을 허용하지 않습니다.|  
|predicate|**nvarchar (3000)**|이벤트에 적용되는 조건자 식입니다. Null을 허용합니다.|  
|predicate_xml|**nvarchar (3000)**|이벤트에 적용되는 XML 조건자 식입니다. Null을 허용합니다.|  
  
## <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="remarks"></a>설명  
 이 뷰는 다음과 같은 관계 카디널리티를 가집니다.  
  
| 시작 | 대상 | 관계 |
| ---- | -- | ------------ |
|sys.server_event_session_events.event_session_id|server_event_sessions. event_session_id|다 대 일|  
  
## <a name="see-also"></a>참고 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;확장 이벤트 카탈로그 뷰 ](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)  
  
  
