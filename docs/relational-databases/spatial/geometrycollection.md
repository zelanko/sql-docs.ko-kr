---
title: GeometryCollection | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
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
- GeomCollection geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 4445c0d9-a66b-4d7c-88e4-a66fa6f7d9fd
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 19b017f9a097b1bf18db2c9d79aaf5793de007a3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="geometrycollection"></a>GeometryCollection
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **GeometryCollection** 은 1개 이상의 **geometry** 또는 **geography** 인스턴스 컬렉션입니다. **GeometryCollection** 은 비워 둘 수 있습니다.  
  
## <a name="geometrycollection-instances"></a>GeometryCollection 인스턴스  
  
### <a name="accepted-instances"></a>허용되는 인스턴스  
 **GeometryCollection** 인스턴스는 빈 **GeometryCollection** 인스턴스이거나 **GeometryCollection** 인스턴스를 구성하는 모든 인스턴스가 허용되는 인스턴스여야 허용됩니다. 다음 예에서는 허용되는 인스턴스를 보여 줍니다.  
  
```  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
 다음 예에서는 `System.FormatException` GeometryCollection **인스턴스의** LinesString **인스턴스가 허용되지 않으므로** 이 발생합니다.  
  
```  
DECLARE @g geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1), POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
### <a name="valid-instances"></a>유효한 인스턴스  
 **GeometryCollection** 인스턴스는 **GeometryCollection** 인스턴스를 구성하는 모든 인스턴스가 유효한 경우 유효합니다. 다음 예에서는 유효한 **GeometryCollection** 인스턴스 세 개와 유효하지 않은 인스턴스 하나를 보여 줍니다.  
  
```  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g4 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, 1 -5, -5 5, -5 -1, -1 -1)))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
 `@g4` 는 **GeometryCollection** 인스턴스의 **Polygon** 인스턴스가 유효하지 않으므로 유효하지 않습니다.  
  
 허용되는 인스턴스와 유효한 인스턴스에 대한 자세한 내용은 [Point](../../relational-databases/spatial/point.md), [MultiPoint](../../relational-databases/spatial/multipoint.md), [LineString](../../relational-databases/spatial/linestring.md), [MultiLineString](../../relational-databases/spatial/multilinestring.md), [Polygon](../../relational-databases/spatial/polygon.md)및 [MultiPolygon](../../relational-databases/spatial/multipolygon.md)을 참조하십시오.  
  
## <a name="examples"></a>예  
 다음 예제에서는 `geometry``GeometryCollection` 인스턴스 및 `Point` 인스턴스가 들어 있는 SRID 1의 Z 값으로 `Polygon` 을 인스턴스화합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomCollFromText('GEOMETRYCOLLECTION(POINT(3 3 1), POLYGON((0 0 2, 1 10 3, 1 0 4, 0 0 2)))', 1);  
```  
  
## <a name="see-also"></a>참고 항목  
 [공간 데이터&#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
