---
description: sys.spatial_indexes(Transact-SQL)
title: sys. spatial_indexes (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 313e28bdda409b96059e95e8ea0f0fca9ef4a6cb
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539476"
---
# <a name="sysspatial_indexes-transact-sql"></a>sys.spatial_indexes(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  공간 인덱스의 주요 인덱스 정보를 나타냅니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|\<inherited columns>||은 (는) [sys. 인덱스](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)에서 열을 상속 합니다.|  
|spatial_index_type|**tinyint**|공간 인덱스 유형:<br /><br /> 1 = 기하학적 공간 인덱스<br /><br /> 2 = 지리적 인덱스|  
|spatial_index_type_desc|**nvarchar(60)**|공간 인덱스의 유형 설명:<br /><br /> GEOMETRY = 기하학적 공간 인덱스<br /><br /> GEOGRAPHY = 지리적 공간 인덱스|  
|tessellation_scheme|**sysname**|공간 분할(tessellation) 구성표 이름:<br /><br /> GEOMETRY_GRID, GEOMETRY_AUTO_GRID,<br /><br /> GEOGRAPHY_GRID, GEOGRAPHY_AUTO_GRID<br /><br /> 참고: 공간 분할 (tessellation) 구성표에 대 한 자세한 내용은 [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)를 참조 하세요.|  
|\<inherited columns>||은 (는) [sys. 인덱스](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)에서 열을 상속 합니다.<br /><br /> 상속된 열 has_filter 및 filter_definition은 공간 인덱스와 관련된 열 다음에 나타납니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.spatial_index_tessellations&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)  
  
  
