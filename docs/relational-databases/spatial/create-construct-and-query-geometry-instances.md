---
title: geometry 인스턴스 만들기, 구성 및 쿼리 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: spatial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- planar spatial data [SQL Server], getting started
- geometry data type [SQL Server], getting started
ms.assetid: c6b5c852-37d2-48d0-a8ad-e43bb80d6514
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 236a8f0c292e6bc491d84ae4532509e345713b37
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32973388"
---
# <a name="create-construct-and-query-geometry-instances"></a>geometry 인스턴스 만들기, 구성 및 쿼리
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  평면 공간 데이터 형식 **geometry**는 유클리드(평면) 좌표계의 데이터를 나타냅니다. 이 형식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 CLR(공용 언어 런타임) 데이터 형식으로 구현됩니다.  
  
 **geometry** 형식은 각 데이터베이스에서 미리 정의되고 사용할 수 있습니다. 다른 CLR 형식을 사용할 때와 동일한 방식으로 **geometry** 형식의 테이블 열을 만들고 **geometry** 데이터에 대한 작업을 수행할 수 있습니다.  
  
 **에서 지원되는** geometry [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식(평면)은 OGC(Open Geospatial Consortium) Simple Features for SQL Specification 버전 1.1.0을 따릅니다.  
  
 OGC 사양에 대한 자세한 내용은 다음을 참조하십시오.  
  
-   [OGC Specifications, Simple Feature Access Part 1 - Common Architecture](http://go.microsoft.com/fwlink/?LinkId=93628)  
  
-   [OGC Specifications, Simple Feature Access Part 2 - SQL Options](http://go.microsoft.com/fwlink/?LinkId=93629)  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 [http://schemas.microsoft.com/sqlserver/profiles/gml/SpatialGML.xsd](http://go.microsoft.com/fwlink/?LinkId=230959) 스키마에 정의된 기존 GML 3.1 표준의 하위 집합을 지원합니다.  
  
##  <a name="creating"></a> 새 geometry 인스턴스 만들기 또는 구성  
  
###  <a name="existing"></a> 기존 인스턴스에서 새 geometry 인스턴스 만들기  
 **geometry** 데이터 형식은 수많은 기본 메서드를 제공합니다. 이러한 메서드를 사용하여 기존 인스턴스를 기반하여 새 **geometry** 인스턴스를 만들 수 있습니다.  
  
 **geometry 버퍼를 만들려면**  
 [STBuffer&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stbuffer-geometry-data-type.md)  
  
 [BufferWithTolerance&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type.md)  
  
 **간단한 geometry 버전을 만들려면**  
 [Reduce&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/reduce-geometry-data-type.md)  
  
 **geometry의 네 점을 만들려면**  
 [STConvexHull&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stconvexhull-geometry-data-type.md)  
  
 **두 geometry의 교집합에서 geometry를 만들려면**  
 [STIntersection&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stintersection-geometry-data-type.md)  
  
 **두 geometry의 합집합에서 geometry를 만들려면**  
 [STUnion&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stunion-geometry-data-type.md)  
  
 **한 geometry가 다른 geometry와 겹치지 않는 점에서 geometry를 만들려면**  
 [STDifference&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stdifference-geometry-data-type.md)  
  
 **두 geometry가 겹치지 않는 점에서 geometry를 만들려면**  
 [STSymDifference&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stsymdifference-geometry-data-type.md)  
  
 **기존 geometry에 있는 임의의 Point 인스턴스를 만들려면**  
 [STPointOnSurface&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stpointonsurface-geometry-data-type.md)  
  
  
###  <a name="wkt"></a> WKT 입력에서 geometry 인스턴스 구성  
 **geometry** 데이터 형식은 OGC(Open Geospatial Consortium) WKT 표현에서 기하 도형을 생성하는 여러 가지 기본 메서드를 제공합니다. WKT 표준은 기하 도형 데이터를 텍스트 형식으로 교환할 수 있는 텍스트 문자열입니다.  
  
 **WKT 입력에서 모든 유형의 geometry 인스턴스를 생성하려면**  
 [STGeomFromText&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stgeomfromtext-geometry-data-type.md)  
  
 [Parse&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/parse-geometry-data-type.md)  
  
 **WKT 입력에서 기하 도형 Point 인스턴스를 생성하려면**  
 [STPointFromText&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stpointfromtext-geometry-data-type.md)  
  
 **WKT 입력에서 기하 도형 MultiPoint 인스턴스를 생성하려면**  
 [STMPointFromText&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stmpointfromtext-geometry-data-type.md)  
  
 **WKT 입력에서 기하 도형 LineString 인스턴스를 생성하려면**  
 [STLineFromText&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stlinefromtext-geometry-data-type.md)  
  
 **WKT 입력에서 기하 도형 MultiLineString 인스턴스를 생성하려면**  
 [STMLineFromText&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stmlinefromtext-geometry-data-type.md)  
  
 **WKT 입력에서 기하 도형 Polygon 인스턴스를 생성하려면**  
 [STPolyFromText&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stpolyfromtext-geometry-data-type.md)  
  
 **WKT 입력에서 기하 도형 MultiPolygon 인스턴스를 생성하려면**  
 [STMPolyFromText&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stmpolyfromtext-geometry-data-type.md)  
  
 **WKT 입력에서 기하 도형 GeometryCollection 인스턴스를 생성하려면**  
 [STGeomCollFromText&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stgeomcollfromtext-geometry-data-type.md)  
  
  
###  <a name="wkb"></a> WKB 입력에서 geometry 인스턴스 구성  
 WKB는 OGC(Open Geospatial Consortium)에서 지정한 이진 형식으로, 클라이언트 응용 프로그램과 SQL 데이터베이스 간에 **geometry** 데이터를 교환하도록 허용합니다. 다음 함수는 WKB 입력을 사용하여 기하 도형을 생성합니다.  
  
 **WKB 입력에서 모든 유형의 geometry 인스턴스를 생성하려면**  
 [STGeomFromWKB&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stgeomfromwkb-geometry-data-type.md)  
  
 **WKB 입력에서 기하 도형 Point 인스턴스를 생성하려면**  
 [STPointFromWKB&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stpointfromwkb-geometry-data-type.md)  
  
 **WKB 입력에서 기하 도형 MultiPoint 인스턴스를 생성하려면**  
 [STMPointFromWKB&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stmpointfromwkb-geometry-data-type.md)  
  
 **WKB 입력에서 기하 도형 LineString 인스턴스를 생성하려면**  
 [STLineFromWKB&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stlinefromwkb-geometry-data-type.md)  
  
 **WKB 입력에서 기하 도형 MultiLineString 인스턴스를 생성하려면**  
 [STMLineFromWKB&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stmlinefromwkb-geometry-data-type.md)  
  
 **WKB 입력에서 기하 도형 Polygon 인스턴스를 생성하려면**  
 [STPolyFromWKB&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stpolyfromwkb-geometry-data-type.md)  
  
 **WKB 입력에서 기하 도형 MultiPolygon 인스턴스를 생성하려면**  
 [STMPolyFromWKB&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stmpolyfromwkb-geometry-data-type.md)  
  
 **WKB 입력에서 기하 도형 GeometryCollection 인스턴스를 생성하려면**  
 [STGeomCollFromWKB&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stgeomcollfromwkb-geometry-data-type.md)  
  
  
###  <a name="gml"></a> GML 텍스트 입력에서 geometry 인스턴스 구성  
 **geometry** 데이터 형식은 기하학적 개체의 XML 표현인 GML에서 **geometry** 인스턴스를 생성하는 메서드를 제공합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 GML 하위 집합을 지원합니다.  
  
 **GML 입력에서 모든 유형의 geometry 인스턴스를 생성하려면**  
 [GeomFromGml&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/geomfromgml-geometry-data-type.md)  
  
  
##  <a name="returning"></a> geometry 인스턴스에서 WKT 및 WKB 반환  
 다음 메서드를 사용하여 **geometry** 인스턴스의 WKT 또는 WKB 형식을 반환할 수 있습니다.  
  
 **geometry 인스턴스의 WKT 표현을 반환하려면**  
 [STAsText&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stastext-geometry-data-type.md)  
  
 [ToString&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/tostring-geometry-data-type.md)  
  
 **Z 및 M 값을 포함하여 geometry 인스턴스의 WKT 표현을 반환하려면**  
 [AsTextZM&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/astextzm-geometry-data-type.md)  
  
 **geometry 인스턴스의 WKB 표현을 반환하려면**  
 [STAsBinary&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stasbinary-geometry-data-type.md)  
  
 **geometry 인스턴스의 GML 표현을 반환하려면**  
 [AsGml&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/asgml-geometry-data-type.md)  
  
  
##  <a name="querying"></a> geometry 인스턴스의 속성 및 동작 쿼리  
 모든 **geometry** 인스턴스에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 제공하는 메서드를 통해 검색할 수 있는 여러 속성이 있습니다. 다음 항목에서는 기하 도형 형식의 속성과 동작 및 각각을 쿼리하는 메서드를 정의합니다.  
  
###  <a name="valid"></a> 유효성, 인스턴스 유형 및 GeometryCollection 정보  
 **geometry** 인스턴스가 생성되면 다음 메서드를 사용하여 이 인스턴스가 잘 구성된 경우 인스턴스 유형을 반환하는지 또는 컬렉션 인스턴스일 경우 특정 **geometry** 인스턴스를 반환하는지를 확인할 수 있습니다.  
  
 **geometry 인스턴스 유형을 반환하려면**  
 [STGeometryType&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)  
  
 **기하 도형이 지정된 인스턴스 유형인지 확인하려면**  
 [InstanceOf&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/instanceof-geometry-data-type.md)  
  
 **geometry 인스턴스가 해당 인스턴스 유형에 대해 형식이 올바른지 확인하려면**  
 [STIsValid&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)  
  
 **geometry 인스턴스를 인스턴스 유형이 있는 올바른 형식의 geometry 인스턴스로 변환하려면**  
 [MakeValid&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/makevalid-geometry-data-type.md)  
  
 **기하 도형 컬렉션 인스턴스에 있는 기하 도형의 개수를 반환하려면**  
 [STNumGeometries&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stnumgeometries-geometry-data-type.md)  
  
 기하 도형 컬렉션 인스턴스에서 특정 기하 도형을 반환하려면  
 [STGeometryN&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stgeometryn-geometry-data-type.md)STGeometryN(geometry 데이터 형식)  
  
  
###  <a name="number"></a> 점 수  
 모든 비어 있지 않은 **geometry** 인스턴스는 *점*으로 구성됩니다. 이러한 점은 기하 도형이 그려지는 평면의 X 및 Y 좌표를 나타냅니다. **geometry** 는 인스턴스의 점을 쿼리하는 데 필요한 수많은 기본 메서드를 제공합니다.  
  
 **인스턴스를 구성하는 점 개수를 반환하려면**  
 [STNumPoints&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stnumpoints-geometry-data-type.md)  
  
 **인스턴스의 특정 점을 반환하려면**  
 [STPointN](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md)  
  
 **인스턴스에 있는 임의의 점을 반환하려면**  
 [STPointOnSurface](../../t-sql/spatial-geometry/stpointonsurface-geometry-data-type.md)  
  
 **인스턴스의 시작점을 반환하려면**  
 [STStartPoint](../../t-sql/spatial-geometry/ststartpoint-geometry-data-type.md)  
  
 **인스턴스의 끝점을 반환하려면**  
 [STEndpoint](../../t-sql/spatial-geometry/stendpoint-geometry-data-type.md)  
  
 **Point 인스턴스의 X 좌표를 반환하려면**  
 [STX&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stx-geometry-data-type.md)  
  
 **Point 인스턴스의 Y 좌표를 반환하려면**  
 [STY](../../t-sql/spatial-geometry/sty-geometry-data-type.md)  
  
 **Polygon, CurvePolygon 또는 MultiPolygon 인스턴스의 기하학적 중심점을 반환하려면**  
 [STCentroid](../../t-sql/spatial-geometry/stcentroid-geometry-data-type.md)  
  
  
###  <a name="dimension"></a> 차원  
 비어 있지 않은 **geometry** 인스턴스는 0, 1 또는 2차원이 될 수 있습니다. **Point**및 **MultiPoint** 와 같은 0차원 **geometry**에는 길이 또는 영역이 없습니다. **LineString, CircularString, CompoundCurve**및 **MultiLineString**과 같은 1차원 개체에는 길이가 있습니다. **Polygon**, **CurvePolygon**및 **MultiPolygon**과 같은 2차원 인스턴스에는 영역과 길이가 있습니다. 비어 있는 인스턴스에서는 -1차원을 보고하고 **GeometryCollection** 에서는 해당 내용의 유형에 따라 다른 영역을 보고합니다.  
  
 **인스턴스의 차원을 반환하려면**  
 [STDimension](../../t-sql/spatial-geometry/stdimension-geometry-data-type.md)  
  
 **인스턴스의 길이를 반환하려면**  
 [STLength](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)  
  
 **인스턴스의 영역을 반환하려면**  
 [STArea](../../t-sql/spatial-geometry/starea-geometry-data-type.md)  
  
  
###  <a name="empty"></a> 비어 있음  
 *empty***geometry** 인스턴스에는 점이 하나도 없습니다. 비어 있는 **LineString, CircularString**, **CompoundCurve**및 **MultiLineString** 인스턴스의 길이는 0입니다. 비어 있는 **Polygon**, **CurvePolygon**및 **MultiPolygon** 인스턴스의 영역은 0입니다.  
  
 **인스턴스가 비어 있는지 확인하려면**  
 [STIsEmpty](../../t-sql/spatial-geometry/stisempty-geometry-data-type.md).  
  
  
###  <a name="simple"></a> 간단  
 **geometry** 인스턴스가 *단순*할 경우 다음 요구 사항을 모두 충족해야 합니다.  
  
-   인스턴스의 각 도형은 끝점을 제외하고 자체 교차해서는 안 됩니다.  
  
-   인스턴스의 도형 두 개가 양쪽의 경계가 아닌 점에서는 서로 교차하지 않아야 합니다.  
  
> [!NOTE]  
>  비어 있는 기하 도형은 항상 단순합니다.  
  
 **인스턴스가 단순한지 확인하려면**  
 [STIsEmpty](../../t-sql/spatial-geometry/stissimple-geometry-data-type.md).  
  
  
###  <a name="boundary"></a> 경계, 내부 및 외부  
 *geometry* 인스턴스의 **내부** 는 인스턴스가 차지하는 공간이고 *외부* 는 해당 인스턴스가 차지하지 않는 공간입니다.  
  
 *경계* 는 다음과 같이 OGC에 의해 정의됩니다.  
  
-   **Point** 및 **MultiPoint** 인스턴스에는 경계가 없습니다.  
  
-   **LineString** 및 **MultiLineString** 경계는 시작점과 끝점으로 구성되며 짝수 횟수에 발생하는 시작점과 끝점은 제거됩니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 1, 0 0, 1 0, 0 1), (1 1, 1 0))');  
SELECT @g.STBoundary().ToString();  
```  
  
 **Polygon** 또는 **MultiPolygon** 인스턴스의 경계는 해당 인스턴스 링의 집합입니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0), (1 1, 1 2, 2 2, 2 1, 1 1))');  
SELECT @g.STBoundary().ToString();  
```  
  
 **인스턴스의 경계를 반환하려면**  
 [STBoundary](../../t-sql/spatial-geometry/stboundary-geometry-data-type.md)  
  
  
###  <a name="envelope"></a> 봉투  
 *geometry* 인스턴스의 **봉투** 는 *경계 상자*로도 알려져 있으며 해당 인스턴스의 최대 및 최소 (X, Y) 좌표로 구성되는 축에 맞춰진 사각형입니다.  
  
 **인스턴스의 봉투를 반환하려면**  
 [STEnvelope](../../t-sql/spatial-geometry/stenvelope-geometry-data-type.md)  
  
  
###  <a name="closure"></a> 닫힘  
 *closed***geometry** 인스턴스는 시작점과 끝점이 같은 도형입니다. **Polygon** 인스턴스는 닫혀 있다고 간주되며, **Point** 인스턴스는 닫혀 있지 않습니다.  
  
 링은 단순하고 닫혀 있는 **LineString** 인스턴스입니다.  
  
 **인스턴스가 닫혀 있는지 확인하려면**  
 [STIsClosed](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)  
  
 **인스턴스가 링인지 확인하려면**  
 [STIsRing](../../t-sql/spatial-geometry/stisring-geometry-data-type.md)  
  
 **Polygon 인스턴스의 외부 링을 반환하려면**  
 [STExteriorRing](../../t-sql/spatial-geometry/stexteriorring-geometry-data-type.md)  
  
 **Polygon에 있는 내부 링의 개수를 반환하려면**  
 [STNumInteriorRing](../../t-sql/spatial-geometry/stnuminteriorring-geometry-data-type.md)  
  
 **Polygon에 지정된 내부 링을 반환하려면**  
 [STInteriorRingN](../../t-sql/spatial-geometry/stinteriorringn-geometry-data-type.md)  
  
  
###  <a name="srid"></a> SRID(Spatial Reference ID)  
 SRID는 **geometry** 인스턴스를 나타내는 좌표계를 지정하는 식별자입니다. 다른 SRID를 사용하는 두 인스턴스는 서로 비교할 수 없습니다.  
  
 **인스턴스의 SRID를 설정하거나 반환하려면**  
 [STSrid](../../t-sql/spatial-geometry/stsrid-geometry-data-type.md)  
  
 이 속성은 수정할 수 있습니다.  
  
  
##  <a name="rel"></a> geometry 인스턴스 간 관계 확인  
 **geometry** 데이터 형식은 수많은 기본 메서드를 제공합니다. 이러한 메서드를 사용하여 두 개의 **geometry** 인스턴스 간 관계를 확인할 수 있습니다.  
  
 **두 인스턴스가 동일한 점 집합으로 구성되었는지 확인하려면**  
 [STEquals](../../t-sql/spatial-geometry/stequals-geometry-data-type.md)  
  
 **두 인스턴스가 결합되지 않았는지 확인하려면**  
 [STDisjoint](../../t-sql/spatial-geometry/stdisjoint-geometry-data-type.md)  
  
 **두 인스턴스가 교차하는지 확인하려면**  
 [STIntersects](../../t-sql/spatial-geometry/stintersects-geometry-data-type.md)  
  
 **두 인스턴스가 액세스하는지 확인하려면**  
 [STTouches](../../t-sql/spatial-geometry/sttouches-geometry-data-type.md)  
  
 **두 인스턴스가 겹치는지 확인하려면**  
 [STOverlaps](../../t-sql/spatial-geometry/stoverlaps-geometry-data-type.md)  
  
 **두 인스턴스가 상호 교차하는지 확인하려면**  
 [STCrosses](../../t-sql/spatial-geometry/stcrosses-geometry-data-type.md)  
  
 **한 인스턴스가 다른 인스턴스 내에 있는지 확인하려면**  
 [STWithin](../../t-sql/spatial-geometry/stwithin-geometry-data-type.md)  
  
 **한 인스턴스에 다른 인스턴스가 있는지 확인하려면**  
 [STContains](../../t-sql/spatial-geometry/stcontains-geometry-data-type.md)  
  
 **한 인스턴스가 다른 인스턴스를 겹치는지 확인하려면**  
 [STOverlaps](../../t-sql/spatial-geometry/stoverlaps-geometry-data-type.md)  
  
 **두 인스턴스가 공간적으로 관련되어 있는지 확인하려면**  
 [STRelate](../../t-sql/spatial-geometry/strelate-geometry-data-type.md)  
  
 **두 geometry의 점 간 최단 길이를 확인하려면**  
 [STDistance](../../t-sql/spatial-geometry/stdistance-geometry-data-type.md)  
  
  
##  <a name="defaultsrid"></a> geometry 인스턴스의 기본값을 SRID 0으로 설정  
 **에서** geometry [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 기본 SRID는 0입니다. **geometry** 공간 데이터를 사용하면 계산을 수행하는 데 공간 인스턴스의 특정 SRID가 필요하지 않으므로 인스턴스가 정의되지 않은 평면 공간에 존재할 수 있습니다. **geometry** 데이터 형식 메서드의 계산에서 정의되지 않은 평면 공간을 나타내려면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 에서는 SRID 0을 사용합니다.  
  
##  <a name="examples"></a> 예  
 다음 두 예에서는 geometry 데이터를 추가하고 쿼리하는 방법을 보여 줍니다.  
  
-   첫 번째 예에서는 ID 열과 `geometry` 열 `GeomCol1`이 있는 테이블을 만듭니다. 세 번째 열에서는 `geometry` 열을 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현으로 렌더링하고 `STAsText()` 메서드를 사용합니다. 그러고 나면 두 개의 행이 삽입됩니다. 이 중 한 행에는 `LineString` 의 `geometry`인스턴스가 들어 있고, 다른 행에는 `Polygon` 인스턴스가 들어 있습니다.  
  
    ```  
    IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
        DROP TABLE dbo.SpatialTable;  
    GO  
  
    CREATE TABLE SpatialTable   
        ( id int IDENTITY (1,1),  
        GeomCol1 geometry,   
        GeomCol2 AS GeomCol1.STAsText() );  
    GO  
  
    INSERT INTO SpatialTable (GeomCol1)  
    VALUES (geometry::STGeomFromText('LINESTRING (100 100, 20 180, 180 180)', 0));  
  
    INSERT INTO SpatialTable (GeomCol1)  
    VALUES (geometry::STGeomFromText('POLYGON ((0 0, 150 0, 150 150, 0 150, 0 0))', 0));  
    GO  
    ```  
  
-   두 번째 예에서는 `STIntersection()` 메서드를 사용하여 앞서 삽입한 두 `geometry` 인스턴스가 교차하는 지점을 반환합니다.  
  
    ```  
    DECLARE @geom1 geometry;  
    DECLARE @geom2 geometry;  
    DECLARE @result geometry;  
  
    SELECT @geom1 = GeomCol1 FROM SpatialTable WHERE id = 1;  
    SELECT @geom2 = GeomCol1 FROM SpatialTable WHERE id = 2;  
    SELECT @result = @geom1.STIntersection(@geom2);  
    SELECT @result.STAsText();  
    ```  
  
  
## <a name="see-also"></a>참고 항목  
 [공간 데이터&#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
