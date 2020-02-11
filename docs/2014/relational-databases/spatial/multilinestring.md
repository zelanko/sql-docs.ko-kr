---
title: MultiLineString | Microsoft 문서
ms.date: 06/14/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 9244f32b2ee9921d1caaa63b5d6aae9c324049ff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66014205"
---
# <a name="multilinestring"></a>MultiLineString
  는 `MultiLineString` 0 개 이상의 `geometry` 또는 **geographyLineString** 인스턴스의 컬렉션입니다.  
  
## <a name="multilinestring-instances"></a>MultiLineString 인스턴스  
 다음 그림에서는 `MultiLineString` 인스턴스의 예를 보여 줍니다.  
  
 ![기하 도형 MultiLineString 인스턴스의 예](../../database-engine/media/multilinestring.gif "기하 도형 MultiLineString 인스턴스의 예")  
  
 그림에 대한 설명:  
  
-   그림 1은 경계가 두 `MultiLineString` `LineString` 요소의 네 끝점 인 단순 인스턴스입니다.  
  
-   그림 2는 `MultiLineString` 요소의 엔드포인트만 교차하므로 단순한 `LineString` 인스턴스입니다. 경계는 두 개의 겹치지 않는 엔드포인트입니다.  
  
-   그림 3은 해당 `MultiLineString` 요소 중 하나의 내부가 교차하므로 단순하지 않은 `LineString` 인스턴스입니다. 이 `MultiLineString` 인스턴스의 경계는 4개의 엔드포인트입니다.  
  
-   그림 4는 단순하지 않고 닫혀 있지 않은 `MultiLineString` 인스턴스입니다.  
  
-   그림 5는 단순하고 닫혀 있지 않은 `MultiLineString` 인스턴스입니다. 해당 `LineStrings` 요소가 닫혀 있지 않으므로 닫혀 있지 않습니다. 
  `LineStrings` 인스턴스의 내부에 교차하는 것이 없으므로 단순합니다.  
  
-   그림 6은 단순하고 닫혀 있는 `MultiLineString` 인스턴스입니다. 이 인스턴스는 해당 요소가 모두 닫혀 있으므로 닫혀 있고, 해당 요소 중 교차하는 것이 없으므로 단순합니다.  
  
### <a name="accepted-instances"></a>허용되는 인스턴스  
 
  `MultiLineString` 인스턴스는 비어 있거나 허용되는 `LineString` 인스턴스로만 구성되어 있어야 허용됩니다. 허용 `LineString` 되는 인스턴스에 대 한 자세한 내용은 [LineString](../spatial/linestring.md)를 참조 하세요. 다음은 허용되는 `MultiLineString` 인스턴스의 예입니다.  
  
```  
DECLARE @g1 geometry = 'MULTILINESTRING EMPTY';  
DECLARE @g2 geometry = 'MULTILINESTRING((1 1, 3 5), (-5 3, -8 -2))';  
DECLARE @g3 geometry = 'MULTILINESTRING((1 1, 5 5), (1 3, 3 1))';  
DECLARE @g4 geometry = 'MULTILINESTRING((1 1, 3 3, 5 5),(3 3, 5 5, 7 7))';  
```  
  
 다음 예에서는 두 번째 `System.FormatException` 인스턴스가 유효하지 않으므로 `LineString`이 발생합니다.  
  
```  
DECLARE @g geometry = 'MULTILINESTRING((1 1, 3 5),(-5 3))';  
```  
  
### <a name="valid-instances"></a>유효한 인스턴스  
 
  `MultiLineString` 인스턴스는 다음 조건을 충족해야 유효합니다.  
  
1.  
  `MultiLineString` 인스턴스를 구성하는 모든 인스턴스가 유효한 `LineString` 인스턴스여야 합니다.  
  
2.  
  `LineString` 인스턴스를 구성하는 두 `MultiLineString` 인스턴스가 일정 간격으로 겹치면 안 됩니다. 
  `LineString` 인스턴스는 제한된 수의 점에서 자체적으로 또는 다른 `LineString` 인스턴스와 교차하는 것만 가능합니다.  
  
 다음 예에서는 유효한 `MultiLineString` 인스턴스 세 개와 유효하지 않은 `MultiLineString` 인스턴스 하나를 보여 줍니다.  
  
```  
DECLARE @g1 geometry = 'MULTILINESTRING EMPTY';  
DECLARE @g2 geometry = 'MULTILINESTRING((1 1, 3 5), (-5 3, -8 -2))';  
DECLARE @g3 geometry = 'MULTILINESTRING((1 1, 5 5), (1 3, 3 1))';  
DECLARE @g4 geometry = 'MULTILINESTRING((1 1, 3 3, 5 5),(3 3, 5 5, 7 7))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
 
  `@g4`는 두 번째 `LineString` 인스턴스가 일정 간격으로 첫 번째 `LineString` 인스턴스와 겹치므로 유효하지 않습니다. 즉, 이 두 인스턴스는 무한한 점에서 접합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [STLength&#40;geometry 데이터 형식&#41;](/sql/t-sql/spatial-geometry/stlength-geometry-data-type)   
 [STIsClosed&#40;geometry 데이터 형식&#41;](/sql/t-sql/spatial-geometry/stisclosed-geometry-data-type)   
 [LineString](../spatial/linestring.md)   
 [공간 데이터&#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md)  
  
  
