---
title: sys. dm_xe_map_values (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_xe_map_values
- dm_xe_map_values
- dm_xe_map_values_TSQL
- sys.dm_xe_map_values_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_map_values dynamic management view
- xe
ms.assetid: c0c5dd7e-9cee-47e2-b65a-88194c00aa1f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 79d26f8ff6a04953f6312ba8749371f6d269b912
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826682"
---
# <a name="sysdm_xe_map_values-transact-sql"></a>sys.dm_xe_map_values(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  내부 숫자 키를 사람이 이해할 수 있는 텍스트 형식으로 매핑하여 반환합니다.  
 
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|name|**nvarchar(256)**|맵 이름입니다. 이름은 로컬 시스템에서 고유 합니다. Null을 허용하지 않습니다.|  
|object_package_guid|**uniqueidentifier**|맵이 포함된 패키지의 GUID입니다. Null을 허용하지 않습니다.|  
|map_key|**int**|내부 키 값입니다. Null을 허용하지 않습니다.|  
|map_value|**nvarchar (3072)**|키 값에 대한 설명입니다. Null을 허용하지 않습니다.|  
  
## <a name="permissions"></a>권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
### <a name="relationship-cardinalities"></a>관계 카디널리티  
  
|시작|대상|관계|  
|----------|--------|------------------|  
|dm_xe_map_values.object_package_guid<br /><br /> dm_xe_map_values.name|sys.dm_xe_objects.package_guid<br /><br /> sys.dm_xe_objects.name|다 대 일| 
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

