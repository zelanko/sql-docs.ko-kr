---
title: 클러스터링 모델 탐색 (기본 데이터 마이닝 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: ce8aa034-161b-473f-baec-9c29e0a8e5f5
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 9bb2c6457122a5ea49824ca178b6950d88f75563
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63280427"
---
# <a name="exploring-the-clustering-model-basic-data-mining-tutorial"></a>클러스터링 모델 탐색(기본 데이터 마이닝 자습서)
  클러스터링 [!INCLUDE[msCoName](../includes/msconame-md.md)] 알고리즘은 사례를 유사한 특성을 포함 하는 클러스터로 그룹화 합니다. 이러한 그룹화는 데이터 탐색, 데이터 내 잘못된 부분 식별, 예측 만들기 등에 유용합니다.  
  
 
  [!INCLUDE[msCoName](../includes/msconame-md.md)] 클러스터 뷰어는 클러스터링 마이닝 모델 탐색 시 사용할 수 있는 다음과 같은 탭을 제공합니다.  
  

  
##  <a name="ClusterDiagramTab"></a>클러스터 다이어그램 탭  
 클러스터 다이어그램 탭에서는 마이닝 모델에 있는 클러스터를 모두 표시합니다. 클러스터 사이의 선은 "일치 정도"를 나타내며 클러스터가 얼마나 비슷한지에 따라 음영 처리됩니다. 각 클러스터의 실제 색은 클러스터에 있는 변수와 상태의 빈도를 나타냅니다.  
  
#### <a name="to-explore-the-model-in-the-cluster-diagram-tab"></a>클러스터 다이어그램 탭에서 모델을 탐색하려면  
  
1.  **마이닝 모델 뷰어** 탭의 위쪽에 있는 `TM_Clustering` **마이닝 모델** 목록을 사용 하 여 모델로 전환할 수 있습니다.  
  
2.  **뷰어** 목록에서 **Microsoft 클러스터 뷰어**를 선택 합니다.  
  
3.  **음영 변수** 상자에서 **자전거 구매자**를 선택 합니다.  
  
     기본 변수는 **채우기**이지만이를 모델의 임의의 특성으로 변경 하 여 원하는 특성을 가진 멤버를 포함 하는 클러스터를 검색할 수 있습니다.  
  
4.  **상태** 상자에서 **1** 을 선택 하 여 자전거를 구매한 경우를 탐색 합니다.  
  
     **밀도** 범례는 음영 변수 및 상태에서 선택한 특성 상태 쌍의 밀도를 설명 합니다. 이 예제에서는 가장 어두운 음영이 있는 clusterwith 최고 비율의 자전거 구매자가 있음을 알려 줍니다.  
  
5.  음영이 가장 짙은 클러스터 위에 마우스를 놓습니다.  
  
     도구 설명에서 특성이 `Bike Buyer = 1`인 사례의 비율을 표시합니다.  
  
6.  밀도가 가장 높은 클러스터를 선택 하 고, 클러스터를 마우스 오른쪽 단추로 클릭 하 고, **클러스터 이름 바꾸기** 를 선택 하 고, 나중에 확인을 위해 **자전거 구매자 높음** 을 입력 합니다. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  음영이 가장 밝고 밀도가 가장 낮은 클러스터를 찾습니다. 클러스터를 마우스 오른쪽 단추로 클릭 하 고 **클러스터 이름 바꾸기** 를 선택 하 고 **자전거 구매자 낮음**을 입력 합니다. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  **자전거 구매자 상위** 클러스터를 클릭 하 고 다른 클러스터에 대 한 연결을 명확 하 게 보여 주는 창 영역으로 끕니다.  
  
     클러스터를 선택하면 이 클러스터를 다른 클러스터에 연결하는 선이 강조 표시되므로 이 클러스터에 대한 모든 관계를 쉽게 볼 수 있습니다. 클러스터를 선택하지 않은 경우 다이어그램에 있는 모든 클러스터 간 관계의 밀접도는 선이 짙은 정도로 알 수 있습니다. 음영이 옅거나 없으면 두 클러스터가 그다지 유사하지 않은 것입니다.  
  
9. 네트워크 왼쪽의 슬라이더를 사용하여 약한 링크를 필터로 제외시키고 가장 밀접한 관계가 있는 클러스터를 찾을 수 있습니다. 
  [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 마케팅 부서에서 대상 메일을 배달하기 위한 최상의 방법을 결정할 때 유사한 클러스터를 함께 결합할 수 있습니다.  
  

  
##  <a name="ClusterProfilesTab"></a>클러스터 프로필 탭  
 **클러스터 프로필** 탭에서는 `TM_Clustering` 모델의 전체 보기를 제공 합니다. **클러스터 프로필** 탭에는 모델의 각 클러스터에 대 한 열이 포함 되어 있습니다. 첫 번째 열에는 적어도 하나의 클러스터와 연결된 특성이 나열됩니다. 뷰어의 나머지 부분에는 각 클러스터에 대한 특성의 상태 분포가 있습니다. 불연속 변수의 분포는 **히스토그램 막대** 목록에 표시 되는 최대 막대 수가 있는 색이 지정 된 막대로 표시 됩니다. 연속 특성은 각 클러스터의 평균과 표준 편차를 나타내는 다이아몬드 차트를 사용하여 표시됩니다.  
  
#### <a name="to-explore-the-model-in-the-cluster-profiles-tab"></a>클러스터 프로필 탭에서 모델을 탐색하려면  
  
1.  **히스토그램** 막대를 **5**로 설정 합니다.  
  
     이 모델에서 5는 어느 한 변수의 상태에 지정할 수 있는 최대값입니다.  
  
2.  **마이닝 범례** 가 **특성 프로필**의 표시를 차단 하는 경우이를 밖으로 이동 합니다.  
  
3.  **자전거 구매자 High** 열을 선택 하 여 **모집단** 열의 오른쪽으로 끕니다.  
  
4.  **자전거 구매자 Low** 열을 선택 하 고 **자전거 구매자 상위** 열의 오른쪽으로 끕니다.  
  
5.  **자전거 구매자 상위** 열을 클릭 합니다.  
  
     **Variables** 열은 해당 클러스터의 중요도 순으로 정렬 됩니다. 열을 스크롤하고 Bike Buyer High 클러스터의 특징을 검토합니다. 예를 들어 이 클러스터에 속한 사람들은 통근 거리가 짧을 가능성이 더 많습니다.  
  
6.  **자전거 구매자 High** 열에서 **Age** 셀을 두 번 클릭 합니다.  
  
     **마이닝 범례** 에는 보다 자세한 보기가 표시 되며 이러한 고객의 연령 범위와 평균 나이가 표시 됩니다.  
  
7.  **자전거 구매자 Low** 열을 마우스 오른쪽 단추로 클릭 하 고 **열 숨기기**를 선택 합니다.  
  

  
##  <a name="ClusterCharacteristicsTab"></a>클러스터 특징 탭  
 **클러스터 특징** 탭을 사용 하 여 클러스터를 구성 하는 특성을 자세히 검토할 수 있습니다. 클러스터 프로필 탭에서 모든 클러스터의 특징을 비교하는 대신 한 번에 하나의 클러스터를 탐색할 수 있습니다. 예를 들어 **클러스터** 목록에서 **자전거 구매자** 를 선택 하는 경우이 클러스터의 고객 특징을 볼 수 있습니다. 클러스터 프로필 뷰어와 다르게 표시되지만 결과는 동일합니다.  
  
> [!NOTE]  
>  **Holdoutseed**에 대 한 초기 값을 설정 하지 않으면 모델을 처리할 때마다 결과가 달라 집니다. 자세한 내용은 [HoldoutSeed 요소](https://docs.microsoft.com/bi-reference/assl/properties/holdoutseed-element) 를 참조 하세요.  
  

  
##  <a name="ClusterDiscriminationTab"></a>클러스터 판별 탭  
 **클러스터 판별** 탭을 사용 하 여 한 클러스터를 다른 클러스터와 구별 하는 특성을 탐색할 수 있습니다. **클러스터 1** 목록에서 두 개의 클러스터를 선택 하 고 클러스터 **2** 목록에서 클러스터를 선택 하면 뷰어는 클러스터 간의 차이점을 계산 하 고 클러스터를 가장 많이 구분 하는 특성 목록을 표시 합니다.  
  
#### <a name="to-explore-the-model-in-the-cluster-discrimination-tab"></a>클러스터 판별 탭에서 모델을 탐색하려면  
  
1.  **클러스터 1** 상자에서 **자전거 구매자 높음**을 선택 합니다.  
  
2.  **클러스터 2** 상자에서 **자전거 구매자 낮음**을 선택 합니다.  
  
3.  사전순으로 정렬 하려면 **변수** 를 클릭 합니다.  
  
     **자전거 구매자** 의 고객과 **자전거 구매자** 의 많은 차이점 중 일부는 나이, 자동차 소유권, 자녀 수 및 지역이 포함 됩니다.  
  
## <a name="related-tasks"></a>관련 작업  
 다른 마이닝 모델을 탐색 하려면 다음 항목을 참조 하십시오.  
  
-   [기본 데이터 마이닝 자습서 &#40;의사 결정 트리 모델 탐색&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [Naive Bayes 모델 &#40;기본 데이터 마이닝 자습서 살펴보기&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [Naive Bayes 모델 &#40;기본 데이터 마이닝 자습서 살펴보기&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>단원의 이전 태스크  
 [기본 데이터 마이닝 자습서 &#40;의사 결정 트리 모델 탐색&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>참고 항목  
 [Microsoft 클러스터 뷰어를 사용 하 여 모델 찾아보기](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)   
 [클러스터 판별 탭 &#40;마이닝 모델 뷰어&#41;](../../2014/analysis-services/cluster-discrimination-tab-mining-model-viewer.md)   
 [마이닝 모델 뷰어를 &#40;클러스터 프로필 탭&#41;](../../2014/analysis-services/cluster-profiles-tab-mining-model-viewer.md)   
 [마이닝 모델 뷰어를 &#40;클러스터 특징 탭&#41;](../../2014/analysis-services/cluster-characteristics-tab-mining-model-viewer.md)   
 [마이닝 모델 뷰어를 &#40;클러스터 다이어그램 탭&#41;](../../2014/analysis-services/cluster-diagram-tab-mining-model-viewer.md)  
  
  
