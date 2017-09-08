---
title: "STDifference (geography 데이터 형식) | Microsoft Docs"
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
- STDifference_TSQL
- STDifference (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDifference (geography Data Type)
ms.assetid: 1cde5054-b91a-41bb-812a-08c9308738af
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5afb37eb29e63d8cf08e9c158b94385a66d4c41f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stdifference-geography-data-type"></a>STDifference(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  점 집합을 나타내는 개체를 반환 **geography** 다른 범위를 벗어난 인스턴스 **geography** 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STDifference ( other_geography )  
```  
  
## <a name="arguments"></a>인수  
 *other_geography*  
 다른 **geography** stdifference ()가 호출 되는 인스턴스에서 제거할 점을 나타내는 인스턴스.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="exceptions"></a>예외  
 이 메서드에서 throw 된 **ArgumentException** 인스턴스에 대척점 하는 경우.  
  
## <a name="remarks"></a>주의  
 항상 null이 반환 하는 경우의 spatial reference identifier (Srid)는 **geography** 인스턴스 일치 하지 않습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 서버에서 반환 된 결과 집합이 확장 되었습니다 **FullGlobe** 인스턴스. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 반구보다 큰 공간 인스턴스를 지원합니다. 입력 인스턴스에 원호 세그먼트가 있을 경우에만 결과에 원호 세그먼트가 포함될 수 있습니다. 이 메서드는 정확하지 않습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-computing-the-difference-between-two-geography-instances"></a>1. 두 geography 인스턴스 간의 차이 계산  
 다음 예제에서는 `STDifference()` 두 간의 차이 계산 하려면 **geography** 인스턴스.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SET @h = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STDifference(@h).ToString();  
```  
  
### <a name="b-using-a-fullglobe-with-stdifference"></a>2. STDifference()에 FullGlobe 사용  
 다음 예에서는 `FullGlobe` 인스턴스를 사용합니다. 첫 번째 결과는 빈 `GeometryCollection`이고 두 번째 결과는 `Polygon` 인스턴스입니다. `STDifference()` 인스턴스가 매개 변수인 경우 `GeometryCollection`는 빈 `FullGlobe`을 반환합니다. 호출하는 `geography` 인스턴스의 모든 점이 `FullGlobe` 인스턴스에 포함됩니다.  
  
 `DECLARE @g geography = 'POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';`  
  
 `DECLARE @h geography = 'FULLGLOBE';`  
  
 `SELECT @g.STDifference(@h).ToString(),`  
  
 `@h.STDifference(@g).ToString();`  
  
## <a name="see-also"></a>관련 항목:  
 [Geography 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
