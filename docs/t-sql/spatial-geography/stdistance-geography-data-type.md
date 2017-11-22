---
title: "STDistance (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STDistance_TSQL
- STDistance (geography Data Type)
dev_langs: TSQL
helpviewer_keywords: STDistance method
ms.assetid: 063d8722-e019-4d3d-8fcf-dbf5325823e7
caps.latest.revision: "22"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f504f3b6617786f4268dfedb16985a9b86f5bb0a
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="stdistance-geography-data-type"></a>STDistance(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  점 간 최단 거리를 반환 합니다.는 **geography** 인스턴스와 다른 지점 **geography** 인스턴스.  
  
> [!NOTE]  
>  `STDistance()`가장 짧은 반환 **LineString** 두 geography 형식 사이의 합니다. 이 길이는 측지 거리와 거의 같습니다. 편차 `STDistance()` 정확한 측 지 거리 일반 지구 모델에는 더 이상. 25%입니다. geodesic 형식에서 길이와 거리의 미세한 차이로 인한 혼동이 발생하지 않습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STDistance ( other_geography )  
```  
  
## <a name="arguments"></a>인수  
 *other_geography*  
 다른 **geography** stdistance () 호출 된 인스턴스 간 거리를 측정 하는 인스턴스. 경우 *other_geography* 빈 설정, stdistance ()는 null을 반환 합니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **float**  
  
 CLR 반환 형식: **SqlDouble**  
  
## <a name="remarks"></a>주의  
 Stdistance ()와 항상 null을 반환의 spatial reference Id (Srid)는 **geography** 인스턴스 일치 하지 않습니다.  
  
> [!NOTE]  
>  에 대 한 메서드는 **geography** 면적 또는 거리를 계산 하는 데이터 형식 메서드에서 사용 되는 인스턴스의 SRID에 따라 다른 결과 반환 합니다.   Srid에 대 한 자세한 내용은 참조 [Spatial Reference Identifier &#40; Srid &#41; ](../../relational-databases/spatial/spatial-reference-identifiers-srids.md).  
  
## <a name="examples"></a>예  
 다음 예제에서는 두 개의 사이의 거리를 찾습니다 **geography** 인스턴스.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SET @h = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.STDistance(@h);  
```  
  
## <a name="see-also"></a>관련 항목:  
 [지리 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
