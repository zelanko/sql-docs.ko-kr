---
title: sys. dm_xe_session_object_columns (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_xe_session_object_columns_TSQL
- sys.dm_xe_session_object_columns_TSQL
- dm_xe_session_object_columns
- sys.dm_xe_session_object_columns
dev_langs:
- TSQL
helpviewer_keywords:
- xe
- sys.dm_xe_session_object_columns dynamic management view
ms.assetid: e97f3307-2da6-4c54-b818-a474faec752e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 56bea991f705a9dfdbcd3189737eb3e2a51a8c63
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85898563"
---
# <a name="sysdm_xe_session_object_columns-transact-sql"></a>sys.dm_xe_session_object_columns(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  세션에 바인딩된 개체의 구성 값을 표시합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|이벤트 세션의 메모리 주소입니다. sys.dm_xe_sessions.address와 다 대 일 관계를 갖습니다. Null을 허용하지 않습니다.|  
|column_name|**nvarchar(256)**|구성 값의 이름입니다. Null을 허용하지 않습니다.|  
|column_id|**int**|열의 ID입니다. 개체 내에서 고유합니다. Null을 허용하지 않습니다.|  
|column_value|**nvarchar (3072)**|열의 구성 값입니다. Null을 허용합니다.|  
|object_type|**nvarchar(60)**|개체의 유형. Null을 허용하지 않습니다. object_type 다음 중 하나입니다.<br /><br /> event<br /><br /> 대상|  
|object_name|**nvarchar(256)**|해당 열이 속한 개체의 이름입니다. Null을 허용하지 않습니다.|  
|object_package_guid|**uniqueidentifier**|개체가 포함된 패키지의 GUID입니다. Null을 허용하지 않습니다.|  
  
## <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
### <a name="relationship-cardinalities"></a>관계 카디널리티  
  
|시작|대상|관계|  
|----------|--------|------------------|  
|dm_xe_session_object_columns. object_name,<br /><br /> dm_xe_session_object_columns.object_package_guid|dm_xe_objects. package_guid,<br /><br /> sys.dm_xe_objects.name|다 대 일|  
|dm_xe_session_object_columns. column_name,<br /><br /> dm_xe_session_object_columns.column_id|sys. dm_xe_object_columns. 이름,<br /><br /> sys.dm_xe_object_columns.column_id|다 대 일|  
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

