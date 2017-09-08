---
title: "STExteriorRing (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STExteriorRing_TSQL
- STExteriorRing (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STExteriorRing (geometry Data Type)
ms.assetid: b402b36f-05bf-4c6d-8cd6-76c0fff19db2
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 11b006c5133b093be43415d4ead27896484f351f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stexteriorring-geometry-data-type"></a>STExteriorRing(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

외부 링을 반환 합니다.는 **기 하 도형** 다각형 인스턴스입니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STExteriorRing ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **SqlGeometry**  
  
 열기 Geospatial Consortium (OGC) 입력: **LineString**  
  
## <a name="remarks"></a>주의  
 이 메서드가 반환 **null** 경우는 **geometry** 인스턴스가 다각형 않습니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 한 `Polygon` 인스턴스 및 사용 하 여 `STExteriorRing()` 으로 다각형의 외부 링을 반환 하는 **LineString**합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0),(2 2, 2 1, 1 1, 1 2, 2 2))', 0);  
SELECT @g.STExteriorRing().ToString();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


