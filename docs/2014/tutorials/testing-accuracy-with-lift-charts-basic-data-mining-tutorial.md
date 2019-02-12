---
title: 리프트 차트 (기본 데이터 마이닝 자습서)를 사용 하 여 정확도 테스트 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 822d414b-4a39-473f-80c3-53476e30655a
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 06cefcdac192b715fe843f842088456f769cdd24
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56033924"
---
# <a name="testing-accuracy-with-lift-charts-basic-data-mining-tutorial"></a>리프트 차트를 사용하여 정확도 테스트(기본 데이터 마이닝 자습서)
  에 **마이닝 정확도 차트** 탭 데이터 마이닝 디자이너의 예측을 사용 하면 각 모델이 얼마나 잘 계산 및 다른 모델의 결과 대해 직접 각 모델의 결과 비교할 수 있습니다. 이 비교 방법을 라고 하는 *리프트 차트*합니다. 일반적으로 마이닝 모델의 예측 정확도는 리프트 또는 분류 정확도를 통해 측정됩니다. 이 자습서에서는 리프트 차트만 사용합니다.  
  
 이 항목에서는 다음 태스크를 수행합니다.  
  
-   [입력된 데이터 선택](#BKMK_InputData)  
  
-   [정확도 차트 매개 변수를 구성 합니다.](#BKMK_Selecting)  
  
##  <a name="BKMK_InputData"></a> 입력된 데이터 선택  
 마이닝 모델의 정확도를 테스트하는 첫 번째 단계는 테스트에 사용할 데이터 원본을 선택하는 것입니다. 모델이 데이터 테스트를 얼마나 잘 수행하는지 테스트한 다음 외부 데이터에 이 모델을 사용합니다.  
  
#### <a name="to-select-the-data-set"></a>데이터 집합을 선택하려면  
  
1.  전환할 합니다 **마이닝 정확도 차트** 데이터 마이닝 디자이너의 탭 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 선택한를 **입력 선택** 탭 합니다.  
  
2.  에 **정확도 차트에 사용할 데이터 집합 선택** 그룹 상자에서 **마이닝 구조 테스트 사례를 사용 하 여**입니다. 이 마이닝 구조를 작성할 때 따로 설정한 테스트 데이터입니다.  
  
     다른 옵션에 대 한 자세한 내용은 참조 하세요. [정확도 차트 유형 선택 및 차트 옵션 설정](../../2014/analysis-services/data-mining/choose-an-accuracy-chart-type-and-set-chart-options.md)합니다.  
  
##  <a name="BKMK_Selecting"></a> 정확도 차트 매개 변수를 설정합니다.  
 정확도 차트를 만들려면 다음 세 가지를 정의 해야 합니다.  
  
-   모델 정확도 차트에 포함 해야?  
  
-   예측 가능한 특성을 측정 하 시겠습니까? 일부 모델에는 여러 대상이 있을 수 있지만 각 차트 한 번에 하나의 결과 측정할 수 있습니다.  
  
     열을 사용 하는 **예측 가능한 열 이름** 정확도 차트를 열의 사용 유형이 있어야 `Predict` 또는 `Predict Only`합니다. 또한 콘텐츠 형식의 대상 열 중 하나 여야 합니다 `Discrete` 또는 `Discretized`합니다. 즉, 리프트 차트를 사용 하 여 연속 숫자 출력에 대 한 정확도 측정할 수 있습니다.  
  
-   모델의 일반적인 정확도 나 특정 값을 예측의 정확도 측정 하 시겠습니까 ([Bike Buyer]와 같은 = 'Yes')  
  
#### <a name="to-generate-the-lift-chart"></a>리프트 차트를 생성 하려면  
  
1.  에 **입력 선택** 데이터 마이닝 디자이너의 탭 아래에 있는 **리프트 차트에 표시할 예측 가능한 마이닝 모델 열 선택**에 대 한 확인란을 선택 **예측 열 동기화 및 값**합니다.  
  
2.  에 **예측 가능한 열 이름** 열 확인 **Bike Buyer** 가 각 모델에 대 한 선택입니다.  
  
3.  에 **표시** 열, 각 선택 모델입니다.  
  
     기본적으로 마이닝 구조에 있는 모델이 모두 선택되어 있습니다. 모델을 포함하지 않을 수도 있지만 이 자습서에서는 모든 모델을 선택된 채로 둡니다.  
  
4.  에 **예측 값** 열 선택 **1**합니다. 예측 가능한 해당 열이 포함된 각 모델에 대해 같은 값이 자동으로 채워집니다.  
  
5.  선택 된 **리프트 차트** 탭 합니다.  
  
     탭을 클릭 하면 테스트 데이터에 대 한 예측을 구하려면 예측 쿼리를 실행 하 고 결과 알려진된 값과 비교 됩니다. 결과가 그래프에 점으로 표시됩니다.  
  
     사용 하 여 특정 대상 결과 지정 하는 경우는 **예측 값** 임의 추측의 결과 및 이상적인 모델의 결과 옵션을 리프트 차트를 그립니다.  
  
    -   임의 추측 선은 정확도 모델 예측을 알리기 위해 모든 데이터를 사용 하지 않고 될 것을 보여 줍니다: 즉, 두 가지 결과 50 ~ 50 분할 합니다. 리프트 차트를 사용 하면 얼마나 잘 모델 수행 하는 임의 추측에 비해 시각화할 수 있습니다.  
  
    -   이상적인 모델 선은 상한 값의 정확도 나타냅니다. 모델에는 항상 정확 하 게 예측 하는 경우 얻을 수 있습니다 최대 가능한 이점을 보여줍니다.  
  
     사용자가 만든 마이닝 모델 간에 이러한 두 가지 극단적인 일반적으로 대체 됩니다. 임의 추측의 향상 된 기능으로 간주 됩니다 *리프트*합니다.  
  
6.  범례를 사용하여 이상적인 모델과 임의 추측 모델을 나타내는 색이 지정된 선을 찾습니다.  
  
     있다는 사실을 알 수는 `TM_Decision_Tree` 모델은 클러스터링 및 Naive Bayes 모델을 능가 하는 가장 큰 리프트를 제공 합니다.  
  
 에 대 한 자세한 설명은이 단원에서 만든 것과 비슷한 리프트 차트를 참조 하세요 [리프트 차트 &#40;Analysis Services-데이터 마이닝&#41;](../../2014/analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [필터링된 된 모델을 테스트 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/testing-a-filtered-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>관련 항목  
 [리프트 차트&#40;Analysis Services - 데이터 마이닝&#41;](../../2014/analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)   
 [리프트 차트 탭 &#40;마이닝 정확도 차트 뷰&#41;](../../2014/analysis-services/lift-chart-tab-mining-accuracy-chart-view.md)  
  
  
