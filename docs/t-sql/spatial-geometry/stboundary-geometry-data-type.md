---
title: "STBoundary (geometry 데이터 형식) | Microsoft Docs"
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
- STBoundary (geometry Data Type)
- STBoundary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STBoundary (geometry Data Type)
ms.assetid: f0551674-e6e8-4926-9038-df03f2c807d7
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9c7db74c44bd314d23c7452722159b769def5777
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="stboundary-geometry-data-type"></a>STBoundary(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  경계를 반환 된 **geometry** 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STBoundary ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="remarks"></a>주의  
 `STBoundary()`빈 반환 **GeometryCollection** 때에 대 한 끝점을 **LineString**, **CircularString**, 또는 **CompoundCurve** 인스턴스 동일합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-stboundary-on-a-linestring-instance-with-different-endpoints"></a>1. 끝점이 다른 LineString 인스턴스에 STBoundary() 사용  
 다음 예제에서는 한 `LineString``geometry` 인스턴스. `STBoundary()`경계를 반환 된 `LineString`합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 0 2, 2 0)', 0);  
SELECT @g.STBoundary().ToString();  
```  
  
### <a name="b-using-stboundary-on-a-linestring-instance-with-the-same-endpoints"></a>2. 끝점이 같은 LineString 인스턴스에 STBoundary() 사용  
 다음 예에서는 끝점이 같은 유효한 `LineString` 인스턴스를 만듭니다. `STBoundary()`는 빈 `GeometryCollection`을 반환합니다.  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 0 2, -2 2, 0 0)', 0);  
 SELECT @g.STBoundary().ToString();
 ```  
  
### <a name="c-using-stboundary-on-a-curvepolygon-instance"></a>3. CurvePolygon 인스턴스에 STBoundary() 사용  
 다음 예에서는 `STBoundary()` on a `CurvePolygon` 인스턴스를 사용합니다. `STBoundary()`는 `CircularString` 인스턴스를 반환합니다.  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::STGeomFromText('CURVEPOLYGON(CIRCULARSTRING(0 0, 2 2, 0 2, -2 2, 0 0))', 0);  
 SELECT @g.STBoundary().ToString();
 ```  
  
## <a name="see-also"></a>관련 항목:  
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
