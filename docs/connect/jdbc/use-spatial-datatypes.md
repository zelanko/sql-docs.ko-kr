---
title: 공간 데이터 형식을 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 01/21/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ce3df0755799e907bb286e10f5711a58a48135bb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66782466"
---
# <a name="using-spatial-datatypes"></a>공간 데이터 형식 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

공간 데이터 형식 (Geometry 및 Geography)은 JDBC 드라이버 미리 보기 릴리스에서 6.5.0부터 지원 됩니다. 공간 데이터는 현재 저장된 프로시저, 테이블 반환 매개 변수 (TVP), BulkCopy, 및 상시 암호화를 사용 하 여 지원 되지 않습니다. 이 페이지는 다양 한 Geometry 및 Geography 데이터 형식의 경우 JDBC 드라이버를 사용 하 여 사용 하 여 표시 됩니다. 공간 데이터 형식에 대 한 개요를 확인 [공간 데이터 형식 개요](https://docs.microsoft.com/sql/relational-databases/spatial/spatial-data-types-overview) 페이지입니다.

## <a name="creating-a-geometry--geography-object"></a>만들 기 하 도형 / 지리 개체

두 가지 주요 Geometry를 만들려면 / 지리 개체-변환에서는 wkt (WELL-KNOWN Text) 또는 wkb (WELL-KNOWN Binary).

### <a name="creating-from-wkt"></a>WKT에서 만들기

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
Geography geogWKT = Geography.STGeomFromText(geoWKT, 4326);
```

SRID 4326을 사용 하 여 LINESTRING Geometry 개체를 사용 하 여 시스템 식별자 SRID (Spatial Reference) 0 및 지리 개체 만들어집니다.

### <a name="creating-from-wkb"></a>WKB에서 만들기

```java
byte[] geomWKB = Hex.decodeHex("00000000010403000000000000000000F03F00000000000000000000000000000000000000000000F03F000000000000F0BF000000000000000001000000010000000001000000FFFFFFFF0000000002".toCharArray());
byte[] geogWKB = Hex.decodeHex("E61000000104030000000000000000000000000000000000F03F000000000000F03F00000000000000000000000000000000000000000000F0BF01000000010000000001000000FFFFFFFF0000000002".toCharArray());

Geometry geomWKT = Geometry.deserialize(geomWKB);
Geography geogWKT = Geography.deserialize(geogWKB);
```

이 WKT에서 이전에 만든 것에 해당 하는 기 하 도형 및 지리 개체를 만듭니다.

## <a name="working-with-a-geometry--geography-object"></a>작업 기 하 도형 / 지리 개체

테이블 아래와 같은 SQL Server에 사용자를 가정 합니다.

```sql
CREATE TABLE sampleTable (c1 geometry)  
```

기 하 도형 값을 삽입 하는 샘플 스크립트는 다음과 같습니다.

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
SQLServerPreparedStatement pstmt = (SQLServerPreparedStatement) connection.prepareStatement("insert into sampleTable values (?)");
pstmt.setGeometry(1, geomWKT);  
pstmt.execute();
```

지리 열을 사용 하 여 Geography 누구를 수행할 수 있습니다 동일 하 고 **setGeography()** 메서드.

읽을 기 하 도형 / 지리 열:

```java
try(SQLServerResultSet rs = (SQLServerResultSet)stmt.executeQuery("select * from geomTable")) {
    while(rs.next()){
        rs.getGeometry(1);
    }
}
```

지리 열을 사용 하 여 Geography 누구를 수행할 수 있습니다 동일 하 고 **getGeography()** 메서드.

## <a name="newly-introduced-apis"></a>새로 도입된 된 Api

클래스에서이 내용을 추가 하 여 도입 된 새로운 공용 Api는 이러한 **SQLServerPreparedStatement**, **SQLServerResultSet**합니다 **기 하 도형**, 및  **Geography**합니다.

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

|메서드|설명|
|:------|:----------|
|void setGeometry(int n, Geometry x)| 지정 된 microsoft.sql.Geometry 클래스 개체에 지정 된 매개 변수를 설정합니다.
|void setGeography (int n, Geography x)| 지정 된 microsoft.sql.Geography 클래스 개체에 지정 된 매개 변수를 설정합니다.

### <a name="sqlserverresultset"></a>SQLServerResultSet

|메서드|설명|
|:------|:----------|
|Geometry getGeometry(int colunIndex)| 이 Java 프로그래밍 언어의에서 com.microsoft.sqlserver.jdbc.Geometry 개체로이 결과 집합 개체의 현재 행에서 지정 된 열의 값을 반환 합니다.
|기 하 도형 getGeometry (문자열 columnName)| 이 Java 프로그래밍 언어의에서 com.microsoft.sqlserver.jdbc.Geometry 개체로이 결과 집합 개체의 현재 행에서 지정 된 열의 값을 반환 합니다.
|Geography getGeography(int colunIndex)| 이 Java 프로그래밍 언어의에서 com.microsoft.sqlserver.jdbc.Geography 개체로이 결과 집합 개체의 현재 행에서 지정 된 열의 값을 반환 합니다.
|Geography getGeography (문자열 columnName)| 이 Java 프로그래밍 언어의에서 com.microsoft.sqlserver.jdbc.Geography 개체로이 결과 집합 개체의 현재 행에서 지정 된 열의 값을 반환 합니다.

### <a name="geometry"></a>geometry

|메서드|설명|
|:------|:----------|
|기 하 도형 STGeomFromText (문자열 wkt, SRID int)| 인스턴스에서 얻어진 Z(높이) 값 및 M(측정값) 값을 사용하여 보강된 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현의 기하 도형 인스턴스에 대한 생성자입니다.
|Geometry STGeomFromWKB(byte[] wkb)| OGC(Open Geospatial Consortium) WKB(Well-Known Binary) 표현의 기하 도형 인스턴스에 대한 생성자입니다.
|기 하 도형 deserialize (byte wkb)| 공간 데이터에 대 한 내부 SQL Server 형식에서 Geometry 인스턴스에 대 한 생성자입니다.
|기 하 도형 구문 분석 문자열 wkt)| OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현의 기하 도형 인스턴스에 대한 생성자입니다. Spatial Reference Identifier 기본값인 0으로 설정 됩니다.
|기하학 지점을 (double 이중 y, x SRID int)| Geometry 인스턴스의 Spatial Reference Identifier를 해당 X 및 Y 값에서 Point 인스턴스를 나타내는 생성자입니다.
|String STAsText()| 기하 도형 인스턴스의 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현을 반환합니다. 이 텍스트에는 인스턴스에서 얻어진 Z(높이) 값 또는 M(측정값) 값이 포함되지 않습니다.
|byte[] STAsBinary()| 기하 도형 인스턴스의 OGC(Open Geospatial Consortium) WKB(Well-Known Binary) 표현을 반환합니다. 이 값에는 인스턴스에서 얻어진 Z값 또는 M값이 포함되지 않습니다.
|byte[] serialize()| 기하 도형 형식의 내부 SQL Server 형식을 나타내는 바이트를 반환합니다.
|부울 hasM()| 개체에 M (측정값) 값을 반환.
|부울 hasZ()| 개체에 Z (높이) 값을 반환 합니다.
|Double getX()| X 좌표 값을 반환합니다.
|Double getY()| Y 좌표 값을 반환합니다.
|Double getM()| 개체의 M (측정값) 값을 반환합니다.
|Double getZ()| 개체의 Z (높이) 값을 반환합니다.
|int getSrid()| 공간 참조 식별자 (SRID)을 반환합니다.
|boolean isNull()| 경우 기 하 도형 개체는 null을 반환 합니다.
|int STNumPoints()| 기 하 도형 개체의 점 개수를 반환합니다.
|String STGeometryType()| geometry 인스턴스로 표현된 OGC(Open Geospatial Consortium) 형식 이름을 반환합니다.
|문자열 asTextZM()| 기 하 도형 개체의 wkt (WELL-KNOWN Text) 표현을 반환합니다.
|String toString()| 기하 도형 개체의 문자열 표현을 반환합니다.

