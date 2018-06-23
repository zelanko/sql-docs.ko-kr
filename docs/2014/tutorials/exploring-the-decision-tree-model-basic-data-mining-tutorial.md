---
title: 의사 결정 트리 모델 (기본 데이터 마이닝 자습서) 탐색 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2e1472c2-3f3e-4dae-acb3-62fca374d397
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 7760bde2165a351876bb0ac84f26f59b1196bf2e
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312881"
---
# <a name="exploring-the-decision-tree-model-basic-data-mining-tutorial"></a>의사 결정 트리 모델 탐색(기본 데이터 마이닝 자습서)
  [!INCLUDE[msCoName](../includes/msconame-md.md)] 의사 결정 트리 알고리즘은 학습 집합의 나머지 열을 기준으로 자전거 구매 결정에 영향을 주는 열을 예측합니다.  
  

  
##  <a name="Decision_Tree_Tab"></a> 의사 결정 트리 탭  
 에 **의사 결정 트리** 탭을 데이터 집합의 모든 예측 가능한 특성에 대 한 의사 결정 트리를 볼 수 있습니다.  
  
 이 경우 모델 하나의 트리만 볼 수 있으므로 열이 하나만, Bike Buyer를 예측 합니다. 트리가 더 경우 사용할 수 있습니다는 **트리** 상자를 다른 트리를 선택 합니다.  
  
 볼 때는 `TM_Decision_Tree` 모델에서는 의사 결정 트리 뷰어의 차트의 왼쪽에 가장 중요 한 특성을 볼 수 있습니다. "가장 중요 한" 이러한 특성에 결과에 가장 큰 영향을 의미 합니다. 추가 트리의 (차트의 오른쪽) 특성이 효과의 작은 있습니다.  
  
 이 예제에서는 자전거 구매 예측에 가장 중요 한 단일 요소 시간은입니다. 모델 연령으로 고객이 그룹화 하 고 각 연령 그룹에 대 한 다음 더 중요 한 특성을 표시 합니다. 예를 들어 34 ~ 40 오래 된 고객의 그룹에서 소유한 자동차 수는 가장 강력한 예측 요인 순서가 합니다.  
  
#### <a name="to-explore-the-model-in-the-decision-tree-tab"></a>의사 결정 트리 탭에서 모델을 탐색하려면  
  
1.  선택 된 **마이닝 모델 뷰어** 탭에서 **데이터 마이닝 디자이너**합니다.  
  
     기본적으로이 경우 구조에 추가 된 첫 번째 모델 디자이너가 열립니다 `TM_Decision_Tree`합니다.  
  
2.  돋보기 단추를 사용하여 트리 표시 크기를 조정합니다.  
  
     기본적으로 [!INCLUDE[msCoName](../includes/msconame-md.md)] 트리 뷰어에는 트리의 처음 세 수준만 표시됩니다. 트리의 수준이 셋 미만이면 뷰어에 기존 수준만 표시됩니다. 사용 하 여 더 많은 수준을 볼 수는 **수준 표시** 슬라이더 또는 **기본 확장** 목록입니다.  
  
3.  슬라이드 **수준 표시** 네 번째 막대로 합니다.  
  
4.  변경 된 **배경** 값을 `1`합니다.  
  
     변경 하 여는 **배경** 를 설정 하면 파악할 수 있습니다에 대상 값의 각 노드에 있는 사례 수 `1` [Bike Buyer]에 대 한 합니다. 이 특정 시나리오에서 각 사례는 고객을 나타냅니다. 값 `1` 고객; 자전거를 구매한 적 나타냅니다 값 **0** 는 고객이 자전거를 구입 하지 않은 나타냅니다. 노드의 음영이 짙을수록 노드에 대상 값을 가진 사례의 비율이 높습니다.  
  
5.  레이블이 지정 된 노드 위에 커서를 놓고 **모든**합니다. 도구 설명에 다음 정보가 표시됩니다.  
  
    -   총 사례 수  
  
    -   자전거를 구매하지 않은 구매자 사례 수  
  
    -   자전거 구매자 사례 수  
  
    -   [Bike Buyer]에 대해 누락된 값이 있는 사례 수  
  
     또는 커서를 트리의 노드에 두면 상위 노드에서 해당 노드에 도달하는 데 필요한 조건이 표시됩니다. 이 정보를 볼 수도 있습니다는 **마이닝 범례**합니다.  
  
