---
title: "geography 인스턴스 만들기, 구성 및 쿼리 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- geography data type [SQL Server]
- geodetic data type [SQL Server]
- geography data type [SQL Server], about geography data type
ms.assetid: b585851e-d15b-411f-adeb-aeabeb777c0b
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 13e7519e11e23d73ff22a3f7d420d0fafc132abf
ms.lasthandoff: 04/11/2017

---
# <a name="create-construct-and-query-geography-instances"></a>geography 인스턴스 만들기, 구성 및 쿼리
  지리 공간 데이터 형식인 **geography**는 둥근 표면 좌표계로 데이터를 나타냅니다. 이 형식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 .NET CLR(공용 언어 런타임) 데이터 형식으로 구현됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **geography** 데이터 형식은 GPS 위도 및 경도 좌표 등의 타원(둥근 표면) 데이터를 저장합니다.  
  
 **geography** 형식은 각 데이터베이스에서 미리 정의되고 사용할 수 있습니다. 다른 시스템 제공 형식을 사용할 때와 동일한 방식으로 **geography** 형식의 테이블 열을 만들고 **geography** 데이터에 대한 작업을 수행할 수 있습니다.  
  
##  <a name="creating"></a> 새 지리 인스턴스 만들기 또는 구성  
  
###  <a name="existing"></a> 기존 인스턴스에서 새 지리 인스턴스 만들기  
 **geography** 데이터 형식은 수많은 기본 메서드를 제공합니다. 이러한 메서드를 사용하여 기존 인스턴스를 기반하여 새 **geography** 인스턴스를 만들 수 있습니다.  
  
 **지리의 버퍼를 만들려면**  
 [STBuffer&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stbuffer-geography-data-type.md)  
  
 **허용 오차를 허용하는 지리의 버퍼를 만들려면**  
 [BufferWithTolerance&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/bufferwithtolerance-geography-data-type.md)  
  
 **두 geography 인스턴스의 교집합에서 지리를 만들려면**  
 [STIntersection&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stintersection-geography-data-type.md)  
  
 **두 geography 인스턴스의 합집합에서 지리를 만들려면**  
 [STUnion&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stunion-geography-data-type.md)  
  
 **한 지리가 다른 지리와 겹치지 않는 점에서 지리를 만들려면**  
 [STDifference&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stdifference-geography-data-type.md)  
  
###  <a name="wkt"></a> WKT 입력으로부터 지리 인스턴스 구성  
 **geography** 데이터 형식은 OGC(Open Geospatial Consortium) WKT 표현에서 지리를 생성하는 여러 가지 기본 메서드를 제공합니다. WKT 표준은 지리 데이터를 텍스트 형식으로 교환할 수 있는 텍스트 문자열입니다.  
  
 **WKT 입력으로부터 지리 인스턴스 유형을 구성하려면**  
 [STGeomFromText&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md)  
  
 [Parse&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/parse-geography-data-type.md)  
  
 **WKT 입력으로부터 지리 Point 인스턴스를 구성하려면**  
 [STPointFromText&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stpointfromtext-geography-data-type.md)  
  
 **WKT 입력으로부터 지리 MultiPoint 인스턴스를 구성하려면**  
 [STMPointFromText&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stmpointfromtext-geography-data-type.md)  
  
 **WKT 입력으로부터 지리 LineString 인스턴스를 구성하려면**  
 STLineFromText(geography 데이터 형식)  
  
 **WKT 입력으로부터 지리 MultiLineString 인스턴스를 구성하려면**  
 [STMLineFromText&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stmlinefromtext-geography-data-type.md)  
  
 **WKT 입력으로부터 지리 Polygon 인스턴스를 구성하려면**  
 [STPolyFromText&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stpolyfromtext-geography-data-type.md)  
  
 **WKT 입력으로부터 지리 MultiPolygon 인스턴스를 구성하려면**  
 [STMPolyFromText&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stmpolyfromtext-geography-data-type.md)  
  
 **WKT 입력으로부터 지리 GeometryCollection 인스턴스를 구성하려면**  
 [STGeomCollFromText&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stgeomcollfromtext-geography-data-type.md)  
  
