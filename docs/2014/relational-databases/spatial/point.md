---
title: 점 | Microsoft 문서
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Point geometry subtype [SQL Server]
- geometry data type [SQL Server], spatial data
ms.assetid: 2a596ec4-8b2f-4962-bcb4-e5c8f77edad5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c680f40a27f0a0ba450d061dae3127872d1262a7
ms.sourcegitcommit: 87f29b23d5ab174248dab5d558830eeca2a6a0a4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51017990"
---
# <a name="point"></a>점
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공간 데이터에서 `Point`는 단일 위치를 나타내는 0차원 개체 이며 Z(높이) 및 M(측정값) 값을 포함할 수 있습니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [MultiPoint](multipoint.md)   
 [STX&#40;geometry 데이터 형식&#41;](/sql/t-sql/spatial-geometry/stx-geometry-data-type)   
 [STY&#40;geometry 데이터 형식&#41;](/sql/t-sql/spatial-geometry/sty-geometry-data-type)   
 [공간 데이터&#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  
