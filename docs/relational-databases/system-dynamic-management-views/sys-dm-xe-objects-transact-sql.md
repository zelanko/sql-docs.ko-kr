---
title: sys.dm_xe_objects (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_xe_objects
- sys.dm_xe_objects
- sys.dm_xe_objects_TSQL
- dm_xe_objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_objects dynamic management view
- extended events [SQL Server], views
ms.assetid: 5d944b99-b097-491b-8cbd-b0e42b459ec0
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b34ce63f29a798db910115fae7db2e0c732dafdc
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmxeobjects-transact-sql"></a>sys.dm_xe_objects(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이벤트 패키지에 의해 표시되는 각 개체에 대해 한 행을 반환합니다. 개체는 다음 중 하나일 수 있습니다.  
  
-   이벤트. 이벤트는 실행 경로에서 관심 지점을 나타내며 모든 이벤트는 관심 지점에 대한 정보를 포함합니다.  
  
-   동작. 이벤트가 발생하면 동작이 동기적으로 실행됩니다. 동작을 실행하여 런타임 데이터를 이벤트에 추가할 수 있습니다.  
  
-   대상. 대상은 이벤트가 발생하는 스레드에서는 동기적으로 이벤트를 사용하고 시스템에서 제공하는 스레드에서는 비동기적으로 이벤트를 사용합니다.  
  
-   조건자. 조건자 원본은 비교 작업에 사용하기 위해 이벤트 원본에서 값을 검색합니다. 조건자 비교는 특정 데이터 형식을 비교하여 부울 값을 반환합니다.  
  
-   형식. 형식은 데이터를 해석하는 데 필요한 바이트 컬렉션의 길이와 특징을 캡슐화합니다.  

 |열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|name|**nvarchar(60)**|개체 이름입니다. 이름은 특정 개체 형식의 패키지 내에서 고유 합니다. Null을 허용하지 않습니다.|  
|object_type|**nvarchar(60)**|개체의 유형. object_type은 다음 중 하나입니다.<br /><br /> 이벤트<br /><br /> action<br /><br /> target<br /><br /> pred_source<br /><br /> pred_compare<br /><br /> 유형<br /><br /> Null을 허용하지 않습니다.|  
|package_guid|**uniqueidentifier**|해당 동작을 표시하는 패키지의 GUID입니다. sys.dm_xe_packages.package_id와의 다 대 일 관계를 갖습니다. Null을 허용하지 않습니다.|  
|description|**nvarchar(256)**|동작에 대한 설명입니다. 설명은은 패키지 작성자가 설정 됩니다. Null을 허용하지 않습니다.|  
|capabilities|**int**|개체의 기능을 설명하는 비트맵입니다. Null을 허용합니다.|  
|capabilities_desc|**nvarchar(256)**|개체의 기능을 모두 나열합니다. Null을 허용합니다.<br /><br /> **모든 개체 유형에 적용 되는 기능**<br /><br /> —<br />                                **개인**합니다. 내부용으로 사용할 수 있는 유일한 개체로, CREATE/ALTER EVENT SESSION DDL을 통해 액세스할 수 없습니다. 내부에서 사용되는 소수의 개체 외에도 감사 이벤트 및 대상이 이 범주에 속합니다.<br /><br /> ===============<br /><br /> **이벤트 기능**<br /><br /> —<br />                                **No_block**합니다. 이벤트는 어떤 이유로도 차단할 수 없는 중요한 코드 경로에 있습니다. 이 기능이 있는 이벤트는 NO_EVENT_LOSS를 지정하는 이벤트 세션에 추가될 수 없습니다.<br /><br /> ===============<br /><br /> **모든 개체 유형에 적용 되는 기능**<br /><br /> —<br />                                **Process_whole_buffers**합니다. 대상에서는 이벤트를 하나씩 사용하지 않고 이벤트 버퍼를 한꺼번에 사용합니다.<br /><br /> —<br />                        **Singleton**합니다. 한 프로세스에 하나의 대상 인스턴스만 존재할 수 있습니다. 여러 이벤트 세션에서 동일한 단일 대상을 참조하는 경우에도 실제로 인스턴스는 하나뿐이며 이 인스턴스는 고유한 각 이벤트를 한 번씩만 표시합니다. 이는 대상이 동일한 이벤트를 수집하는 여러 세션에 추가된 경우에 중요합니다.<br /><br /> —<br />                                **Synchronous**: 컨트롤이 호출 코드 줄에 반환되기 전에 이벤트를 생성하는 스레드에서 대상이 실행됩니다.|  
|type_name|**nvarchar(60)**|pred_source 및 pred_compare 개체의 이름입니다. Null을 허용합니다.|  
|type_package_guid|**uniqueidentifier**|해당 개체가 작동하는 유형을 표시하는 패키지의 GUID입니다. Null을 허용합니다.|  
|type_size|**int**|데이터 형식의 크기(바이트)이며 유효한 개체 유형에만 사용됩니다. Null을 허용합니다.|  
  
## <a name="permissions"></a>Permissions  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
### <a name="relationship-cardinalities"></a>관계 카디널리티  
  
|보낸 사람|수행할 작업|관계|  
|----------|--------|------------------|  
|sys.dm_xe_objects.package_guid|sys.dm_xe_packages.guid|다 대 일|  
  
## <a name="see-also"></a>관련 항목:  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

