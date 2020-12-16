---
description: 공간 데이터 형식 개요
title: 공간 데이터 형식 개요 | Microsoft 문서
ms.date: 07/21/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geometry data type [SQL Server], understanding
- geography data type [SQL Server], spatial data
- planar spatial data [SQL Server], geometry data type
- spatial data types [SQL Server]
ms.assetid: 1615db50-69de-4778-8be6-4e058c00ccd4
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 668d1fda7e4b979e52377c03daaddb0cb2286cdd
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462964"
---
# <a name="spatial-data-types-overview"></a>공간 데이터 형식 개요

[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]
  
공간 데이터 형식은 두 가지가 있습니다. **geometry** 데이터 형식은 평면, 즉 유클리드(평평한 표면) 데이터를 지원합니다. **geometry** 데이터 형식은 ‘OGC(Open Geospatial Consortium)의 Simple Features for SQL Specification’ 버전 1.1.0을 따르며 SQL MM(ISO 표준) 규격을 준수합니다.
또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 GPS 위도 및 경도 좌표 등의 타원(둥근 표면) 데이터를 저장하는 **geography** 데이터 형식을 지원합니다.

## <a name="spatial-data-objects"></a>공간 데이터 개체

**geometry** 및 **geography** 데이터 형식은 16개의 공간 데이터 개체 또는 인스턴스 유형을 지원합니다. 그러나 이러한 인스턴스 유형 중 11개만 ‘인스턴스화할 수 있고’ 데이터베이스에서 이러한 인스턴스를 만들고 작업(인스턴스화)할 수 있습니다. 이러한 인스턴스는 부모 데이터 형식에서 특정 속성을 파생시킵니다.

아래 그림에서는 **geometry** 및 **geometry** 데이터 형식의 기반인 geography 계층을 보여 줍니다. **geometry** 및 **geography** 의 인스턴스화할 수 있는 형식은 파란색으로 표시되어 있습니다.  

![geom_hierarchy](../../relational-databases/spatial/media/geom-hierarchy.png)

geography 데이터 형식의 경우 인스턴스화할 수 있는 추가 형식인 **FullGlobe** 이 있습니다. **geometry** 및 **geography** 형식은 인스턴스가 명시적으로 정의되어 있지 않더라도 형식이 올바르다면 특정 인스턴스를 인식할 수 있습니다. 예를 들어 STPointFromText() 메서드를 사용하여 **Point** 인스턴스를 명시적으로 정의할 경우, 올바른 형식의 메서드 입력에 한해 **geometry** 및 **geography** 는 해당 인스턴스를 **Point** 로 인식합니다. `STGeomFromText()` 메서드를 사용하여 동일한 인스턴스를 정의할 경우 **geometry** 및 **geography** 데이터 형식은 해당 인스턴스를 **Point** 로 인식합니다.  

geometry 및 geography 형식의 하위 형식은 단순 형식과 컬렉션 형식으로 나뉩니다.  `STNumCurves()` 와 같은 일부 메서드는 단순 형식에서만 작동합니다.  

단순 형식은 다음과 같습니다.

- [Point](../../relational-databases/spatial/point.md)  
- [LineString](../../relational-databases/spatial/linestring.md)  
- [CircularString](../../relational-databases/spatial/circularstring.md)  
- [CompoundCurve](../../relational-databases/spatial/compoundcurve.md)  
- [Polygon](../../relational-databases/spatial/polygon.md)  
- [CurvePolygon](../../relational-databases/spatial/curvepolygon.md)  

컬렉션 형식은 다음과 같습니다.

- [MultiPoint](../../relational-databases/spatial/multipoint.md)  
- [MultiLineString](../../relational-databases/spatial/multilinestring.md)  
- [MultiPolygon](../../relational-databases/spatial/multipolygon.md)  
- [GeometryCollection](../../relational-databases/spatial/geometrycollection.md)  

## <a name="geometry-and-geography-data-type-differences"></a>geometry 데이터 형식과 geography 데이터 형식의 차이

공간 데이터의 두 가지 형식은 종종 매우 비슷하게 작동하지만 데이터가 저장되고 조작되는 방식에서 몇 가지 주요 차이점이 있습니다.  

### <a name="how-connecting-edges-are-defined"></a>연결 가장자리가 정의되는 방식

