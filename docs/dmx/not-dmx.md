---
title: NOT (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b4a28c6be2c956636f303ccc561936f799c63b64
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68008255"
---
# <a name="not-dmx"></a>NOT(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  숫자 식에서 논리 부정을 수행하는 논리 연산자입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Expression1*  
 숫자 값을 반환하는 유효한 DMX 식입니다.  
  
## <a name="return-value"></a>Return Value  
 인수가 TRUE로 계산되면 FALSE를 반환하고 그렇지 않으면 TRUE를 반환하는 부울 값입니다.  
  
## <a name="remarks"></a>설명  
 이 인수는 연산자가 논리 부정을 수행하기 전에 부울 값(0은 FALSE, 0이 아닌 경우 TRUE)으로 처리됩니다. *Expression1* 가 TRUE 이면 연산자는 FALSE를 반환 합니다. *Expression1* 가 FALSE 이면 연산자는 TRUE를 반환 합니다. 다음 표에서는 논리 결합이 수행되는 방법을 설명합니다.  
  
|Expression1의 값|반환 값|  
|-----------------------|---------------------|  
|TRUE|FALSE|  
|FALSE|TRUE|  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [논리 연산자 &#40;DMX&#41;](../dmx/operators-logical.md)   
 [&#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
