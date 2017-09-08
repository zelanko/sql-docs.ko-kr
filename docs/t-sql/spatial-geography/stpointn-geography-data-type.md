---
title: "STPointN (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STPointN_TSQL
- STPointN (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPointN method
ms.assetid: 47670feb-b9e0-4b4b-af83-b9bba7da66ac
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 15a196cf9ac1c5f560a2eeee3d0262829f88480b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stpointn-geography-data-type"></a>STPointN(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  지정된 된 점을 반환는 **geography** 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STPointN ( expression )  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 이 **int** 1 사이 있는 점의 개수 식은 **geography** 인스턴스.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
 열기 Geospatial Consortium (OGC) 입력: **지점**  
  
## <a name="remarks"></a>주의  
 경우는 **geography** 인스턴스는 사용자가 만든, STPointN() 반환 하 여 지정 된 지점 *식* 는 원래 입력 된 순서 대로 정렬 하 여 합니다.  
  
 경우는 **geography** 시스템 인스턴스를 생성, STPointN() 반환 하 여 지정 된 지점 *식* 동일한 순서로 모든 요소를 정렬 하 여 출력 예상 되: 하 여 첫 번째  **geography** 인스턴스, 인스턴스 (해당 되는 경우) 내의 링 차례로 링 내의 합니다. 이 순서는 결정적입니다.  
  
 이 메서드는 1 보다 작은 값으로,이 throw 한 **ArgumentOutOfRangeException**합니다.  
  
 인스턴스에 있는 점 개수보다 큰 값을 사용하여 이 메서드를 호출하면 이 메서드는 Null을 반환합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `LineString` 인스턴스를 만들고 `STPointN()`을 사용하여 인스턴스의 설명에 있는 두 번째 점을 검색합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STPointN(2).ToString();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geography 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
