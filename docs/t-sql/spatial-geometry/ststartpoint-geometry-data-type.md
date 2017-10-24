---
title: "STStartPoint (geometry 데이터 형식) | Microsoft Docs"
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
- STStartPoint_TSQL
- STStartPoint (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STStartPoint (geometry Data Type)
ms.assetid: 049917db-3f76-4053-8cd2-bc54158e89bc
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0b3349376cd0f8e23aabea6a4cb456aa216bbab6
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="ststartpoint-geometry-data-type"></a>STStartPoint(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

시작점을 반환 된 **geometry** 인스턴스.
  
## <a name="syntax"></a>구문  
  
```  
  
.STStartPoint ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **SqlGeometry**  
  
 열기 Geospatial Consortium (OGC) 입력: **지점**  
  
## <a name="remarks"></a>주의  
 `STStartPoint()`에 해당 [STPointN](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md) (1).  
  
## <a name="examples"></a>예  
 다음 예에서는 `LineString` 인스턴스를 만들고 `STStartPoint()`를 사용하여 인스턴스의 시작점을 검색합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0;  
SELECT @g.STStartPoint().ToString();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [STPointN&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md)   
 [Geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


