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
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026937"
---
# <a name="using-spatial-datatypes"></a>공간 데이터 형식 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

JDBC Driver preview 릴리스 6.5.0을 시작 하는 공간 데이터 형식 (Geometry 및 Geography)이 지원 됩니다. 공간 데이터 형식은 현재 저장 프로시저, TVP (테이블 반환 매개 변수), 대량 복사 및 Always Encrypted에서 지원 되지 않습니다. 이 페이지에서는 JDBC 드라이버를 사용 하 여 Geometry 및 Geography 데이터 형식의 다양 한 사용 사례를 보여 줍니다. 공간 데이터 형식에 대 한 개요는 [공간 데이터 형식 개요](https://docs.microsoft.com/sql/relational-databases/spatial/spatial-data-types-overview) 페이지를 참조 하세요.

## <a name="creating-a-geometry--geography-object"></a>Geometry/geography 개체 만들기

기 하 도형/지리 개체를 만드는 두 가지 주요 방법은 WKT (잘 알려진 텍스트)에서 변환 하거나 WKB (잘 알려진 이진)로 변환 하는 것입니다.

### <a name="creating-from-wkt"></a>WKT에서 만들기

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
Geography geogWKT = Geography.STGeomFromText(geoWKT, 4326);
```

그러면 SRID (공간 참조 시스템 식별자) 0과 SRID 4326를 사용 하는 Geography 개체가 있는 LINESTRING Geometry 개체가 만들어집니다.

### <a name="creating-from-wkb"></a>WKB에서 만들기

```java
byte[] geomWKB = Hex.decodeHex("00000000010403000000000000000000F03F00000000000000000000000000000000000000000000F03F000000000000F0BF000000000000000001000000010000000001000000FFFFFFFF0000000002".toCharArray());
byte[] geogWKB = Hex.decodeHex("E61000000104030000000000000000000000000000000000F03F000000000000F03F00000000000000000000000000000000000000000000F0BF01000000010000000001000000FFFFFFFF0000000002".toCharArray());

Geometry geomWKT = Geometry.deserialize(geomWKB);
Geography geogWKT = Geography.deserialize(geogWKB);
```

이렇게 하면 이전에 WKT에서 만든 것과 동일한 Geometry 및 Geography 개체가 만들어집니다.

## <a name="working-with-a-geometry--geography-object"></a>Geometry/Geography 개체 작업

사용자에 게 다음과 같은 SQL Server 테이블이 있다고 가정 합니다.

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

Geography 열과 **Setgeography ()** 메서드를 사용 하 여 지리에 상응 하는 경우에도 마찬가지입니다.

Geometry/Geography 열을 읽으려면 다음을 수행 합니다.

```java
try(SQLServerResultSet rs = (SQLServerResultSet)stmt.executeQuery("select * from geomTable")) {
    while(rs.next()){
        rs.getGeometry(1);
    }
}
```

Geography 열과 **Getgeography ()** 메서드를 사용 하 여 지리에 상응 하는 경우에도 마찬가지입니다.

## <a name="newly-introduced-apis"></a>새로 도입 된 Api

이러한 Api는이 추가를 통해 **SQLServerPreparedStatement**, **SQLServerResultSet**, **Geometry**및 **Geography**클래스에서 도입 된 새로운 공용 api입니다.

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

|메서드|설명|
|:------|:----------|
|void setGeometry(int n, Geometry x)| 지정 된 매개 변수를 지정 된 microsoft Geometry 클래스 개체로 설정 합니다.
|void setGeography (int n, Geography x)| 지정 된 매개 변수를 지정 된 microsoft .sql. Geography 클래스 개체로 설정 합니다.

### <a name="sqlserverresultset"></a>SQLServerResultSet

|메서드|설명|
|:------|:----------|
|Geometry getGeometry(int colunIndex)| 이 ResultSet 개체의 현재 행에서 지정 된 열의 값을 반환 합니다 .이 개체는 Java 프로그래밍 언어의 .com 개체입니다.
|Geometry getGeometry (문자열 columnName)| 이 ResultSet 개체의 현재 행에서 지정 된 열의 값을 반환 합니다 .이 개체는 Java 프로그래밍 언어의 .com 개체입니다.
|Geography getGeography(int colunIndex)| 이 ResultSet 개체의 현재 행에서 지정 된 열의 값을 반환 합니다 .이 개체는 Java 프로그래밍 언어의
|Geography getGeography (columnName 문자열)| 이 ResultSet 개체의 현재 행에서 지정 된 열의 값을 반환 합니다 .이 개체는 Java 프로그래밍 언어의

### <a name="geometry"></a>geometry

|메서드|설명|
|:------|:----------|
|Geometry STGeomFromText (String wkt, int SRID)| 인스턴스에서 얻어진 Z(높이) 값 및 M(측정값) 값을 사용하여 보강된 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현의 기하 도형 인스턴스에 대한 생성자입니다.
|Geometry STGeomFromWKB(byte[] wkb)| OGC(Open Geospatial Consortium) WKB(Well-Known Binary) 표현의 기하 도형 인스턴스에 대한 생성자입니다.
|기 하 도형 deserialize (byte [] wkb)| 공간 데이터에 대 한 내부 SQL Server 형식의 기 하 도형 인스턴스에 대 한 생성자입니다.
|Geometry 구문 분석 (String wkt)| OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현의 기하 도형 인스턴스에 대한 생성자입니다. 공간 참조 식별자의 기본값은 0입니다.
|기 하 도형 점 (이중 x, 이중 y, int SRID)| 해당 X 및 Y 값에서 Point 인스턴스를 나타내는 Geometry 인스턴스 및 공간 참조 식별자에 대 한 생성자입니다.
|String STAsText()| 기하 도형 인스턴스의 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현을 반환합니다. 이 텍스트에는 인스턴스에서 얻어진 Z(높이) 값 또는 M(측정값) 값이 포함되지 않습니다.
|byte[] STAsBinary()| 기하 도형 인스턴스의 OGC(Open Geospatial Consortium) WKB(Well-Known Binary) 표현을 반환합니다. 이 값에는 인스턴스에서 얻어진 Z값 또는 M값이 포함되지 않습니다.
|byte[] serialize()| 기하 도형 형식의 내부 SQL Server 형식을 나타내는 바이트를 반환합니다.
|부울 hasM ()| 개체에 M (측정값) 값이 포함 되어 있으면를 반환 합니다.
|부울 hasZ ()| 개체에 Z (높이) 값이 포함 되어 있으면를 반환 합니다.
|Double getX()| X 좌표 값을 반환 합니다.
|Double getY()| Y 좌표 값을 반환 합니다.
|Double getM()| 개체의 M (측정값) 값을 반환 합니다.
|Double getZ()| 개체의 Z (높이) 값을 반환 합니다.
|int getSrid()| SRID (공간 참조 식별자) 값을 반환 합니다.
|boolean isNull()| Geometry 개체가 null 이면를 반환 합니다.
|int STNumPoints()| Geometry 개체의 요소 수를 반환 합니다.
|String STGeometryType()| geometry 인스턴스로 표현된 OGC(Open Geospatial Consortium) 형식 이름을 반환합니다.
|문자열 asTextZM ()| Geometry 개체의 잘 알려진 텍스트 (WKT) 표현을 반환 합니다.
|String toString()| 기하 도형 개체의 문자열 표현을 반환합니다.

### <a name="geography"></a>지리

|메서드|설명|
|:------|:----------|
|Geography STGeomFromText (String wkt, int SRID)| 인스턴스에서 얻어진 Z(높이) 값 및 M(측정값) 값을 사용하여 보강된 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현의 지리 인스턴스에 대한 생성자입니다.
|Geography STGeomFromWKB (byte [] wkb)| OGC(Open Geospatial Consortium) WKB(Well-Known Binary) 표현의 지리 인스턴스에 대한 생성자입니다.
|Geography deserialize (byte [] wkb)| 공간 데이터에 대 한 내부 SQL Server 형식의 Geography 인스턴스에 대 한 생성자입니다.
|지리 구문 분석 (문자열 wkt)| OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현의 지리 인스턴스에 대한 생성자입니다. 공간 참조 식별자의 기본값은 0입니다.
|지리 지점 (이중 lon, 이중 lat, int SRID)| 해당 위도 및 경도와 SRID(Spatial Reference Identifier)의 지점 인스턴스를 나타내는 지리 인스턴스에 대한 생성자입니다.
|String STAsText()| 지리 인스턴스의 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현을 반환합니다. 이 텍스트에는 인스턴스에서 얻어진 Z(높이) 값 또는 M(측정값) 값이 포함되지 않습니다.
|byte[] STAsBinary())| 지리 인스턴스의 OGC(Open Geospatial Consortium) WKB(Well-Known Binary) 표현을 반환합니다. 이 값에는 인스턴스에서 얻어진 Z값 또는 M값이 포함되지 않습니다.
|byte[] serialize()| 지리 형식의 내부 SQL Server 형식을 나타내는 바이트를 반환합니다.
|부울 hasM ()| 개체에 M (측정값) 값이 포함 되어 있으면를 반환 합니다.
|부울 hasZ ()| 개체에 Z (높이) 값이 포함 되어 있으면를 반환 합니다.
|Double getLatitude()| 위도 값을 반환 합니다.
|Double getLongitude()| 경도 값을 반환 합니다.
|Double getM()| 개체의 M (측정값) 값을 반환 합니다.
|Double getZ()| 개체의 Z (높이) 값을 반환 합니다.
|int getSrid()| SRID (공간 참조 식별자) 값을 반환 합니다.
|boolean isNull()| Geography 개체가 null 이면를 반환 합니다.
|int STNumPoints()| Geography 개체의 요소 수를 반환 합니다.
|String STGeographyType()| geography 인스턴스로 표현된 OGC(Open Geospatial Consortium) 형식 이름을 반환합니다.
|문자열 asTextZM ()| Geography 개체의 WKT (잘 알려진 텍스트) 표현을 반환 합니다.
|String toString()| 지리 개체의 문자열 표현을 반환합니다.

## <a name="limitations-of-spatial-datatypes"></a>공간 데이터 형식의 제한 사항

1. 공간 하위 데이터 형식 **CircularString**, **CompoundCurve**, **CurvePolygon**및 **fullglobe** 는 SQL Server 2012 이상 에서만 지원 됩니다.

2. Always Encrypted 공간 데이터 형식에 사용할 수 없습니다.

3. 저장 프로시저, TVP 및 대량 복사 작업은 현재 공간 데이터 형식에서 지원 되지 않습니다.

## <a name="see-also"></a>관련 항목:

[공간 데이터 형식 샘플(JDBC)](../../connect/jdbc/spatial-data-types-sample.md)
