---
title: "STNumPoints (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STNumPoints (geography Data Type)
- STNumPoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumPoints method
ms.assetid: 25ff7ad1-ba5f-4cfb-816a-59255ac1591d
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 803e631cb1e0250ebedd28a97afe4e20476396cf
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stnumpoints-geography-data-type"></a>STNumPoints(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  각 도형에 있는 점의 총 개수를 반환 된 **geography** 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STNumPoints ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **int**  
  
 CLR 반환 형식: **SqlInt32**  
  
## <a name="remarks"></a>주의  
 이 방법에 대 한 설명에 있는 점을 셉니다는 **geography** 인스턴스. 중복 점도 개수에 포함되지만 세그먼트 사이의 연결 점은 한 번만 셉니다. 이 인스턴스가 컬렉션인 경우 이 메서드는 컬렉션에 있는 점의 총 개수를 반환합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-retrieving-the-total-number-of-points-in-a-linestring"></a>1. LineString에 있는 점의 총 개수 검색  
 다음 예에서는 `LineString` 인스턴스를 만들고 `STNumPoints()`를 사용하여 인스턴스의 설명에 사용된 점의 수를 확인합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STNumPoints();  
```  
  
### <a name="b-retrieving-the-total-number-of-points-in-a-geometrycollection"></a>2. GeometryCollection에 있는 점의 총 개수 검색  
 다음 예에서는 `GeometryCollection`에 있는 모든 요소에 대해 점의 합계를 반환합니다.  
  
```  
DECLARE @g geography = 'GEOMETRYCOLLECTION(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)  
    ,CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)))';  
SELECT @g.STNumPoints();  
```  
  
### <a name="c-returning-the-number-of-points-in-a-compoundcurve"></a>3. CompoundCurve에 있는 점의 개수 반환  
 다음 예에서는 CompoundCurve 인스턴스에 있는 점의 개수를 반환합니다. STNumPoints()가 세그먼트 사이의 연결 점을 한 번만 세므로 쿼리는 6이 아닌 5를 반환합니다.  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658),( -122.348 47.658, -121.56 48.12, -122.358 47.653))'  
 SELECT @g.STNumPoints();
 ```  
  
## <a name="see-also"></a>관련 항목:  
 [Geography 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

