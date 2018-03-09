---
title: sys.spatial_index_tessellations (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fdac2e76ed1bc15a97981d91285569b4a18eb0a1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sysspatialindextessellations-transact-sql"></a>sys.spatial_index_tessellations(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

 공간 분할 구성표 및 각 공간 인덱스의 매개 변수에 대한 정보를 나타냅니다.  
  
> [!NOTE]  
>  공간 분할에 대 한 정보를 참조 하십시오. [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)합니다.  
  

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|인덱스가 정의된 개체의 ID입니다. 각 (object_id, index_id) 쌍 해당 하는 항목에 [sys.spatial_indexes](../../relational-databases/system-catalog-views/sys-spatial-indexes-transact-sql.md)합니다.|  
|index_id|**int**|인덱싱된 열이 정의된 공간 인덱스의 ID입니다.|  
|tessellation_scheme|**sysname**|중 하나는 공간 분할 구성표의 이름: GEOMETRY_GRID, GEOGRAPHY_GRID|  
|bounding_box_xmin|**float(53)**|경계의 왼쪽 아래 모퉁이의 X 좌표 상자 중 하나: NULL = (예: GEOGRAPHY_GRID) 지정 된 공간 분할 구성표에 적용할 수 없음  *n*  = tessellation_scheme이 GEOMETRY_GRID 인에 대 한 x-m 좌표 경우 값입니다.                     **참고:** 경계 상자 매개 변수에 의해 정의 된 좌표에 따라 각 개체에 대 한 해석 되는 해당 [Spatial Reference Identifier (SRID)](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)합니다.|  
|bounding_box_ymin|**float(53)**|경계의 왼쪽 아래 모퉁이의 Y-좌표 상자 중 하나: NULL = (예: GEOGRAPHY_GRID) 지정 된 공간 분할 구성표에 적용할 수 없음  *n*  = tessellation_scheme이 GEOMETRY_GRID 인에 대 한 y-m 좌표 경우 값|  
|bounding_box_xmax|**float(53)**|경계의 오른쪽 위 모퉁이의 X 좌표 상자 중 하나: NULL = (예: GEOGRAPHY_GRID) 지정 된 공간 분할 구성표에 적용할 수 없음  *n*  = tessellation_scheme이 GEOMETRY_GRID 인 x 최대값 좌표 경우 값|  
|bounding_box_ymax|**float(53)**|경계의 오른쪽 위 모퉁이의 Y-좌표 상자 중 하나: NULL = (예: GEOGRAPHY_GRID) 지정 된 공간 분할 구성표에 적용할 수 없음  *n*  = tessellation_scheme이 GEOMETRY_GRID 인 y-max 좌표 값|  
|level_1_grid|**smallint**|최상위 표의 밀도입니다. Tessellation_scheme이 GEOMETRY_GRID 또는 GEOGRAPHY_GRID 중 경우: 16 표 (높음) NULL 하 여 4 표 (LOW) 64 = 8 8 표 (MEDIUM) 256 = 16으로 하 여 16 = 4 = 지정 된 공간 인덱스 유형 또는 공간 분할 구성표에 적용할 수 없습니다.  새 SQL Server 11 공간 분할(tessellation)이 사용되면 Null이 반환됩니다.|  
|level_1_grid_desc|**nvarchar (60)**|중 하나에서 최상위 표의 밀도: 낮은 중간 높은 NULL = 지정 된 공간 인덱스 유형 또는 공간 분할 구성표에 적용할 수 없습니다.  새 SQL Server 11 공간 분할(tessellation)이 사용되면 Null이 반환됩니다.|  
|level_2_grid|**smallint**|둘째 수준 표의 밀도입니다. Tessellation_scheme이 GEOMETRY_GRID 또는 GEOGRAPHY_GRID 중 경우: 16 표 (높음) NULL 하 여 4 표 (LOW) 64 = 8 8 표 (MEDIUM) 256 = 16으로 하 여 16 = 4 = 지정 된 공간 인덱스 유형 또는 공간 분할 구성표에 적용할 수 없습니다.  새 SQL Server 11 공간 분할(tessellation)이 사용되면 Null이 반환됩니다.|  
|level_2_grid_desc|**nvarchar (60)**|중 하나는 둘째 수준 표의 밀도: 낮은 중간 높은 NULL = 지정 된 공간 인덱스 유형 또는 공간 분할 구성표에 적용할 수 없습니다.  새 SQL Server 11 공간 분할(tessellation)이 사용되면 Null이 반환됩니다.|  
|level_3_grid|**smallint**|셋째 수준 표의 밀도입니다.   Tessellation_scheme이 GEOMETRY_GRID 또는 GEOGRAPHY_GRID 중 경우: 16 표 (높음) NULL 하 여 4 표 (LOW) 64 = 8 8 표 (MEDIUM) 256 = 16으로 하 여 16 = 4 = 지정 된 공간 인덱스 유형 또는 공간 분할 구성표에 적용할 수 없습니다.  새 SQL Server 11 공간 분할(tessellation)이 사용되면 Null이 반환됩니다.|  
|level_3_grid_desc|**nvarchar (60)**|중 하나가 셋째 수준 표의 밀도: 낮은 중간 높은 NULL = 지정 된 공간 인덱스 유형 또는 공간 분할 구성표에 적용할 수 없습니다.  새 SQL Server 11 공간 분할(tessellation)이 사용되면 Null이 반환됩니다.|  
|level_4_grid|**smallint**|넷째 수준 표의 밀도입니다. Tessellation_scheme이 GEOMETRY_GRID 또는 GEOGRAPHY_GRID 중 경우: 16 표 (높음) NULL 하 여 4 표 (LOW) 64 = 8 8 표 (MEDIUM) 256 = 16으로 하 여 16 = 4 = 지정 된 공간 인덱스 유형 또는 공간 분할 구성표에 적용할 수 없습니다.  새 SQL Server 11 공간 분할(tessellation)이 사용되면 Null이 반환됩니다.|  
|level_4_grid_desc|**nvarchar (60)**|중 하나가 넷째 수준 표의 밀도입니다: < 낮은 중간 높은 NULL = 지정 된 공간 인덱스 유형 또는 공간 분할 구성표에 적용할 수 없습니다.  새 SQL Server 11 공간 분할(tessellation)이 사용되면 Null이 반환됩니다.|  
|cells_per_object|**int**|중 하나는 공간 개체당 셀 개수: tessellation_scheme이 GEOMETRY_GRID 또는 GEOGRAPHY_GRID 인 경우  *n*  = NULL 개체당 셀 개수 = 지정 된 공간 인덱스 유형 또는 공간 분할 구성표에 적용할 수 없음|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>관련 항목:  
 [개체 카탈로그 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [sys.objects &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.spatial_indexes &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-spatial-indexes-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
