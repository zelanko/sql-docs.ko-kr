---
description: sys.dm_xe_database_session_object_columns(Azure SQL Database)
title: sys.dm_xe_database_session_object_columns
titleSuffix: Azure SQL Database
ms.date: 06/10/2016
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 0e6adc54-4d97-4ef0-bf4f-b4538d69f136
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-current
ms.custom: seo-dt-2019
ms.openlocfilehash: 92d1bb472d9d8369e116501b31f78dd2c5d3c8ff
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97440708"
---
# <a name="sysdm_xe_database_session_object_columns-azure-sql-database"></a>sys.dm_xe_database_session_object_columns(Azure SQL Database)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  세션에 바인딩된 개체의 구성 값을 표시합니다.  
  
||  
|-|  
|**적용** 대상: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 이상 버전.|  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|이벤트 세션의 메모리 주소입니다. Sys.dm_xe_database_sessions와 다 대 일 관계가 있습니다. Null을 허용하지 않습니다.|  
|column_name|**nvarchar(60)**|구성 값의 이름입니다. Null을 허용하지 않습니다.|  
|column_id|**int**|열의 ID입니다. 개체 내에서 고유합니다. Null을 허용하지 않습니다.|  
|column_value|**nvarchar(2048)**|열의 구성 값입니다. Null을 허용합니다.|  
|object_type|**nvarchar(60)**|개체의 형식입니다.  다음 중 하나가 nullable.object_type 않습니다.<br /><br /> 이벤트<br /><br /> 대상|  
|object_name|**nvarchar(60)**|해당 열이 속한 개체의 이름입니다. Null을 허용하지 않습니다.|  
|object_package_guid|**uniqueidentifier**|개체가 포함된 패키지의 GUID입니다. Null을 허용하지 않습니다.|  
  
## <a name="permissions"></a>사용 권한  
 VIEW DATABASE STATE 권한이 필요합니다.  
  
### <a name="relationship-cardinalities"></a>관계 카디널리티  
  
|From|대상|관계|  
|----------|--------|------------------|  
|dm_xe_database_session_object_columns dm_xe_database_session_object_columns.object_name<br /><br /> dm_xe_database_session_object_columns dm_xe_database_session_object_columns.object_package_guid|sys.dm_xe_objects.package_guid<br /><br /> sys.dm_xe_objects.name|다 대 일|  
|dm_xe_database_session_object_columns dm_xe_database_session_object_columns.column_name<br /><br /> dm_xe_database_session_object_columns dm_xe_database_session_object_columns.column_id|sys.dm_xe_object_columns.name<br /><br /> sys.dm_xe_object_columns.column_id|다 대 일|  
  
## <a name="see-also"></a>참고 항목  
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)  
  
  