### <a name="geography"></a>지리

|메서드|설명|
|:------|:----------|
|Geography STGeomFromText (문자열 wkt, SRID int)| 인스턴스에서 얻어진 Z(높이) 값 및 M(측정값) 값을 사용하여 보강된 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현의 지리 인스턴스에 대한 생성자입니다.
|Geography STGeomFromWKB (byte wkb)| OGC(Open Geospatial Consortium) WKB(Well-Known Binary) 표현의 지리 인스턴스에 대한 생성자입니다.
|Geography (byte wkb)를 deserialize 합니다.| 공간 데이터에 대 한 내부 SQL Server 형식에서 Geography 인스턴스에 대 한 생성자입니다.
|Geography 구문 분석 문자열 wkt)| OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현의 지리 인스턴스에 대한 생성자입니다. Spatial Reference Identifier 기본값인 0으로 설정 됩니다.
|지리 지점을 (lon, lat double, int SRID double)| 해당 위도 및 경도와 SRID(Spatial Reference Identifier)의 지점 인스턴스를 나타내는 지리 인스턴스에 대한 생성자입니다.
|String STAsText()| 지리 인스턴스의 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현을 반환합니다. 이 텍스트에는 인스턴스에서 얻어진 Z(높이) 값 또는 M(측정값) 값이 포함되지 않습니다.
|byte[] STAsBinary())| 지리 인스턴스의 OGC(Open Geospatial Consortium) WKB(Well-Known Binary) 표현을 반환합니다. 이 값에는 인스턴스에서 얻어진 Z값 또는 M값이 포함되지 않습니다.
|byte[] serialize()| 지리 형식의 내부 SQL Server 형식을 나타내는 바이트를 반환합니다.
|부울 hasM()| 개체에 M (측정값) 값을 반환.
|부울 hasZ()| 개체에 Z (높이) 값을 반환 합니다.
|Double getLatitude()| 위도 값을 반환합니다.
|Double getLongitude()| 경도 값을 반환합니다.
|Double getM()| 개체의 M (측정값) 값을 반환합니다.
|Double getZ()| 개체의 Z (높이) 값을 반환합니다.
|int getSrid()| 공간 참조 식별자 (SRID)을 반환합니다.
|boolean isNull()| 경우 Geography 개체는 null을 반환 합니다.
|int STNumPoints()| Geography 개체의 점 개수를 반환합니다.
|String STGeographyType()| geography 인스턴스로 표현된 OGC(Open Geospatial Consortium) 형식 이름을 반환합니다.
|문자열 asTextZM()| Geography 개체의 wkt (WELL-KNOWN Text) 표현을 반환합니다.
|String toString()| 지리 개체의 문자열 표현을 반환합니다.

## <a name="limitations-of-spatial-datatypes"></a>공간 데이터 형식의 제한 사항

1. 공간 sub datatypes **CircularString**를 **CompoundCurve**합니다 **CurvePolygon**, 및 **FullGlobe** 에서만 지원 됩니다 SQL Server 2012 이상.

2. 항상 암호화 된 공간 데이터 형식으로 사용할 수 없습니다.

3. 저장 프로시저, TVP를 및 BulkCopy 작업은 현재 공간 데이터 형식으로 지원 되지 않습니다.

## <a name="see-also"></a>참고 항목

[공간 데이터 형식 샘플(JDBC)](../../connect/jdbc/spatial-data-types-sample.md)
