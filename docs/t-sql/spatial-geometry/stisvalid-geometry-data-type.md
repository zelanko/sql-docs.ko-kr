---
title: "STIsValid (geometry 데이터 형식) | Microsoft Docs"
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
- STIsValid (geometry Data Type)
- STIsValid_TSQL
dev_langs: TSQL
helpviewer_keywords: STIsValid (geometry Data Type)
ms.assetid: 6da39bea-0f67-4660-98fc-d7214f9b2138
caps.latest.revision: "23"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2b2d68cd92401a37a5ed19f4cd23165e6c0b9701
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="stisvalid-geometry-data-type"></a>STIsValid(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

이면 true를 반환은 **geometry** 인스턴스가 제대로 구성 된 해당 Open Geospatial Consortium (OGC) 형식을 기반으로 합니다. 되었으면 false를 반환 된 **기 하 도형** 인스턴스 형식이 잘못 되었습니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STIsValid ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **비트**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>주의  
 OGC 형식은 **geometry** 를 호출 하 여 인스턴스를 확인할 수 있습니다 [stgeometrytype ()](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]유효한 생성 **기 하 도형** 인스턴스에 하지만 검색의 잘못 된 인스턴스 확인 하 고 저장소에 대 한 허용 합니다. 잘못된 인스턴스의 동일한 점 집합을 나타내는 올바른 인스턴스는 `MakeValid()` 메서드를 사용하여 검색할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `geometry` 인스턴스를 만들고 `STIsValid()`를 사용하여 인스턴스가 올바른지 테스트합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STIsValid();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Stgeometrytype&#40; geometry 데이터 형식 &#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)   
 [MakeValid&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/makevalid-geometry-data-type.md)   
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

