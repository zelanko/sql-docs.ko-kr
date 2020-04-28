---
title: '4 단원: 시퀀스 클러스터링 시나리오 구축 (중급 데이터 마이닝 자습서) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], tutorials
- sequence clustering algorithms [Analysis Services]
- tutorials [Data Mining]
ms.assetid: 63436bbd-0f73-4012-b6f1-358c81e4d92a
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d34125b7b750daa1da25c9e8788172b5d9ca2c35
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62710605"
---
# <a name="lesson-4-building-a-sequence-clustering-scenario-intermediate-data-mining-tutorial"></a>4단원: 시퀀스 클러스터링 시나리오 구축(중급 데이터 마이닝 자습서)
  [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 의 마케팅 부서에서 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 웹 사이트를 방문한 고객의 이동 방식을 파악하려고 합니다. 이 회사에서는 고객이 시장 바구니에 제품을 넣는 순서에 일정한 패턴이 있으리라고 생각합니다. 이들은 구매 시퀀스 순서를 분석하여 고객의 시장 바구니에 관련된 항목을 추가하는 방식을 알아보고자 합니다. 이 정보로 웹 사이트의 흐름을 능률화하여 고객의 추가 제품 구매를 유도할 수 있습니다.  
  
 이 단원의 태스크를 완료하면 고객이 시장 바구니에 넣을 다음 항목을 예측할 수 있는 [!INCLUDE[msCoName](../includes/msconame-md.md)] 시퀀스 클러스터링 알고리즘을 사용하는 마이닝 모델을 만들게 됩니다. 두 버전의 모델을 사용합니다. 한 버전은 시장 바구니의 제품 순서만 분석하고 다른 버전에는 클러스터링할 추가 고객 통계가 포함되어 있습니다. 마지막으로 이 모델을 사용하여 고객에게 제품을 권장하는 데 사용할 수 있는 예측을 작성합니다.  
  
 이 단원의 태스크를 완료 하려면 [3 단원: 시장 바구니 시나리오 구축 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)에서 만든 시장 바구니 마이닝 구조를 사용 합니다. 이 단원에서는 다음 태스크를 다룹니다.  
  
-   [중간 데이터 마이닝 자습서를 &#40;시퀀스 클러스터링 마이닝 모델 구조 만들기&#41;](../../2014/tutorials/create-sequence-clustering-mining-model-intermediate-data-mining.md)  
  
-   [시퀀스 클러스터링 모델 처리](../../2014/tutorials/processing-the-sequence-clustering-model.md)  
  
-   [시퀀스 클러스터링 모델 탐색 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/exploring-the-sequence-clustering-model-intermediate-data-mining-tutorial.md)  
  
-   [관련 된 시퀀스 클러스터링 모델 만들기 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial.md)  
  
-   [시퀀스 클러스터링 모델에서 예측 만들기 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/create-predictions-on-model-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [중간 데이터 마이닝 자습서를 &#40;시퀀스 클러스터링 마이닝 모델 구조 만들기&#41;](../../2014/tutorials/create-sequence-clustering-mining-model-intermediate-data-mining.md)  
  
## <a name="all-lessons"></a>모든 단원  
 [1 단원: 중급 데이터 마이닝 자습서를 &#40;중급 데이터 마이닝 솔루션 만들기&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 [2 단원: 중급 데이터 마이닝 자습서 &#40;예측 시나리오 구축&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
 [3단원: 시장 바구니 시나리오 구축&#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
 4단원: 시퀀스 클러스터링 시나리오(중급 데이터 마이닝 자습서)  
  
 [5단원: 신경망 및 로지스틱 회귀 모델 작성&#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>참고 항목  
 [기본 데이터 마이닝 자습서](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [Analysis Services 데이터 마이닝&#41;&#40;중급 데이터 마이닝 자습서](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)  
  
  
