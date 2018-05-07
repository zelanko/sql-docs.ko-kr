---
title: sys.dm_xe_object_columns (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_xe_object_columns
- sys.dm_xe_object_columns_TSQL
- dm_xe_object_columns_TSQL
- dm_xe_object_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_object_columns dynamic management view
- extended events [SQL Server], views
ms.assetid: d96a14f3-4284-45ff-b1fe-4858e540a013
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6b751ef75af9fd9ec246410d51cb483297144886
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmxeobjectcolumns-transact-sql"></a>sys.dm_xe_object_columns(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  모든 개체에 대한 스키마 정보를 반환합니다.  
  
> [!NOTE]  
>  이벤트 개체는 읽기 전용 및 읽기/쓰기 데이터 모두에 대해 고정 스키마를 표시합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|name|**nvarchar(60)**|열 이름입니다. 이름은 개체 내에서 고유 합니다. Null을 허용하지 않습니다.|  
|column_id|**int**|열 식별자입니다. column_id는 column_type과 함께 사용할 경우 개체 내에서 고유 합니다. Null을 허용하지 않습니다.|  
|object_name|**nvarchar(60)**|해당 열이 속한 개체의 이름입니다. sys.dm_xe_objects.id와 다 대 일 관계를 갖습니다. Null을 허용하지 않습니다.|  
|object_package_guid|**uniqueidentifier**|개체가 포함된 패키지의 GUID입니다. Null을 허용하지 않습니다.|  
|type_name|**nvarchar(60)**|해당 열의 유형 이름입니다. Null을 허용하지 않습니다.|  
|type_package_guid|**uniqueidentifier**|열 데이터 형식이 포함된 패키지의 GUID입니다. Null을 허용하지 않습니다.|  
|column_type|**nvarchar(60)**|해당 열이 사용되는 방식을 나타냅니다. Null을 허용하지 않습니다. column_type은 다음 중 하나일 수 있습니다.<br /><br /> 읽기 전용. 열이 변경할 수 없는 정적 값을 포함합니다.<br /><br /> 데이터. 열이 개체에 의해 표시되는 런타임 데이터를 포함합니다.<br /><br /> 사용자 지정 가능. 열이 변경 가능한 값을 포함합니다.<br /><br /> 참고:이 값을 변경 개체의 동작을 수정할 수 있습니다.|  
|column_value|**nvarchar(256)**|개체 열과 연관된 정적 값을 표시합니다. Null을 허용합니다.|  
|capabilities|**int**|열의 기능을 설명하는 비트맵입니다. Null을 허용합니다.|  
|capabilities_desc|**nvarchar(256)**|해당 개체 열의 기능에 대한 설명입니다. 이 값은 다음 중 하나일 수 있습니다.<br /><br /> 필수. 부모 개체를 이벤트 세션에 바인딩하는 경우 값을 설정해야 합니다.<br /><br /> NULL|  
|description|**nvarchar(256)**|해당 개체 열에 대한 설명입니다. Null을 허용합니다.|  
  
## <a name="permissions"></a>Permissions  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
### <a name="relationship-cardinalities"></a>관계 카디널리티  
  
|보낸 사람|수행할 작업|관계|  
|----------|--------|------------------|  
|sys.dm_xe_object_columns.object_name, sys.dm_xe_object_columns.object_package_guid|sys.dm_xe_objects.name,<br /><br /> sys.dm_xe_objects.package_guid|다 대 일|  
|sys.dm_xe_object_columns.type_name<br /><br /> sys.dm_xe_object_columns.type_package_guid|sys.dm_xe_objects.name<br /><br /> sys.dm_xe_objects.package_guid|다 대 일|  
  
## <a name="see-also"></a>관련 항목:  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

