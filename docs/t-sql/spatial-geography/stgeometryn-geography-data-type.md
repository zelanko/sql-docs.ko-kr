---
title: "STGeometryN (geography 데이터 형식) | Microsoft Docs"
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
- STGeometryN (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeometryN method
ms.assetid: 53755f69-cd50-475b-b3b8-a1a9157cf03a
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d5d11dc77ce692543068cba6739ef982bc8264c8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stgeometryn-geography-data-type"></a>STGeometryN(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  지정 된 반환 **geography** 요소에는 **GeometryCollection** 또는 그 하위 중 하나입니다. 점의의 하위 형식에 사용 되는 경우는 **GeometryCollection**와 같은 **MultiPoint** 또는 **MultiLineString**,이 메서드는 반환 된 **geography**  N = 1을 사용 하 여 호출 하는 경우 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STGeometryN ( expression )  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 이 **int** 식 1과의 수 **geography** 인스턴스에 **GeometryCollection**합니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>주의  
 이 메서드는 매개 변수가의 결과 보다 크면 null을 반환 [stnumgeometries ()](../../t-sql/spatial-geography/stnumgeometries-geography-data-type.md) throw 됩니다는 **ArgumentOutOfRangeException** 경우는 *식* 매개 변수가 1 보다 작은 경우  
  
## <a name="examples"></a>예  
 다음 예제에서는 한 `MultiPoint``geography` 인스턴스 및 사용 하 여 `STGeometryN()` 두 번째 찾으려고 `geography` 의 인스턴스는 **GeometryCollection**합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STGeometryN(2).ToString();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geography 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
