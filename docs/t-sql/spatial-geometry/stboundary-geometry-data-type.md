---
title: STBoundary(geometry Data Type) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STBoundary (geometry Data Type)
- STBoundary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STBoundary (geometry Data Type)
ms.assetid: f0551674-e6e8-4926-9038-df03f2c807d7
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 671e27f0e35e450b89c3eaaadc3b31612114348a
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65939086"
---
# <a name="stboundary-geometry-data-type"></a>STBoundary(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **geometry** 인스턴스의 경계를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STBoundary ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geometry**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 `STBoundary()`은 **LineString**, **CircularString** 또는 **CompoundCurve** 인스턴스의 엔드포인트가 같을 때 빈 **GeometryCollection**을 반환합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-stboundary-on-a-linestring-instance-with-different-endpoints"></a>1. 엔드포인트가 다른 LineString 인스턴스에 STBoundary() 사용  
 다음 예에서는 `LineString``geometry` 인스턴스를 만듭니다. `STBoundary()`는 `LineString`의 경계를 반환합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 0 2, 2 0)', 0);  
SELECT @g.STBoundary().ToString();  
```  
  
### <a name="b-using-stboundary-on-a-linestring-instance-with-the-same-endpoints"></a>2. 엔드포인트가 같은 LineString 인스턴스에 STBoundary() 사용  
 다음 예에서는 엔드포인트가 같은 유효한 `LineString` 인스턴스를 만듭니다. `STBoundary()`는 빈 `GeometryCollection`을 반환합니다.  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 0 2, -2 2, 0 0)', 0);  
 SELECT @g.STBoundary().ToString();
 ```  
  
### <a name="c-using-stboundary-on-a-curvepolygon-instance"></a>C. CurvePolygon 인스턴스에 STBoundary() 사용  
 다음 예에서는 `STBoundary()` on a `CurvePolygon` 인스턴스를 사용합니다. `STBoundary()`는 `CircularString` 인스턴스를 반환합니다.  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::STGeomFromText('CURVEPOLYGON(CIRCULARSTRING(0 0, 2 2, 0 2, -2 2, 0 0))', 0);  
 SELECT @g.STBoundary().ToString();
 ```  
  
## <a name="see-also"></a>참고 항목  
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
