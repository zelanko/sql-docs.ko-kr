---
title: "STPointN (geometry 데이터 형식) | Microsoft Docs"
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
- STPointN_TSQL
- STPointN (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: STPointN (geometry Data Type)
ms.assetid: 8f0bb3b7-5cd9-42c2-b9f8-f04628653bd0
caps.latest.revision: "22"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6e35a1bc7b4466a688274a825de3a34081149207
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="stpointn-geometry-data-type"></a>STPointN(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

에 지정된 된 점을 반환는 **geometry** 인스턴스.
  
## <a name="syntax"></a>구문  
  
```  
  
.STPointN ( expression )  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 이 **int** 1 사이 있는 점의 개수 식은 **기 하 도형** 인스턴스.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **SqlGeometry**  
  
 열기 Geospatial Consortium (OGC) 입력: **지점**  
  
## <a name="remarks"></a>주의  
 경우는 **geometry** 인스턴스는 사용자가 만든, `STPointN()` 로 지정 된 점을 반환 *식* 는 원래 입력 된 순서 대로 정렬 하 여 합니다.  
  
 경우는 **geometry** 인스턴스가 시스템에서 생성 된 `STPointN()` 로 지정 된 점을 반환 *식* 동일한 순서로 모든 요소를 정렬 하 여 출력 예상 되: geometry, 다음 첫 번째 geometry (필요한 경우) 한 다음 링 내의으로 링입니다. 이 순서는 결정적입니다.  
  
 이 메서드는 1 보다 작은 값으로,이 throw 한 **ArgumentOutOfRangeException**합니다.  
  
 인스턴스에 있는 점 개수보다 큰 값을 사용하여 이 메서드를 호출하면 이 메서드는 Null을 반환합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `LineString` 인스턴스를 만들고 `STPointN()`을 사용하여 인스턴스의 설명에 있는 두 번째 점을 검색합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STPointN(2).ToString();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

