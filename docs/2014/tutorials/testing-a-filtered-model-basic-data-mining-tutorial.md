---
title: 필터링 된 모델 테스트 (기본 데이터 마이닝 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f0d74f8c-600d-4df5-a742-695e6947a071
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: baa4910b2849c4eb2dd04c6d0115c83683ee8bea
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63044098"
---
# <a name="testing-a-filtered-model-basic-data-mining-tutorial"></a>필터링된 모델 테스트(기본 데이터 마이닝 자습서)
  이제 `TM_Decision_Tree` 모델이 가장 정확 하다 고 판단 되 면 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 타겟 메일링 캠페인의 요구에 맞게 모델을 사용자 지정 합니다. 특히 마케팅 부서는 남성와 여성 고객 간에 차이가 있는지 알고 싶습니다. 이 정보를 통해 광고에 사용할 잡지를 결정 하는 데 도움이 될 수 있습니다.  
  
## <a name="using-filters"></a>필터 사용  
 필터링을 사용하면 데이터의 하위 집합을 기반으로 하는 모델을 쉽게 만들 수 있습니다. 필터는 모델에만 적용되고 기본 데이터 원본을 변경하지는 않습니다.  
  
 이 단원에서는 세임 및 여성의 구매 동작에 가장 영향을 주는 특성을 예측 하기 위해 성별에 대해 필터링 된 모델을 만듭니다.  
  
 먼저 `TM_Decision_Tree` 모델의 복사본을 만듭니다.  
  
#### <a name="to-copy-the-decision-tree-model"></a>의사 결정 트리 모델을 복사하려면  
  
1.  의 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]솔루션 탐색기에서 **BasicDataMining**을 선택 합니다.  
  
2.  **마이닝 모델** 탭을 클릭합니다.  
  
3.  모델을 마우스 오른쪽 단추로 클릭 하 고 **새 마이닝 모델을 선택 합니다.** `TM_Decision_Tree`  
  
4.  **모델 이름** 필드에을 입력 `TM_Decision_Tree_Male`합니다.  
  
5.  **확인**을 클릭합니다.  
  
 다음으로 해당 성을 기반으로 하는 모델에 대한 고객을 선택하는 필터를 만듭니다.  
  
#### <a name="to-create-a-case-filter-on-a-mining-model"></a>마이닝 모델에 사례 필터를 만들려면  
  
1.  `TM_Decision_Tree_Male` 마이닝 모델을 마우스 오른쪽 단추로 클릭 하 여 바로 가기 메뉴를 엽니다.  
  
     -- 또는 --  
  
     모델을 선택합니다. **마이닝 모델** 메뉴에서 **모델 필터 설정**을 선택합니다.  
  
2.  **모델 필터** 대화 상자의 **마이닝 구조 열** 입력란에서 표의 첫 행을 클릭합니다.  
  
     드롭다운 목록에서 해당 테이블에 있는 열의 이름만 표시합니다.  
  
3.  마이닝 구조 열 입력란에서 **성별**을 선택 합니다.  
  
     입력란의 왼쪽에 있는 아이콘이 변경되어 선택한 항목이 테이블인지 또는 열인지를 나타냅니다.  
  
4.  **연산자** 입력란을 클릭 하 고 목록에서 등호 (=) 연산자를 선택 합니다.  
  
5.  **값** 입력란을 클릭 하 고 **M**을 입력 합니다.  
  
6.  표에서 다음 행을 클릭합니다.  
  
7.  **확인** 을 클릭 하 여 **모델 필터** 대화 상자를 닫습니다.  
  
     필터가 **속성** 창에 표시 됩니다. 또는 **속성** 창에서 **모델 필터** 대화 상자를 시작할 수 있습니다.  
  
8.  위의 단계를 반복 하 되 이번에는 모델 `TM_Decision_Tree_Female` 이름을로, **값** 텍스트 상자에 **F** 를 입력 합니다.  
  
