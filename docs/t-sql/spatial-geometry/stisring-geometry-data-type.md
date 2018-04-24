---
title: STIsRing(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STIsRing_TSQL
- STIsRing (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIsRing (geometry Data Type)
ms.assetid: ea0063be-1c74-4cc4-ac6f-b65321ddfa54
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2752540d244af88c083d185d2aceaecbae41a858
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="stisring-geometry-data-type"></a>STIsRing(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**geometry** 인스턴스가 다음 요구 사항을 충족하면 1을 반환합니다.
-   해당 인스턴스가 **LineString** 인스턴스입니다.  
-   해당 인스턴스가 닫혀 있습니다.  
-   해당 인스턴스가 단순합니다.  
-   **LineString**인스턴스가 해당 요구 사항을 충족하지 못하면 0을 반환합니다.  

 **geometry** 인스턴스가 닫히고 단순하려면 [STIsClosed()](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)와 [STIsSimple()](../../t-sql/spatial-geometry/stissimple-geometry-data-type.md)이 해당 인스턴스에서 호출될 때 1을 반환해야 합니다. **geometry**의 인스턴스 형식을 확인하려면 [STGeometryType()](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)을 사용하세요.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STIsRing ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **bit**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 이 메서드는 인스턴스가 **LineString**이 아니면 Null을 반합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `LineString` 인스턴스를 만들고 `STIsRing()`을 사용하여 인스턴스가 링인지 테스트합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0, 0 0)', 0);  
SELECT @g.STIsRing();  
```  
  
## <a name="see-also"></a>참고 항목  
 [STIsClosed&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)   
 [STGeometryType&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)   
 [STIsSimple&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stissimple-geometry-data-type.md)   
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

