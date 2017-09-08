---
title: "STCentroid (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STCentroid_TSQL
- STCentroid (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STCentroid (geometry Data Type)
ms.assetid: 4dc5a004-7a53-4cce-81dd-9f5e1dd0db78
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c34e8eb334190b72a560086a9d5e862ba6667dec
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stcentroid-geometry-data-type"></a>STCentroid(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

기 하 도형 중심을 반환 합니다.는 **geometry** 이상의 다각형으로 구성 된 인스턴스.
  
## <a name="syntax"></a>구문  
  
```  
  
.STCentroid ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **SqlGeometry**  
  
 열기 Geospatial Consortium (OGC) 입력: **지점**  
  
## <a name="remarks"></a>주의  
 `STCentroid()`경우 null을 반환은 **기 하 도형** 인스턴스가 않습니다는 **Polygon, CurvePolygon**, 또는 **MultiPolygon** 유형입니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-computing-the-centroid-of-a-polygon-instance"></a>1. Polygon 인스턴스의 중심 계산  
 다음 예제에서는 `STCentroid()` 중심을 계산 하는 `polygon``geometry` 인스턴스:  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0),(2 2, 2 1, 1 1, 1 2, 2 2))', 0);  
SELECT @g.STCentroid().ToString();  
```  
  
### <a name="b-computing-the-centroid-of-a-curvepolygon-instance"></a>2. CurvePolygon 인스턴스의 중심 계산  
 다음 예에서는 `CurvePolygon` 인스턴스의 중심을 계산합니다.  
  
 `DECLARE @g geometry = 'CURVEPOLYGON(CIRCULARSTRING(0 4, 4 0, 8 4, 4 8, 0 4), CIRCULARSTRING(2 4, 4 2, 6 4, 4 6, 2 4))';`  
  
 `SELECT @g.STCentroid().ToString() AS Centroid`  
  
## <a name="see-also"></a>관련 항목:  
 [Geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


