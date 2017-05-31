---
title: "점 | Microsoft 문서"
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
- Point geometry subtype [SQL Server]
- geometry data type [SQL Server], spatial data
ms.assetid: 2a596ec4-8b2f-4962-bcb4-e5c8f77edad5
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3ab4b354292130b01c73f771c221a13b595bdbdc
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="point"></a>점
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공간 데이터에서 **Point** 는 단일 위치를 나타내는 0차원 개체 이며 Z(높이) 및 M(측정값) 값을 포함할 수 있습니다.  
  
## <a name="geography-data-type"></a>geography 데이터 형식  
 Geography 데이터 형식의 점 유형은 *Lat* 와 *Long* 가 각각 경도와 위도를 나타내는 단일 위치를 나타냅니다. 경도와 위도 값은 각도로 측정됩니다. 위도 값은 항상 [-90, 90] 사이에 있고 이 범위를 벗어난 값을 입력하면 예외를 발생합니다. 경도 값은 항상 [-180, 180] 사이에 있고 이 범위를 벗어나서 입력된 값은 이 범위 안에 있는 값으로 랩 어라운드(wrap-around)됩니다. 예를 들어 경도 값에 190을 입력하면 그 값은 -170으로 래핑됩니다. *SRID* 는 반환할 **geography** 인스턴스의 Spatial Reference ID를 나타냅니다.  
  
## <a name="geometry-data-type"></a>Geometry 데이터 형식  
 Geometry 데이터 형식의 점 유형은 *X* 와 *Y* 가 각각 생성 중인 지점의 X 및 Y 좌표를 나타내는 단일 위치를 나타냅니다. *SRID* 는 반환할 **geometry** 인스턴스의 Spatial Reference ID를 나타냅니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 SRID가 0인 점(3, 4)을 나타내는 `geometry Point`인스턴스를 만듭니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT (3 4)', 0);  
```  
  
 다음 예제에서는 Z(높이) 값이 7이고 M(측정값) 값이 2.5이며 기본 SRID가 0인 점(3, 4)을 나타내는 `geometry``Point` 인스턴스를 만듭니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('POINT(3 4 7 2.5)');  
```  
  
 마지막 예에서는 `geometry``Point` 인스턴스에 대한 X, Y, Z, M 값을 반환합니다.  
  
```  
SELECT @g.STX;  
SELECT @g.STY;  
SELECT @g.Z;  
SELECT @g.M;  
```  
  
 Z 및 M 값은 다음 예에 표시된 대로 명시적으로 NULL로 지정할 수 있습니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('POINT(3 4 NULL NULL)');  
```  
  
## <a name="see-also"></a>참고 항목  
 [MultiPoint](../../relational-databases/spatial/multipoint.md)   
 [STX&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stx-geometry-data-type.md)   
 [STY&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/sty-geometry-data-type.md)   
 [공간 데이터&#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
