---
title: "STUnion (geometry 데이터 형식) | Microsoft Docs"
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
- STUnion (geometry Data Type)
- STUnion_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STUnion (geometry Data Type)
ms.assetid: 5b168118-137d-402f-9173-fee3f365a89c
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3c41cbcf144e8772cd17cbfb43da403aea29a353
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stunion-geometry-data-type"></a>STUnion(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

합집합을 나타내는 개체를 반환 된 **geometry** 인스턴스와 다른 **기 하 도형** 인스턴스.
  
## <a name="syntax"></a>구문  
  
```  
  
.STUnion ( other_geometry )  
```  
  
## <a name="arguments"></a>인수  
 *other_geometry*  
 다른 **geometry** 인스턴스와 통합할을 형성 하는 인스턴스 `STUnion()` 가 호출 되 합니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="remarks"></a>주의  
 항상 null이 반환 하는 경우의 spatial reference Id (Srid)는 **geometry** 인스턴스 일치 하지 않습니다. 입력 인스턴스에 원호 세그먼트가 있을 경우에만 결과에 원호 세그먼트가 포함될 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-computing-the-union-of-two-polygon-instances"></a>1. 두 Polygon 인스턴스의 통합 계산  
 다음 예에서는 `STUnion()`을 사용하여 두 `Polygon` 인스턴스의 통합을 계산합니다.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 2 2, 2 0, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STUnion(@h).ToString();  
```  
  
### <a name="b-computing-the-union-of-a-polygon-instance-with-a-curvepolygon-instance"></a>2. CurvePolygon 인스턴스가 있는 Polygon 인스턴스의 통합 계산  
 다음 예에서는 원호 세그먼트를 포함하는 `GeometryCollection` 인스턴스를 반환합니다.  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(CIRCULARSTRING(0 -4, 4 0, 0 4, -4 0, 0 -4))';  
 DECLARE @h geometry = 'POLYGON((5 -1, 5 -3, 7 -3, 7 -1, 5 -1))';  
 SELECT @g.STUnion(@h).ToString();
 ```  
  
 `STUnion()`을 호출한 인스턴스는 원호 세그먼트를 포함하므로 `STUnion()`은 원호 세그먼트를 포함하는 결과를 반환합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


