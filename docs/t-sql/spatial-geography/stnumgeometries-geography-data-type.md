---
title: "STNumGeometries (geography 데이터 형식) | Microsoft Docs"
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
- STNumGeometries (geography Data Type)
- STNumGeometries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumGeometries method
ms.assetid: 6ae7fac2-62f1-420f-9fc9-a09606be9605
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4b309210790056ed6e938e037a28d7634f1582c8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stnumgeometries-geography-data-type"></a>STNumGeometries(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  개수를 반환 **기 하 도형** 구성 하는 한 **geography** 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STNumGeometries ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **int**  
  
 CLR 반환 형식: **SqlInt32**  
  
## <a name="remarks"></a>주의  
 이 메서드는 경우 1을 반환는 **geography** 인스턴스가 않습니다는 **MultiPoint**, **MultiLineString**, **MultiPolygon**, 또는 **GeometryCollection** 인스턴스 또는 인 경우 0은 **geography** 인스턴스가 비어 있습니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 한 `MultiPoint` 인스턴스 및 사용 하 여 `STNumGeometries()` 방법을 찾기 위해 많은 **기 하 도형** 인스턴스를 포함 합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT((-122.360 47.656), (-122.343 47.656))', 4326);  
SELECT @g.STNumGeometries();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geography 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

