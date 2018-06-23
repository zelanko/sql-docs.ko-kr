---
title: 공간 데이터 형식 개요 | Microsoft 문서
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- geometry data type [SQL Server], understanding
- geography data type [SQL Server], spatial data
- planar spatial data [SQL Server], geometry data type
- spatial data types [SQL Server]
ms.assetid: 1615db50-69de-4778-8be6-4e058c00ccd4
caps.latest.revision: 48
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e328be1225999a629d93ab16c55b2bc4b7f15d5c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172393"
---
# <a name="spatial-data-types-overview"></a>공간 데이터 형식 개요
  공간 데이터 형식은 두 가지가 있습니다. `geometry` 데이터 형식은 평면, 즉 유클리드(평평한 표면) 데이터를 지원합니다. `geometry` 데이터 형식은 OGC(Open Geospatial Consortium)의 Simple Features for SQL Specification 버전 1.1.0을 따르며 SQL MM(ISO 표준)과 호환됩니다.  
  
 또한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 지원는 `geography` GPS 위도 및 경도 좌표 등의 타원 (둥근 표면) 데이터를 저장 하는 데이터 형식입니다.  
  
> [!IMPORTANT]  
>  향상된 공간 데이터 형식을 비롯한 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]의 공간 기능에 대한 자세한 설명 및 예제를 보려면 [SQL Server 코드 이름 "Denali"의 새로운 공간 기능](http://go.microsoft.com/fwlink/?LinkId=226407)백서를 다운로드하세요.  
  
##  <a name="objects"></a> 공간 데이터 개체  
 `geometry` 및 `geography` 데이터 형식은 16개의 공간 데이터 개체 또는 인스턴스 유형을 지원합니다. 그러나 이러한 인스턴스 유형 중 11개만 *인스턴스화할 수 있고*데이터베이스에서 이러한 인스턴스를 만들고 작업(인스턴스화)할 수 있습니다. 이러한 인스턴스는 특정 속성으로 구분 하는 부모 데이터 형식에서 파생 `Points`, **LineStrings, CircularStrings**, `CompoundCurves`, `Polygons`, `CurvePolygons` 또는 여러 `geometry`또는 `geography` 인스턴스에 `GeometryCollection`합니다. `Geography` 형식에는 `FullGlobe`라는 추가 인스턴스 유형이 있습니다.  
  
 아래 그림은 `geometry` 계층은 `geometry` 및 `geography` 데이터 형식의 기반인 합니다. 인스턴스화할 수 있는 유형의 `geometry` 및 `geography` 파란색으로 표시 되어 있습니다.  
  
 ![Geometry 유형의 계층 구조](../../database-engine/media/geom-hierarchy.gif "geometry 유형의 계층 구조")  
  
 그림 표시 된 대로의 인스턴스화할 수 있는 10 개의 형식은 `geometry` 및 `geography` 데이터 형식은 `Point`, `MultiPoint`, `LineString`, `CircularString`, `MultiLineString`, `CompoundCurve`, `Polygon`, `CurvePolygon`, `MultiPolygon`, 및 `GeometryCollection`합니다. 하나의 추가 형식이 인스턴스화할 수 있는 지리 데이터 형식에 대 한: `FullGlobe`합니다. `geometry` 및 `geography` 형식을 인식할 수 특정 인스턴스를 올바른 형식의 인스턴스가으로 인스턴스가 명시적으로 정의 되지 않은 경우에 합니다. 예를 들어, 정의 하는 경우는 `Point` STPointFromText() 메서드를 사용 하 여 명시적 인스턴스 `geometry` 및 `geography` 해당 인스턴스를 인식는 `Point`경우, 올바른 형식의 메서드 입력이 있습니다. `STGeomFromText()` 메서드를 사용하여 동일한 인스턴스를 정의할 경우 `geometry` 및 `geography` 데이터 형식은 해당 인스턴스를 `Point`로 인식합니다.  
  
 geometry 및 geography 형식의 하위 형식은 단순 형식과 컬렉션 형식으로 나뉩니다.  `STNumCurves()` 와 같은 일부 메서드는 단순 형식에서만 작동합니다.  
  
 단순 형식에는 다음이 포함됩니다.  
  
-   [Point](../spatial/point.md)  
  
-   [LineString](../spatial/linestring.md)  
  
-   [CircularString](../spatial/circularstring.md)  
  
-   [CompoundCurve](../spatial/compoundcurve.md)  
  
-   [다각형](../spatial/polygon.md)  
  
-   [CurvePolygon](../spatial/curvepolygon.md)  
  
 컬렉션 형식에는 다음이 포함됩니다.  
  
-   [MultiPoint](../spatial/multipoint.md)  
  
-   [MultiLineString](../spatial/multilinestring.md)  
  
-   [MultiPolygon](../spatial/multipolygon.md)  
  
-   [GeometryCollection](../spatial/geometrycollection.md)  
  
  
##  <a name="differences"></a> geometry 데이터 형식과 geography 데이터 형식의 차이점  
 공간 데이터의 두 가지 형식은 종종 매우 비슷하게 작동하지만 데이터가 저장되고 조작되는 방식에서 몇 가지 주요 차이점이 있습니다.  
  
### <a name="how-connecting-edges-are-defined"></a>연결 가장자리가 정의되는 방식  
 `LineString` 및 `Polygon` 형식을 정의하는 데이터는 꼭지점뿐입니다.  geometry 형식에서 두 꼭지점을 잇는 연결 가장자리는 직선입니다.  그러나 geography 형식에서는 두 꼭지점을 잇는 연결 가장자리가 두 꼭지점 사이의 짧고 큰 타원 호입니다.  큰 타원은 타원면과 타원면의 중심을 관통하는 평면이 교차하는 지점이고 큰 타원 호는 큰 타원의 호 세그먼트입니다.  
  
### <a name="how-circular-arc-segments-are-defined"></a>원호 세그먼트가 정의되는 방식  
 geometry 형식의 원호 세그먼트는 XY 데카르트 좌표 평면(Z 값은 무시됨)에 정의됩니다. geography 형식의 원호 세그먼트는 참조 구의 곡선 세그먼트로 정의됩니다. 참조 구의 위도선은 두 호의 점이 일정한 위도를 갖는 두 개의 보완 원호로 정의될 수 있습니다.  
  
### <a name="measurements-in-spatial-data-types"></a>공간 데이터 형식의 측정  
 평면(또는 평평한 표면) 시스템에서 거리와 영역의 측정은 좌표와 동일한 측정 단위로 지정됩니다. 사용 하는 `geometry` 데이터 형식, 사이의 거리 (2, 2)와 (5, 6)는 사용 된 단위에 관계 없이 5 단위입니다.  
  
 타원 또는 둥근 지구 시스템에서 좌표는 위도와 경도의 도 단위로 지정됩니다. 그러나 길이 및 영역은 일반적으로 측정 됩니다와 제곱 미터로 측정의 spatial reference identifier (SRID)에 종속 될 수 있지만 `geography` 인스턴스. 가장 일반적인에 대 한 측정 단위는 `geography` 데이터 형식은 미터입니다.  
  
### <a name="orientation-of-spatial-data"></a>공간 데이터의 방향  
 평면 시스템에서 다각형의 링 방향은 중요한 요소가 아닙니다. 예를 들어 ((0, 0), (10, 0), (0, 20), (0, 0))로 나타내는 다각형은 ((0, 0), (0, 20), (10, 0), (0, 0))로 나타내는 다각형과 동일합니다. OGC Simple Features for SQL Specification에서는 링 순서를 지정하지 않으며 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 링 순서를 강제로 지정하지 않습니다.  
  
 타원 시스템에서 방향이 없는 다각형은 아무 의미가 없거나 모호합니다. 적도 주변 링이 남반구 또는 북반구를 나타내는지 여부를 예로 들 수 있습니다. 사용 하는 경우는 `geography` 공간 인스턴스를 저장할 데이터 형식에서는 링의 방향을 지정 하 고 정확 하 고 인스턴스의 위치를 설명 해야 합니다. 타원 시스템의 다각형 내부는 왼쪽 규칙으로 정의됩니다.  
  
 호환성 수준이 100 인 경우 또는 그 아래에 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 하면 `geography` 데이터 형식에는 다음과 같은 제한:  
  
-   각 `geography` 인스턴스가 단일 반구 내에 포함되어야 합니다. 반구보다 큰 공간 개체는 저장할 수 없습니다.  
  
-   반구보다 큰 개체를 생성하는 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 또는 WKB(Well-Known Binary) 표현의 모든 `geography` 인스턴스에서 `ArgumentException`이 발생합니다.  
  
-   `geography` 데이터 형식 메서드는 두 개의 입력이 필요 `geography` stintersection (), stunion (), stdifference () 및 stsymdifference ()와 같은 인스턴스 메서드의 결과가 단일 반구 내에 맞지 않는 경우 null을 반환 합니다. STBuffer()도 결과가 단일 반구를 초과할 경우 null을 반환합니다.  
  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]에서 `FullGlobe`는 전체 구형을 포함하는 특수한 유형의 다각형입니다. `FullGlobe`에는 영역이 있지만 테두리나 꼭지점은 없습니다.  
  
