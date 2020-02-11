---
title: 구조 데이터에 드릴스루 사용 (기본 데이터 마이닝 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a693979c-0564-4d6d-b35d-cbbc8f350469
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 68d5d29a4aed7380bd7a53c65d140aac24912392
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62745544"
---
# <a name="using-drillthrough-on-structure-data-basic-data-mining-tutorial"></a>구조 데이터에 드릴스루 사용(기본 데이터 마이닝 자습서)
  광고 캠페인의 일환으로 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 는 34-40 시대의 인구 통계에서 잠재 고객에 게 메일을 보내는 중입니다. 마케팅 부서에서는 5년 전에 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 에서 자전거를 구매한 고객에게도 메일러를 보내려고 합니다. 이 단원에서는 오래 전에 자전거를 구매한 고객을 식별하고 그들의 연락처 정보를 검색합니다. 이 정보는 모델에 포함되어 있지 않지만 구조에는 포함되어 있습니다. 연락처 정보를 검색하려면 먼저 구조에 대해 드릴스루를 사용할 수 있는지 확인한 다음 드릴스루를 사용하여 대상 고객의 이름과 주소를 확인합니다.  
  
### <a name="to-enable-drillthrough-on-a-mining-model"></a>마이닝 모델에서 드릴스루를 사용하려면  
  
1.  에서 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]데이터 마이닝 디자이너의 **마이닝 모델** 탭에 있는 **TM_Decision_Tree** 모델을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.  
  
2.  
  속성 창에서 **AllowDrillthrough**를 클릭하고 **True**를 선택합니다.  
  
3.  
  마이닝 모델 탭에서 모델을 마우스 오른쪽 단추로 클릭하고 **모델 처리**를 선택합니다.  
  
 자세한 내용은 [드릴스루 쿼리 &#40;데이터 마이닝](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md) 을 참조 하세요&#41;  
  
### <a name="to-view-drillthrough-data-from-a-mining-model"></a>마이닝 모델에서 드릴스루 데이터를 보려면  
  
1.  데이터 마이닝 디자이너에서 **마이닝 모델 뷰어** 탭을 클릭합니다.  
  
2.  **마이닝 모델** 목록에서 **TM_Decision_Tree** 모델을 선택 합니다.  
  
3.  **배경** 값을로 `1`변경 합니다. 이렇게 하면 모델 중에서 자전거를 구매한 고객과 관련된 부분만 표시됩니다.  
  
4.  
  **뷰어** 목록에서 Microsoft 트리 뷰어를 선택합니다. 그러면 뷰어가 새 필터 조건으로 새로 고쳐집니다. 그런 다음 **Age >= 34 및 <41** 노드를 찾아 해당 노드를 마우스 오른쪽 단추로 클릭 합니다.  
  
5.  
  **드릴스루**를 선택한 다음 **모델 및 구조 열** 을 선택하여 **드릴스루** 창을 엽니다.  
  
6.  
  **Structure.Date First Purchase** 열로 스크롤하여 오래 전에 구매한 자전거에 대한 구매 날짜를 확인합니다.  
  
7.  데이터를 클립보드에 복사하려면 테이블에서 임의의 행을 마우스 오른쪽 단추로 클릭하고 **모두 복사**를 선택합니다.  
  
 축하합니다. 기본 데이터 마이닝 자습서를 완료했습니다. 이제 데이터 마이닝 도구를 능숙하게 사용할 수 있게 되었으므로 예측, 시장 바구니 분석 및 시퀀스 클러스터링에 대한 모델을 만드는 방법을 보여 주는 중급 데이터 마이닝 자습서도 완료하는 것이 좋습니다.  
  
## <a name="previous-task-in-lesson"></a>단원의 이전 태스크  
 [&#40;기본 데이터 마이닝 자습서&#41;예측 만들기](../../2014/tutorials/creating-predictions-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>참고 항목  
 [예측 쿼리 작성기를 사용하여 예측 쿼리 만들기](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  
