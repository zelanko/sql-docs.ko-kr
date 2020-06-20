---
title: LineString | Microsoft 문서
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- LineString geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: e50d0b86-8b31-4285-be71-ad05c7712cbd
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 5a0f77959cfe4492eca6c38951ba2868452d41ad
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "84996327"
---
# <a name="linestring"></a>LineString
  `LineString`은 일련의 점과 이 점을 연결하는 선분을 나타내는 1차원 개체입니다.

## <a name="linestring-instances"></a>LineString 인스턴스
 다음 그림에서는 `LineString` 인스턴스의 예를 보여 줍니다.

 ![geometry LineString 인스턴스의 예](../../database-engine/media/linestring.gif "geometry LineString 인스턴스의 예")

 그림에 대한 설명:

-   그림 1은 단순하고 닫혀 있지 않은 `LineString` 인스턴스입니다.

-   그림 2는 단순하지 않고 닫혀 있지 않은 `LineString` 인스턴스입니다.

-   그림 3은 닫혀 있고 단순한 `LineString` 인스턴스이므로 링입니다.

-   그림 4는 닫혀 있고 단순하지 않은 `LineString` 인스턴스이므로 링이 아닙니다.

### <a name="accepted-instances"></a>허용되는 인스턴스
 허용되는 `LineString` 인스턴스는 기하 도형 변수에 입력될 수 있지만 유효한 `LineString` 인스턴스가 아닐 수 있습니다. `LineString` 인스턴스가 허용되려면 다음 조건을 충족해야 합니다. 인스턴스는 2개 이상의 점으로 구성되어야 하거나 비어 있어야 합니다. 다음 LineString 인스턴스가 허용됩니다.

```
DECLARE @g1 geometry = 'LINESTRING EMPTY';
DECLARE @g2 geometry = 'LINESTRING(1 1,2 3,4 8, -6 3)';
DECLARE @g3 geometry = 'LINESTRING(1 1, 1 1)';
```

 `@g3`에서는 `LineString` 인스턴스를 허용할 수 있지만 유효하지 않음을 보여 줍니다.

 다음 `LineString` 인스턴스가 허용되지 않습니다. 이 인스턴스에서 `System.FormatException`이 발생합니다.

```
DECLARE @g geometry = 'LINESTRING(1 1)';
```

### <a name="valid-instances"></a>유효한 인스턴스
 `LineString` 인스턴스는 다음 조건을 충족해야 유효합니다.

1.  `LineString` 인스턴스가 허용되어야 합니다.

2.  `LineString` 인스턴스가 비어 있지 않는 경우 해당 인스턴스에 2개 이상의 고유 점이 포함되어야 합니다.

3.  `LineString` 인스턴스는 두 개 이상의 연속 점 간격으로 자체적으로 겹쳐질 수 없습니다.

 다음 `LineString` 인스턴스는 유효합니다.

```
DECLARE @g1 geometry= 'LINESTRING EMPTY';
DECLARE @g2 geometry= 'LINESTRING(1 1, 3 3)';
DECLARE @g3 geometry= 'LINESTRING(1 1, 3 3, 2 4, 2 0)';
DECLARE @g4 geometry= 'LINESTRING(1 1, 3 3, 2 4, 2 0, 1 1)';
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();

```

 다음 `LineString` 인스턴스는 유효하지 않습니다.

```
DECLARE @g1 geometry = 'LINESTRING(1 4, 3 4, 2 4, 2 0)';
DECLARE @g2 geometry = 'LINESTRING(1 1, 1 1)';
SELECT @g1.STIsValid(), @g2.STIsValid();
```

> [!WARNING]
>  `LineString`의 겹침 여부가 정확하지 않은 부동 소수점 계산을 기준으로 검색됩니다.

## <a name="examples"></a>예
 다음 예에서는 세 점이 있고 SRID가 0인 `geometry``LineString` 인스턴스를 만드는 방법을 보여 줍니다.

```
DECLARE @g geometry;
SET @g = geometry::STGeomFromText('LINESTRING(1 1, 2 4, 3 9)', 0);
```

 `LineString` 인스턴스의 각 점에는 Z(높이) 및 M(측정값) 값을 포함할 수 있습니다. 이 예에서는 위의 예에서 만들어진 `LineString` 인스턴스에 M 값을 추가합니다. M 및 Z는 Null 값이 될 수 있습니다.

```
DECLARE @g geometry;
SET @g = geometry::STGeomFromText('LINESTRING(1 1 NULL 0, 2 4 NULL 12.3, 3 9 NULL 24.5)', 0);
```

 다음 예에서는 동일한 점 두 개로 `geometry LineString` 인스턴스를 만드는 방법을 보여 줍니다. `IsValid`에 대한 호출은 `LineString` 인스턴스가 유효하지 않음을 나타내며 `MakeValid` 호출 시 `LineString` 인스턴스가 `Point`로 변환됩니다.

```sql
DECLARE @g geometry
SET @g = geometry::STGeomFromText('LINESTRING(1 3, 1 3)',0);
IF @g.STIsValid() = 1
  BEGIN
     SELECT @g.ToString() + ' is a valid LineString.';  
  END
ELSE
  BEGIN
     SELECT @g.ToString() + ' is not a valid LineString.';
     SET @g = @g.MakeValid();
     SELECT @g.ToString() + ' is a valid Point.';  
  END

```

 위의 코드 조각은 다음과 같은 결과를 생성합니다.

```
LINESTRING(1 3, 1 3) is not a valid LineString
POINT(1 3) is a valid Point.
```

## <a name="see-also"></a>참고 항목
 [Stlength &#40;geometry 데이터 형식&#41;](/sql/t-sql/spatial-geometry/stlength-geometry-data-type) [stlength &#40;geometry 데이터 형식](/sql/t-sql/spatial-geometry/ststartpoint-geometry-data-type) [stlength &#40;](/sql/t-sql/spatial-geometry/stendpoint-geometry-data-type) geometry 데이터 형식&#41;stststn [&#40;](/sql/t-sql/spatial-geometry/stpointn-geometry-data-type) geometry 데이터 형식&#41;[stnumpoints](/sql/t-sql/spatial-geometry/stnumpoints-geometry-data-type) &#40;geometry 데이터 형식&#41;[Stisring &#40;geometry](/sql/t-sql/spatial-geometry/stisring-geometry-data-type) 데이터 형식&#41;[STIsClosed &#40;geometry 데이터 형식](/sql/t-sql/spatial-geometry/stisclosed-geometry-data-type)&#41;[stpointonsurface &#40;geometry 데이터](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type) 형식&#41;[공간 데이터 &#40;](../spatial/spatial-data-sql-server.md) SQL Server


