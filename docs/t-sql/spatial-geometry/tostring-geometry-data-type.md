---
title: "ToString (geometry 데이터 형식) | Microsoft Docs"
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
f1_keywords: ToString (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: ToString (geometry Data Type)
ms.assetid: 2e55fa98-aa22-4baa-a516-7c233a33e212
caps.latest.revision: "21"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 06bf05558bfefdf679d479429f5e71afcfcb7c6b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="tostring-geometry-data-type"></a>ToString(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

인스턴스에서 얻어진 Z(높이) 값 및 M(측정값) 값을 사용하여 보강된 geometry 인스턴스의 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.ToString ()  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **nvarchar (max)**  
  
 CLR 반환 형식: **SqlString**  
  
## <a name="remarks"></a>주의  
 이 메서드는 Null 인스턴스가 호출되면 문자열 "Null"을 반환합니다.  
  
 Null이 아닌 인스턴스에서 이 메서드는 `AsTextZM().`을 사용하는 것과 동일합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 만들기는 `LineString` 인스턴스 및 사용 하 여 `ToString()` 를 인스턴스의 텍스트 설명을 인출 합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 0 1, 1 0)', 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Stastext&#40; geometry 데이터 형식 &#41;](../../t-sql/spatial-geometry/stastext-geometry-data-type.md)   
 [geometry 인스턴스의 확장 메서드](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

