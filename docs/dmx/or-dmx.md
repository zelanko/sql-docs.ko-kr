---
title: "또는 (DMX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: OR
dev_langs: DMX
helpviewer_keywords: OR operator
ms.assetid: 727a38a9-7f75-4963-8e8a-aa703c129d30
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 02c668382e80e240f7728639105a5beeac836707
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="or-dmx"></a>OR(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  두 숫자 식에서 논리 분리를 수행하는 논리 연산자입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Expression1 OR Expression2  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Expression1*  
 숫자 값을 반환하는 유효한 DMX(Data Mining Extensions) 식입니다.  
  
 *Expression2*  
 숫자 값을 반환하는 유효한 DMX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 인수 중 하나 또는 둘 모두가 TRUE로 계산되면 TRUE를 반환하고 그렇지 않으면 FALSE를 반환하는 부울 값입니다.  
  
## <a name="remarks"></a>주의  
 이 두 인수는 연산자가 논리 분리를 수행하기 전에 부울 값(0은 FALSE, 0이 아닌 경우 TRUE)으로 처리됩니다. 인수 중 하나 또는 둘 모두가 TRUE로 계산되는 경우 이 연산자는 TRUE를 반환합니다. 경우 *Expression1* TRUE로 평가 되 고 *Expression2* FALSE로 계산 연산자는 TRUE를 반환 합니다.  
  
 다음 표에서는 논리 분리가 수행되는 방법을 설명합니다.  
  
|Expression1의 값|Expression2의 값|반환 값|  
|-----------------------|-----------------------|---------------------|  
|TRUE|TRUE|TRUE|  
|TRUE|FALSE|TRUE|  
|FALSE|TRUE|TRUE|  
|FALSE|FALSE|FALSE|  
  
## <a name="see-also"></a>관련 항목:  
 [Data Mining Extensions &#40; DMX &#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [논리 연산자 &#40; DMX &#41;](../dmx/operators-logical.md)   
 [연산자 &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  