### <a name="outer-and-inner-rings-not-important-in-geography-data-type"></a>geography 데이터 형식에서 중요하지 않은 외부 및 내부 링  
 OGC Simple Features for SQL Specification에서는 외부 링 및 내부 링에 설명 하지만 이러한 구분이에 대해 거의 의미가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `geography` 데이터 형식; 다각형의 링 수행할 수는 외부 링으로 합니다.  
  
 OGC 사양에 대한 자세한 내용은 다음을 참조하십시오.  
  
-   [OGC Specifications, Simple Feature Access Part 1 - Common Architecture](http://go.microsoft.com/fwlink/?LinkId=93627)  
  
-   [OGC Specifications, Simple Feature Access Part 2 - SQL Options](http://go.microsoft.com/fwlink/?LinkId=93628)  
  
  
##  <a name="circular"></a> 원호 세그먼트  
 인스턴스화할 수 있는 세 가지 형식은 원호 세그먼트를 걸릴 수 있습니다: `CircularString`, `CompoundCurve`, 및 `CurvePolygon`합니다.  원호 세그먼트는 2차원 평면에서 3개의 점으로 정의되며 세 번째 점은 첫 번째 점과 같을 수 없습니다.  
  
 그림 A와 B에서는 일반적인 원호 세그먼트를 보여 줍니다. 세 개의 각 점이 원의 둘레에 어떻게 놓이는지 확인하십시오.  
  
 그림 C와 D에서는 선 세그먼트를 원호 세그먼트로 정의할 수 있는 방법을 보여 줍니다.  두 개의 점으로만 정의할 수 있는 일반적인 선 세그먼트와 달리 원호 세그먼트를 정의하려면 세 개의 점이 필요합니다.  
  
 원호 세그먼트 형식에서 작동하는 메서드는 직선 세그먼트를 사용하여 원호를 대략적으로 나타냅니다. 호를 대략적으로 나타내는 데 사용되는 선 세그먼트의 수는 호의 길이와 곡률에 따라 달라집니다. 각 원호 세그먼트 형식에 대해 Z 값을 저장할 수 있지만 메서드는 계산에 Z 값을 사용하지 않습니다.  
  
> [!NOTE]  
>  원호 세그먼트에 Z 값이 지정된 경우 원호 세그먼트의 모든 점에 대해 Z 값이 동일해야만 해당 원호 세그먼트를 입력할 수 있습니다. 예: `CIRCULARSTRING(0 0 1, 2 2 1, 4 0 1)` 은 허용되지만 `CIRCULARSTRING(0 0 1, 2 2 2, 4 0 1)` 은 허용되지 않습니다.  
  
### <a name="linestring-and-circularstring-comparison"></a>LineString 및 CircularString 비교  
 다음 다이어그램에서는 동일한 이등변 삼각형을 보여 줍니다. 삼각형 A는 선 세그먼트를 사용하여 삼각형을 정의하고 삼각형 B는 원호 세그먼트를 사용하여 삼각형을 정의합니다.  
  
 ![](../../database-engine/media/7e382f76-59da-4b62-80dc-caf93e637c14.png "7e382f76-59da-4b62-80dc-caf93e637c14")  
  
 모두 사용 하 여 위의 이등변 삼각형을 저장 하는 방법을 보여 주는이 예제는 `LineString` 인스턴스 및 `CircularString` 인스턴스:  
  
```tsql  
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
  
 삼각형을 정의하는 데 `CircularString` 인스턴스에는 7개의 점이 필요하지만 `LineString` 인스턴스에는 4개의 점만 필요합니다. 이는 `CircularString` 인스턴스가 원호 세그먼트만 저장하고 선 세그먼트는 저장하지 않기 때문입니다. 따라서 `CircularString` 인스턴스에 저장된 삼각형의 면은 ABC, CDE 및 EFA이지만 `LineString` 인스턴스에 저장된 삼각형의 면은 AC, CE 및 EA입니다.  
  
 다음 코드 조각을 참조하십시오.  
  
```tsql  
SET @g1 = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 4 0)', 0);  
SET @g2 = geometry::STGeomFromText('CIRCULARSTRING(0 0, 2 2, 4 0)', 0);  
SELECT @g1.STLength() AS [LS Length], @g2.STLength() AS [CS Length];  
```  
  
 이 조각은 다음 결과를 생성합니다.  
  
```  
LS LengthCS Length  
5.65685…6.28318…  
```  
  
 다음 그림은 각 형식이 저장 되는 방법을 보여 줍니다 (빨간색 선은 `LineString``@g1`을 나타내고 파란색 선은 `CircularString``@g2`):  
  
 ![](../../database-engine/media/e52157b5-5160-4a4b-8560-50cdcf905b76.png "e52157b5-5160-4a4b-8560-50cdcf905b76")  
  
 위의 그림과 같이 `CircularString` 인스턴스 사용 하 여 적은 수의 요소가와 정확도 높은 곡선 경계를 저장 `LineString` 인스턴스. `CircularString` 인스턴스는 특정 지점에서 반경 32km 이내 검색과 같이 원 경계를 저장하는 데 유용합니다. `LineString` 인스턴스는 사각형 도시 블록과 같이 선형인 경계를 저장하는 데 유용합니다.  
  
### <a name="linestring-and-compoundcurve-comparison"></a>LineString 및 CompoundCurve 비교  
 다음 코드 예제는 사용 하 여 동일한 그림을 저장 하는 방법을 보여 `LineString` 및 `CompoundCurve` 인스턴스:  
  
```tsql  
SET @g = geometry::Parse('LINESTRING(2 2, 4 2, 4 4, 2 4, 2 2)');  
SET @g = geometry::Parse('COMPOUNDCURVE((2 2, 4 2), (4 2, 4 4), (4 4, 2 4), (2 4, 2 2))');  
SET @g = geometry::Parse('COMPOUNDCURVE((2 2, 4 2, 4 4, 2 4, 2 2))');  
```  
  
 로 구분하거나 여러  
  
 위 예제에는 `LineString` 인스턴스 또는 `CompoundCurve` 인스턴스는 그림을 저장할 수 있습니다.  사용 하는 다음 예제는 `CompoundCurve` 원형 조각을 저장 하려면:  
  
```tsql  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(2 2, 1 3, 0 2),(0 2, 1 0, 2 2))');  
```  
  
 A `CompoundCurve` 인스턴스 직접 저장할 수는 원호 세그먼트 (2 2, 1 3, 0 2) 반면는 `LineString` 인스턴스는 곡선을 몇 개의 작은 선 세그먼트로 변환 해야 합니다.  
  
### <a name="circularstring-and-compoundcurve-comparison"></a>CircularString 및 CompoundCurve 비교  
 다음 코드 예제에서는 `CircularString` 인스턴스에 원형 조각을 저장하는 방법을 보여 줍니다.  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CIRCULARSTRING( 0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)');  
SELECT @g.ToString(), @g.STLength();  
```  
  
 `CircularString` 인스턴스를 사용하여 원형 조각을 저장하려면 각 선 세그먼트에 세 개의 점을 사용해야 합니다.  중간 점을 알 수 없으면 다음 조각과 같이 선 세그먼트의 끝점을 계산하거나 따옴표로 묶어야 합니다.  
  
