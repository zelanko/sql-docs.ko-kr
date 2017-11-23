---
title: "STDimension (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STDimension_TSQL
- STDimension (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: STDimension (geometry Data Type)
ms.assetid: 4fbd27dd-317b-4916-a8ae-4df1b8a6f27c
caps.latest.revision: "29"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: feac8d21701070ee31d191e823b66875f7d9177a
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="stdimension-geometry-data-type"></a>STDimension(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

최대 차원을 반환는 **geometry** 인스턴스.
  
## <a name="syntax"></a>구문  
  
```  
  
.STDimension ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **int**  
  
 CLR 반환 형식: **SqlInt32**  
  
## <a name="remarks"></a>주의  
 `STDimension()`-1을 반환 하는 경우는 **기 하 도형** 인스턴스가 비어 있습니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 보유 하는 테이블 변수 **기 하 도형** 인스턴스를 삽입 하는 `Point`, `LineString`, 및 `Polygon`합니다.  다음 사용 하 여 `STDimension()` 각각의 크기를 반환할 **geometry** 인스턴스.  
  
```  
DECLARE @temp table ([name] varchar(10), [geom] geometry);  
INSERT INTO @temp values ('Point', geometry::STGeomFromText('POINT(3 3)', 0));  
INSERT INTO @temp values ('LineString', geometry::STGeomFromText('LINESTRING(0 0, 3 3)', 0));  
INSERT INTO @temp values ('Polygon', geometry::STGeomFromText('POLYGON((0 0, 3 0, 0 3, 0 0))', 0));  
SELECT [name], [geom].STDimension() as [dim]  
FROM @temp;  
```  
  
 그런 다음 이 예에서는 각 `geometry` 인스턴스의 차원을 반환합니다.  
  
|name|dim|  
|----------|---------|  
|점|0|  
|LineString|1.|  
|다각형|2|  
  
## <a name="see-also"></a>관련 항목:  
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

