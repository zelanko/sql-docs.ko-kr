---
title: "MultiPolygon | Microsoft 문서"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: spatial
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-spatial
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MultiPolygon geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 2c5db358-2a16-49d9-aac5-a74e86813932
caps.latest.revision: "20"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5019063adb70a4f8935f23fae0af89aec18e506a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="multipolygon"></a>MultiPolygon
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] **MultiPolygon** 인스턴스는 0개 이상의 **Polygon** 인스턴스 컬렉션입니다.  
  
## <a name="polygon-instances"></a>Polygon 인스턴스  
 다음 그림에서는 **MultiPolygon** 인스턴스의 예를 보여 줍니다.  
  
 ![geometry MultiPolygon 인스턴스의 예](../../relational-databases/spatial/media/multipolygon.gif "geometry MultiPolygon 인스턴스의 예")  
  
 그림에 대한 설명:  
  
-   그림 1은 두 개의 **Polygon** 요소가 있는 **MultiPolygon** 인스턴스입니다. 경계는 두 개의 외부 링과 세 개의 내부 링으로 정의됩니다.  
  
-   그림 2는 두 개의 **MultiPolygon** 요소가 있는 **Polygon** 인스턴스입니다. 경계는 두 개의 외부 링과 세 개의 내부 링으로 정의됩니다. 두 개의 **Polygon** 요소는 탄젠트 점에서 교차합니다.  
  
### <a name="accepted-instances"></a>허용되는 인스턴스  
 다음 조건 중 하나가 만족되면 **MultiPolygon** 인스턴스는 허용됩니다.  
  
-   빈 **MultiPolygon** 인스턴스인 경우  
  
-   **MultiPolygon** 인스턴스를 구성하는 모든 인스턴스가 허용되는 **Polygon** 인스턴스인 경우. 허용되는 **Polygon** 인스턴스에 대한 자세한 내용은 [Polygon](../../relational-databases/spatial/polygon.md)을 참조하십시오.  
  
 다음 예에서는 허용되는 **MultiPolygon** 인스턴스를 보여 줍니다.  
  
```  
DECLARE @g1 geometry = 'MULTIPOLYGON EMPTY';  
DECLARE @g2 geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
DECLARE @g3 geometry = 'MULTIPOLYGON(((2 2, 2 -2, -2 -2, -2 2, 2 2)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
```  
  
 다음 예에서는 `System.FormatException`을 발생시키는 MultiPolygon 인스턴스를 보여 줍니다.  
  
```  
DECLARE @g geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3)))';  
```  
  
 MultiPolygon의 두 번째 인스턴스는 허용되는 Polygon 인스턴스가 아닌 LineString 인스턴스입니다.  
  
### <a name="valid-instances"></a>유효한 인스턴스  
 **MultiPolygon** 인스턴스는 빈 **MultiPolygon** 인스턴스이거나 다음 조건이 만족되는 경우 유효합니다.  
  
1.  **MultiPolygon** 인스턴스를 구성하는 모든 인스턴스가 유효한 **Polygon** 인스턴스인 경우. 유효한 **Polygon** 인스턴스에 대한 자세한 내용은 [Polygon](../../relational-databases/spatial/polygon.md)을 참조하십시오.  
  
2.  **Polygon** 인스턴스를 구성하는 어떤 **MultiPolygon** 인스턴스도 겹치지 않는 경우  
  
 다음 예에서는 유효한 **MultiPolygon** 인스턴스 두 개와 유효하지 않은 **MultiPolygon** 인스턴스 하나를 보여 줍니다.  
  
```  
DECLARE @g1 geometry = 'MULTIPOLYGON EMPTY';  
DECLARE @g2 geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
DECLARE @g3 geometry = 'MULTIPOLYGON(((2 2, 2 -2, -2 -2, -2 2, 2 2)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
```  
  
 `@g2` 는 두 **Polygon** 인스턴스가 탄젠트 점에서만 접하므로 유효합니다. `@g3` 은 두 **Polygon** 인스턴스의 내부가 서로 겹치므로 유효하지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 `geometry``MultiPolygon` 인스턴스를 만드는 방법을 보여 주고 두 번째 구성 요소의 WKT(Well-Known Text)를 반환합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTIPOLYGON(((0 0, 0 3, 3 3, 3 0, 0 0), (1 1, 1 2, 2 1, 1 1)), ((9 9, 9 10, 10 9, 9 9)))');  
SELECT @g.STGeometryN(2).STAsText();  
```  
  
 이 예에서는 빈 `MultiPolygon` 인스턴스를 인스턴스화합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTIPOLYGON EMPTY');  
```  
  
## <a name="see-also"></a>참고 항목  
 [Polygon](../../relational-databases/spatial/polygon.md)   
 [STArea&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/starea-geometry-data-type.md)   
 [STCentroid&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stcentroid-geometry-data-type.md)   
 [STPointOnSurface&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stpointonsurface-geometry-data-type.md)   
 [공간 데이터&#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
