---
title: "STIntersects (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STIntersects (geography Data Type)
- STIntersects_TSQL
dev_langs: TSQL
helpviewer_keywords: STIntersects method
ms.assetid: c9db8b42-83c7-48c6-8963-fce54eb34c05
caps.latest.revision: "16"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 252deed5ef67690f599f9f1a5827884031a08c4e
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="stintersects-geography-data-type"></a>STIntersects(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

  1을 반환는 **geography** 다른 인스턴스와 교차 **geography** 인스턴스. 그렇지 않으면 0을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STIntersects ( other_geography )  
```  
  
## <a name="arguments"></a>인수  
 *other_geography*  
 다른 **geography** 인스턴스와 비교할 인스턴스 `STIntersects()` 가 호출 됩니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **비트**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>주의  
 이 메서드는 항상 반환 **NULL** 경우의 spatial reference Id (Srid)는 **geography** 인스턴스 일치 하지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `STIntersects()`를 사용하여 두 `geography` 인스턴스가 서로 교차하는지 확인합니다.  
  
```  
 DECLARE @g geography;  
 DECLARE @h geography;  
 SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
 SET @h = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
```  
  
 ```
 SELECT CASE @g.STIntersects(@h) 
 WHEN 1 THEN '@g intersects @h'  
 ELSE '@g does not intersect @h'  
 END;
 ```  
  
## <a name="see-also"></a>관련 항목:  
 [지리 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
