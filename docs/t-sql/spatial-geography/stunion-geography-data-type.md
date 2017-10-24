---
title: "STUnion (geography 데이터 형식) | Microsoft Docs"
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
- STUnion (geography Data Type)
- STUnion_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STUnion method
ms.assetid: 9bf87691-efd8-4c53-bd2f-eefe0acd19ca
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5e200f81a17e9b512986795077fe487e54a489f2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stunion-geography-data-type"></a>STUnion(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  합집합을 나타내는 개체를 반환 된 **geography** 인스턴스와 다른 **geography** 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STUnion ( other_geography )  
```  
  
## <a name="arguments"></a>인수  
 *other_geography*  
 다른 **geography** stunion ()가 호출 되는 인스턴스와 통합할 인스턴스.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="exceptions"></a>예외  
 이 메서드에서 throw 된 **ArgumentException** 인스턴스에 대척점 하는 경우.  
  
## <a name="remarks"></a>주의  
 항상 null이 반환 하는 경우의 spatial reference identifier (Srid)는 **geography** 인스턴스 일치 하지 않습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 반구보다 큰 공간 인스턴스를 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 서버에서 반환 된 결과 집합이 확장 되었습니다 **FullGlobe** 인스턴스.  
  
 입력 인스턴스에 원호 세그먼트가 있을 경우에만 결과에 원호 세그먼트가 포함될 수 있습니다.  
  
 이 메서드는 정확하지 않습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-computing-the-union-of-two-polygons"></a>1. 두 Polygon의 통합 계산  
 다음 예에서는 `STUnion()`을 사용하여 두 `Polygon` 인스턴스의 통합을 계산합니다.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SET @h = geography::STGeomFromText('POLYGON((-122.351 47.656, -122.341 47.656, -122.341 47.661, -122.351 47.661, -122.351 47.656))', 4326);  
SELECT @g.STUnion(@h).ToString();  
```  
  
### <a name="b-producing-a-fullglobe-result"></a>2. FullGlobe 결과 생성  
 다음 예에서는 `FullGlobe`이 두 개의 `STUnion()` 인스턴스를 조합할 때 `Polygon`를 생성합니다.  
  
```
 DECLARE @g geography = 'POLYGON ((-122.358 47.653, -122.358 47.658,-122.348 47.658, -122.348 47.649, -122.358 47.653))';  
 DECLARE @h geography = 'POLYGON ((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STUnion(@h).ToString();
 ```  
  
### <a name="c-producing-a-triagonal-hole-from-a-union-of-a-curvepolygon-and-a-traigonal-hole"></a>3. CurvePolygon과 삼각 구멍을 합하여 삼각 구멍 생성  
 다음 예에서는 `CurvePolygon`을 `Polygon` 인스턴스와 합하여 삼각 구멍을 만듭니다.  
  
```
 DECLARE @g geography = 'POLYGON ((-0.5 0, 0 1, 0.5 0.5, -0.5 0))';  
 DECLARE @h geography = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 0, 0.7 0.7, 0 1), (0 1, 0 0)))';  
 SELECT @g.STUnion(@h).ToString();
 ```  
  
## <a name="see-also"></a>관련 항목:  
 [Geography 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

