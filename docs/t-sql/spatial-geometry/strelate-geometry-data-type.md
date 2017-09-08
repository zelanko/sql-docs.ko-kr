---
title: "STRelate (geometry 데이터 형식) | Microsoft Docs"
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
- STRelate (geometry Data Type)
- STRelate_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRelate (geometry Data Type)
ms.assetid: 9dcb5f58-35ab-4bb3-86ee-2d29eefba6d3
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 68978595626be0dae1c81c5dbc1f1187dbed6d5f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="strelate-geometry-data-type"></a>STRelate(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  1을 반환는 **geometry** 인스턴스는 다른 관련이 **기 하 도형** 관계 Extended 9 Intersection Model (DE 9IM) 패턴 행렬 값으로 정의 되 고, 그렇지 않으면 여기서는 인스턴스 를 0을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STRelate ( other_geometry, intersection_pattern_matrix )  
```  
  
## <a name="arguments"></a>인수  
 *other_geometry*  
 다른 **geometry** 인스턴스와 비교할 인스턴스 `STRelate()` 가 호출 됩니다.  
  
 *intersection_pattern_matrix*  
 문자열 형식의 **nchar(9)** 둘 사이의 DE 9IM 패턴 행렬 장치에 적합 한 값을 인코딩 **geometry** 인스턴스.  
  
## <a name="remarks"></a>주의  
 항상 null이 반환 하는 경우의 spatial reference Id (Srid)는 **geometry** 인스턴스 일치 하지 않습니다. 이 메서드는 throw 된 **ArgumentException** 행렬 잘 구성 되지 않은 경우.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **비트**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="examples"></a>예  
 다음 예제에서는 `STRelate()` 두 테스트에 **geometry** 을 통해 공간적는 명시적 DE 9IM 패턴에 대 한 인스턴스.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('POINT(5 5)', 0);  
SELECT @g.STRelate(@h, 'FF*FF****');  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

