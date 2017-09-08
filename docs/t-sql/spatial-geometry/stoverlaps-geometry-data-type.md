---
title: "STOverlaps (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STOverlaps (geometry Data Type)
- STOverlaps_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STOverlaps (geometry Data Type)
ms.assetid: 1813cba1-5780-456a-9489-6b40a79569b3
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 350456751135ecb710abd8cfa775c9906997022b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stoverlaps-geometry-data-type"></a>STOverlaps(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

1을 반환는 **geometry** 인스턴스가 다른를 겹치는 지 **기 하 도형** 인스턴스. 그렇지 않으면 0을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STOverlaps ( other_geometry )  
```  
  
## <a name="arguments"></a>인수  
 *other_geometry*  
 다른 **geometry** 인스턴스와 비교할 인스턴스 `STOverlaps()` 가 호출 됩니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **비트**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>주의  
 두 개의 **geometry** 인스턴스가 겹치는 교차점을 나타내는 영역의 차원이 동일 하며 지역 인스턴스 중 하나를 같지 않습니다.  
  
 `STOverlaps()`항상 0을 반환 하는 경우 지점 위치는 **기 하 도형** 인스턴스가 교차 없는 동일한 차원의 합니다.  
  
 항상 null이 반환 하는 경우의 spatial reference Id (Srid)는 **geometry** 인스턴스 일치 하지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 `STOverlaps()` 두 테스트에 **geometry** 겹쳐진 부분에 대 한 인스턴스.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 2 0, 2 2, 0 2, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STOverlaps(@h);  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


