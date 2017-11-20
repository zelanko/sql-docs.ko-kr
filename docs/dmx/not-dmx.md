---
title: "없습니다 (DMX) | Microsoft Docs"
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
f1_keywords:
- NOT
dev_langs:
- DMX
helpviewer_keywords:
- NOT operator [DMX]
ms.assetid: 6d91b3d9-270c-4a68-b41f-169cff5faa0e
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 947d066f9dd13d7f4af15407987fcf218c275cc2
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

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
  
## <a name="remarks"></a>주의  
 이 인수는 연산자가 논리 부정을 수행하기 전에 부울 값(0은 FALSE, 0이 아닌 경우 TRUE)으로 처리됩니다. 경우 *Expression1* 은 TRUE, FALSE 연산자를 반환 합니다. 경우 *Expression1* 가 FALSE 이면 연산자는 TRUE를 반환 합니다. 다음 표에서는 논리 결합이 수행되는 방법을 설명합니다.  
  
|Expression1의 값|반환 값|  
|-----------------------|---------------------|  
|TRUE|FALSE|  
|FALSE|TRUE|  
  
## <a name="see-also"></a>관련 항목:  
 [Data Mining Extensions &#40; DMX &#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [논리 연산자 &#40; DMX &#41;](../dmx/operators-logical.md)   
 [연산자 &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  

