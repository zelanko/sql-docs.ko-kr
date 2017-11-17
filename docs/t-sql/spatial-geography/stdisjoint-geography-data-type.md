---
title: "STDisjoint (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STDisjoint (geography Data Type)
- STDisjoint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STDisjoint
ms.assetid: 98328a02-e018-47d6-aa93-de162b8aef62
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a9f0a6aaadb3bfa84d7b08f547c399574c9bcfa4
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stdisjoint-geography-data-type"></a>STDisjoint(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  1을 반환는 **geography** 인스턴스가 공간적으로 다른 **geography** 인스턴스. 그렇지 않으면 0을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STDisjoint ( other_geography )  
```  
  
## <a name="arguments"></a>인수  
 *other_geography*  
 다른 **geography** STDisjoint() 호출 된 인스턴스에 대해 비교할 인스턴스입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **비트**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>주의  
 두 개의 **geography** 인스턴스가 결합 되지 않았는지 점 집합이 교차 비어 있습니다.  
  
 항상 null이 반환 하는 경우의 spatial reference Id (Srid)는 **geography** 인스턴스 일치 하지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `STDisjoint()`를 사용하여 두 `geography` 인스턴스가 공간적으로 분리되어 있는지 테스트합니다.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SET @h = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.STDisjoint(@h);  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geography 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

