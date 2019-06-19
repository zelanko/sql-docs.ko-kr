---
title: STEndpoint(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STEndpoint (geometry Data Type)
- STEndpoint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STEndpoint (geometry Data Type)
ms.assetid: 61773c45-b568-4e0c-94da-1310c42de7f5
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: a51bb784c2cb4a9ef4ab54d46379d0dcc60d18b4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65938961"
---
# <a name="stendpoint-geometry-data-type"></a>STEndpoint(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**geometry** 인스턴스의 엔드포인트를 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STEndPoint ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geometry**  
  
 CLR 반환 형식: **SqlGeometry**  
  
 OGC(Open Geospatial Consortium) 형식: **Point**  
  
## <a name="remarks"></a>Remarks  
 `STEndPoint()`는 [STPointN](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md)(x.NumPoints())과 동일합니다.  
  
 이 메서드는 비어 있는 **geometry** 인스턴스에서 호출되면 Null을 반환합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `LineString`를 사용하여 `STGeomFromText()` 인스턴스를 만들고 `STEndpoint()`를 사용하여 `LineString`의 끝점을 검색합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STEndPoint().ToString();  
```  
  
## <a name="see-also"></a>참고 항목  
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