###  <a name="wkb"></a> WKB 입력으로부터 지리 인스턴스 구성  
 WKB는 클라이언트 응용 프로그램과 SQL 데이터베이스 간에 **Geography** 데이터를 교환할 수 있도록 OGC에서 지정하는 이진 형식입니다. 다음 함수는 WKB 입력을 사용하여 geography 인스턴스를 생성합니다.  
  
 **WKB 입력으로부터 지리 인스턴스 유형을 구성하려면**  
 [STGeomFromWKB&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stgeomfromwkb-geography-data-type.md)  
  
 **WKB 입력으로부터 지리 Point 인스턴스를 구성하려면**  
 [STPointFromWKB&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stpointfromwkb-geography-data-type.md)  
  
 **WKB 입력으로부터 지리 MultiPoint 인스턴스를 구성하려면**  
 [STMPointFromWKB&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stmpointfromwkb-geography-data-type.md)  
  
 **WKB 입력으로부터 지리 LineString 인스턴스를 구성하려면**  
 [STLineFromWKB&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stlinefromwkb-geography-data-type.md)  
  
 **WKB 입력으로부터 지리 MultiLineString 인스턴스를 구성하려면**  
 [STMLineFromWKB&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stmlinefromwkb-geography-data-type.md)  
  
 **WKB 입력으로부터 지리 Polygon 인스턴스를 구성하려면**  
 [STPolyFromWKB&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stpolyfromwkb-geography-data-type.md)  
  
 **WKB 입력으로부터 지리 MultiPolygon 인스턴스를 구성하려면**  
 [STMPolyFromWKB&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stmpolyfromwkb-geography-data-type.md)  
  
 **WKB 입력으로부터 지리 GeometryCollection 인스턴스를 구성하려면**  
 [STGeomCollFromWKB&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stgeomcollfromwkb-geography-data-type.md)STGeomCollFromWKB(geography 데이터 형식)  
  
