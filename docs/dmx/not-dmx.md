---
description: NOT(DMX)
title: NOT (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 03a8ea859160af36b9c822bf01c4197e8b4c3175
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426265"
---
# <a name="not-dmx"></a>NOT(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  숫자 식에서 논리 부정을 수행하는 논리 연산자입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Expression1*  
 숫자 값을 반환하는 유효한 DMX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 인수가 TRUE로 계산되면 FALSE를 반환하고 그렇지 않으면 TRUE를 반환하는 부울 값입니다.  
  
## <a name="remarks"></a>설명  
 이 인수는 연산자가 논리 부정을 수행하기 전에 부울 값(0은 FALSE, 0이 아닌 경우 TRUE)으로 처리됩니다. *Expression1* 가 TRUE 이면 연산자는 FALSE를 반환 합니다. *Expression1* 가 FALSE 이면 연산자는 TRUE를 반환 합니다. 다음 표에서는 논리 결합이 수행되는 방법을 설명합니다.  
  
|Expression1의 값|반환 값|  
|-----------------------|---------------------|  
|true|FALSE|  
|FALSE|TRUE|  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [논리 연산자 &#40;DMX&#41;](../dmx/operators-logical.md)   
 [&#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
