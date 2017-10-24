---
title: "STDifference (geometry 데이터 형식) | Microsoft Docs"
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
- STDifference_TSQL
- STDifference (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDifference (geometry Data Type)
ms.assetid: 737f39bb-8750-4ffb-8594-23febc2f1075
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7c6b79813c903e5c5541b2aab8d09ba1858f28f0
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stdifference-geometry-data-type"></a>STDifference(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

점 집합을 나타내는 개체를 반환 **geometry** 다른 내에 포함 하지 않는 인스턴스 **geometry** 인스턴스.
  
## <a name="syntax"></a>구문  
  
```  
  
.STDifference ( other_geometry )  
```  
  
## <a name="arguments"></a>인수  
 *other_geometry*  
 다른 **geometry** 기반이 인스턴스에서 제거할 점을 나타내는 인스턴스 `STDifference()` 가 호출 되 합니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="remarks"></a>주의  
 항상 null이 반환 하는 경우의 spatial reference Id (Srid)는 **geometry** 인스턴스 일치 하지 않습니다.   입력 인스턴스에 원호 세그먼트가 있을 경우에만 결과에 원호 세그먼트가 포함될 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-computing-the-difference-between-two-polygon-instances"></a>1. 두 Polygon 인스턴스 사이의 차이 계산  
 다음 예에서는 `STDifference()`를 사용하여 두 다각형 간의 차이를 계산합니다.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 2 2, 2 0, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STDifference(@h).ToString();  
```  
  
### <a name="b-invoking-stdifference-on-a-curvepolygon-instance"></a>2. CurvePolygon 인스턴스에서 STDifference() 호출  
 다음 예에서는 CurvePolygon 인스턴스에서 STDifference()를 사용합니다.  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON (CIRCULARSTRING (0 -4, 4 0, 0 4, -4 0, 0 -4))';  
 DECLARE @h geometry = 'POLYGON ((1 -1, 5 -1, 5 3, 1 3, 1 -1))';  
 -- Note the different results returned by the two SELECT statements  
 SELECT @h.STDifference(@g).ToString(), @g.STDifference(@h).ToString();
 ```  
  
## <a name="see-also"></a>관련 항목:  
 [Geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


