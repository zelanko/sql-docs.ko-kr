---
title: sys.dm_xe_database_sessions (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
ms.assetid: 33ea5179-16bb-4abd-96cc-9bc696e80987
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 732d0bc450c23413fb31c7336e93dbf3dc785bec
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51662782"
---
# <a name="sysdmxedatabasesessions-azure-sql-database"></a>sys.dm_xe_database_sessions(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  세션 이벤트에 대한 정보를 반환합니다. 이벤트는 불연속 실행 지점입니다. 조건자를 이벤트에 적용하여 이벤트가 필요한 정보를 포함하지 않을 경우 발생하지 않도록 할 수 있습니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 이상 모든 버전.|  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|이벤트 세션의 메모리 주소입니다. Null을 허용하지 않습니다.|  
|event_name|**nvarchar(60)**|동작이 바인딩된 이벤트의 이름입니다. Null을 허용하지 않습니다.|  
|event_package_guid|**uniqueidentifier**|이벤트가 포함된 패키지의 GUID입니다. Null을 허용하지 않습니다.|  
|event_predicate|**nvarchar(2048)**|이벤트에 적용되는 조건자 트리의 XML 표현입니다. Null을 허용합니다.|  
  
## <a name="permissions"></a>사용 권한  
 VIEW DATABASE STATE 권한이 필요합니다.  
  
### <a name="relationship-cardinalities"></a>관계 카디널리티  
2015-07-13 일부 터 'sys.dm_xe_objects' 이름에 ' _database 포함 하지 않는 이러한 Xevent Dmv 중 하나입니다. 오타 또는 다음 테이블의 오른쪽 열에는 오류가 아닙니다. 이름은 Microsoft SQL Server 및 Azure SQL Database에서 동일 합니다. GeneMi 합니다.  
  
|보낸 사람|수행할 작업|관계|  
|--------|------|----------------|  
|sys.dm_xe_database_session_events.event_session_address|sys.dm_xe_database_sessions.address|다 대 일|  
|sys.dm_xe_database_session_events.event_package_guid, sys.dm_xe_database_session_events.event_name|sys.dm_xe_objects.name, sys.dm_xe_objects.package_guid|다 대 일|  
  
## <a name="see-also"></a>관련 항목  
[Azure SQL Database의 확장된 이벤트](https://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)  
[확장 이벤트](../../relational-databases/extended-events/extended-events.md)  
  
 
