---
title: BufferWithTolerance(지리 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- BufferWithTolerance_TSQL
- BufferWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- BefferWithTolerance method
ms.assetid: f1783e6b-0f17-464f-b1c7-1c3f7d8aa042
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f83a4174fb599170e466a28ab06eb0d2772fd604
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52391358"
---
# <a name="bufferwithtolerance-geography-data-type"></a>BufferWithTolerance(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  지정된 허용 오차를 고려하여 **geography** 인스턴스와의 거리가 지정된 값보다 작거나 같은 모든 요소 값의 합집합을 나타내는 기하학적 개체를 반환합니다.  
  
 이 geography 데이터 형식 메서드는 **FullGlobe** 인스턴스 또는 반구보다 큰 공간 인스턴스를 지원합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.BufferWithTolerance ( distance, tolerance, relative )  
```  
  
## <a name="arguments"></a>인수  
 *distance*  
 해당 버퍼를 계산할 **geography** 인스턴스와의 거리를 지정하는 **float** 식입니다.  
  
 버퍼의 최대 거리는 0.999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 지구 둘레의 1/2) 또는 전체 구형을 초과할 수 없습니다.  
  
 *tolerance*  
 버퍼 거리에 대한 허용 오차를 지정하는 **float** 식입니다.  
  
 *tolerance* 값은 반환된 선형 근사값에 대한 이상적인 버퍼 거리의 최대 편차를 나타냅니다.  
  
 예를 들어 요소의 이상적인 버퍼 거리는 원이지만 이는 다각형으로 대략 나타내야 합니다. 허용 오차가 작을수록 다각형의 점 개수가 늘어나 결과가 더 복잡해지지만 오류는 줄어듭니다.  
  
 최소 제한은 거리의 0.1%이며, 이보다 작은 허용 오차는 최소 제한으로 올림됩니다.  
  
 *relative*  
 *tolerance* 값이 상대적인지, 아니면 절대적인지를 지정하는 **비트**입니다. 'TRUE' 또는 1인 경우 허용 오차는 상대적이며 *tolerance* 매개 변수와 각 범위 \* 타원면의 종반지름으로 계산됩니다. 'FALSE' 또는 0인 경우 허용 오차는 절대적이며 *tolerance* 값은 반환된 선형 근사값에 대한 이상적인 버퍼 거리의 최대 절대 편차입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 이 메서드는 *distance*가 숫자가 아니거나(NAN), *distance*가 양 또는 음의 무한대인 경우 **ArgumentException**을 생성합니다.  이 메서드는 *tolerance*가 0이 아니거나, 숫자가 아니거나(NaN), 양 또는 음의 무한대인 경우 **ArgumentException**을 생성합니다.  
  
 `STBuffer()`는 경우에 따라 **FullGlobe** 인스턴스를 반환합니다. 예를 들어 `STBuffer()`는 버퍼 거리가 적도에서 극지방까지의 거리보다 큰 경우 두 극지방에서 **FullGlobe** 인스턴스를 반환합니다.  
  
 이 메서드는 버퍼 거리가 다음 제한을 초과하는 경우 **FullGlobe** 인스턴스에서 **ArgumentException**을 생성합니다.  
  
 0.999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 지구 둘레의 1/2)  
  
 이론 버퍼와 계산된 버퍼 간의 오류는 최대입니다(허용 오차, 익스텐트 \* 1.E-7). 여기서 허용 오차는 *tolerance* 매개 변수의 값입니다. 익스텐트에 대한 자세한 내용은 [geometry 데이터 형식 메서드 참조](https://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e)를 확인하세요.  
  
 이 메서드는 정확하지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Point` 인스턴스를 만들고 `BufferWithTolerance()`를 사용하여 인스턴스 주위의 대략적인 버퍼를 구합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.BufferWithTolerance(1, .5, 0).ToString();  
```  
  
## <a name="see-also"></a>참고 항목  
 [STBuffer &#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stbuffer-geography-data-type.md)   
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
