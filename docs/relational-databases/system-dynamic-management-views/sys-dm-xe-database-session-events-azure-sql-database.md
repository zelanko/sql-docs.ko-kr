---
description: sys.dm_xe_database_session_events(Azure SQL Database)
title: sys.dm_xe_database_session_events
titleSuffix: Azure SQL Database
ms.date: 06/10/2016
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 9e985a19-f93f-4c56-b644-12c529298011
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-lt-2019
ms.openlocfilehash: 6e8175b720a109c11ebdeeb4843360ff2ade340b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546413"
---
# <a name="sysdm_xe_database_session_events-azure-sql-database"></a>sys.dm_xe_database_session_events(Azure SQL Database)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  세션 이벤트에 대한 정보를 반환합니다. 이벤트는 불연속 실행 지점입니다. 조건자를 이벤트에 적용하여 이벤트가 필요한 정보를 포함하지 않을 경우 발생하지 않도록 할 수 있습니다.  
  
||  
|-|  
|**적용**대상: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 이상 버전.|  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|이벤트 세션의 메모리 주소입니다. Null을 허용하지 않습니다.|  
|event_name|**nvarchar(60)**|동작이 바인딩된 이벤트의 이름입니다. Null을 허용하지 않습니다.|  
|event_package_guid|**uniqueidentifier**|이벤트가 포함된 패키지의 GUID입니다. Null을 허용하지 않습니다.|  
|event_predicate|**nvarchar(2048)**|이벤트에 적용되는 조건자 트리의 XML 표현입니다. Null을 허용합니다.|  
  
## <a name="permissions"></a>사용 권한  
 VIEW DATABASE STATE 권한이 필요합니다.  
  
### <a name="relationship-cardinalities"></a>관계 카디널리티  
  
|시작|대상|관계|  
|----------|--------|------------------|  
|dm_xe_database_session_events. event_session_address|dm_xe_database_sessions. 주소|다 대 일|  
|dm_xe_database_session_events. event_package_guid, dm_xe_database_session_events event_name|sys.dm_xe_objects.name, sys.dm_xe_objects.package_guid|다 대 일|  
  
  
