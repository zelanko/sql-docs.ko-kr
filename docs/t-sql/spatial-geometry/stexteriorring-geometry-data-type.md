---
description: STExteriorRing(geometry 데이터 형식)
title: STExteriorRing(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STExteriorRing_TSQL
- STExteriorRing (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STExteriorRing (geometry Data Type)
ms.assetid: b402b36f-05bf-4c6d-8cd6-76c0fff19db2
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 7bdf05ddaa39a225bf77538fd492387c481c4749
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88416919"
---
# <a name="stexteriorring-geometry-data-type"></a>STExteriorRing(geometry 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

다각형인 **geometry** 인스턴스의 외부 링을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STExteriorRing ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geometry**  
  
 CLR 반환 형식: **SqlGeometry**  
  
 OGC(Open Geospatial Consortium) 형식: **LineString**  
  
## <a name="remarks"></a>설명  
 이 메서드는 **geometry** 인스턴스가 다각형이 아니면 **Null**을 반환합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 `Polygon` 인스턴스를 만들고 `STExteriorRing()`을 사용하여 다각형의 외부 링을 **LineString**으로 반환합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0),(2 2, 2 1, 1 1, 1 2, 2 2))', 0);  
SELECT @g.STExteriorRing().ToString();  
```  
  
## <a name="see-also"></a>참고 항목  
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

