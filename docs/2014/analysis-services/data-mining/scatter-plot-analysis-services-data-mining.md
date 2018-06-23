---
title: 산 점도 (Analysis Services-데이터 마이닝) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- charts [Analysis Services]
- mining models [Analysis Services], validating
- scatter charts
- regression algorithms [Analysis Services]
ms.assetid: 166812ec-fd1c-47c8-88db-d5041142be91
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3d087d615a5e2852cdc8d7a72a9facc5df4f33b8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082177"
---
# <a name="scatter-plot-analysis-services---data-mining"></a>산점도(Analysis Services - 데이터 마이닝)
  *산점도* 는 모델로 예측되는 값과 데이터의 실제 값을 비교하여 그래프로 표시합니다. 산점도에서 실제 값은 X축을 따라 표시되고 예측 값은 Y축을 따라 표시됩니다. 또한 예측 값과 실제 값이 정확하게 일치하는 완벽한 예측을 보여 주는 선이 표시됩니다. 이 이상적인 45도 각도 선으로부터 점의 거리는 예측의 정확도를 나타냅니다.  
  
## <a name="understanding-the-scatter-plot"></a>산점도 이해  
 마케팅 부서에서 발송된 홍보 전자 메일에 포함된 링크가 클릭된 횟수를 기반으로 일일 판매를 예측하는 모델이 있다고 가정합니다. 클릭 횟수와 판매량 모두 연속적인 숫자 값이므로 클릭 횟수를 독립 변수로 사용하고 판매를 종속 변수로 사용하여 해당 값을 그래프로 표시할 수 있습니다. 이렇게 하면 직선으로 예상 선형 관계가 표시되고 해당 선 주위에 흩어져 있는 점으로 실제 데이터와 예상 데이터의 차이가 표시됩니다. 이 분석을 통해 사용자는 결과 집합과 특정 입력 간의 상관 관계 및 이상적인 모델과의 편차를 한 눈에 확인할 수 있습니다.  
  
## <a name="interpreting-the-results"></a>결과 해석  
 다음 다이어그램에서는 방금 설명한 시나리오에 맞게 만든 산점도의 예를 보여 줍니다.  
  
 ![선형 회귀에 대 한 산 점도의 예](../media/scatterplot-callctr.gif "선형 회귀에 대 한 산 점도의 예")  
  
 선 주위에 흩어져 있는 임의의 점 위에 마우스를 놓으면 도구 설명에 예측 값 및 실제 값이 표시됩니다. 산점도에 대한 **마이닝 범례** 는 없지만 차트 자체에 모델과 관련된 점수를 표시하는 범례가 포함되어 있습니다. 점수를 해석하는 방법에 대한 자세한 내용은 [선형 회귀 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)를 참조하세요.  
  
 차트의 시각적 표현은 클립보드로 복사할 수 있지만 기본 데이터 또는 수식은 복사할 수 없습니다. 선의 회귀 수식을 보려면 모델에 대한 내용 쿼리를 만듭니다. 자세한 내용은 [선형 회귀 모델 쿼리 예제](linear-regression-model-query-examples.md)를 참조하세요.  
  
## <a name="restrictions-on-scatter-plots"></a>산점도에 대한 제한 사항  
 산점도는 **입력 선택** 탭에서 선택한 열에 예측 가능한 연속 특성이 포함되어 있는 경우에만 만들 수 있습니다. 추가로 선택할 필요는 없습니다. 산점도 차트 종류는 모델 및 특성 유형을 기반으로 **리프트 차트** 탭에 자동으로 표시됩니다.  
  
 시계열 모델에서 연속 숫자를 예측하는 경우에도 산점도를 사용하여 시계열 모델의 정확도를 측정할 수는 없습니다. 기록 데이터의 일부를 예약하는 등과 같은 다른 방법을 사용할 수 있습니다. 자세한 내용은 [시계열 모델 쿼리 예제](time-series-model-query-examples.md)를 참조하세요.  
  
## <a name="related-content"></a>관련 내용  
 다음 항목에는 산점도와 관련 정확도 차트를 만들고 사용하는 방법에 대한 자세한 내용이 나와 있습니다.  
  
|항목|링크|  
|------------|-----------|  
|타겟 메일링 모델에 대한 리프트 차트를 만드는 방법을 보여 주는 연습을 제공합니다.|[기본 데이터 마이닝 자습서](../../tutorials/basic-data-mining-tutorial.md)<br /><br /> [리프트 차트를 사용 하 여 정확도 테스트 &#40;기본 데이터 마이닝 자습서&#41;](../../tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)|  
|관련 차트 종류에 대해 설명합니다.|[리프트 차트 &#40;Analysis Services-데이터 마이닝&#41;](lift-chart-analysis-services-data-mining.md)<br /><br /> [수익 차트 &#40;Analysis Services-데이터 마이닝&#41;](profit-chart-analysis-services-data-mining.md)<br /><br /> [분류 행렬 &#40;Analysis Services-데이터 마이닝&#41;](classification-matrix-analysis-services-data-mining.md)|  
|마이닝 모델 및 마이닝 구조에 대한 교차 유효성 검사의 용도를 설명합니다.|[교차 유효성 검사 &#40;Analysis Services-데이터 마이닝&#41;](cross-validation-analysis-services-data-mining.md)|  
|리프트 차트 및 기타 정확도 차트를 만드는 단계를 설명합니다.|[테스트 및 유효성 검사 태스크 및 방법 &#40;데이터 마이닝&#41;](testing-and-validation-tasks-and-how-tos-data-mining.md)|  
  
## <a name="see-also"></a>관련 항목  
 [테스트 및 유효성 검사 &#40;데이터 마이닝&#41;](testing-and-validation-data-mining.md)  
  
  