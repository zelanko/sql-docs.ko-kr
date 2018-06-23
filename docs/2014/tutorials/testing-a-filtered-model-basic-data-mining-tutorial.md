---
title: 필터링된 된 모델 (기본 데이터 마이닝 자습서) 테스트 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f0d74f8c-600d-4df5-a742-695e6947a071
caps.latest.revision: 28
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0dfb4b3ae34b230c591071f02cdaa9b0984cf05e
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312551"
---
# <a name="testing-a-filtered-model-basic-data-mining-tutorial"></a>필터링된 모델 테스트(기본 데이터 마이닝 자습서)
  확인 했으므로 했으므로 `TM_Decision_Tree` 가장 정확한 모델 임을 모델, 모델의 요구에 맞게 사용자 지정할는 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 타겟 메일링 캠페인입니다. 특히, 마케팅 부서에서는 고객 male 및 female 사이 차이가 있는지 알고 싶습니다. 정보 잡지와 광고에 대 한 사용을 결정 하는 데 도움이 수 및 제품을 통과 하도록 메일에 있습니다.  
  
## <a name="using-filters"></a>필터 사용  
 필터링을 사용하면 데이터의 하위 집합을 기반으로 하는 모델을 쉽게 만들 수 있습니다. 필터는 모델에만 적용되고 기본 데이터 원본을 변경하지는 않습니다.  
  
 이 단원에서는 성별로 대부분 남성과 female의 구매 행동에 영향을 줄는 특징을 예측에 필터링 된 모델을 만듭니다.  
  
 먼저의 복사본을 만듭니다는 `TM_Decision_Tree` 모델입니다.  
  
#### <a name="to-copy-the-decision-tree-model"></a>의사 결정 트리 모델을 복사하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], 솔루션 탐색기에서 선택 **BasicDataMining**합니다.  
  
2.  **마이닝 모델** 탭을 클릭합니다.  
  
3.  마우스 오른쪽 단추로 클릭는 `TM_Decision_Tree` 모델을 마우스 선택 **새 마이닝 모델입니다.**  
  
4.  에 **모델 이름** 필드를 입력 `TM_Decision_Tree_Male`합니다.  
  
5.  **확인**을 클릭합니다.  
  
 다음으로 해당 성을 기반으로 하는 모델에 대한 고객을 선택하는 필터를 만듭니다.  
  
#### <a name="to-create-a-case-filter-on-a-mining-model"></a>마이닝 모델에 사례 필터를 만들려면  
  
1.  마우스 오른쪽 단추로 클릭는 `TM_Decision_Tree_Male` 바로 가기 메뉴를 열고 마이닝 모델입니다.  
  
     -- 또는 --  
  
     모델을 선택합니다. **마이닝 모델** 메뉴에서 **모델 필터 설정**을 선택합니다.  
  
2.  **모델 필터** 대화 상자의 **마이닝 구조 열** 입력란에서 표의 첫 행을 클릭합니다.  
  
     드롭다운 목록에서 해당 테이블에 있는 열의 이름만 표시합니다.  
  
3.  마이닝 구조 열 입력란에 선택 **성별**합니다.  
  
     입력란의 왼쪽에 있는 아이콘이 변경되어 선택한 항목이 테이블인지 또는 열인지를 나타냅니다.  
  
4.  클릭는 **연산자** 텍스트 상자와 목록에서 등호 (=) 연산자를 선택 합니다.  
  
5.  클릭는 **값** 텍스트 상자 **M**합니다.  
  
6.  표에서 다음 행을 클릭합니다.  
  
7.  클릭 **확인** 를 닫으려면는 **모델 필터** 대화 상자.  
  
     필터에 표시 된 **속성** 창. 또는 시작할 수 있습니다는 **모델 필터** 에서 대화 상자는 **속성** 창.  
  
8.  반복에서 위의 단계를 하지만이 이번에는 모델 이름을 `TM_Decision_Tree_Female` 유형과 **F** 에 **값** 입력란.  
  
## <a name="process-the-filtered-models"></a>필터링된 모델 처리  
 모델은 배포 및 처리될 때까지 사용할 수 없습니다. 모델 처리에 대 한 자세한 내용은 참조 하십시오. [대상 메일 구조에서 모델 처리 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial.md)합니다.  
  
#### <a name="to-process-the-filtered-model"></a>필터링된 모델을 처리하려면  
  
1.  마우스 오른쪽 단추로 클릭는 `TM_Decision_Tree_Male` 모델링 하 고 선택 **모든 모델과 마이닝 구조 처리**s  
  
