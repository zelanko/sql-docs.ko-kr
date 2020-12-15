---
description: sys.database_event_session_fields(Azure SQL Database)
title: sys.database_event_session_fields (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
ms.assetid: 9b5c94d6-612c-4e0f-976d-ac6ba55da3ac
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 729e24203a471cf3bdea3a18ee510cf2cced9987
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97458536"
---
# <a name="sysdatabase_event_session_fields-azure-sql-database"></a>sys.database_event_session_fields(Azure SQL Database)
[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  이벤트 및 대상에 명시적으로 설정된 각 사용자 지정 가능 열에 대해 한 행을 반환합니다.  
  
||  
|-|  
|**적용** 대상: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 이상 버전.|  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|이벤트 세션의 ID입니다. Null을 허용하지 않습니다.|  
|object_id|**int**|이 필드와 관련된 개체의 ID입니다. Null을 허용하지 않습니다.|  
|name|**sysname**|필드의 이름입니다. Null을 허용하지 않습니다.|  
|value|**sql_variant**|필드의 값입니다. Null을 허용하지 않습니다.|  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 VIEW DATABASE STATE 권한이 필요합니다.  
  
## <a name="remarks"></a>설명  
 이 뷰는 다음과 같은 관계 카디널리티를 가집니다.  
  
| From | 대상 | 관계 |
| ---- | -- | ------------ |
|sys.database_event_session_actions sys.database_event_session_actions.event_session_id|sys.database_event_sessions sys.database_event_sessions.event_session_id|다 대 일|  
|sys.database_event_session_actions sys.database_event_session_actions.event_id<br /><br /> sys.database_event_session_actions sys.database_event_session_actions.object_id<br /><br /> sys.database_event_session_actions sys.database_event_session_actions.event_session_id|sys.database_event_session_events sys.database_event_session_events.event_session_id<br /><br /> sys.database_event_session_events sys.database_event_session_events.event_id|다 대 일|  
|sys.database_event_session_actions sys.database_event_session_actions.event_session_id<br /><br /> sys.database_event_session_actions sys.database_event_session_actions.object_id|sys.database_event_session_targets sys.database_event_session_targets.event_session_id<br /><br /> sys.database_event_session_targets sys.database_event_session_targets.target_id|다 대 일|  
  
## <a name="see-also"></a>참고 항목  
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)  
  
  
