---
title: Naive Bayes 모델 탐색 (기본 데이터 마이닝 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b06708d5-4477-4a51-bf8d-0b1e3c1f9ebb
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: eb35c829b798335a27a37629711acf299ac2c7c9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62472887"
---
# <a name="exploring-the-naive-bayes-model-basic-data-mining-tutorial"></a>Naive Bayes 모델 탐색(기본 데이터 마이닝 자습서)
  Naive [!INCLUDE[msCoName](../includes/msconame-md.md)] Bayes 알고리즘은 자전거 구매와 입력 특성 간의 상호 작용을 표시 하는 여러 가지 방법을 제공 합니다.  
  
 Naive [!INCLUDE[msCoName](../includes/msconame-md.md)] Bayes 뷰어는 Naive Bayes 마이닝 모델 탐색에 사용할 다음 탭을 제공 합니다.  
  
 
  
##  <a name="dependency-network"></a><a name="DependencyNetwork"></a>종속성 네트워크  
 **종속성 네트워크** 탭은 [!INCLUDE[msCoName](../includes/msconame-md.md)] 트리 뷰어의 **종속성 네트워크** 탭과 동일한 방식으로 작동 합니다. 뷰어의 각 노드는 특성을, 노드 사이의 선은 관계를 나타냅니다. 뷰어에서 예측 가능한 특성인 Bike Buyer의 상태에 영향을 주는 특성을 모두 확인할 수 있습니다.  
  
#### <a name="to-explore-the-model-in-the-dependency-network-tab"></a>종속성 네트워크 탭에서 모델을 탐색하려면  
  
1.  **마이닝 모델 뷰어** 탭의 위쪽에 있는 `TM_NaiveBayes` **마이닝 모델** 목록을 사용 하 여 모델로 전환할 수 있습니다.  
  
2.  **뷰어** 목록을 사용 하 여 **Microsoft Naive Bayes Viewer**로 전환 합니다.  
  
3.  노드를 `Bike Buyer` 클릭 하 여 해당 종속성을 식별 합니다.  
  
     분홍색 음영은 모든 특성이 자전거 구매에 영향을 준다는 것을 나타냅니다.  
  
4.  슬라이더를 조정하여 가장 큰 영향을 주는 특성을 식별합니다.  
  
     슬라이더를 내리면 [Bike Buyer] 열에 가장 큰 영향을 주는 특성만 남습니다. 슬라이더를 조정하여 소유 차량 대수, 통근 거리 및 총 자녀 수가 가장 영향을 주는 특성 중 일부임을 알 수 있습니다.  
 
  
##  <a name="attribute-profiles"></a><a name="AttributeProfiles"></a> 특성 프로필  
 **특성 프로필** 탭은 입력 특성의 여러 상태가 예측 가능한 특성의 결과에 미치는 영향을 설명 합니다.  
  
#### <a name="to-explore-the-model-in-the-attribute-profiles-tab"></a>특성 프로필 탭에서 모델을 탐색하려면  
  
1.  **예측** 가능 상자에서 `Bike Buyer` 가 선택 되어 있는지 확인 합니다.  
  
2.  **마이닝 범례** 가 **특성 프로필**의 표시를 차단 하 고 있는 경우이를 밖으로 이동 합니다.  
  
3.  **히스토그램** 막대 상자에서 **5**를 선택 합니다.  
  
     이 모델에서 5는 어느 한 변수의 상태에 지정할 수 있는 최대값입니다.  
  
     입력 특성의 각 상태 값 및 해당 특성이 예측 가능한 특성의 각 상태에서 가지는 분포와 함께 이 예측 가능 특성의 상태에 영향을 주는 특성이 나열됩니다.  
  
4.  **특성** 열에서 **소유한 자동차 수**를 찾습니다.  히스토그램에서 자전거 구매자(레이블이 1인 열)와 비구매자(레이블이 0인 열) 간의 차이를 확인하십시오. 차가 한 대 있거나 한 대도 없는 사람이 자전거를 구매할 확률이 더 높습니다.  
  
5.  자전거 구매자 (레이블이 1 인 열) 열에서 **자동차가 소유한 셀 수** 를 두 번 클릭 합니다.  
  
     **마이닝 범례** 에 보다 자세한 보기가 표시 됩니다.  
  
  
##  <a name="attribute-characteristics"></a><a name="AttributeCharacteristics"></a> 특성 특징  
 **특성 특징** 탭을 사용 하 여 특성 및 값을 선택 하 여 선택한 값 사례에서 다른 특성의 값이 표시 되는 빈도를 확인할 수 있습니다.  
  
#### <a name="to-explore-the-model-in-the-attribute-characteristics-tab"></a>특성 특징 탭에서 모델을 탐색하려면  
  
1.  **특성** 목록에서 `Bike Buyer` 가 선택 되어 있는지 확인 합니다.  
  
2.  **값** 을 **1**로 설정 합니다.  
  
     뷰어에서 자녀가 없고, 통근 거리가 짧고, 북아메리카 지역에 사는 고객이 자전거를 구매할 가능성이 더 많음을 알 수 있습니다.  
  
  
##  <a name="attribute-discrimination"></a><a name="AttributeDiscrimination"></a> 특성 판별  
 **특성 판별** 탭을 사용 하 여 자전거 구매 및 기타 특성 값의 두 불연속 값 간의 관계를 조사할 수 있습니다. `TM_NaiveBayes` 모델에는 1과 0 이라는 두 가지 상태만 있으므로 뷰어를 변경할 필요가 없습니다.  
  
 뷰어에서 차량을 소유하지 않은 사람들이 자전거를 구매하고 두 대의 차량을 소유한 사람들이 자전거를 구매하지 않는 경향이 있음을 확인할 수 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
 다른 마이닝 모델을 탐색 하려면 다음 항목을 참조 하십시오.  
  
-   [기본 데이터 마이닝 자습서 &#40;의사 결정 트리 모델 탐색&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [기본 데이터 마이닝 자습서 &#40;클러스터링 모델 탐색&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>다음 단원  
 [5 단원: 모델 테스트 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>단원의 이전 태스크  
 [기본 데이터 마이닝 자습서 &#40;클러스터링 모델 탐색&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>참고 항목  
 [Microsoft Naive Bayes Viewer를 사용 하 여 모델 찾아보기](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)   
 [마이닝 모델 뷰어를 &#40;특성 판별 탭&#41;](../../2014/analysis-services/attribute-discrimination-tab-mining-model-viewer.md)   
 [마이닝 모델 뷰어 &#40;특성 프로필 탭&#41;](../../2014/analysis-services/attribute-profiles-tab-mining-model-viewer.md)   
 [마이닝 모델 뷰어 &#40;특성 특징 탭&#41;](../../2014/analysis-services/attribute-characteristics-tab-mining-model-viewer.md)   
 [&#40;마이닝 모델 뷰어&#41;종속성 네트워크 탭](../../2014/analysis-services/dependency-network-tab-mining-model-viewer.md)  
  
  