###  <a name="gml"></a> GML 텍스트 입력으로부터 지리 인스턴스 구성  
 **geography** 데이터 형식은 **geography** 인스턴스의 XML 표현인 GML에서 **geography** 인스턴스를 생성하는 메서드를 제공합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 GML 하위 집합을 지원합니다.  
  
 Geography Markup Language에 대한 자세한 내용은 OGC 사양: [OGC 사양, Geography Markup Language](http://go.microsoft.com/fwlink/?LinkId=93629)를 참조하세요.  
  
 **GML 입력으로부터 지리 인스턴스 유형을 구성하려면**  
 [GeomFromGML&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/geomfromgml-geography-data-type.md)  
  
##  <a name="returning"></a> 지리 인스턴스에서 WKT 및 WKB 반환  
 다음 메서드를 사용하여 **geography** 인스턴스의 WKT 또는 WKB 형식을 반환할 수 있습니다.  
  
 **지리 인스턴스의 WKT 표현을 반환하려면**  
 [STAsText&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stastext-geography-data-type.md)  
  
 [ToString&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/tostring-geography-data-type.md)  
  
 **Z 및 M 값을 포함하여 지리 인스턴스의 WKT 표현을 반환하려면**  
 [AsTextZM&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/astextzm-geography-data-type.md)  
  
 **지리 인스턴스의 WKB 표현을 반환하려면**  
 [STAsBinary&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stasbinary-geography-data-type.md)  
  
 **지리 인스턴스의 GML 표현을 반환하려면**  
 [AsGml&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/asgml-geography-data-type.md)  
  
##  <a name="query"></a> 지리 인스턴스의 속성 및 동작 쿼리  
 모든 **geography** 인스턴스에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 제공하는 메서드를 통해 검색할 수 있는 여러 속성이 있습니다. 다음 항목에서는 geography 형식의 속성과 동작 및 각각을 쿼리하는 메서드를 정의합니다.  
  
###  <a name="valid"></a> 유효성, 인스턴스 유형 및 GeometryCollection 정보  
 **geography** 인스턴스를 구성한 후 다음과 같은 방법으로 인스턴스 유형을 반환할 수 있습니다. **GeometryCollection** 인스턴스인 경우 특정 **geography** 인스턴스를 반환할 수 있습니다.  
  
 **geography 인스턴스 유형을 반환하려면**  
 [STGeometryType&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md)  
  
 **지리가 지정된 인스턴스 유형인지 확인하려면**  
 [InstanceOf&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/instanceof-geography-data-type.md)  
  
 **geography 인스턴스가 해당 인스턴스 유형에 대해 형식이 올바른지 확인하려면**  
 [STNumGeometries&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stnumgeometries-geography-data-type.md)  
  
 **GeometryCollection 인스턴스에서 특정 지리를 반환하려면**  
 [STGeometryN&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stgeometryn-geography-data-type.md)STGeometryN(geography 데이터 형식)  
  
###  <a name="number"></a> 점 수  
 모든 비어 있지 않은 **geography** 인스턴스는 *점*으로 구성됩니다. 이러한 점은 **geography** 인스턴스가 그려지는 지구의 위도 및 경도 좌표를 나타냅니다. **geography** 데이터 형식은 인스턴스의 점을 쿼리하는 데 필요한 수많은 기본 메서드를 제공합니다.  
  
 **인스턴스를 구성하는 점 개수를 반환하려면**  
 [STNumPoints&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stnumpoints-geography-data-type.md)  
  
 **인스턴스의 특정 점을 반환하려면**  
 [STPointN&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md)  
  
 **인스턴스의 시작점을 반환하려면**  
 [STStartPoint&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/ststartpoint-geography-data-type.md)  
  
 **인스턴스의 끝점을 반환하려면**  
 [STEndpoint&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stendpoint-geography-data-type.md)  
  
###  <a name="dimension"></a> 차원  
 비어 있지 않은 **geography** 인스턴스는 0, 1 또는 2차원이 될 수 있습니다. **Point** 및 **MultiPoint** 와 같은 0차원 **geography**인스턴스에는 길이 또는 영역이 없습니다. **LineString, CircularString**, **CompoundCurve**및 **MultiLineString**과 같은 1차원 개체에는 길이가 있습니다. **Polygon, CurvePolygon**및 **MultiPolygon**과 같은 2차원 인스턴스에는 영역과 길이가 있습니다. 비어 있는 인스턴스에서는 -1차원을 보고하고 **GeometryCollection** 에서는 해당 내용의 최대 차원을 보고합니다.  
  
 **인스턴스의 차원을 반환하려면**  
 [STDimension&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stdimension-geography-data-type.md)  
  
 **인스턴스의 길이를 반환하려면**  
 [STLength&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stlength-geography-data-type.md)  
  
 **인스턴스의 영역을 반환하려면**  
 [STArea&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/starea-geography-data-type.md)  
  
###  <a name="empty"></a> 비어 있음  
 *비어 있는***geography** 인스턴스에는 점이 하나도 없습니다. 비어 있는 **LineString, CircularString**, **CompoundCurve**및 **MultiLineString** 인스턴스의 길이는 0입니다. 비어 있는 **Polygon, CurvePolygon** 및 **MultiPolygon** 인스턴스의 영역은 0입니다.  
  
 **인스턴스가 비어 있는지 확인하려면**  
 [STIsEmpty&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stisempty-geography-data-type.md)  
  
###  <a name="closure"></a> 닫힘  
 *닫혀 있는***geography** 인스턴스는 시작점과 끝점이 같은 도형입니다. **Polygon** 인스턴스는 닫혀 있다고 간주되며, **Point** 인스턴스는 닫혀 있지 않습니다.  
  
 링은 단순하고 닫혀 있는 **LineString** 인스턴스입니다.  
  
 **인스턴스가 닫혀 있는지 확인하려면**  
 [STIsClosed&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stisclosed-geography-data-type.md)  
  
 **Polygon 인스턴스에 있는 내부 링의 개수를 반환하려면**  
 [NumRings&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/numrings-geography-data-type.md)  
  
 **geography 인스턴스에 지정된 링을 반환하려면**  
 [RingN&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/ringn-geography-data-type.md)  
  
###  <a name="srid"></a> SRID(Spatial Reference ID)  
 SRID(Spatial Reference ID)는 **geography** 인스턴스를 나타내는 타원 좌표계를 지정하는 식별자입니다. 다른 SRID를 사용하는 두 **geography** 인스턴스는 서로 비교할 수 없습니다.  
  
 **인스턴스의 SRID를 설정하거나 반환하려면**  
 [STSrid&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stsrid-geography-data-type.md)  
  
 이 속성은 수정할 수 있습니다.  
  
##  <a name="rel"></a> 지리 인스턴스 간 관계 확인  
 **geography** 데이터 형식은 수많은 기본 메서드를 제공합니다. 이러한 메서드를 사용하여 두 개의 **geography** 인스턴스 간 관계를 확인할 수 있습니다.  
  
 **두 인스턴스가 동일한 점 집합으로 구성되었는지 확인하려면**  
 [STEquals&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stequals-geometry-data-type.md)  
  
 **두 인스턴스가 결합되지 않았는지 확인하려면**  
 [STDisjoint&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stdisjoint-geometry-data-type.md)  
  
 **두 인스턴스가 교차하는지 확인하려면**  
 [STIntersects&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stintersects-geometry-data-type.md)  
  
 **두 인스턴스가 교차하는 점을 확인하려면**  
 [STIntersection&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stintersection-geography-data-type.md)  
  
 **두 geography 인스턴스의 점 간 최단 길이를 확인하려면**  
 [STDistance&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stdistance-geometry-data-type.md)  
  
 **두 geography 인스턴스 간 점의 차이를 확인하려면**  
 [STDifference&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stdifference-geography-data-type.md)  
  
 **한 개의 지리 인스턴스를 다른 인스턴스와 비교하여 대칭 차이 또는 고유 점을 파생하려면**  
 [STSymDifference&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stsymdifference-geography-data-type.md)  
  
##  <a name="supportedsrid"></a> 지원되는 SRID를 사용해야 하는 geography 인스턴스  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 EPSG 표준을 기준으로 하는 SRID를 지원합니다. 계산을 수행하거나 지리 공간 데이터가 있는 메서드를 사용할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]geography **인스턴스에** 지원 SRID가 사용되어야 합니다. SRID는 **sys.spatial_reference_systems** 카탈로그 뷰에 표시된 SRID 중 하나와 일치해야 합니다. 앞에서 설명한 대로 각 타원면에는 특정 SRID가 지정되므로 **geography** 데이터 형식을 사용하여 공간 데이터에서 계산을 수행할 경우 데이터를 만드는 데 사용된 타원면에 따라 결과가 달라집니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 메서드를 사용할 경우 **geography** 인스턴스 간 관계를 확인할 수 있습니다. WGS 84(또는 SRID 4326)가 아닌 공간 참조 시스템의 데이터를 사용할 경우 지리 공간 데이터에 대해 특정 SRID를 결정해야 합니다.  
  
##  <a name="examples"></a> 예  
 다음 예에서는 geography 데이터를 추가하고 쿼리하는 방법을 보여 줍니다.  
  
-   첫 번째 예에서는 ID 열과 `geography` 열 `GeogCol1`이 있는 테이블을 만듭니다. 세 번째 열에서는 `geography` 열을 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현으로 렌더링하고 `STAsText()` 메서드를 사용합니다. 그러고 나면 두 개의 행이 삽입됩니다. 이 중 한 행에는 `LineString` 의 `geography`인스턴스가 들어 있고, 다른 행에는 `Polygon` 인스턴스가 들어 있습니다.  
  
    ```  
    IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
        DROP TABLE dbo.SpatialTable;  
    GO  
  
    CREATE TABLE SpatialTable   
        ( id int IDENTITY (1,1),  
        GeogCol1 geography,   
        GeogCol2 AS GeogCol1.STAsText() );  
    GO  
  
    INSERT INTO SpatialTable (GeogCol1)  
    VALUES (geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326));  
  
    INSERT INTO SpatialTable (GeogCol1)  
    VALUES (geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326));  
    GO  
    ```  
  
-   두 번째 예에서는 `STIntersection()` 메서드를 사용하여 앞서 삽입한 두 `geography` 인스턴스가 교차하는 지점을 반환합니다.  
  
    ```  
    DECLARE @geog1 geography;  
    DECLARE @geog2 geography;  
    DECLARE @result geography;  
  
    SELECT @geog1 = GeogCol1 FROM SpatialTable WHERE id = 1;  
    SELECT @geog2 = GeogCol1 FROM SpatialTable WHERE id = 2;  
    SELECT @result = @geog1.STIntersection(@geog2);  
    SELECT @result.STAsText();  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [공간 데이터&#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
