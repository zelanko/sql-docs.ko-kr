---
title: sys.server_event_session_actions (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.server_event_session_actions
- server_event_session_actions_TSQL
- server_event_session_actions
- sys.server_event_session_actions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_session_actions catalog view
- xe
ms.assetid: 1d8c604e-4361-4846-8661-14cfd1c44f63
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7d5593ee2852542af4bee958846172f30a2b0a07
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysservereventsessionactions-transact-sql"></a>sys.server_event_session_actions(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이벤트 세션의 각 이벤트의 동작에 대해 한 행을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|이벤트 세션의 ID입니다. Null을 허용하지 않습니다.|  
|event_id|**int**|이벤트 ID입니다. 이 ID는 이벤트 세션 개체 내에서 고유합니다. Null을 허용하지 않습니다.|  
|name|**sysname**|작업 이름입니다. Null을 허용합니다.|  
|패키지|**sysname**|이벤트가 포함된 이벤트 패키지의 이름입니다. Null을 허용합니다.|  
|module|**sysname**|이벤트가 포함된 모듈의 이름입니다. Null을 허용합니다.|  
  
## <a name="permissions"></a>Permissions  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="remarks"></a>주의  
 이 뷰는 다음과 같은 관계 카디널리티를 가집니다.  
  
||||  
|-|-|-|  
|보낸 사람|수행할 작업|관계|  
|sys.server_event_session_actions.event_session_id|sys.sys.server_event_sessions.event_session_id|다 대 일|  
|sys.server_event_session_actions.event_id<br /><br /> sys.server_event_session_actions.event_session_id|sys.server_event_session_events.event_session_id<br /><br /> sys.server_event_session_events.event_id|다 대 일|  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [확장 이벤트 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)  
  
  
