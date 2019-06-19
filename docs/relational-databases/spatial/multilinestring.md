---
title: MultiLineString | Microsoft 문서
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- MultiLineString geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 95deeefe-d6c5-4a11-b347-379e4486e7b7
author: MladjoA
ms.author: mlandzic
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f8df41184356f29e3037f36d519c9957f2f3e5b7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65936436"
---
# <a name="multilinestring"></a>MultiLineString
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **MultiLineString** 은 0개 이상의 **geometry** 또는 **geographyLineString** 인스턴스 컬렉션입니다.  
  
## <a name="multilinestring-instances"></a>MultiLineString 인스턴스  
 다음 그림에서는 **MultiLineString** 인스턴스의 예를 보여 줍니다.  
  
 ![geometry MultiLineString 인스턴스의 예](../../relational-databases/spatial/media/multilinestring.gif "geometry MultiLineString 인스턴스의 예")  
  
 그림에 대한 설명:  
  
-   그림 1은 두 **MultiLineString** 요소의 네 엔드포인트가 경계인 단순한 **LineString** 인스턴스입니다.  
  
-   그림 2는 **MultiLineString** 요소의 엔드포인트만 교차하므로 단순한 **LineString** 인스턴스입니다. 경계는 두 개의 겹치지 않는 엔드포인트입니다.  
  
-   그림 3은 해당 **MultiLineString** 요소 중 하나의 내부가 교차하므로 단순하지 않은 **LineString** 인스턴스입니다. 이 **MultiLineString** 인스턴스의 경계는 4개의 엔드포인트입니다.  
  
-   그림 4는 단순하지 않고 닫혀 있지 않은 **MultiLineString** 인스턴스입니다.  
  
-   그림 5는 단순하고 닫혀 있지 않은 **MultiLineString**인스턴스입니다. 이 인스턴스는 해당 **LineStrings** 요소가 닫혀 있지 않으므로 닫혀 있지 않고, **LineStrings** 인스턴스의 내부에 교차하는 것이 없으므로 단순합니다.  
  
-   그림 6은 단순하고 닫혀 있는 **MultiLineString** 인스턴스입니다. 이 인스턴스는 해당 요소가 모두 닫혀 있으므로 닫혀 있고, 해당 요소 중 교차하는 것이 없으므로 단순합니다.  
  
### <a name="accepted-instances"></a>허용되는 인스턴스  
 **MultiLineString** 인스턴스는 비어 있거나 허용되는 **LineString** 인스턴스로만 구성되어 있어야 허용됩니다. 허용되는 **LineString** 인스턴스에 대한 자세한 내용은 [LineString](../../relational-databases/spatial/linestring.md)을 참조하십시오. 다음은 허용되는 **MultiLineString** 인스턴스의 예입니다.  
  
```sql  
DECLARE @g1 geometry = 'MULTILINESTRING EMPTY';  
DECLARE @g2 geometry = 'MULTILINESTRING((1 1, 3 5), (-5 3, -8 -2))';  
DECLARE @g3 geometry = 'MULTILINESTRING((1 1, 5 5), (1 3, 3 1))';  
DECLARE @g4 geometry = 'MULTILINESTRING((1 1, 3 3, 5 5),(3 3, 5 5, 7 7))';  
```  
  
다음 예제에서는 두 번째 `System.FormatException` LineString **인스턴스가 유효하지 않으므로** 이 발생합니다.  
  
```sql  
DECLARE @g geometry = 'MULTILINESTRING((1 1, 3 5),(-5 3))';  
```  
  
### <a name="valid-instances"></a>유효한 인스턴스  
**MultiLineString** 인스턴스는 다음 조건을 충족해야 유효합니다.  
  
1.  **MultiLineString** 인스턴스를 구성하는 모든 인스턴스가 유효한 **LineString** 인스턴스여야 합니다.  
  
2.  **LineString** 인스턴스를 구성하는 두 **MultiLineString** 인스턴스가 일정 간격으로 겹치면 안 됩니다. **LineString** 인스턴스는 제한된 수의 점에서 자체적으로 또는 다른 **LineString** 인스턴스와 교차하는 것만 가능합니다.  
  
다음 예에서는 유효한 **MultiLineString** 인스턴스 세 개와 유효하지 않은 **MultiLineString** 인스턴스 하나를 보여 줍니다.  
  
```sql  
DECLARE @g1 geometry = 'MULTILINESTRING EMPTY';  
DECLARE @g2 geometry = 'MULTILINESTRING((1 1, 3 5), (-5 3, -8 -2))';  
DECLARE @g3 geometry = 'MULTILINESTRING((1 1, 5 5), (1 3, 3 1))';  
DECLARE @g4 geometry = 'MULTILINESTRING((1 1, 3 3, 5 5),(3 3, 5 5, 7 7))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
`@g4` 는 두 번째 **LineString** 인스턴스가 일정 간격으로 첫 번째 **LineString** 인스턴스와 겹치므로 유효하지 않습니다. 즉, 이 두 인스턴스는 무한한 점에서 접합니다.  
  
## <a name="examples"></a>예  
다음 예제에서는 SRID 0으로 두 개의 `geometry``MultiLineString` 요소를 포함하는 단순한 `LineString` 인스턴스를 만듭니다.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 2, 1 1), (1 0, 1 1))');  
```  
  
다른 SRID로 이 인스턴스를 인스턴스화하려면 `STGeomFromText()` 또는 `STMLineStringFromText()`를 사용합니다. 또는 다음 예와 같이 `Parse()` 를 사용한 다음 SRID를 수정할 수도 있습니다.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 2, 1 1), (1 0, 1 1))');  
SET @g.STSrid = 13;  
```  
  
## <a name="see-also"></a>참고 항목  
 [STLength&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STIsClosed&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)   
 [LineString](../../relational-databases/spatial/linestring.md)   
 [공간 데이터&#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
