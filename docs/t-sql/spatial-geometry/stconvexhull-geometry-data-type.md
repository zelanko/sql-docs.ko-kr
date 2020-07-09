---
title: STConvexHull(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STConvexHull (geometry Data Type)
- STConvexHull_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STConvexHull (geometry Data Type)
ms.assetid: 60a520a6-1a7c-486b-8d91-34401edf6233
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: ba1d23e85d18215092768e41f7962516b3ff036a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85748726"
---
# <a name="stconvexhull-geometry-data-type"></a>STConvexHull(geometry 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**geometry** 인스턴스의 볼록 집합을 나타내는 개체를 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STConvexHull ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geometry**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="remarks"></a>설명  
 `STConvexHull()`은 지정된 **geometry** 인스턴스가 포함된 가장 작은 볼록 다각형(convex polygon)을 반환합니다. **Point** 또는 동축 **LineString** 인스턴스는 입력 형식과 동일한 형식의 인스턴스를 생성합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `STConvexHull()`을 사용하여 비볼록 `Polygon``geometry` 인스턴스의 볼록 집합을 찾습니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 1 1, 2 2, 2 0, 0 0))', 0);  
SELECT @g.STConvexHull().ToString();  
```  
  
## <a name="see-also"></a>참고 항목  
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