**LineString** 및 **Polygon** 형식을 정의하는 데이터는 꼭지점뿐입니다. geometry 형식에서 두 꼭지점을 잇는 연결 가장자리는 직선입니다. 그러나 geography 형식에서는 두 꼭지점을 잇는 연결 가장자리가 두 꼭지점 사이의 짧고 큰 타원 호입니다. 큰 타원은 타원면과 타원면의 중심을 관통하는 평면이 교차하는 지점이고 큰 타원 호는 큰 타원의 호 세그먼트입니다.  

### <a name="how-circular-arc-segments-are-defined"></a>원호 세그먼트가 정의되는 방식

geometry 형식의 원호 세그먼트는 XY 데카르트 좌표 평면(Z 값은 무시됨)에 정의됩니다. geography 형식의 원호 세그먼트는 참조 구의 곡선 세그먼트로 정의됩니다. 참조 구의 위도선은 두 호의 점이 일정한 위도를 갖는 두 개의 보완 원호로 정의될 수 있습니다.  

### <a name="measurements-in-spatial-data-types"></a>공간 데이터 형식의 측정

평면(평평한 표면) 시스템에서 거리와 영역의 측정은 좌표와 동일한 측정 단위로 지정됩니다. **geometry** 데이터 형식을 이용하면 사용한 단위에 상관없이 (2, 2)와 (5, 6) 사이의 거리는 5단위입니다.  

타원 또는 둥근 지구 시스템에서 좌표는 위도와 경도의 도 단위로 지정됩니다. 그러나 **geography** 인스턴스의 [공간 참조 식별자](./spatial-reference-identifiers-srids.md)에 따라 측정이 달라지더라도 길이 및 영역은 일반적으로 미터와 제곱미터로 측정됩니다. 가장 일반적인 **geography** 데이터 형식의 측정 단위는 미터입니다.  

### <a name="orientation-of-spatial-data"></a>공간 데이터의 방향

평면 시스템에서 다각형의 링 방향은 중요한 요소가 아닙니다. *OGC Simple Features for SQL Specification* 에서는 링 순서를 지정하지 않으며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 링 순서를 강제로 지정하지 않습니다.  

타원 시스템에서 방향이 없는 다각형은 아무 의미가 없거나 모호합니다. 적도 주변 링이 남반구 또는 북반구를 나타내는지 여부를 예로 들 수 있습니다. **geography** 데이터 형식을 사용하여 공간 인스턴스를 저장할 경우 링의 방향을 지정하고 인스턴스의 위치를 정확하게 나타내야 합니다.

타원 시스템에서 다각형의 내부는 "왼쪽 규칙"에 의해 정의됩니다. 지리적 다각형의 링을 점들이 나열된 순서대로 점을 따라 걷고 있다고 상상해보면 왼쪽의 영역은 다각형의 내부로 처리되고 오른쪽은 다각형의 외부로 처리됩니다.

