---
title: '5 단원: 신경망 및 로지스틱 회귀 모델 (중급 데이터 마이닝 자습서) 빌드 | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- logistic regression [Analysis Services]
- data mining [Analysis Services], tutorials
- neural networks
- tutorials [Data Mining]
- neural network model [Analysis Services]
ms.assetid: 42c3701a-1fd2-44ff-b7de-377345bbbd6b
caps.latest.revision: 22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 93946e13e9836aef4cd10bc39ec964e7f8c0d531
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37222343"
---
# <a name="lesson-5-building-neural-network-and-logistic-regression-models-intermediate-data-mining-tutorial"></a>5단원: 신경망 및 로지스틱 회귀 모델 작성(중급 데이터 마이닝 자습서)
  
  
 운영 부서가 [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] 콜 센터를 사용 하 여 고객 만족도 개선 하기 위해 프로젝트에 참여 하는 합니다. 이 부서에서는 콜 센터를 관리하고 콜 센터 효율성에 대한 메트릭을 보고할 한 업체를 선정하고 여러분에게 이 업체가 제공한 일부 예비 정보를 분석하는 업무를 요청합니다. 이 부서에서는 업체가 보고한 정보에 관심이 갈 만한 내용이 있는지 알고 싶습니다. 특히 이 데이터에서 직원 배치의 문제점 또는 고객 만족도를 개선하는 방법을 제안하는지 알고 싶습니다.  
  
 데이터 집합은 작으며 30일간의 콜 센터 운영 기간만 포함합니다. 데이터는 각 교대조의 신규 및 경력 전화 상담원 수, 수신 전화 수, 주문 수는 물론 해결해야 할 문제 및 고객의 평균 통화 응답 대기 시간을 추적합니다. 또한 데이터에는 고객 불만 지표인 *중단율*을 기반으로 한 서비스 품질 메트릭도 포함됩니다.  
  
 데이터가 나타내는 내용에 대해 사전에 어떠한 예측도 하지 않았으므로 신경망 모델을 사용하여 가능한 상관 관계를 탐색하기로 결정했습니다. 신경망 모델은 많은 입력과 출력 간의 복잡한 관계를 분석하기 때문에 자주 탐색에 사용됩니다.  
  
## <a name="what-you-will-learn"></a>학습 내용  
 이 단원에서는 신경망 알고리즘을 사용하여 여러분과 운영 팀이 데이터의 추세를 이해하는 데 사용할 수 있는 모델을 작성합니다. 이 단원을 통해 다음 질문에 답할 수 있습니다.  
  
-   고객 만족에 영향을 주는 요인은 무엇입니까?  
  
-   콜 센터가 서비스 품질을 개선하기 위해 할 수 있는 일은 무엇입니까?  
  
 결과에 따라 예측에 사용할 수 있는 로지스틱 회귀 모델을 작성합니다. 운영 팀에서는 예측을 통해 호출 센터 운영을 보다 쉽게 계획할 수 있습니다.  
  
 이 단원에서는 다음 항목을 다룹니다.  
  
-   [추가 데이터 원본 뷰의 콜 센터 데이터에 대 한 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/add-data-source-view-call-center-data-intermediate-data-mining.md)  
  
-   [신경망 구조 및 모델 만들기 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/creating-a-neural-network-structure-and-model-intermediate-data-mining-tutorial.md)  
  
-   [콜 센터 모델 탐색 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/exploring-the-call-center-model-intermediate-data-mining-tutorial.md)  
  
-   [콜 센터 구조에 로지스틱 회귀 모델 추가 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/add-logistic-regression-model-to-call-center-intermediate-data-mining.md)  
  
-   [콜 센터 모델에 대 한 예측을 만드는 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/create-predictions-call-center-models-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [추가 데이터 원본 뷰의 콜 센터 데이터에 대 한 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/add-data-source-view-call-center-data-intermediate-data-mining.md)  
  
## <a name="all-lessons"></a>모든 단원  
 [1 단원: 중간 데이터 마이닝 솔루션 만들기 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 [2 단원: 예측 시나리오 구축 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
 [3 단원: 시장 바구니 시나리오 구축 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
 [4 단원: 시퀀스 클러스터링 시나리오 구축 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
  
 5단원: 신경망 및 로지스틱 회귀 시나리오(중급 데이터 마이닝 자습서)  
  
## <a name="see-also"></a>관련 항목  
 [기본 데이터 마이닝 자습서](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [중급 데이터 마이닝 자습서 &#40;Analysis Services-데이터 마이닝&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)  
  
  
