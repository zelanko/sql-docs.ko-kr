---
description: PredictCaseLikelihood(DMX)
title: PredictCaseLikelihood (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b182e4a3a842065152b050ed1b428d71b7d0cf07
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426125"
---
# <a name="predictcaselikelihood-dmx"></a>PredictCaseLikelihood(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  이 함수는 입력 사례가 기존 모델에 적합할 가능성을 반환합니다. 클러스터링 모델에서만 사용합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
PredictCaseLikelihood([NORMALIZED|NONNORMALIZED])  
```  
  
## <a name="arguments"></a>인수  
 NORMALIZED  
 모델에 있는 사례의 확률을 모델이 없는 사례의 확률로 나눈 값이 반환됩니다.  
  
 NONNORMALIZED  
 사례 특성의 확률을 곱한 값인 사례의 원시 확률이 반환됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [!INCLUDE[msCoName](../includes/msconame-md.md)]클러스터링 및 시퀀스 클러스터링 알고리즘을 사용 하 여 작성 된 모델 [!INCLUDE[msCoName](../includes/msconame-md.md)] 입니다.  
  
## <a name="return-type"></a>반환 형식  
 0에서 1 사이의 배정밀도 부동 소수점 숫자입니다. 1에 가까울수록 이 모델에 사례가 나타날 확률이 높음을 나타내고 0에 가까울수록 이 모델에 사례가 나타날 가능성이 낮음을 나타냅니다.  
  
## <a name="remarks"></a>설명  
 기본적으로 **PredictCaseLikelihood** 함수의 결과는 정규화 됩니다. 일반적으로 정규화된 값은 사례 증가에 있는 특성 수와 두 사례의 원시 확률 간 차이가 작을수록 더 유용합니다.  
  
 다음 수식은 x와 y가 제공될 경우 정규화된 값을 계산하는 데 사용됩니다.  
  
-   x = 클러스터링 모델을 기반으로 하는 사례가 나타날 가능성  
  
-   y = 학습 사례 수를 기반으로 하는 사례의 로그 유사도로 계산되는 한계 사례가 나타날 가능성  
  
-   Z = Exp (log (x)-Log (Y))  
  
 정규화 된 = (z/(1 + z))  
  
## <a name="examples"></a>예제  
 다음 예에서는 [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW 데이터베이스를 기반으로 하는 클러스터링 모델에 지정한 사례가 나타날 가능성을 반환합니다.  
  
```  
SELECT  
  PredictCaseLikelihood() AS Default_Likelihood,  
  PredictCaseLikelihood(NORMALIZED) AS Normalized_Likelihood,  
  PredictCaseLikelihood(NONNORMALIZED) AS Raw_Likelihood,  
FROM  
  [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
 예상 결과:  
  
|Default_Likelihood|Normalized_Likelihood|Raw_Likelihood|  
|-------------------------|----------------------------|---------------------|  
|6.30672792729321E-08|6.30672792729321E-08|9.5824454056846E-48|  
  
 이러한 결과 간의 차이는 정규화의 효과를 보여 줍니다. **CaseLikelihood** 에 대 한 원시 값은 사례의 확률이 약 20% 임을 나타냅니다. 그러나 결과를 정규화 하면 사례의 가능성이 매우 낮을 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 알고리즘 &#40;Analysis Services 데이터 마이닝&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX &#40;함수&#41;](../dmx/functions-dmx.md)   
 [DMX&#41;일반 예측 함수 &#40;](../dmx/general-prediction-functions-dmx.md)  
  
  
