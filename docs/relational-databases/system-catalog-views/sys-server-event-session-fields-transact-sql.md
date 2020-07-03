---
title: sys. server_event_session_fields (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_event_session_fields
- server_event_session_fields_TSQL
- sys.server_event_session_fields
- sys.server_event_session_fields_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_session_fields catalog view
- xe
ms.assetid: 7109f9fb-8a1f-432c-92d1-6f8af3e96af1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 33aaf6a258c81dbf615f439b20031b23c01840fa
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85893739"
---
# <a name="sysserver_event_session_fields-transact-sql"></a>sys.server_event_session_fields(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이벤트 및 대상에 명시적으로 설정된 각 사용자 지정 가능 열에 대해 한 행을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|이벤트 세션의 ID입니다. Null을 허용하지 않습니다.|  
|object_id|**int**|이 필드와 관련된 개체의 ID입니다. Null을 허용하지 않습니다.|  
|name|**sysname**|필드 이름입니다. Null을 허용하지 않습니다.|  
|값|**sql_variant**|필드 값입니다. Null을 허용하지 않습니다.|  
  
## <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="remarks"></a>설명  
 이 뷰는 다음과 같은 관계 카디널리티를 가집니다.  
  
||||  
|-|-|-|  
|시작|대상|관계|  
|sys.server_event_session_actions.event_session_id|server_event_sessions. event_session_id|다 대 일|  
|sys.server_event_session_actions.event_id<br /><br /> sys.server_event_session_actions.object_id<br /><br /> sys.server_event_session_actions.event_session_id|sys.server_event_session_events.event_session_id<br /><br /> sys.server_event_session_events.event_id|다 대 일|  
|sys.server_event_session_actions.event_session_id<br /><br /> sys.server_event_session_actions.object_id|sys.server_event_session_targets.event_session_id<br /><br /> sys.server_event_session_targets.target_id|다 대 일|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;카탈로그 뷰](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;확장 이벤트 카탈로그 뷰](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)  
  
  
