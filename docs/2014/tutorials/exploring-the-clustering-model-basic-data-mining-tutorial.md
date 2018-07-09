---
title: 클러스터링 모델 (기본 데이터 마이닝 자습서) 탐색 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ce8aa034-161b-473f-baec-9c29e0a8e5f5
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 35cbe12526fbd8ead78132f8560368b62e50aa61
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37153384"
---
# <a name="exploring-the-clustering-model-basic-data-mining-tutorial"></a>클러스터링 모델 탐색(기본 데이터 마이닝 자습서)
  [!INCLUDE[msCoName](../includes/msconame-md.md)] 경우 비슷한 특징을 가진 클러스터로 그룹화 하는 클러스터링 알고리즘입니다. 이러한 그룹화는 데이터 탐색, 데이터 내 잘못된 부분 식별, 예측 만들기 등에 유용합니다.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] 클러스터 뷰어는 클러스터링 마이닝 모델 탐색 시 사용할 수 있는 다음과 같은 탭을 제공합니다.  
  

  
##  <a name="ClusterDiagramTab"></a> 클러스터 다이어그램 탭  
 클러스터 다이어그램 탭에서는 마이닝 모델에 있는 클러스터를 모두 표시합니다. 클러스터 사이의 선은 "일치 정도"를 나타내며 클러스터가 얼마나 비슷한지에 따라 음영 처리됩니다. 각 클러스터의 실제 색은 클러스터에 있는 변수와 상태의 빈도를 나타냅니다.  
  
#### <a name="to-explore-the-model-in-the-cluster-diagram-tab"></a>클러스터 다이어그램 탭에서 모델을 탐색하려면  
  
1.  사용 하 여는 **마이닝 모델** 목록 맨 위에 있는 합니다 **마이닝 모델 뷰어** 탭으로 전환 합니다 `TM_Clustering` 모델.  
  
2.  에 **뷰어** 목록에서 **Microsoft 클러스터 뷰어**합니다.  
  
3.  에 **음영 변수** 상자에서 **Bike Buyer**합니다.  
  
     기본 변수는 **채우기**, 원하는 특성이 있는 멤버를 포함 하는 클러스터 검색할 모델의 모든 특성에이 변경할 수 있습니다.  
  
4.  선택 **1** 에 **상태** 자전거를 구매한 사례만 탐색 하는 상자입니다.  
  
     합니다 **밀도** 범례에서는 음영 변수 및 상태에서 선택한 특성 상태 쌍의 밀도 설명 합니다. 이 예제를 보여 줍니다 clusterwith 가장 짙은 음영이 자전거 구매자 비율이 가장 높은 있습니다.  
  
5.  음영이 가장 짙은 클러스터 위에 마우스를 놓습니다.  
  
     도구 설명에서 특성이 `Bike Buyer = 1`인 사례의 비율을 표시합니다.  
  
6.  밀도가 가장 높은, 클러스터를 마우스 오른쪽 단추로 클릭을 선택 하는 클러스터를 선택 **클러스터 이름 바꾸기** 유형과 **Bike Buyers High** 나중에 식별에 대 한 합니다. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  음영이 가장 밝고 밀도가 가장 낮은 클러스터를 찾습니다. 클러스터를 마우스 오른쪽 단추로 클릭 한 다음를 선택 합니다 **클러스터 이름 바꾸기** 유형과 **Bike Buyers Low**합니다. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  클릭 합니다 **Bike Buyers High** 클러스터를 다른 클러스터에 대 한 연결의 확실 한 시야를 얻을 수 있는 창의 영역으로 끌어 놓습니다.  
  
     클러스터를 선택하면 이 클러스터를 다른 클러스터에 연결하는 선이 강조 표시되므로 이 클러스터에 대한 모든 관계를 쉽게 볼 수 있습니다. 클러스터를 선택하지 않은 경우 다이어그램에 있는 모든 클러스터 간 관계의 밀접도는 선이 짙은 정도로 알 수 있습니다. 음영이 옅거나 없으면 두 클러스터가 그다지 유사하지 않은 것입니다.  
  
9. 네트워크 왼쪽의 슬라이더를 사용하여 약한 링크를 필터로 제외시키고 가장 밀접한 관계가 있는 클러스터를 찾을 수 있습니다. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 마케팅 부서에서 대상 메일을 배달하기 위한 최상의 방법을 결정할 때 유사한 클러스터를 함께 결합할 수 있습니다.  
  

  
##  <a name="ClusterProfilesTab"></a> 클러스터 프로필 탭  
 합니다 **클러스터 프로필** 탭의 전체 보기를 제공 합니다 `TM_Clustering` 모델입니다. 합니다 **클러스터 프로필** 탭에는 모델의 각 클러스터에 대 한 열이 포함 되어 있습니다. 첫 번째 열에는 적어도 하나의 클러스터와 연결된 특성이 나열됩니다. 뷰어의 나머지 부분에는 각 클러스터에 대한 특성의 상태 분포가 있습니다. 불연속 변수의 분포는 막대의 최대 수를 사용 하 여 색이 지정 된 막대로 표시 합니다 **히스토그램 막대** 목록입니다. 연속 특성은 각 클러스터의 평균과 표준 편차를 나타내는 다이아몬드 차트를 사용하여 표시됩니다.  
  
