---
title: sys.spatial_indexes (Transact SQL) | Microsoft Docs
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
- sys.spatial_indexes_TSQL
- spatial_indexes
- spatial_indexes_TSQL
- sys.spatial_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.spatial_indexes catalog view
ms.assetid: 40e967d5-2e8d-45af-bf5e-5251493cf7cb
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 709c692ed9eacf6307995d7273eb5a7a2e906580
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="sysspatialindexes-transact-sql"></a>sys.spatial_indexes(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  공간 인덱스의 주요 인덱스 정보를 나타냅니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|\<열을 상속 >||열을 상속 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)합니다.|  
|spatial_index_type|**tinyint**|공간 인덱스 유형:<br /><br /> 1 = 기하학적 공간 인덱스<br /><br /> 2 = 지리적 인덱스|  
|spatial_index_type_desc|**nvarchar (60)**|공간 인덱스의 유형 설명:<br /><br /> GEOMETRY = 기하학적 공간 인덱스<br /><br /> GEOGRAPHY = 지리적 공간 인덱스|  
|tessellation_scheme|**sysname**|공간 분할(tessellation) 구성표 이름:<br /><br /> GEOMETRY_GRID, GEOMETRY_AUTO_GRID,<br /><br /> GEOGRAPHY_GRID, GEOGRAPHY_AUTO_GRID<br /><br /> 참고: 공간 분할 구성표에 대 한 정보에 대 한 참조 [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)합니다.|  
|\<열을 상속 >||열을 상속 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)합니다.<br /><br /> 상속된 열 has_filter 및 filter_definition은 공간 인덱스와 관련된 열 다음에 나타납니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>관련 항목:  
 [sys.objects &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.spatial_index_tessellations &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)  
  
  
