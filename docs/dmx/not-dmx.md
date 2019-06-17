---
title: 없습니다 (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 053eb905edb1379bfdc40ec010dc6d4efadcba26
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62503849"
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
  
## <a name="return-value"></a>반환 값  
 인수가 TRUE로 계산되면 FALSE를 반환하고 그렇지 않으면 TRUE를 반환하는 부울 값입니다.  
  
## <a name="remarks"></a>Remarks  
 이 인수는 연산자가 논리 부정을 수행하기 전에 부울 값(0은 FALSE, 0이 아닌 경우 TRUE)으로 처리됩니다. 하는 경우 *Expression1* 가 TRUE 인 연산자 FALSE를 반환 합니다. 하는 경우 *Expression1* 은 FALSE 연산자 TRUE를 반환 합니다. 다음 표에서는 논리 결합이 수행되는 방법을 설명합니다.  
  
|Expression1의 값|반환 값|  
|-----------------------|---------------------|  
|TRUE|FALSE|  
|false|TRUE|  
  
## <a name="see-also"></a>관련 항목  
 [Data Mining Extensions &#40;DMX&#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [논리 연산자 &#40;DMX&#41;](../dmx/operators-logical.md)   
 [연산자 &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
