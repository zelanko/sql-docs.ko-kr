---
title: 리프트 차트를 사용 하 여 정확도 테스트 (기본 데이터 마이닝 자습서) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63042676"
---
# <a name="testing-accuracy-with-lift-charts-basic-data-mining-tutorial"></a>리프트 차트를 사용하여 정확도 테스트(기본 데이터 마이닝 자습서)
  데이터 마이닝 디자이너의 **마이닝 정확도 차트** 탭에서 각 모델이 얼마나 잘 예측 하는지 계산 하 고 각 모델의 결과를 다른 모델의 결과와 직접 비교할 수 있습니다. 이 비교 방법을 *리프트 차트*라고 합니다. 일반적으로 마이닝 모델의 예측 정확도는 리프트 또는 분류 정확도를 통해 측정됩니다. 이 자습서에서는 리프트 차트만 사용합니다.  
  
 이 항목에서는 다음 태스크를 수행합니다.  
  
-   [입력 데이터 선택](#BKMK_InputData)  
  
-   [정확도 차트 매개 변수 구성](#BKMK_Selecting)  
  
##  <a name="BKMK_InputData"></a>입력 데이터 선택  
 마이닝 모델의 정확도를 테스트하는 첫 번째 단계는 테스트에 사용할 데이터 원본을 선택하는 것입니다. 모델이 데이터 테스트를 얼마나 잘 수행하는지 테스트한 다음 외부 데이터에 이 모델을 사용합니다.  
  
#### <a name="to-select-the-data-set"></a>데이터 집합을 선택하려면  
  
1.  의 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 데이터 마이닝 디자이너에서 **마이닝 정확도 차트** 탭으로 전환 하 고 **입력 선택** 탭을 선택 합니다.  
  
2.  **정확도 차트에 사용할 데이터 집합을 선택** 하십시오. 그룹 상자에서 **마이닝 구조 테스트 사례 사용**을 선택 합니다. 이는 마이닝 구조를 만들 때 따로 설정 하는 테스트 데이터입니다.  
  
     다른 옵션에 대 한 자세한 내용은 [정확도 차트 유형 선택 및 차트 옵션 설정](../../2014/analysis-services/data-mining/choose-an-accuracy-chart-type-and-set-chart-options.md)을 참조 하세요.  
  
##  <a name="BKMK_Selecting"></a>정확도 차트 매개 변수 설정  
 정확도 차트를 만들려면 다음 세 가지를 정의 해야 합니다.  
  
-   정확도 차트에 포함 해야 하는 모델은 무엇 인가요?  
  
-   측정할 예측 가능한 특성을 선택 하십시오. 일부 모델에는 대상이 여러 개 있을 수 있지만 각 차트는 한 번에 하나의 결과를 측정할 수 있습니다.  
  
     정확도 차트에서 열을 **예측 가능한 열 이름** 으로 사용 하려면 열이 또는 `Predict` `Predict Only`의 사용 유형 이어야 합니다. 또한 대상 열의 콘텐츠 형식은 `Discrete` 또는 `Discretized`이어야 합니다. 즉, 리프트 차트를 사용 하 여 연속 숫자 출력에 대 한 정확도를 측정할 수 없습니다.  
  
-   모델의 일반 정확도를 측정 하거나 특정 값 (예: [자전거 구매자] = ' 예 ')을 예측할 때 정확도를 측정 하 시겠습니까?  
  
#### <a name="to-generate-the-lift-chart"></a>리프트 차트를 생성 하려면  
  
1.  데이터 마이닝 디자이너의 **입력 선택** 탭에 있는 **리프트 차트에 표시할 예측 가능한 마이닝 모델 열을 선택**하십시오 .에서 **예측 열과 값 동기화**에 대 한 확인란을 선택 합니다.  
  
2.  **예측 가능한 열 이름** 열에서 각 모델에 대해 **자전거 구매자** 가 선택 되어 있는지 확인 합니다.  
  
3.  **표시** 열에서 각 모델을 선택 합니다.  
  
     기본적으로 마이닝 구조에 있는 모델이 모두 선택되어 있습니다. 모델을 포함하지 않을 수도 있지만 이 자습서에서는 모든 모델을 선택된 채로 둡니다.  
  
4.  **예측 값** 열에서 **1**을 선택 합니다. 예측 가능한 해당 열이 포함된 각 모델에 대해 같은 값이 자동으로 채워집니다.  
  
5.  **리프트 차트** 탭을 선택 합니다.  
  
     탭을 클릭 하면 예측 쿼리가 실행 되어 테스트 데이터에 대 한 예측을 가져오고 결과를 알려진 값과 비교 합니다. 결과가 그래프에 점으로 표시됩니다.  
  
     **Predict 값** 옵션을 사용 하 여 특정 대상 결과를 지정한 경우 리프트 차트는 임의 추측 결과와 이상적인 모델의 결과를 표시 합니다.  
  
    -   임의 추측 선은 데이터를 사용 하 여 예측에 알리지 않는 모델의 정확도를 표시 합니다. 즉, 두 결과 사이에 50-50을 분할 합니다. 리프트 차트를 사용 하면 임의 추측과 비교 하 여 모델의 성능을 향상 시킬 수 있습니다.  
  
    -   이상적인 모델 선은 정확도의 상한을 나타냅니다. 모델이 항상 정확 하 게 예측 되는 경우 달성할 수 있는 최대한의 이점을 보여 줍니다.  
  
     만든 마이닝 모델은 일반적으로 이러한 두 극단 사이에 있습니다. 임의 추측의 향상 률은 *리프트*로 간주 됩니다.  
  
6.  범례를 사용하여 이상적인 모델과 임의 추측 모델을 나타내는 색이 지정된 선을 찾습니다.  
  
     모델은 `TM_Decision_Tree` 클러스터링 및 Naive Bayes 모델을 모두 수행 하는 가장 큰 리프트를 제공 합니다.  
  
 이 단원에서 만든 리프트 차트와 비슷한 리프트 차트에 대 한 자세한 설명은 [차트 &#40;Analysis Services-데이터 마이닝&#41;](../../2014/analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)를 참조 하세요.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [기본 데이터 마이닝 자습서를 &#40;필터링 된 모델 테스트&#41;](../../2014/tutorials/testing-a-filtered-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>참고 항목  
 [리프트 차트 &#40;Analysis Services-데이터 마이닝&#41;](../../2014/analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)   
 [리프트 차트 탭 &#40;마이닝 정확도 차트 뷰&#41;](../../2014/analysis-services/lift-chart-tab-mining-accuracy-chart-view.md)  
  
  