## <a name="process-the-filtered-models"></a>필터링된 모델 처리  
 모델은 배포 및 처리될 때까지 사용할 수 없습니다. 모델 처리에 대 한 자세한 내용은 [기본 데이터 마이닝 자습서 &#40;대상 메일 구조에서 모델 처리 ](../../2014/tutorials/processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial.md)를 참조 하세요&#41;.  
  
#### <a name="to-process-the-filtered-model"></a>필터링된 모델을 처리하려면  
  
1.  모델을 마우스 오른쪽 `TM_Decision_Tree_Male` 단추로 클릭 하 고 **마이닝 구조 및 모든 모델 처리를**선택 합니다.  
  
2.  **실행** 을 클릭 하 여 새 모델을 처리 합니다.  
  
3.  처리가 완료 되 면 두 처리 창에서 **닫기** 를 클릭 합니다.  
  
     **마이닝 모델** 탭에 새 모델이 두 개 표시 됩니다.  
  
## <a name="evaluate-the-results"></a>결과 평가  
 이전 세 개의 모델에 대해 수행했던 방식과 거의 동일한 방식으로 결과를 검토하고 필터링된 모델의 정확도를 평가합니다. 자세한 내용은 다음을 참조하세요.  
  
 [기본 데이터 마이닝 자습서 &#40;의사 결정 트리 모델 탐색&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
 [리프트 차트를 사용하여 정확도 테스트&#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
#### <a name="to-explore-the-filtered-models"></a>필터링된 모델을 탐색하려면  
  
1.  **데이터 마이닝 디자이너**에서 **마이닝 모델 뷰어** 탭을 선택 합니다.  
  
2.  마이닝 모델 상자에서를 선택 `TM_Decision_Tree_Male`합니다.  
  
3.  **쇼 수준** 을로 `3`이동 합니다.  
  
4.  **배경** 값을로 `1`변경 합니다.  
  
5.  **모두** 레이블이 지정 된 노드에 커서를 놓아 자전거 구매자와 비 자전거 구매자의 수를 확인 합니다.  
  
6.  에 대해 1-5 단계 `TM_Decision_Tree_Female`를 반복 합니다.  
  
7.  `TM_Decision_Tree` 및 성별에 대해 필터링 된 모델에 대 한 결과를 살펴봅니다. 모든 자전거 구매자와 비교해 볼 때 남성 자전거 구매자와 여성 자전거 구매자는 필터링되지 않은 자전거 구매자와 동일한 특징을 일부 공유하지만 이 세 범주의 구매자에게는 흥미로운 차이점도 있습니다. 이는 마케팅 캠페인을 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 개발 하는 데 사용할 수 있는 유용한 정보입니다.  
  
#### <a name="to-test-the-lift-of-the-filtered-models"></a>필터링된 모델의 리프트를 테스트하려면  
  
1.  의 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 데이터 마이닝 디자이너에서 **마이닝 정확도 차트** 탭으로 전환 하 고 **입력 선택** 탭을 선택 합니다.  
  
2.  **정확도 차트에 사용할 데이터 집합을 선택** 하십시오. 그룹 상자에서 **마이닝 구조 테스트 사례 사용**을 선택 합니다.  
  
3.  데이터 마이닝 디자이너의 **입력 선택** 탭에 있는 **리프트 차트에 표시할 예측 가능한 마이닝 모델 열을 선택**하십시오 .에서 **예측 열과 값 동기화**에 대 한 확인란을 선택 합니다.  
  
4.  **예측 가능한 열 이름** 열에서 각 모델에 대해 **자전거 구매자** 가 선택 되어 있는지 확인 합니다.  
  
5.  **표시** 열에서 각 모델을 선택 합니다.  
  
6.  **예측 값** 열에서을 선택 `1`합니다.  
  
7.  **리프트 차트 탭을** 선택 하 여 리프트 차트를 표시 합니다.  
  
     세 가지 의사 결정 트리 모델은 모두 임의 추측 모델과 비교했을 때 유효한 리프트를 제공할 뿐만 아니라 클러스터링 및 Naive-Bayes 모델보다 성능이 뛰어납니다.  
  
## <a name="related-tasks"></a>관련 작업  
 필터에 대 한 자세한 내용은 [데이터 마이닝&#41;Analysis Services &#40;마이닝 모델에 대 한 필터 ](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)를 참조 하세요.  
  
 중첩 테이블에 필터를 적용 하는 방법에 대 한 예는 [Analysis Services-데이터 마이닝&#41;&#40;중급 데이터 마이닝 자습서 ](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)를 참조 하세요.  
  
## <a name="previous-task-in-lesson"></a>단원의 이전 태스크  
 [리프트 차트를 사용하여 정확도 테스트&#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>다음 단원  
 [6단원: 예측 만들기 및 작업&#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>참고 항목  
 [Analysis Services 데이터 마이닝&#41;&#40;중급 데이터 마이닝 자습서](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [마이닝 모델 태스크 및 방법](../../2014/analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [마이닝 모델에서 필터 삭제](../../2014/analysis-services/data-mining/delete-a-filter-from-a-mining-model.md)   
 [마이닝 모델에 대한 필터&#40;Analysis Services - 데이터 마이닝&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)  
  
  