#### <a name="to-explore-the-model-in-the-cluster-profiles-tab"></a>클러스터 프로필 탭에서 모델을 탐색하려면  
  
1.  설정할 **히스토그램** 막대가 **5**합니다.  
  
     이 모델에서 5는 어느 한 변수의 상태에 지정할 수 있는 최대값입니다.  
  
2.  경우는 **마이닝 범례** 의 표시를 차단 합니다 **특성 프로필**,으로 이동 합니다.  
  
3.  선택 합니다 **Bike Buyers High** 열 오른쪽으로 끌어서 놓습니다 합니다 **채우기** 열.  
  
4.  선택 합니다 **Bike Buyers Low** 열 오른쪽으로 끌어서 놓습니다 합니다 **Bike Buyers High** 열입니다.  
  
5.  클릭 합니다 **Bike Buyers High** 열입니다.  
  
     합니다 **변수** 열이 해당 클러스터에 대 한 중요도 순으로 정렬 합니다. 열을 스크롤하고 Bike Buyer High 클러스터의 특징을 검토합니다. 예를 들어 이 클러스터에 속한 사람들은 통근 거리가 짧을 가능성이 더 많습니다.  
  
6.  두 번 클릭 합니다 **Age** 셀에 **Bike Buyers High** 열입니다.  
  
     합니다 **마이닝 범례** 보다 자세하게 표시 보기 하는 평균 뿐만 아니라 이러한 고객의 연령 범위를 볼 수 있습니다.  
  
7.  마우스 오른쪽 단추로 클릭 합니다 **Bike Buyers Low** 선택한 열 **Hide Column**합니다.  
  

  
##  <a name="ClusterCharacteristicsTab"></a> 클러스터 특징 탭  
 사용 하 여 합니다 **클러스터 특징** 탭을 검사할 수 있습니다 자세히 클러스터를 구성 하는 특성입니다. 클러스터 프로필 탭에서 모든 클러스터의 특징을 비교하는 대신 한 번에 하나의 클러스터를 탐색할 수 있습니다. 예를 들어, 선택 하는 경우 **Bike Buyers High** 에서 합니다 **클러스터** 목록에서이 클러스터의 고객 특징을 볼 수 있습니다. 클러스터 프로필 뷰어와 다르게 표시되지만 결과는 동일합니다.  
  
> [!NOTE]  
>  초기 값을 설정 하지 않으면 **holdoutseed**, 결과 모델을 처리할 때마다 달라 집니다. 자세한 내용은 참조 하세요. [HoldoutSeed 요소](../analysis-services/scripting/properties/holdoutseed-element.md)  
  

  
##  <a name="ClusterDiscriminationTab"></a> 클러스터 판별 탭  
 사용 하 여 합니다 **클러스터 판별** 탭에서 다른 클러스터를 구별 하는 특징을 탐색할 수 있습니다. 두 클러스터를 선택한 후는 **클러스터 1** 목록 및 합니다 **Cluster 2** 뷰어의 클러스터 간의 차이가 계산 되어 목록과 특성 목록을 표시 하는 대부분의 클러스터를 구분 합니다.  
  
#### <a name="to-explore-the-model-in-the-cluster-discrimination-tab"></a>클러스터 판별 탭에서 모델을 탐색하려면  
  
1.  에 **클러스터 1** 상자에서 **Bike Buyers High**합니다.  
  
2.  에 **클러스터 2** 상자에서 **Bike Buyers Low**합니다.  
  
3.  클릭 **변수** 으로 사전순으로 정렬 합니다.  
  
     고객 간에 더 큰 차이점 중 일부는 **Bike Buyers Low** 하 고 **Bike Buyers High** 클러스터 나가, 자동차 소유 여부, 지역 및 자식의 수를 포함 합니다.  
  
## <a name="related-tasks"></a>관련 작업  
 다른 마이닝 모델을 탐색 하려면 다음 항목을 참조 하세요.  
  
-   [의사 결정 트리 모델 탐색 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [Naive Bayes 모델 탐색 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [Naive Bayes 모델 탐색 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>단원의 이전 태스크  
 [의사 결정 트리 모델 탐색 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft 클러스터 뷰어를 사용 하 여 모델 찾아보기](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)   
 [클러스터 판별 탭 &#40;마이닝 모델 뷰어&#41;](../../2014/analysis-services/cluster-discrimination-tab-mining-model-viewer.md)   
 [클러스터 프로필 탭 &#40;마이닝 모델 뷰어&#41;](../../2014/analysis-services/cluster-profiles-tab-mining-model-viewer.md)   
 [클러스터 특징 탭 &#40;마이닝 모델 뷰어&#41;](../../2014/analysis-services/cluster-characteristics-tab-mining-model-viewer.md)   
 [클러스터 다이어그램 탭 &#40;마이닝 모델 뷰어&#41;](../../2014/analysis-services/cluster-diagram-tab-mining-model-viewer.md)  
  
  
