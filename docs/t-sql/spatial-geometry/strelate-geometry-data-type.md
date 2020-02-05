---
title: STRelate(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STRelate (geometry Data Type)
- STRelate_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRelate (geometry Data Type)
ms.assetid: 9dcb5f58-35ab-4bb3-86ee-2d29eefba6d3
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 1e50ca09fc8ac7c9c61c17227448deebe8c69bc8
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68066307"
---
# <a name="strelate-geometry-data-type"></a>STRelate(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  **geometry** 인스턴스가 다른 **geometry** 인스턴스와 관련되어 있으며 해당 관계가 DE-9IM(Dimensionally Extended 9 Intersection Model) 패턴 행렬 값으로 정의되어 있으면 1을 반환하고, 그렇지 않으면 0을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STRelate ( other_geometry, intersection_pattern_matrix )  
```  
  
## <a name="arguments"></a>인수  
 *other_geometry*  
 **를 호출할 인스턴스와 비교할 다른** geometry`STRelate()` 인스턴스입니다.  
  
 *intersection_pattern_matrix*  
 두 **geometry** 인스턴스 간에서 DE-9IM 패턴 행렬 디바이스에 대해 인코딩을 사용할 수 있는 값 **nchar(9)** 형식의 문자열입니다.  
  
## <a name="remarks"></a>설명  
 이 메서드는 **geometry** 인스턴스의 SRID(spatial Reference ID)가 일치하지 않으면 항상 Null을 반환합니다. 이 메서드는 행렬의 형식이 잘못된 경우 **ArgumentException**을 throw합니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **bit**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="examples"></a>예  
 다음 예제에서는 `STRelate()`를 사용하여 두 **geometry** 인스턴스가 명시적 DE-9IM 패턴을 통해 공간적으로 분리되어 있는지 테스트합니다.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('POINT(5 5)', 0);  
SELECT @g.STRelate(@h, 'FF*FF****');  
```  
  
## <a name="see-also"></a>참고 항목  
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
