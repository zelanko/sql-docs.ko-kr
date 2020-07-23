---
title: PredictSequence (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: acb1982e61e622b150ee79af08e36ddcf24048ba
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970751"
---
# <a name="predictsequence-dmx"></a>PredictSequence(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  지정한 시퀀스 데이터 집합에 대한 미래의 시퀀스 값을 예측합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
PredictSequence(<table column reference>)  
PredictSequence(\<table column reference, n>)  
PredictSequence(\<table column reference, n-start, n-end>)  
```  
  
## <a name="return-type"></a>반환 형식  
 \<table expression>.  
  
## <a name="remarks"></a>설명  
 *N* 매개 변수를 지정 하면 다음 값이 반환 됩니다.  
  
-   *N* 이 0 보다 크면 다음 *n* 단계에서 가장 가능성이 높은 시퀀스 값이 반환 됩니다.  
  
-   *N-시작* 및 *n 끝* 이 모두 지정 된 경우 *n-시작* 에서 *n-end*까지의 시퀀스 값입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Sequence Clustering 마이닝 모델을 기반으로 하는 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] 데이터베이스에서 고객이 구매할 가능성이 가장 높은 다섯 개의 제품 시퀀스를 반환합니다.  
  
```  
SELECT  
  PredictSequence([Sequence Clustering].[v Assoc Seq Line Items],5)  
From  
  [Sequence Clustering]  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX &#40;함수&#41;](../dmx/functions-dmx.md)   
 [DMX&#41;일반 예측 함수 &#40;](../dmx/general-prediction-functions-dmx.md)  
  
  