6.  에 대 한 노드를 클릭 **Age > = 34 및 < 41**합니다. 히스토그램이 노드에 가는 가로 막대로 표시되며, 이 연령 범위에서 이전에 자전거를 구매한 고객(분홍색)과 구매하지 않은 고객(파란색)의 분포를 나타냅니다. 뷰어를 통해 한 대의 자동차를 보유하거나 보유하지 않은 34 ~ 40대의 고객이 자전거를 구매할 가능성이 있음을 알 수 있습니다. 이 단계를 더욱 발전시킨 결과 고객의 실제 나이가 38 ~ 40인 경우 자전거를 구매할 가능성이 늘어난다는 것을 알았습니다.  
  
 구조와 모델을 만들 때 드릴스루를 사용했기 때문에 마이닝 모델에 포함되지 않은 열을 비롯하여(예: emailAddress, FirstName) 모델 사례 및 마이닝 구조의 세부 정보를 검색할 수 있습니다.  
  
 자세한 내용은 [드릴스루 쿼리&#40;데이터 마이닝&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)를 참조하세요.  
  
#### <a name="to-drill-through-to-case-data"></a>사례 데이터를 드릴스루하려면  
  
1.  노드를 마우스 오른쪽 단추로 클릭 하 고 선택 **드릴스루** 다음 **모델 열만**합니다.  
  
     각 학습 사례에 대한 세부 사항은 스프레드시트 형식으로 표시됩니다. 이러한 세부 사항은 마이닝 구조를 작성할 때 사례 테이블로 선택한 vTargetMail 뷰에서 가져옵니다.  
  
2.  노드를 마우스 오른쪽 단추로 클릭 하 고 선택 **드릴스루** 다음 **모델 및 구조 열**합니다.  
  
     끝에 구조 열이 추가된 같은 스프레드시트가 표시됩니다.  
  
  
###  <a name="Dependency_Network_Tab"></a> 종속성 네트워크 탭  
 **종속성 네트워크** 탭은 마이닝 모델의 예측 기능에 기여 하는 특성 간의 관계를 표시 합니다. 종속성 네트워크 뷰어에서 Age 및 Region이 자전거 구매 예측에 중요한 요소임을 나타냅니다.  
  
##### <a name="to-explore-the-model-in-the-dependency-network-tab"></a>종속성 네트워크 탭에서 모델을 탐색하려면  
  
1.  클릭는 `Bike Buyer` 노드를 해당 종속성을 식별 합니다.  
  
     종속성 네트워크의 가운데 노드인 `Bike Buyer`, 마이닝 모델에 예측 가능한 특성을 나타냅니다. 그래프에는 예측 가능한 특성에 영향을 미칠는 연결 된 노드가 강조 표시 합니다.  
  
2.  조정는 **모든 링크** 슬라이더를 가장 큰 영향을 주는 특성을 식별 합니다.  
  
     슬라이더를 아래로 끌면 [Bike Buyer] 열에 영향을 약한 있는 특성을 그래프에서 제거 됩니다. 슬라이더를 조정 하 여 나 이와 지역이 자전거 구매자를 예측에 가장 큰 요인 되는지 확인할 수 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
 다른 종류의 모델을 사용 하 여 데이터를 탐색 하려면 다음이 항목을 참조 합니다.  
  
-   [클러스터링 모델 탐색 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
-   [Naive Bayes 모델 탐색 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [클러스터링 모델 탐색 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>관련 항목  
 [마이닝 모델 뷰어 태스크 및 방법](../../2014/analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [트리 탭 의사 결정 &#40;마이닝 모델 뷰어&#41;](../../2014/analysis-services/decision-tree-tab-mining-model-viewer.md)   
 [종속성 네트워크 탭 &#40;마이닝 모델 뷰어&#41;](../../2014/analysis-services/dependency-network-tab-mining-model-viewer.md)   
 [Microsoft 트리 뷰어를 사용하여 모델 찾아보기](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)  
  
  