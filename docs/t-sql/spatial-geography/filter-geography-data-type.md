---
title: "필터 (geography 데이터 형식) | Microsoft Docs"
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
- Filter
- Filter_TSQL
- Filter (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Filter method
ms.assetid: 82a8f54a-3a47-4e20-b13a-b148029c5448
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 537e3a05ad368be5278eef9dc9c3d29d19754322
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="filter-geography-data-type"></a>Filter(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  여부를 확인 하는 빠른 인덱스 전용 교차 방법을 제공 하는 메서드는 **geography** 다른 인스턴스와 교차 **geography** 인스턴스와 인덱스를 사용할 수 있습니다.  
  
 1을 반환는 **geography** 교차 될 가능성이 다른 **geography** 인스턴스. 이 메서드는 거짓 긍정 결과를 반환할 수 있으며 정확한 결과는 계획에 따라 다릅니다. 교차 부분이 있는 경우 정확한 0 값 (참 부정 결과)를 반환 **geography** 인스턴스를 찾을 수 있습니다.  
  
 인덱스를 사용할 수 없거나는 사용 되지 않는 경우에서 메서드가 동일한 값으로 반환 됩니다 **stintersects ()** 동일한 매개 변수를 사용 하 여 호출 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.Filter ( other_geography )  
```  
  
## <a name="arguments"></a>인수  
 *other_geography*  
 다른 **geography** Filter() 호출 된 인스턴스에 대해 비교할 인스턴스입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **비트**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>주의  
 이 메서드는 비결정적이고 정확하지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Filter()`를 사용하여 두 `geography` 인스턴스가 서로 교차하는지 확인합니다.  
  
```  
CREATE TABLE sample (id int primary key, g geography);  
INSERT INTO sample VALUES  
   (0, geography::Point(45, -120, 4326)),  
   (1, geography::Point(45, -120.1, 4326)),  
   (2, geography::Point(45, -120.2, 4326)),  
   (3, geography::Point(45, -120.3, 4326)),  
   (4, geography::Point(45, -120.4, 4326));  
  
CREATE SPATIAL INDEX sample_idx on sample(g);  
SELECT id  
FROM sample   
WHERE g.Filter(geography::Parse(  
   'POLYGON((-120.1 44.9, -119.9 44.9, -119.9 45.1, -120.1 45.1, -120.1 44.9))')) = 1;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geography 인스턴스의 확장된 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [Stintersects&#40; geography 데이터 형식 &#41;](../../t-sql/spatial-geography/stintersects-geography-data-type.md)  
  
  
