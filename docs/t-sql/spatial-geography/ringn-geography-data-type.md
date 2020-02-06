---
title: RingN(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RingN
- RingN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- RingN method
ms.assetid: 30f47275-2727-4d22-bbec-c0c54bcb3ac2
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 8de2f7c47572e8f25fdc38ce6bb537dadfc38d7d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68042666"
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
  
## <a name="return-value"></a>Return Value  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>설명  
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
  
  