[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 호환성 수준이 100 이하일 경우 **geography** 데이터 형식에는 다음과 같은 제한 사항이 있습니다.

- 각 **geography** 인스턴스가 단일 반구 내에 포함되어야 합니다. 반구보다 큰 공간 개체는 저장할 수 없습니다.

- 반구보다 큰 개체를 생성하는 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 또는 WKB(Well-Known Binary) 표현의 모든 **geography** 인스턴스에서 **ArgumentException** 이 발생합니다.  

- STIntersection(), STUnion(), STDifference() 및 STSymDifference()와 같이 두 개의 **geography** 인스턴스를 입력해야 하는 **geography** 데이터 형식 메서드는 이 메서드의 결과가 단일 반구 내에 포함되지 않을 경우 null을 반환합니다. STBuffer()도 결과가 단일 반구를 초과할 경우 null을 반환합니다.  

[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 **FullGlobe** 는 전체 구형을 포함하는 특수한 유형의 다각형입니다. 면적은 있지만 테두리나 꼭지점은 없습니다.  

### <a name="outer-and-inner-rings-in-geography-data-type"></a>`geography` 데이터 형식의 외부 및 내부 링

*OGC Simple Features for SQL Specification* 에서는 외부 링 및 내부 링에 대해 설명하지만 구분이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **geography** 데이터 형식에는 거의 의미가 없습니다. 다각형의 링은 외부 링으로 사용될 수 있습니다.  

OGC 사양에 대한 자세한 내용은 다음 문서를 참조하세요.

- [OGC Specifications, Simple Feature Access Part 1 - Common Architecture](https://go.microsoft.com/fwlink/?LinkId=93627)  
- [OGC Specifications, Simple Feature Access Part 2 - SQL Options](https://go.microsoft.com/fwlink/?LinkId=93628)  

## <a name="circular-arc-segments"></a>원호 세그먼트

인스턴스화할 수 있는 세 가지 형식인 **CircularString**, **CompoundCurve** 및 **CurvePolygon** 을 사용할 수 있습니다.  원호 세그먼트는 2차원 평면에서 3개의 점으로 정의되며 세 번째 점은 첫 번째 점과 같을 수 없습니다. 다음은 원호 세그먼트의 몇 가지 예입니다.

![circular_arc_segments](../../relational-databases/spatial/media/7e382f76-59da-4b62-80dc-caf93e637c14.gif)

처음 두 개의 예는 일반적인 원호 세그먼트를 보여 줍니다. 세 개의 각 점이 원의 둘레에 놓이는 것을 볼 수 있습니다.  

나머지 두 개의 예는 직선 세그먼트가 원호 세그먼트로 정의될 수 있음을 보여 줍니다. 두 개의 점으로만 정의할 수 있는 일반적인 직선 세그먼트와 달리 원호 세그먼트를 정의하려면 세 개의 점이 필요합니다.

원호 세그먼트 형식에서 작동하는 메서드는 직선 세그먼트를 사용하여 원호를 대략적으로 나타냅니다. 호를 대략적으로 나타내는 데 사용되는 선 세그먼트의 수는 호의 길이와 곡률에 따라 달라집니다. 각 원호 세그먼트 형식에 대해 Z 값을 저장할 수 있지만 계산에는 사용되지 않습니다.  

> [!NOTE]  
> 원호 세그먼트에 Z 값이 지정된 경우 원호 세그먼트의 모든 점에 대해 Z 값이 동일해야만 해당 원호 세그먼트를 입력할 수 있습니다. 예: `CIRCULARSTRING(0 0 1, 2 2 1, 4 0 1)` 은 허용되지만 `CIRCULARSTRING(0 0 1, 2 2 2, 4 0 1)` 은 허용되지 않습니다.  

### <a name="linestring-and-circularstring-comparison"></a>LineString 및 CircularString 비교

이 예에서는 **LineString** 인스턴스와 **CircularString** 인스턴스를 모두 사용하여 동일한 이등변 삼각형을 저장하는 방법을 보여줍니다.  

```sql
DECLARE @g1 geometry;
DECLARE @g2 geometry;
SET @g1 = geometry::STGeomFromText('LINESTRING(1 1, 5 1, 3 5, 1 1)', 0);
SET @g2 = geometry::STGeomFromText('CIRCULARSTRING(1 1, 3 1, 5 1, 4 3, 3 5, 2 3, 1 1)', 0);
IF @g1.STIsValid() = 1 AND @g2.STIsValid() = 1
  BEGIN
      SELECT @g1.ToString(), @g2.ToString()
      SELECT @g1.STLength() AS [LS Length], @g2.STLength() AS [CS Length]
  END
```  

삼각형을 정의하는 데 **CircularString** 인스턴스에는 7개의 점이 필요하지만 **LineString** 인스턴스에는 4개의 점만 필요합니다. 이는 **CircularString** 인스턴스가 원호 세그먼트만 저장하고 선 세그먼트는 저장하지 않기 때문입니다. **CircularString** 인스턴스에 저장된 삼각형의 면은 ABC, CDE 및 EFA이지만 **LineString** 인스턴스에 저장된 삼각형의 면은 AC, CE 및 EA입니다.  

다음과 같은 예제를 참조하세요.  

```sql
SET @g1 = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 4 0)', 0);
SET @g2 = geometry::STGeomFromText('CIRCULARSTRING(0 0, 2 2, 4 0)', 0);
SELECT @g1.STLength() AS [LS Length], @g2.STLength() AS [CS Length];
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```sql
LS Length    CS Length
5.65685...   6.28318...
```

**CircularString** 인스턴스는 보다 적은 수의 점을 사용하여 **LineString** 인스턴스보다 정확도가 높은 곡선 경계를 저장합니다. **CircularString** 인스턴스는 특정 지점에서 반경 20마일 이내 검색과 같이 원 경계를 저장하는 데 유용합니다. **LineString** 인스턴스는 사각형 도시 블록과 같이 선형인 경계를 저장하는 데 유용합니다.  

### <a name="linestring-and-compoundcurve-comparison"></a>LineString 및 CompoundCurve 비교

다음 코드 예제에서는 **LineString** 및 **CompoundCurve** 인스턴스를 사용하여 동일한 그림을 저장하는 방법을 보여 줍니다.

```sql
SET @g = geometry::Parse('LINESTRING(2 2, 4 2, 4 4, 2 4, 2 2)');
SET @g = geometry::Parse('COMPOUNDCURVE((2 2, 4 2), (4 2, 4 4), (4 4, 2 4), (2 4, 2 2))');
SET @g = geometry::Parse('COMPOUNDCURVE((2 2, 4 2, 4 4, 2 4, 2 2))');
```

위 예제에서 **LineString** 인스턴스나 **CompoundCurve** 인스턴스는 그림을 저장할 수 있습니다.  다음 예제에서는 **CompoundCurve** 를 사용하여 원형 조각을 저장합니다.  

```sql
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(2 2, 1 3, 0 2),(0 2, 1 0, 2 2))');  
```  

**CompoundCurve** 인스턴스는 원호 세그먼트(2 2, 1 3, 0 2)를 직접 저장할 수 있지만 **LineString** 인스턴스는 곡선을 몇 개의 작은 직선 세그먼트로 변환해야 합니다.  

### <a name="circularstring-and-compoundcurve-comparison"></a>CircularString 및 CompoundCurve 비교

다음 코드 예제에서는 **CircularString** 인스턴스에 원형 조각을 저장하는 방법을 보여 줍니다.  

```sql
DECLARE @g geometry;
SET @g = geometry::Parse('CIRCULARSTRING( 0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)');
SELECT @g.ToString(), @g.STLength();
```

**CircularString** 인스턴스를 사용하여 원형 조각을 저장하려면 각 직선 세그먼트에 세 개의 점을 사용해야 합니다. 중간 점을 알 수 없으면 다음 조각과 같이 직선 세그먼트의 엔드포인트를 계산하거나 따옴표로 묶어야 합니다.  

```sql
SET @g = geometry::Parse('CIRCULARSTRING( 0 0, 3 6.3246, 3 6.3246, 0 7, -3 6.3246, 0 0, 0 0)');
```

**CompoundCurve** 인스턴스는 **LineString** 및 **CircularString** 구성 요소를 모두 허용하므로 원형 조각의 선 세그먼트에 대한 두 개의 점만 알면 됩니다.  이 코드 예제에서는 **CompoundCurve** 를 사용하여 동일한 그림을 저장하는 방법을 보여 줍니다.

```sql
DECLARE @g geometry;
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING( 3 6.3246, 0 7, -3 6.3246), (-3 6.3246, 0 0, 3 6.3246))');
SELECT @g.ToString(), @g.STLength();
```

### <a name="polygon-and-curvepolygon-comparison"></a>Polygon 및 CurvePolygon 비교

**CurvePolygon** 인스턴스는 외부 및 내부 링을 정의할 때 **CircularString** 및 **CompoundCurve** 인스턴스를 사용할 수 있습니다. **Polygon** 인스턴스는 그럴 수 없습니다.

## <a name="see-also"></a>참고 항목

- [공간 데이터(SQL Server)](./spatial-data-sql-server.md)
- [geometry 데이터 형식 메서드 참조](../../t-sql/spatial-geometry/spatial-types-geometry-transact-sql.md)
- [geography 데이터 형식 메서드 참조](../../t-sql/spatial-geography/spatial-types-geography.md)
- [STNumCurves&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stnumcurves-geometry-data-type.md)
- [STNumCurves&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stnumcurves-geography-data-type.md)
- [STGeomFromText&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stgeomfromtext-geometry-data-type.md)
- [STGeomFromText&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md)