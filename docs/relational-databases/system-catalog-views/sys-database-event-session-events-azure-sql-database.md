---
title: sys.database_event_session_events (Azure SQL Database) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.component: system-catalog-views
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
ms.assetid: f4c9eb0a-173c-4c66-8dd8-6f7176b2657f
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: d49ac2e05868cfa4a9fd4a3bb1b9f799d4876687
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39549973"
---
# <a name="sysdatabaseeventsessionevents-azure-sql-database"></a>sys.database_event_session_events(Azure SQL Database)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  이벤트 세션의 각 이벤트에 대해 한 행을 반환합니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 이상 모든 버전.|  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|이벤트 세션의 ID입니다. Null을 허용하지 않습니다.|  
|event_id|**int**|이벤트 ID입니다. 이 ID는 이벤트 세션 개체 내에서 고유합니다. Null을 허용하지 않습니다.|  
|NAME|**sysname**|이벤트의 이름입니다. Null을 허용하지 않습니다.|  
|패키지|**sysname**|이벤트가 포함된 이벤트 패키지의 이름입니다. Null을 허용하지 않습니다.|  
|module|**sysname**|이벤트가 포함된 모듈의 이름입니다. Null을 허용하지 않습니다.|  
|predicate|**nvarchar(3000)**|이벤트에 적용되는 조건자 식입니다. Null을 허용합니다.|  
|predicate_xml|**nvarchar(3000)**|이벤트에 적용되는 XML 조건자 식입니다. Null을 허용합니다.|  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 VIEW DATABASE STATE 권한이 필요합니다.  
  
## <a name="remarks"></a>Remarks  
 이 뷰는 다음과 같은 관계 카디널리티를 가집니다.  
  
||||  
|-|-|-|  
|보낸 사람|수행할 작업|관계|  
|sys.database_event_session_events.event_session_id|sys.database_event_sessions.event_session_id|다 대 일|  
  
## <a name="see-also"></a>관련 항목  
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)  
  
  
