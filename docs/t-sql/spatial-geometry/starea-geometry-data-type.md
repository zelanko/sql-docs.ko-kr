---
title: "STArea (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STArea (geometry Data Type)
- STArea_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STArea (geometry Data Type)
ms.assetid: a7dd6083-c649-4ac3-885d-1234e0db62f1
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5ec0a874d0dc2dd8bb37ce7e04fe71cbea85f860
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="starea-geometry-data-type"></a>STArea(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  전체 표면적 반환는 **geometry** 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STArea ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **float**  
  
 CLR 반환 형식: **SqlDouble**  
  
## <a name="remarks"></a>주의  
 `STArea()`0을 반환는 **기 하 도형** 인스턴스가 0 및 1 차원 도형만 포함 하거나 비어 있는 경우 합니다. `STArea()`반환 **NULL** 경우는 **geometry** 인스턴스가 초기화 되지 않았습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-computing-the-area-of-a-polygon-instance"></a>1. Polygon 인스턴스의 면적 계산  
 다음 예제에서는 한 `Polygon``geometry` 인스턴스 선택한 다각형의 면적을 계산 합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0),(2 2, 2 1, 1 1, 1 2, 2 2))', 0);  
SELECT @g.STArea();  
```  
  
### <a name="b-computing-the-area-of-a-curvepolygon-instance"></a>2. CurvePolygon 인스턴스의 면적 계산  
 다음 예에서는 `CurvePolygon` 인스턴스의 면적을 계산합니다.  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 2, 2 0, 4 2, 4 2, 0 2))');  
 SELECT @g.STArea() AS Area;
 ```  
  
## <a name="see-also"></a>관련 항목:  
 [Geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

