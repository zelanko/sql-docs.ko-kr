---
description: sys.spatial_index_tessellations(Transact-SQL)
title: sys. spatial_index_tessellations (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- spatial_index_tessellations
- sys.spatial_index_tessellations_TSQL
- spatial_index_tessellations_TSQL
- sys.spatial_index_tessellations
dev_langs:
- TSQL
helpviewer_keywords:
- sys.spatial_index_tessellations catalog view
ms.assetid: 8b17a9a4-b57f-4220-8138-fc73581b1670
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a86ba88f46944140da647133ab7f8a72a81dd279
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88376599"
---
# <a name="sysspatial_index_tessellations-transact-sql"></a>sys.spatial_index_tessellations(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

 공간 분할 구성표 및 각 공간 인덱스의 매개 변수에 대한 정보를 나타냅니다.  
  
> [!NOTE]  
>  공간 분할에 대한 자세한 내용은 [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)를 참조하세요.  
  

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|인덱스가 정의된 개체의 ID입니다. 각 (object_id, index_id) 쌍에는 [spatial_indexes](../../relational-databases/system-catalog-views/sys-spatial-indexes-transact-sql.md)에 해당 하는 항목이 있습니다.|  
|index_id|**int**|인덱싱된 열이 정의된 공간 인덱스의 ID입니다.|  
|tessellation_scheme|**sysname**|공간 분할 (tessellation) 구성표의 이름이 며 다음 중 하나 GEOMETRY_GRID GEOGRAPHY_GRID|  
|bounding_box_xmin|**float(53)**|경계 상자의 왼쪽 아래 모퉁이에 대 한 X 좌표입니다. 지정 된 공간 분할 (tessellation) 구성표에 적용할 수 없는 NULL = (예: GEOGRAPHY_GRID) *n* = tessellation_scheme GEOMETRY_GRID 경우 x 분 좌표 값입니다.                     **참고:** 경계 상자 매개 변수에서 정의한 좌표는 [SRID (공간 참조 식별자)](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)에 따라 각 개체에 대해 해석 됩니다.|  
|bounding_box_ymin|**float(53)**|경계 상자의 왼쪽 아래 모퉁이의 Y 좌표입니다. NULL = 지정 된 공간 분할 (tessellation) 구성표에 적용할 수 없는 (예: GEOGRAPHY_GRID) *n* = tessellation_scheme GEOMETRY_GRID y 분 좌표 값|  
|bounding_box_xmax|**float(53)**|경계 상자의 오른쪽 위 모퉁이에 대 한 X 좌표입니다. 다음 중 하나는 지정 된 공간 분할 (tessellation) 구성표에 적용할 수 없습니다 (예: GEOGRAPHY_GRID) *n* = tessellation_scheme GEOMETRY_GRID 경우 x 최대값 좌표 값|  
|bounding_box_ymax|**float(53)**|경계 상자의 오른쪽 위 모퉁이에 대 한 Y 좌표 이며 지정 된 공간 분할 (tessellation) 구성표에 적용할 수 없는 NULL = (예: GEOGRAPHY_GRID) *n* = tessellation_scheme GEOMETRY_GRID 경우 y-최대 좌표 값|  
|level_1_grid|**smallint**|최상위 표의 밀도입니다. Tessellation_scheme GEOMETRY_GRID 또는 GEOGRAPHY_GRID 인 경우 16 = 4 x 4 그리드 (낮음) 64 = 8 x 8 그리드 (중간) 256 = 16 x 16 그리드 (높음) NULL = 지정 된 공간 인덱스 유형 또는 공간 분할 (tessellation) 구성표에 적용할 수 없습니다.  새 SQL Server 11 공간 분할(tessellation)이 사용되면 Null이 반환됩니다.|  
|level_1_grid_desc|**nvarchar(60)**|최상위 표에 대 한 표 밀도, 지정 된 공간 인덱스 유형 또는 공간 분할 (tessellation) 구성표에 적용할 수 없음: 낮음 MEDIUM HIGH NULL =  새 SQL Server 11 공간 분할(tessellation)이 사용되면 Null이 반환됩니다.|  
|level_2_grid|**smallint**|둘째 수준 표의 밀도입니다. Tessellation_scheme GEOMETRY_GRID 또는 GEOGRAPHY_GRID 인 경우 16 = 4 x 4 그리드 (낮음) 64 = 8 x 8 그리드 (중간) 256 = 16 x 16 그리드 (높음) NULL = 지정 된 공간 인덱스 유형 또는 공간 분할 (tessellation) 구성표에 적용할 수 없습니다.  새 SQL Server 11 공간 분할(tessellation)이 사용되면 Null이 반환됩니다.|  
|level_2_grid_desc|**nvarchar(60)**|둘째 수준 표의 밀도입니다. 다음 중 하나는 지정 된 공간 인덱스 유형 또는 공간 분할 (tessellation) 구성표에 적용할 수 없습니다.  새 SQL Server 11 공간 분할(tessellation)이 사용되면 Null이 반환됩니다.|  
|level_3_grid|**smallint**|셋째 수준 표의 밀도입니다.   Tessellation_scheme GEOMETRY_GRID 또는 GEOGRAPHY_GRID 인 경우 16 = 4 x 4 그리드 (낮음) 64 = 8 x 8 그리드 (중간) 256 = 16 x 16 그리드 (높음) NULL = 지정 된 공간 인덱스 유형 또는 공간 분할 (tessellation) 구성표에 적용할 수 없습니다.  새 SQL Server 11 공간 분할(tessellation)이 사용되면 Null이 반환됩니다.|  
|level_3_grid_desc|**nvarchar(60)**|세 번째 수준 표에 대 한 표 밀도 이며 지정 된 공간 인덱스 유형 또는 공간 분할 (tessellation) 구성표에 적용할 수 없음: 낮은 MEDIUM 높음 NULL =  새 SQL Server 11 공간 분할(tessellation)이 사용되면 Null이 반환됩니다.|  
|level_4_grid|**smallint**|넷째 수준 표의 밀도입니다. Tessellation_scheme GEOMETRY_GRID 또는 GEOGRAPHY_GRID 인 경우 16 = 4 x 4 그리드 (낮음) 64 = 8 x 8 그리드 (MEDIUM) 256 = 16 x 16 그리드 (높음) NULL = 지정 된 공간 인덱스 유형 또는 공간 분할 (tessellation) 구성표에 적용할 수 없습니다.  새 SQL Server 11 공간 분할(tessellation)이 사용되면 Null이 반환됩니다.|  
|level_4_grid_desc|**nvarchar(60)**|네 번째 수준 표의 밀도입니다. 다음 중 하나는 지정 된 공간 인덱스 유형 또는 공간 분할 (tessellation) 구성표에 적용할 수 없습니다. < LOW MEDIUM HIGH NULL =  새 SQL Server 11 공간 분할(tessellation)이 사용되면 Null이 반환됩니다.|  
|cells_per_object|**int**|공간 개체당 셀 수 이며 다음 중 하나입니다. tessellation_scheme GEOMETRY_GRID 또는 GEOGRAPHY_GRID 경우 *n* = 개체당 셀 수 = 지정 된 공간 인덱스 유형 또는 공간 분할 (tessellation) 구성표에 적용할 수 없습니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [sys. 개체 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.spatial_indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-spatial-indexes-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