2.  클릭 **실행** 새 모델을 처리할 수 있습니다.  
  
3.  처리가 완료 되 면 클릭 **닫기** 두 처리 창에 있습니다.  
  
     두 개의 새 모델이 표시 해야는 **마이닝 모델** 탭 합니다.  
  
## <a name="evaluate-the-results"></a>결과 평가  
 이전 세 개의 모델에 대해 수행했던 방식과 거의 동일한 방식으로 결과를 검토하고 필터링된 모델의 정확도를 평가합니다. 참조 항목:  
  
 [의사 결정 트리 모델 탐색 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
 [리프트 차트를 사용 하 여 정확도 테스트 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
#### <a name="to-explore-the-filtered-models"></a>필터링된 모델을 탐색하려면  
  
1.  선택 된 **마이닝 모델 뷰어** 탭에서 **데이터 마이닝 디자이너**합니다.  
  
2.  마이닝 모델 상자에서 선택 `TM_Decision_Tree_Male`합니다.  
  
3.  슬라이드 **수준 표시** 를 `3`합니다.  
  
4.  변경 된 **배경** 값을 `1`합니다.  
  
5.  레이블이 지정 된 노드 위에 커서를 놓고 **모든** 자전거 구매자와 자전거 비 구매자의 수를 확인 합니다.  
  
6.  에 대 한 1-5 단계를 반복 `TM_Decision_Tree_Female`합니다.  
  
7.  탐색에 대 한 결과 `TM_Decision_Tree` 및 성별에 대 한 필터링 된 모델입니다. 모든 자전거 구매자와 비교해 볼 때 남성 자전거 구매자와 여성 자전거 구매자는 필터링되지 않은 자전거 구매자와 동일한 특징을 일부 공유하지만 이 세 범주의 구매자에게는 흥미로운 차이점도 있습니다. 이 유용한 정보를 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 마케팅 캠페인을 개발 하는 데 사용할 수 있습니다.  
  
#### <a name="to-test-the-lift-of-the-filtered-models"></a>필터링된 모델의 리프트를 테스트하려면  
  
1.  전환 하는 **마이닝 정확도 차트** 탭의 데이터 마이닝 디자이너에서 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 선택 하 고는 **입력 선택** 탭 합니다.  
  
2.  에 **정확도 차트에 사용할 데이터 집합 선택** 그룹 상자에서 **마이닝 구조 테스트 사례를 사용 하 여**합니다.  
  
3.  에 **입력 선택** 데이터 마이닝 디자이너의 탭 아래에서 **리프트 차트에 표시할 예측 가능한 마이닝 모델 열 선택**에 대 한 확인란을 선택 **예측 열 동기화 및 값**합니다.  
  
4.  에 **예측 가능한 열 이름** 열 되어 있는지 확인 **Bike Buyer** 각 모델에 대해 선택 되어 있습니다.  
  
5.  에 **표시** , 각 선택은 모델의 열입니다.  
  
6.  에 **예측 값** 열에서 선택 `1`합니다.  
  
7.  선택 된 **리프트 차트** 리프트 차트를 표시 합니다.  
  
     세 가지 의사 결정 트리 모델은 모두 임의 추측 모델과 비교했을 때 유효한 리프트를 제공할 뿐만 아니라 클러스터링 및 Naive-Bayes 모델보다 성능이 뛰어납니다.  
  
## <a name="related-tasks"></a>관련 작업  
 필터에 대 한 자세한 내용은 참조 하십시오. [마이닝 모델에 대 한 필터 &#40;Analysis Services-데이터 마이닝&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)합니다.  
  
 중첩된 테이블에 필터를 적용 하는 방법의 예제를 보려면 [중급 데이터 마이닝 자습서 &#40;Analysis Services-데이터 마이닝&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)합니다.  
  
## <a name="previous-task-in-lesson"></a>단원의 이전 태스크  
 [리프트 차트를 사용 하 여 정확도 테스트 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>다음 단원  
 [6 단원: 만들기 및 예측 작업 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>관련 항목  
 [중급 데이터 마이닝 자습서 &#40;Analysis Services-데이터 마이닝&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [마이닝 모델 태스크 및 방법](../../2014/analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [마이닝 모델에서 필터 삭제](../../2014/analysis-services/data-mining/delete-a-filter-from-a-mining-model.md)   
 [마이닝 모델에 대 한 필터 &#40;Analysis Services-데이터 마이닝&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)  
  
  