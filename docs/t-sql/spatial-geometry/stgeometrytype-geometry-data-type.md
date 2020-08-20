---
description: STGeometryType(geometry 데이터 형식)
title: STGeometryType(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeometryType_TSQL
- STGeometryType (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeometryType (geometry Data Type)
ms.assetid: 224cdc83-aa83-4ad4-bb82-b7481031e910
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: b297708cbd8820967463f395d765474c9881189b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454318"
---
# <a name="stgeometrytype-geometry-data-type"></a>STGeometryType(geometry 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**geometry** 인스턴스로 표현된 OGC(Open Geospatial Consortium) 형식 이름을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STGeometryType ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **nvarchar(4000)**  
  
 CLR 반환 형식: **SqlString**  
  
## <a name="remarks"></a>설명  
 `STGeometryType()`에 의해 반환될 수 있는 OGC 형식 이름은 **Point**, **LineString**, **CircularString**, **CompoundCurve**, **Polygon, CurvePolygon**, **GeometryCollection**, **MultiPoint**, **MultiLineString** 및  **MultiPolygon**입니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `Polygon` 인스턴스를 만들고 `STGeometryType()`을 사용하여 이 인스턴스가 다각형인지 확인합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0))', 0);  
SELECT @g.STGeometryType();  
```  
  
## <a name="see-also"></a>참고 항목  
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

