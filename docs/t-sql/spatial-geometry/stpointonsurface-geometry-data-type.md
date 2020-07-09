---
title: STPointOnSurface(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STPointOnSurface (geometry Data Type)
- STPointOnSurface_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STPointOnSurface (geometry Data Type)
ms.assetid: 23b2b8eb-4176-49fb-ace0-92398928d60e
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 8f3e3296ec37048fbb2bf6ba20d75db0f3b46283
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762211"
---
# <a name="stpointonsurface-geometry-data-type"></a>STPointOnSurface(geometry 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**geometry** 인스턴스의 내부에 있는 임의의 점을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STPointOnSurface ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geometry**  
  
 CLR 반환 형식: **SqlGeometry**  
  
 OGC(Open Geospatial Consortium) 형식: **Point**  
  
## <a name="remarks"></a>설명  
 이 메서드는 인스턴스가 비어 있으면 Null을 반합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Polygon` 인스턴스를 만들고 `STPointOnSurface()`를 사용하여 인스턴스의 점을 찾습니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0),(2 2, 2 1, 1 1, 1 2, 2 2))', 0);  
SELECT @g.STPointOnSurface().ToString();  
```  
  
## <a name="see-also"></a>참고 항목  
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

