---
title: sys.dm_xe_packages (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_xe_packages_TSQL
- sys.dm_xe_packages_TSQL
- dm_xe_packages
- sys.dm_xe_packages
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_packages dynamic management view
- extended events [SQL Server], views
ms.assetid: 2e5ecbe9-3ea8-45e6-a161-e31671a03e1d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cab25279fe7842d21b3657d34edef8234ae058cf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47738864"
---
# <a name="sysdmxepackages-transact-sql"></a>sys.dm_xe_packages(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  확장 이벤트 엔진에 등록된 패키지를 모두 나열합니다.  
  
 
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|NAME|**nvarchar(60)**|패키지의 이름입니다. 설명은 패키지 자체에서 표시됩니다. Null을 허용하지 않습니다.|  
|guid|**uniqueidentifier**|패키지를 식별하는 GUID입니다. Null을 허용하지 않습니다.|  
|description|**nvarchar(256)**|패키지 설명입니다. descriptionis는 패키지 작성자가 설정한 이며 null을 허용 하지 않습니다.|  
|capabilities|**int**|해당 패키지의 기능을 설명하는 비트맵입니다. Null을 허용합니다.|  
|capabilities_desc|**nvarchar(256)**|이 패키지에 사용할 수 있는 모든 기능 목록입니다. Null을 허용합니다.|  
|module_guid|**uniqueidentifier**|이 패키지를 표시하는 모듈의 GUID입니다. Null을 허용하지 않습니다.|  
|module_address|**varbinary(8)**|패키지를 포함하는 모듈이 로드된 기준 주소입니다. 한 개의 모듈이 여러 개의 패키지를 표시할 수 있습니다. Null을 허용하지 않습니다.|  
  
## <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="remarks"></a>Remarks  
 확장 이벤트 엔진에 등록된 패키지는 이벤트, 이벤트 발생 시 취할 수 있는 동작 및 이벤트 데이터의 동기/비동기 처리 대상을 표시합니다.  
  
 이 패키지는 프로세스 주소 공간에 동적으로 로드될 수 있습니다. 패키지는 로드될 때 해당 패키지가 표시하는 모든 개체를 확장 이벤트 엔진에 등록합니다.  
  
## <a name="relationship-cardinalities"></a>관계 카디널리티  
  
||||  
|-|-|-|  
|보낸 사람|수행할 작업|관계|  
|sys.dm_xe_packages.module_address|sys.dm_os_loaded_modules.base_address|다 대 일|  
  
## <a name="see-also"></a>참고자료  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

