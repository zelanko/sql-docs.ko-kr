---
title: "BufferWithTolerance (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BufferWithTolerance_TSQL
- BufferWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- BefferWithTolerance method
ms.assetid: f1783e6b-0f17-464f-b1c7-1c3f7d8aa042
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: feaa401cfd6e2077035d164412941392412011ae
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="bufferwithtolerance-geography-data-type"></a>BufferWithTolerance(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  인스턴스와의 거리가 값 하는 모든 점의 합집합을 나타내는 기하학적 개체를 반환 된 **geography** 인스턴스는 지정된 된 허용 오차 범위 지정된 된 값 보다 작습니다.  
  
 이 geography 데이터 형식 메서드 지원 **FullGlobe** 인스턴스 또는 반구 보다 큰 공간 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
  
.BufferWithTolerance ( distance, tolerance, relative )  
```  
  
## <a name="arguments"></a>인수  
 *거리*  
 한 **float** 거리를 지정 하는 식의 **geography** 인스턴스와의 버퍼를 계산할 합니다.  
  
 버퍼의 최대 거리는 0.999를 초과할 수 없습니다 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 지구 둘레의 1/2) 또는 전체 구형입니다.  
  
 *허용 오차*  
 이 **float** 버퍼 거리의 허용 오차를 지정 하는 식입니다.  
  
 *허용 오차* 값은 반환된 된 선형 근사값에 대 한 이상적인 버퍼 거리의 최대 편차를 나타냅니다.  
  
 예를 들어 요소의 이상적인 버퍼 거리는 원이지만 이는 다각형으로 대략 나타내야 합니다. 허용 오차가 작을수록 다각형의 점 개수가 늘어나 결과가 더 복잡해지지만 오류는 줄어듭니다.  
  
 최소 제한은 거리의 0.1%이며, 이보다 작은 허용 오차는 최소 제한으로 올림됩니다.  
  
 *상대*  
 **비트** 지정 여부는 *허용 오차* 상대 또는 절대 값이 합니다. 경우 '값은 TRUE' 또는 1 인 경우 허용 오차는 상대적 이며의 곱으로 계산 되는 *허용 오차* 매개 변수와 각 범위 \* 타원 면의 반지름입니다. 'FALSE' 또는 0 허용 오차는 절대적 하는 경우 및 *허용 오차* 값은 반환된 된 선형 근사값에 대 한 이상적인 버퍼 거리의 최대 절대 편차입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>주의  
 이 메서드는 throw는 **ArgumentException** 경우는 *거리* (NAN) 숫자가 아니거나 경우 *거리* 은 양수 또는 음수 infinity 합니다.  이 메서드는 또한 throw 한 **ArgumentException** 경우 *허용 오차* 가 영 (0), 하지 NaN (숫자가), 음수 또는 양 또는 음의 무한대 합니다.  
  
 `STBuffer()`반환는 **FullGlobe** ; 특정 한 경우에는 인스턴스 예를 들어 `STBuffer()` 반환는 **FullGlobe** 는 버퍼 거리가 적도 거리 보다 큰 경우 두 극 지방에서 인스턴스 극 지방 합니다.  
  
 이 메서드는 throw 된 **ArgumentException** 에 **FullGlobe** 버퍼 거리는 다음과 같은 제한 사항이 초과 하는 인스턴스:  
  
 0.999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 지구 둘레의 1/2)  
  
 이론적 버퍼와 계산 된 버퍼 간의 오차는 최대 (허용 오차, 익스텐트 \* 1.E-7) 허용 오차는의 값은 *허용 오차* 매개 변수입니다. 익스텐트에 대 한 자세한 내용은 참조 하십시오. [geography 데이터 형식 메서드 참조](http://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e)합니다.  
  
 이 메서드는 정확하지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Point` 인스턴스를 만들고 `BufferWithTolerance()`를 사용하여 인스턴스 주위의 대략적인 버퍼를 구합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.BufferWithTolerance(1, .5, 0).ToString();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Stbuffer&#40; geography 데이터 형식 &#41;](../../t-sql/spatial-geography/stbuffer-geography-data-type.md)   
 [Geography 인스턴스의 확장된 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  

