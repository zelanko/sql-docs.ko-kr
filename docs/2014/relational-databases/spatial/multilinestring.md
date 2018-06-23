---
title: MultiLineString | Microsoft 문서
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
- MultiLineString geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 95deeefe-d6c5-4a11-b347-379e4486e7b7
caps.latest.revision: 19
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e87912fc00924698bf2fe735c0bd9ce9433cdb1e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092827"
---
# <a name="multilinestring"></a>MultiLineString
  A `MultiLineString` 0 개 이상의 컬렉션이 `geometry` 또는 **geographyLineString** 인스턴스.  
  
## <a name="multilinestring-instances"></a>MultiLineString 인스턴스  
 다음 그림에서는 예를 보여 줍니다. `MultiLineString` 인스턴스.  
  
 ![geometry MultiLineString 인스턴스의 예](../../database-engine/media/multilinestring.gif "geometry MultiLineString 인스턴스의 예")  
  
 그림에 대한 설명:  
  
-   그림 1은 단순 `MultiLineString` 인스턴스 두 4 개의 끝점이 `LineString` 요소입니다.  
  
-   그림 2는 `MultiLineString` 요소의 끝점만 교차하므로 단순한 `LineString` 인스턴스입니다. 경계는 두 개의 겹치지 않는 끝점입니다.  
  
-   그림 3은 해당 `MultiLineString` 요소 중 하나의 내부가 교차하므로 단순하지 않은 `LineString` 인스턴스입니다. 이 경계 `MultiLineString` 인스턴스는 4 개의 끝점입니다.  
  
-   그림 4는 단순 하지 않고 닫혀 있지 않은 `MultiLineString` 인스턴스.  
  
-   그림 5는 단순하고 닫혀 있지 않은 `MultiLineString` 인스턴스입니다. 때문에 닫히지 해당 `LineStrings` 요소가 닫혀 있지 않습니다. 간단 하기 때문에 모든 내부는 `LineStrings` 인스턴스가 교차 합니다.  
  
-   그림 6은 단순 하 고 닫혀 `MultiLineString` 인스턴스. 이 인스턴스는 해당 요소가 모두 닫혀 있으므로 닫혀 있고, 해당 요소 중 교차하는 것이 없으므로 단순합니다.  
  
### <a name="accepted-instances"></a>허용되는 인스턴스  
 에 대 한는 `MultiLineString` 만 허용 하거나 다음 조건을 충족 해야 하는 인스턴스 수 비어 있거나 `LineString` 허용 되는 인스턴스로만 구성 되어 있습니다. 대 한 자세한 내용은 허용 `LineString` 인스턴스 참조 [LineString](../spatial/linestring.md)합니다. 다음은 허용되는 `MultiLineString` 인스턴스의 예입니다.  
  
```  
DECLARE @g1 geometry = 'MULTILINESTRING EMPTY';  
DECLARE @g2 geometry = 'MULTILINESTRING((1 1, 3 5), (-5 3, -8 -2))';  
DECLARE @g3 geometry = 'MULTILINESTRING((1 1, 5 5), (1 3, 3 1))';  
DECLARE @g4 geometry = 'MULTILINESTRING((1 1, 3 3, 5 5),(3 3, 5 5, 7 7))';  
```  
  
 다음 예제에서는 throw 한 `System.FormatException` 때문에 두 번째 `LineString` 인스턴스가 유효 하지 않습니다.  
  
```  
DECLARE @g geometry = 'MULTILINESTRING((1 1, 3 5),(-5 3))';  
```  
  
### <a name="valid-instances"></a>유효한 인스턴스  
 에 대 한는 `MultiLineString` 인스턴스는 다음 조건을 충족 해야 유효 합니다.  
  
1.  `MultiLineString` 인스턴스를 구성하는 모든 인스턴스가 유효한 `LineString` 인스턴스여야 합니다.  
  
2.  `LineString` 인스턴스를 구성하는 두 `MultiLineString` 인스턴스가 일정 간격으로 겹치면 안 됩니다. `LineString` 인스턴스는 제한된 수의 점에서 자체적으로 또는 다른 `LineString` 인스턴스와 교차하는 것만 가능합니다.  
  
 다음 예에서는 유효한 `MultiLineString` 인스턴스 세 개와 유효하지 않은 `MultiLineString` 인스턴스 하나를 보여 줍니다.  
  
```  
DECLARE @g1 geometry = 'MULTILINESTRING EMPTY';  
DECLARE @g2 geometry = 'MULTILINESTRING((1 1, 3 5), (-5 3, -8 -2))';  
DECLARE @g3 geometry = 'MULTILINESTRING((1 1, 5 5), (1 3, 3 1))';  
DECLARE @g4 geometry = 'MULTILINESTRING((1 1, 3 3, 5 5),(3 3, 5 5, 7 7))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
 `@g4` 유효 하지 때문에 두 번째 `LineString` 인스턴스가 겹치는 첫 번째 지 `LineString` 인스턴스는 간격입니다. 즉, 이 두 인스턴스는 무한한 점에서 접합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 SRID 0으로 두 개의 `geometry``MultiLineString` 요소를 포함하는 단순한 `LineString` 인스턴스를 만듭니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 2, 1 1), (1 0, 1 1))');  
```  
  
 다른 SRID로 이 인스턴스를 인스턴스화하려면 `STGeomFromText()` 또는 `STMLineStringFromText()`를 사용합니다. 또는 다음 예와 같이 `Parse()` 를 사용한 다음 SRID를 수정할 수도 있습니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 2, 1 1), (1 0, 1 1))');  
SET @g.STSrid = 13;  
```  
  
## <a name="see-also"></a>관련 항목  
 [STLength&#40;geometry 데이터 형식&#41;](/sql/t-sql/spatial-geometry/stlength-geometry-data-type)   
 [STIsClosed&#40;geometry 데이터 형식&#41;](/sql/t-sql/spatial-geometry/stisclosed-geometry-data-type)   
 [LineString](../spatial/linestring.md)   
 [공간 데이터&#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md)  
  
  
