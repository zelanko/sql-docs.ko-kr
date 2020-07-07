---
title: database_event_session_actions (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
ms.assetid: 32494df1-7ab7-4b88-a858-6b1021d67433
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a5e0e31418e2399a8d2fcfb35fde2422636d2469
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86003052"
---
# <a name="sysdatabase_event_session_actions-azure-sql-database"></a>sys.database_event_session_actions(Azure SQL Database)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  이벤트 세션의 각 이벤트의 동작에 대해 한 행을 반환합니다.  
  
||  
|-|  
|**적용**대상: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 이상 버전.|  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|이벤트 세션의 ID입니다. Null을 허용하지 않습니다.|  
|event_id|**int**|이벤트 ID입니다. 이 ID는 이벤트 세션 개체 내에서 고유합니다. Null을 허용하지 않습니다.|  
|name|**sysname**|작업 이름입니다. Null을 허용합니다.|  
|패키지|**sysname**|이벤트가 포함된 이벤트 패키지의 이름입니다. Null을 허용합니다.|  
|모듈(module)|**sysname**|이벤트가 포함된 모듈의 이름입니다. Null을 허용합니다.|  
  
## <a name="permissions"></a>권한  
 서버에 대한 VIEW DATABASE STATE 권한이 필요합니다.  
  
## <a name="remarks"></a>설명  
 이 뷰는 다음과 같은 관계 카디널리티를 가집니다.  
  
||||  
|-|-|-|  
|시작|대상|관계|  
|database_event_session_actions. event_session_id|sys.sys. database_event_sessions event_session_id|다 대 일|  
|database_event_session_actions. event_id<br /><br /> database_event_session_actions. event_session_id|database_event_session_events. event_session_id<br /><br /> database_event_session_events. event_id|다 대 일|  
  
  
