---
title: "= (같음) (DMX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: DMX
helpviewer_keywords:
- equal operator (=)
- = (equals operator)
ms.assetid: 6ac019b1-6373-4e2c-a1ad-fe2dc6188ac3
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 6144552c3fabed866a5f85e2293f177a2e8b41f0
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="-equal-to-dmx"></a>=(같음)(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  하나의 DMX(Data Mining Extensions) 식의 값이 다른 DMX 식의 값과 같은지 확인하는 비교 연산을 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DMX_Expression = DMX_Expression   
```  
  
#### <a name="parameters"></a>매개 변수  
 *DMX_Expression*  
 유효한 DMX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 두 매개 변수가 모두 Null이 아니고 첫 번째 매개 변수 값이 두 번째 매개 변수 값과 같은 경우 부울 값에 TRUE가 포함됩니다. 두 매개 변수가 모두 Null이 아니고 첫 번째 매개 변수 값이 두 번째 매개 변수 값과 다를 경우 부울 값에 FALSE가 포함됩니다. 매개 변수 중 하나 또는 둘 모두가 Null 값으로 계산되면 부울 값에 Null 값이 포함됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [비교 연산자 &#40; DMX &#41;](../dmx/operators-comparison.md)   
 [Data Mining Extensions &#40; DMX &#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [연산자 &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  
