---
title: "STDisjoint (geometry 데이터 형식) | Microsoft Docs"
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
- STDisjoint_TSQL
- STDisjoint (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDisjoint (geometry Data Type)
ms.assetid: 90acdb21-e826-4d81-afe8-45a71f33282a
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5052e2181dffe8c0404e7f33d1bbcd1ca139a45f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stdisjoint-geometry-data-type"></a>STDisjoint(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  1을 반환는 **geometry** 인스턴스가 공간적으로 다른 **geometry** 인스턴스. 그렇지 않으면 0을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STDisjoint ( other_geometry )  
```  
  
## <a name="arguments"></a>인수  
 *other_geometry*  
 다른 **geometry** 인스턴스와 비교할 인스턴스 `STDisjoint()` 가 호출 됩니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **비트**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>주의  
 두 개의 **기 하 도형** 인스턴스가 결합 되지 않았는지 점 집합이 교차 비어 있습니다.  
  
 항상 null이 반환 하는 경우의 spatial reference Id (Srid)는 **geometry** 인스턴스 일치 하지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 `STDisjoint()` 두 테스트에 **geometry** 에 대 한 인스턴스 공간 비연속입니다.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('POINT(1 1)', 0);  
SELECT @g.STDisjoint(@h);  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

