---
title: 공간 데이터 형식 사용 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f133fa066ef2c486cf7bb40c5b653c99e077bc46
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69026937"
---
# <a name="using-spatial-datatypes"></a>공간 데이터 형식 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

공간 데이터 형식(기하 도형 및 지리)은 JDBC 드라이버 미리 보기 릴리스 6.5.0부터 지원됩니다. 공간 데이터 형식은 현재 저장 프로시저, TVP(Table Valued Parameters), BulkCopy 및 Always Encrypted에서 지원되지 않습니다. 이 페이지에서는 JDBC 드라이버를 사용하여 기하 도형 및 지리 데이터 형식의 다양한 사용 사례를 보여 줍니다. 공간 데이터 형식에 대한 개요는 [공간 데이터 형식 개요](https://docs.microsoft.com/sql/relational-databases/spatial/spatial-data-types-overview) 페이지를 참조하세요.

## <a name="creating-a-geometry--geography-object"></a>기하 도형/지리 개체 만들기

기하 도형/지리 개체를 만드는 두 가지 주요 방법은 WKT(Well-Known Text)에서 변환하거나 WKB(Well-Known Binary)로 변환하는 것입니다.

### <a name="creating-from-wkt"></a>WKT에서 만들기

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
Geography geogWKT = Geography.STGeomFromText(geoWKT, 4326);
```

SRID(Spatial Reference System Identifier)가 0인 LINESTRING 기하 도형 개체와 SRID 4326이 있는 지리 개체가 생성됩니다.

### <a name="creating-from-wkb"></a>WKB에서 만들기

```java
byte[] geomWKB = Hex.decodeHex("00000000010403000000000000000000F03F00000000000000000000000000000000000000000000F03F000000000000F0BF000000000000000001000000010000000001000000FFFFFFFF0000000002".toCharArray());
byte[] geogWKB = Hex.decodeHex("E61000000104030000000000000000000000000000000000F03F000000000000F03F00000000000000000000000000000000000000000000F0BF01000000010000000001000000FFFFFFFF0000000002".toCharArray());

Geometry geomWKT = Geometry.deserialize(geomWKB);
Geography geogWKT = Geography.deserialize(geogWKB);
```

이전에 WKT에서 만든 것과 동일한 기하 도형 및 지리 개체가 생성됩니다.

## <a name="working-with-a-geometry--geography-object"></a>기하 도형/지리 개체 작업

사용자에게 다음과 같은 SQL Server 테이블이 있다고 가정합니다.

```sql
CREATE TABLE sampleTable (c1 geometry)  
```

기하 도형 값을 삽입하는 샘플 스크립트는 다음과 같습니다.

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
SQLServerPreparedStatement pstmt = (SQLServerPreparedStatement) connection.prepareStatement("insert into sampleTable values (?)");
pstmt.setGeometry(1, geomWKT);  
pstmt.execute();
```

지리 열을 사용하고 **setGeography()** 메서드를 사용하여 지리에 대해 동일한 작업을 수행할 수 있습니다.

기하 도형/지리 열을 읽으려면 다음을 수행합니다.

```java
try(SQLServerResultSet rs = (SQLServerResultSet)stmt.executeQuery("select * from geomTable")) {
    while(rs.next()){
        rs.getGeometry(1);
    }
}
```

지리 열을 사용하고 **getGeography()** 메서드를 사용하여 지리에 대해 동일한 작업을 수행할 수 있습니다.

## <a name="newly-introduced-apis"></a>새로 도입된 API

**SQLServerPreparedStatement**, **SQLServerResultSet**, **Geometry**, **Geography** 클래스에서 추가로 도입된 새로운 공개 API입니다.

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

|방법|Description|
|:------|:----------|
|void setGeometry(int n, Geometry x)| 지정된 매개 변수를 지정된 microsoft.sql.Geometry 클래스 개체로 설정합니다.
|void setGeography(int n, Geography x)| 지정된 매개 변수를 지정된 microsoft.sql.Geography 클래스 개체로 설정합니다.

### <a name="sqlserverresultset"></a>SQLServerResultSet

|방법|Description|
|:------|:----------|
|Geometry getGeometry(int colunIndex)| 이 ResultSet 개체의 현재 행에서 지정된 열의 값을 Java 프로그래밍 언어의 com.microsoft.sqlserver.jdbc.Geometry 개체로 반환합니다.
|Geometry getGeometry(String columnName)| 이 ResultSet 개체의 현재 행에서 지정된 열의 값을 Java 프로그래밍 언어의 com.microsoft.sqlserver.jdbc.Geometry 개체로 반환합니다.
|Geography getGeography(int colunIndex)| 이 ResultSet 개체의 현재 행에서 지정된 열의 값을 Java 프로그래밍 언어의 com.microsoft.sqlserver.jdbc.Geography 개체로 반환합니다.
|Geography getGeography(String columnName)| 이 ResultSet 개체의 현재 행에서 지정된 열의 값을 Java 프로그래밍 언어의 com.microsoft.sqlserver.jdbc.Geography 개체로 반환합니다.

### <a name="geometry"></a>geometry

|방법|Description|
|:------|:----------|
|Geometry STGeomFromText(String wkt, int SRID)| 인스턴스에서 얻어진 Z(높이) 값 및 M(측정값) 값을 사용하여 보강된 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현의 기하 도형 인스턴스에 대한 생성자입니다.
|Geometry STGeomFromWKB(byte[] wkb)| OGC(Open Geospatial Consortium) WKB(Well-Known Binary) 표현의 기하 도형 인스턴스에 대한 생성자입니다.
|Geometries deserialize(byte[] wkb)| 공간 데이터에 대한 내부 SQL Server 형식의 기하 도형 인스턴스 생성자입니다.
|Geometry parse(String wkt)| OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현의 기하 도형 인스턴스에 대한 생성자입니다. SRID(Spatial Reference Identifier)의 기본값은 0입니다.
|Geometry point(double x, double y, int SRID)| 해당 X 및 Y 값과 SRID(Spatial Reference Identifier)의 지점 인스턴스를 나타내는 기하 도형 인스턴스에 대한 생성자입니다.
|String STAsText()| 기하 도형 인스턴스의 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현을 반환합니다. 이 텍스트에는 인스턴스에서 얻어진 Z(높이) 값 또는 M(측정값) 값이 포함되지 않습니다.
|byte[] STAsBinary()| 기하 도형 인스턴스의 OGC(Open Geospatial Consortium) WKB(Well-Known Binary) 표현을 반환합니다. 이 값에는 인스턴스에서 얻어진 Z값 또는 M값이 포함되지 않습니다.
|byte[] serialize()| 기하 도형 형식의 내부 SQL Server 형식을 나타내는 바이트를 반환합니다.
|boolean hasM()| 개체에 M(측정값) 값이 포함되어 있으면 반환합니다.
|boolean hasZ()| 개체에 Z(높이) 값이 포함되어 있으면 반환합니다.
|Double getX()| X 좌표 값을 반환합니다.
|Double getY()| Y 좌표 값을 반환합니다.
|Double getM()| 개체의 M(측정값) 값을 반환합니다.
|Double getZ()| 개체의 Z(높이) 값을 반환합니다.
|int getSrid()| SRID(Spatial Reference Identifier) 값을 반환합니다.
|boolean isNull()| 기하 도형 개체가 null이면 반환합니다.
|int STNumPoints()| 기하 도형 개체의 포인트 수를 반환합니다.
|String STGeometryType()| geometry 인스턴스로 표현된 OGC(Open Geospatial Consortium) 형식 이름을 반환합니다.
|String asTextZM()| 기하 도형 개체의 WKT(Well-Known Text) 표현을 반환합니다.
|String toString()| 기하 도형 개체의 문자열 표현을 반환합니다.

### <a name="geography"></a>Geography

|방법|Description|
|:------|:----------|
|Geography STGeomFromText(String wkt, int SRID)| 인스턴스에서 얻어진 Z(높이) 값 및 M(측정값) 값을 사용하여 보강된 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현의 지리 인스턴스에 대한 생성자입니다.
|Geography STGeomFromWKB(byte[] wkb)| OGC(Open Geospatial Consortium) WKB(Well-Known Binary) 표현의 지리 인스턴스에 대한 생성자입니다.
|Geography deserialize(byte[] wkb)| 공간 데이터에 대한 내부 SQL Server 형식의 지리 인스턴스 생성자입니다.
|Geography parse(String wkt)| OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현의 지리 인스턴스에 대한 생성자입니다. SRID(Spatial Reference Identifier)의 기본값은 0입니다.
|Geography point(double lon, double lat, int SRID)| 해당 위도 및 경도와 SRID(Spatial Reference Identifier)의 지점 인스턴스를 나타내는 지리 인스턴스에 대한 생성자입니다.
|String STAsText()| 지리 인스턴스의 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현을 반환합니다. 이 텍스트에는 인스턴스에서 얻어진 Z(높이) 값 또는 M(측정값) 값이 포함되지 않습니다.
|byte[] STAsBinary())| 지리 인스턴스의 OGC(Open Geospatial Consortium) WKB(Well-Known Binary) 표현을 반환합니다. 이 값에는 인스턴스에서 얻어진 Z값 또는 M값이 포함되지 않습니다.
|byte[] serialize()| 지리 형식의 내부 SQL Server 형식을 나타내는 바이트를 반환합니다.
|boolean hasM()| 개체에 M(측정값) 값이 포함되어 있으면 반환합니다.
|boolean hasZ()| 개체에 Z(높이) 값이 포함되어 있으면 반환합니다.
|Double getLatitude()| 위도 값을 반환합니다.
|Double getLongitude()| 경도 값을 반환합니다.
|Double getM()| 개체의 M(측정값) 값을 반환합니다.
|Double getZ()| 개체의 Z(높이) 값을 반환합니다.
|int getSrid()| SRID(Spatial Reference Identifier) 값을 반환합니다.
|boolean isNull()| 지리 개체가 null이면 반환합니다.
|int STNumPoints()| 지리 개체의 포인트 수를 반환합니다.
|String STGeographyType()| geography 인스턴스로 표현된 OGC(Open Geospatial Consortium) 형식 이름을 반환합니다.
|String asTextZM()| 지리 개체의 WKT(Well-Known Text) 표현을 반환합니다.
|String toString()| 지리 개체의 문자열 표현을 반환합니다.

## <a name="limitations-of-spatial-datatypes"></a>공간 데이터 형식의 제한 사항

1. 공간 하위 데이터 형식 **CircularString**, **CompoundCurve**, **CurvePolygon**, **FullGlobe**는 SQL Server 2012 이상부터만 지원됩니다.

2. Always Encrypted는 공간 데이터 형식에 사용할 수 없습니다.

3. 저장 프로시저, TVP 및 BulkCopy 작업은 현재 공간 데이터 형식에서 지원되지 않습니다.

## <a name="see-also"></a>참고 항목

[공간 데이터 형식 샘플(JDBC)](../../connect/jdbc/spatial-data-types-sample.md)
