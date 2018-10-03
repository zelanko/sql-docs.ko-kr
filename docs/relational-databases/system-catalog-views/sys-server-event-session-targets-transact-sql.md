---
title: sys.server_event_session_targets (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_event_session_targets_TSQL
- sys.server_event_session_targets_TSQL
- sys.server_event_session_targets
- server_event_session_targets
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_session_targets catalog view
- xe
ms.assetid: dda4879d-57ae-4267-b410-1ef5c37404c7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d14c76210dcd74c2ebee59df8961624389a0ac61
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47823951"
---
# <a name="sysservereventsessiontargets-transact-sql"></a>sys.server_event_session_targets(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이벤트 세션의 각 이벤트 대상에 대해 한 행을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|이벤트 세션의 ID입니다. Null을 허용하지 않습니다.|  
|target_id|**int**|대상의 ID입니다. ID는 이벤트 세션 개체 내에서 고유합니다. Null을 허용하지 않습니다.|  
|NAME|**sysname**|이벤트 대상의 이름입니다. Null을 허용하지 않습니다.|  
|패키지|**sysname**|이벤트 대상이 포함된 이벤트 패키지의 이름입니다. Null을 허용하지 않습니다.|  
|module|**sysname**|이벤트 대상이 포함된 모듈의 이름입니다. Null을 허용하지 않습니다.|  
  
## <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="remarks"></a>Remarks  
 이 뷰는 다음과 같은 관계 카디널리티를 가집니다.  
  
||||  
|-|-|-|  
|보낸 사람|수행할 작업|관계|  
|sys.server_event_session_targets.event_session_id|sys.server_event_sessions.event_session_id|다 대 일|  
  
## <a name="see-also"></a>관련 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [확장 이벤트 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)  
  
  
