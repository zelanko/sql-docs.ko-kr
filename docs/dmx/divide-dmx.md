---
title: 나누면 (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 01d9c838e8b7a40d19a59997ae670eee19e6309b
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969854"
---
# <a name="divide-dmx"></a>(나누기)(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  한 수를 다른 수로 나누는 산술 연산을 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Dividend / Divisor  
```  
  
#### <a name="parameters"></a>매개 변수  
 *배당*  
 숫자 값을 반환하는 유효한 DMX(Data Mining Extensions) 식입니다.  
  
 *나누기*  
 숫자 값을 반환하는 유효한 DMX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 우선 순위가 더 높은 매개 변수의 데이터 형식을 갖는 값입니다.  
  
## <a name="remarks"></a>설명  
 이 연산자가 반환하는 값은 첫 번째 식을 두 번째 식으로 나누어 나온 몫입니다.  
  
 두 식이 모두 동일한 데이터 형식으로 되어 있거나 식 하나가 암시적으로 다른 식의 데이터 형식으로 변환될 수 있어야 합니다. Divisor가 Null 값으로 계산되는 경우에는 오류가 발생합니다. Divisor와 Dividend가 모두 Null 값으로 계산되는 경우 연산자는 Null 값을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [산술 연산자 &#40;DMX&#41;](../dmx/operators-arithmetic.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [&#40;DMX&#41;](../dmx/operators-dmx.md)   
 [&#40;SSIS 식&#41;나눕니다.](../integration-services/expressions/divide-ssis-expression.md)   
 [Transact-sql&#41;&#41; &#40;&#40;분할](../t-sql/language-elements/divide-transact-sql.md)  
  
  
