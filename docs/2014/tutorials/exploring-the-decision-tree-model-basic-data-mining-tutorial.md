---
title: 의사 결정 트리 모델 탐색 (기본 데이터 마이닝 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2e1472c2-3f3e-4dae-acb3-62fca374d397
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e7b77b445ff8cbef8be3acb72ef9cdb6fa3af159
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63224594"
---
# <a name="exploring-the-decision-tree-model-basic-data-mining-tutorial"></a>의사 결정 트리 모델 탐색(기본 데이터 마이닝 자습서)
  
  [!INCLUDE[msCoName](../includes/msconame-md.md)] 의사 결정 트리 알고리즘은 학습 집합의 나머지 열을 기준으로 자전거 구매 결정에 영향을 주는 열을 예측합니다.  
  

  
##  <a name="Decision_Tree_Tab"></a>의사 결정 트리 탭  
 **의사 결정 트리** 탭에서 데이터 집합의 모든 예측 가능한 특성에 대 한 의사 결정 트리를 볼 수 있습니다.  
  
 이 경우 모델은 하나의 열 자전거 구매자만 예측 하므로 볼 트리가 하나만 있습니다. 트리가 더 있으면 **트리** 상자를 사용 하 여 다른 트리를 선택할 수 있습니다.  
  
 의사 결정 트리 뷰어에서 `TM_Decision_Tree` 모델을 볼 때 차트 왼쪽에서 가장 중요 한 특성을 볼 수 있습니다. "가장 중요 한"는 이러한 특성이 결과에 가장 큰 영향을 주는 것을 의미 합니다. 트리의 아래쪽에 있는 특성 (차트 오른쪽)은 효과가 낮습니다.  
  
 이 예제에서 age는 자전거 구매를 예측 하는 데 가장 중요 한 단일 요소입니다. 이 모델은 사용자를 age로 그룹화 하 고 각 연령 그룹에 대해 다음으로 더 중요 한 특성을 표시 합니다. 예를 들어 34에서 40 까지의 고객 그룹에서 소유 하 고 있는 자동차의 수는 age 이후 가장 강력한 예측입니다.  
  
#### <a name="to-explore-the-model-in-the-decision-tree-tab"></a>의사 결정 트리 탭에서 모델을 탐색하려면  
  
1.  **데이터 마이닝 디자이너**에서 **마이닝 모델 뷰어** 탭을 선택 합니다.  
  
     기본적으로 디자이너는 구조에 추가 된 첫 번째 모델 (이 경우)을 엽니다 `TM_Decision_Tree`.  
  
2.  돋보기 단추를 사용하여 트리 표시 크기를 조정합니다.  
  
     기본적으로 [!INCLUDE[msCoName](../includes/msconame-md.md)] 트리 뷰어에는 트리의 처음 세 수준만 표시됩니다. 트리의 수준이 셋 미만이면 뷰어에 기존 수준만 표시됩니다. **수준 표시** 슬라이더 또는 **기본 확장** 목록을 사용 하 여 더 많은 수준을 볼 수 있습니다.  
  
3.  슬라이드 **쇼 수준을** 네 번째 막대로 이동 합니다.  
  
4.  **배경** 값을로 `1`변경 합니다.  
  
     **배경** 설정을 변경 하 여 [자전거 구매자] `1` 에 대 한 대상 값을 가진 각 노드의 사례 수를 빠르게 확인할 수 있습니다. 이 특정 시나리오에서 각 사례는 고객을 나타냅니다. 이 값 `1` 은 고객이 이전에 자전거를 구매한 것을 나타냅니다. 값 **0** 은 고객이 자전거를 구매 하지 않았음을 나타냅니다. 노드의 음영이 짙을수록 노드에 대상 값을 가진 사례의 비율이 높습니다.  
  
5.  **모두**레이블이 지정 된 노드 위에 커서를 놓습니다. 도구 설명에 다음 정보가 표시됩니다.  
  
    -   총 사례 수  
  
    -   자전거를 구매하지 않은 구매자 사례 수  
  
    -   자전거 구매자 사례 수  
  
    -   [Bike Buyer]에 대해 누락된 값이 있는 사례 수  
  
     또는 커서를 트리의 노드에 두면 상위 노드에서 해당 노드에 도달하는 데 필요한 조건이 표시됩니다. **마이닝 범례**에서도 동일한 정보를 볼 수 있습니다.  
  
6.  **Age >= 34 및 < 41**에 대 한 노드를 클릭 합니다. 히스토그램이 노드에 가는 가로 막대로 표시되며, 이 연령 범위에서 이전에 자전거를 구매한 고객(분홍색)과 구매하지 않은 고객(파란색)의 분포를 나타냅니다. 뷰어를 통해 한 대의 자동차를 보유하거나 보유하지 않은 34 ~ 40대의 고객이 자전거를 구매할 가능성이 있음을 알 수 있습니다. 이 단계를 더욱 발전시킨 결과 고객의 실제 나이가 38 ~ 40인 경우 자전거를 구매할 가능성이 늘어난다는 것을 알았습니다.  
  
 구조와 모델을 만들 때 드릴스루를 사용했기 때문에 마이닝 모델에 포함되지 않은 열을 비롯하여(예: emailAddress, FirstName) 모델 사례 및 마이닝 구조의 세부 정보를 검색할 수 있습니다.  
  
 자세한 내용은 [드릴스루 쿼리&#40;데이터 마이닝&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)를 참조하세요.  
  
#### <a name="to-drill-through-to-case-data"></a>사례 데이터를 드릴스루하려면  
  
1.  노드를 마우스 오른쪽 단추로 클릭 하 고 **드릴스루** 를 선택한 다음 **모델 열만**을 선택 합니다.  
  
     각 학습 사례에 대한 세부 사항은 스프레드시트 형식으로 표시됩니다. 이러한 세부 사항은 마이닝 구조를 작성할 때 사례 테이블로 선택한 vTargetMail 뷰에서 가져옵니다.  
  
2.  노드를 마우스 오른쪽 단추로 클릭 하 고 **드릴스루** , **모델 및 구조 열**을 차례로 선택 합니다.  
  
     끝에 구조 열이 추가된 같은 스프레드시트가 표시됩니다.  
  
  
###  <a name="Dependency_Network_Tab"></a>종속성 네트워크 탭  
 **종속성 네트워크** 탭에는 마이닝 모델의 예측 기능에 영향을 주는 특성 간의 관계가 표시 됩니다. 종속성 네트워크 뷰어에서 Age 및 Region이 자전거 구매 예측에 중요한 요소임을 나타냅니다.  
  
##### <a name="to-explore-the-model-in-the-dependency-network-tab"></a>종속성 네트워크 탭에서 모델을 탐색하려면  
  
1.  노드를 `Bike Buyer` 클릭 하 여 해당 종속성을 식별 합니다.  
  
     종속성 네트워크 `Bike Buyer`의 중심 노드인는 마이닝 모델의 예측 가능한 특성을 나타냅니다. 그래프는 예측 가능한 특성에 영향을 주는 모든 연결 된 노드를 강조 표시 합니다.  
  
2.  **모든 링크** 슬라이더를 조정 하 여 가장 영향력 있는 특성을 식별 합니다.  
  
     슬라이더를 아래로 끌면 [자전거 구매자] 열에 weak 효과가 있는 특성만 그래프에서 제거 됩니다. 슬라이더를 조정 하 여 해당 나이가 나 지역이 자전거 구매자 인지 여부를 예측 하는 가장 큰 요인이 될 수 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
 다른 종류의 모델을 사용 하 여 데이터를 탐색 하려면 다음 항목을 참조 하세요.  
  
-   [기본 데이터 마이닝 자습서 &#40;클러스터링 모델 탐색&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
-   [Naive Bayes 모델 &#40;기본 데이터 마이닝 자습서 살펴보기&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [기본 데이터 마이닝 자습서 &#40;클러스터링 모델 탐색&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>참고 항목  
 [마이닝 모델 뷰어 태스크 및 방법](../../2014/analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [마이닝 모델 뷰어를 &#40;의사 결정 트리 탭&#41;](../../2014/analysis-services/decision-tree-tab-mining-model-viewer.md)   
 [&#40;마이닝 모델 뷰어&#41;종속성 네트워크 탭](../../2014/analysis-services/dependency-network-tab-mining-model-viewer.md)   
 [Microsoft 트리 뷰어를 사용하여 모델 찾아보기](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)  
  
  
