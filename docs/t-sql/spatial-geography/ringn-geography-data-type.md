---
title: RingN(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- RingN
- RingN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- RingN method
ms.assetid: 30f47275-2727-4d22-bbec-c0c54bcb3ac2
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e55b7990948e84d9a4cb43fe242b8304f3e9cb92
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="ringn-geography-data-type"></a>RingN(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **geography** 인스턴스의 지정된 링 `1 ≤ n ≤ NumRings()`를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.RingN (expression )  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 1부터 **polygon** 인스턴스의 링 개수 사이의 **int** 식입니다.  
  
## <a name="return-value"></a>반환 값  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 링 인덱스 **n** 값이 1보다 작으면 이 메서드는 **ArgumentOutOfRangeException**을 throw합니다. 링 인덱스 값은 1보다 크거나 같아야 하고 `NumRings()`로 반환된 숫자보다 작거나 같아야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 두 개의 링이 있는 `Polygon` 인스턴스를 만들고 두 번째 링을 반환합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653), (-122.357 47.654, -122.357 47.657, -122.349 47.657, -122.349 47.650, -122.357 47.654))', 4326);  
SELECT @g.RingN(2).ToString();  
```  
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [NumRings&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/numrings-geography-data-type.md)  
  
  
