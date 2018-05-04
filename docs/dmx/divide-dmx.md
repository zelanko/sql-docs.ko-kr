---
title: (나누기) (DMX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- / (divide)
- divide operator (/)
ms.assetid: 7afc06cd-054b-48c3-9c3c-9a0c17d15e63
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 9b24f49594003f453f3258c431881bd0ddda0f70
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="divide-dmx"></a>(나누기) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  한 수를 다른 수로 나누는 산술 연산을 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Dividend / Divisor  
```  
  
#### <a name="parameters"></a>매개 변수  
 *피제수*  
 숫자 값을 반환하는 유효한 DMX(Data Mining Extensions) 식입니다.  
  
 *제 수*  
 숫자 값을 반환하는 유효한 DMX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 우선 순위가 더 높은 매개 변수의 데이터 형식을 갖는 값입니다.  
  
## <a name="remarks"></a>주의  
 이 연산자가 반환하는 값은 첫 번째 식을 두 번째 식으로 나누어 나온 몫입니다.  
  
 두 식이 모두 동일한 데이터 형식으로 되어 있거나 식 하나가 암시적으로 다른 식의 데이터 형식으로 변환될 수 있어야 합니다. Divisor가 Null 값으로 계산되는 경우에는 오류가 발생합니다. Divisor와 Dividend가 모두 Null 값으로 계산되는 경우 연산자는 Null 값을 반환합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [산술 연산자 &#40;DMX&#41;](../dmx/operators-arithmetic.md)   
 [Data Mining Extensions &#40;DMX&#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [연산자 &#40;DMX&#41;](../dmx/operators-dmx.md)   
 [나누기 &#40;SSIS 식&#41;](../integration-services/expressions/divide-ssis-expression.md)   
 [&#40;나누기&#41; &#40;Transact SQL&#41;](../t-sql/language-elements/divide-transact-sql.md)  
  
  
