---
title: '3 단원: 시장 바구니 시나리오 (중급 데이터 마이닝 자습서) 구축 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], tutorials
- association algorithms [Analysis Services]
- nested tables
- tutorials [Data Mining]
ms.assetid: 651eef38-772e-4d97-af51-075b1b27fc5a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f31a323320487623339170043112fceb7ba65d3b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48109423"
---
# <a name="lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial"></a>3단원: 시장 바구니 시나리오 구축(중급 데이터 마이닝 자습서)
  마케팅 부서 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 교차 판매 홍보 회사 웹 사이트를 개선 하려고 합니다. 사이트 업데이트의 일부로 이 부서에서는 고객의 온라인 시장 바구니에 이미 있는 다른 제품을 기반으로 고객이 구매할 제품을 예측하려고 합니다. 또한 구매될 가능성이 높은 항목이 함께 배열되도록 웹 사이트를 디자인하여 고객의 구매 행동을 더 잘 파악하고자 합니다. 이 부서에서는 데이터 마이닝이 이러한 종류의 *시장 바구니 분석* 에 특히 유용하다는 것을 알게 되었으며 데이터 마이닝 모델 개발을 요구해 왔습니다.  
  
 이 단원의 태스크를 마치면 고객의 거래 내역에서 항목 그룹을 보여 주는 마이닝 모델이 마련됩니다. 또한 이 마이닝 모델을 사용하여 고객이 구매할 수 있는 추가 항목을 예측할 수 있습니다.  
  
 이 단원의 태스크를 완료 하려면의 첫 번째 단원에서 만든 솔루션과 데이터 원본을 사용할지를 [중급 데이터 마이닝 자습서 &#40;Analysis Services-데이터 마이닝&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)합니다. 고객 구매에 대한 중첩 테이블을 비롯하여 고객에 대한 테이블이 포함된 데이터 원본 뷰를 추가하여 이 솔루션을 수정합니다.  그런 다음 시장 바구니 시나리오에 적합한 Microsoft 연결 규칙 알고리즘을 사용하는 마이닝 모델을 작성합니다.  
  
 이 단원에서는 다음 항목을 다룹니다.  
  
-   [추가 데이터 원본 뷰에 중첩된 테이블이 있는 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial.md)  
  
-   [시장 바구니 구조 및 모델 만들기 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial.md)  
  
-   [시장 바구니 모델 수정 및 처리 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/modify-process-market-basket-model-intermediate-data-mining-tutorial.md)  
  
-   [시장 바구니 모델 탐색 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/exploring-the-market-basket-models-intermediate-data-mining-tutorial.md)  
  
-   [마이닝 모델의 중첩된 테이블 필터링 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/filtering-a-nested-table-in-a-mining-model-intermediate-data-mining-tutorial.md)  
  
-   [연결 예측 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/predicting-associations-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [추가 데이터 원본 뷰에 중첩된 테이블이 있는 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial.md)  
  
## <a name="all-lessons"></a>모든 단원  
 [1 단원: 중간 데이터 마이닝 솔루션 만들기 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 [2 단원: 예측 시나리오 구축 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
 3단원: 시장 바구니 시나리오(중급 데이터 마이닝 자습서)  
  
 [4 단원: 시퀀스 클러스터링 시나리오 구축 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
  
 [5 단원: 신경망 및 로지스틱 회귀 모델 작성 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>관련 항목  
 [기본 데이터 마이닝 자습서](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [2 단원: 예측 시나리오 구축 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)   
 [4 단원: 시퀀스 클러스터링 시나리오 구축 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
  
  
