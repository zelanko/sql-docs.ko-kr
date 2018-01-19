---
title: "STIntersection (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- STIntersection_TSQL
- STIntersection (geography Data Type)
dev_langs: TSQL
helpviewer_keywords: STIntersection method
ms.assetid: 7e09468f-499f-4a38-ba4b-bb30b8821e3b
caps.latest.revision: "27"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 90030f0f7482f2b8b888ad095301401c4d83dc38
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="stintersection-geography-data-type"></a>STIntersection(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  점을 나타내는 개체를 반환 위치는 **geography** 다른 인스턴스와 교차 **geography** 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STIntersection ( other_geography )  
```  
  
## <a name="arguments"></a>인수  
 *other_geography*  
 다른 **geography** 인스턴스에 stintersection ()가 호출 되는 인스턴스를 비교할 개체입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>주의  
 두 geography 인스턴스의 교집합을 반환합니다.  
  
 Stintersection ()는 항상 null를 반환 하는 경우의 spatial reference identifier (Srid)는 **geography** 인스턴스 일치 하지 않습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 반구보다 큰 공간 인스턴스를 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]포함 될 수 있습니다 **FullGlobe** 가능한 결과 집합에 인스턴스가 서버에서 반환 합니다.  
  
 입력 인스턴스에 원호 세그먼트가 있을 경우에만 결과에 원호 세그먼트가 포함될 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-computing-the-intersection-of-a-polygon-and-a-linestring"></a>1. Polygon 및 LineString의 교집합 계산  
 다음 예에서는 `STIntersection()`을 사용하여 `Polygon`과 `LineString`의 교차점을 계산합니다.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SET @h = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STIntersection(@h).ToString();  
```  
  
### <a name="b-computing-the-intersection-of-a-polygon-and-a-curvepolygon"></a>2. Polygon 및 CurvePolygon의 교집합 계산  
 다음 예에서는 원호 세그먼트를 포함하는 인스턴스를 반환합니다.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SET @h = geography::STGeomFromText('CURVEPOLYGON(CIRCULARSTRING(-122.351 47.656, -122.341 47.656, -122.341 47.661, -122.351 47.661, -122.351 47.656))', 4326);  
SELECT @g.STIntersection(@h).ToString();  
```  
  
### <a name="c-computing-the-symmetric-difference-with-fullglobe"></a>3. FullGlobe와의 대칭 차이 계산  
 다음 예에서는 `Polygon`와 `FullGlobe`의 대칭 차이를 비교합니다.  
  
```  
DECLARE @g geography = 'POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
SELECT @g.STIntersection('FULLGLOBE').ToString();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [지리 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
