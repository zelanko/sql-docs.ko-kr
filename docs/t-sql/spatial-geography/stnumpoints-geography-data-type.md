---
title: STNumPoints(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STNumPoints (geography Data Type)
- STNumPoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumPoints method
ms.assetid: 25ff7ad1-ba5f-4cfb-816a-59255ac1591d
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 372dea8b43f386795d49274ed63d62b862ecff43
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552469"
---
# <a name="stnumpoints-geography-data-type"></a>STNumPoints(geography 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  **geography** 인스턴스의 각 도형에 있는 점의 총 개수를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STNumPoints ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **int**  
  
 CLR 반환 형식: **SqlInt32**  
  
## <a name="remarks"></a>설명  
 이 메서드는 **geography** 인스턴스의 설명에 있는 점을 셉니다. 중복 점도 개수에 포함되지만 세그먼트 사이의 연결 점은 한 번만 셉니다. 이 인스턴스가 컬렉션인 경우 이 메서드는 컬렉션에 있는 점의 총 개수를 반환합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-retrieving-the-total-number-of-points-in-a-linestring"></a>A. LineString에 있는 점의 총 개수 검색  
 다음 예에서는 `LineString` 인스턴스를 만들고 `STNumPoints()`를 사용하여 인스턴스의 설명에 사용된 점의 수를 확인합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STNumPoints();  
```  
  
### <a name="b-retrieving-the-total-number-of-points-in-a-geometrycollection"></a>B. GeometryCollection에 있는 점의 총 개수 검색  
 다음 예에서는 `GeometryCollection`에 있는 모든 요소에 대해 점의 합계를 반환합니다.  
  
```  
DECLARE @g geography = 'GEOMETRYCOLLECTION(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)  
    ,CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)))';  
SELECT @g.STNumPoints();  
```  
  
### <a name="c-returning-the-number-of-points-in-a-compoundcurve"></a>C. CompoundCurve에 있는 점의 개수 반환  
 다음 예에서는 CompoundCurve 인스턴스에 있는 점의 개수를 반환합니다. STNumPoints()가 세그먼트 사이의 연결 점을 한 번만 세므로 쿼리는 6이 아닌 5를 반환합니다.  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658),( -122.348 47.658, -121.56 48.12, -122.358 47.653))'  
 SELECT @g.STNumPoints();
 ```  
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