```tsql  
SET @g = geometry::Parse('CIRCULARSTRING( 0 0, 3 6.3246, 3 6.3246, 0 7, -3 6.3246, 0 0, 0 0)');  
```  
  
 `CompoundCurve` 인스턴스를 둘 다 `LineString` 및 `CircularString` 구간이 필요한 원형 조각의 선 세그먼트를 가리키도록 하는 두 개의 구성 요소입니다.  사용 하는 방법을 보여 주는 코드 예제는 `CompoundCurve` 동일한 그림을 저장 하려면:  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING( 3 6.3246, 0 7, -3 6.3246), (-3 6.3246, 0 0, 3 6.3246))');  
SELECT @g.ToString(), @g.STLength();  
```  
  
### <a name="polygon-and-curvepolygon-comparison"></a>Polygon 및 CurvePolygon 비교  
 `CurvePolygon` 인스턴스는 사용할 `CircularString` 및 `CompoundCurve` 인스턴스는 외부 및 내부 링을 정의할 때.  `Polygon` 인스턴스는 원호 세그먼트 유형을 사용할 수 없습니다: `CircularString` 및 `CompoundCurve`합니다.  
  
  
## <a name="see-also"></a>관련 항목  
 [공간 데이터&#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md)   
 [geometry 데이터 형식 메서드 참조](/sql/t-sql/spatial-geometry/spatial-types-geometry-transact-sql)   
 [geography 데이터 형식 메서드 참조](/sql/t-sql/spatial-geography/spatial-types-geography)   
 [STNumCurves &#40;geometry 데이터 형식&#41;](/sql/t-sql/spatial-geometry/stnumcurves-geometry-data-type)   
 [STNumCurves &#40;geography 데이터 형식&#41;](/sql/t-sql/spatial-geography/stnumcurves-geography-data-type)   
 [STGeomFromText &#40;geometry 데이터 형식&#41;](/sql/t-sql/spatial-geometry/stgeomfromtext-geometry-data-type)   
 [STGeomFromText&#40;geography 데이터 형식&#41;](/sql/t-sql/spatial-geography/stgeomfromtext-geography-data-type)  
  
  
