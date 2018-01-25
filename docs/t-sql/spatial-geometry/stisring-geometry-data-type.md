---
title: "STIsRing (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STIsRing_TSQL
- STIsRing (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: STIsRing (geometry Data Type)
ms.assetid: ea0063be-1c74-4cc4-ac6f-b65321ddfa54
caps.latest.revision: "21"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e54455f50c306b4a13df2c815b75995fc15dc06a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="stisring-geometry-data-type"></a>STIsRing(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

1을 반환는 **geometry** 인스턴스가 다음 요구 사항을 충족 합니다.
-   한 **LineString** 인스턴스.  
-   해당 인스턴스가 닫혀 있습니다.  
-   해당 인스턴스가 단순합니다.  
-   0을 반환 된 **LineString** 인스턴스가 요구 사항을 충족 하지 않습니다.  

 에 대 한는 **geometry** 인스턴스가 닫히고 단순, 둘 다 [stisclosed ()](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md) 및 [stissimple ()](../../t-sql/spatial-geometry/stissimple-geometry-data-type.md) 해당 인스턴스에서 호출 하는 경우 1을 반환 해야 합니다. 인스턴스 형식을 확인 하는 **geometry**를 사용 하 여 [stgeometrytype ()](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STIsRing ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **비트**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>주의  
 이 메서드는 인스턴스가 아닌 경우 null을 반환 합니다는 **LineString**합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `LineString` 인스턴스를 만들고 `STIsRing()`을 사용하여 인스턴스가 링인지 테스트합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0, 0 0)', 0);  
SELECT @g.STIsRing();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [STIsClosed&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)   
 [Stgeometrytype&#40; geometry 데이터 형식 &#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)   
 [STIsSimple &#40; geometry 데이터 형식 &#41;](../../t-sql/spatial-geometry/stissimple-geometry-data-type.md)   
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

