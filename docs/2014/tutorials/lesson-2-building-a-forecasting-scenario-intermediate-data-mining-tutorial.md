---
title: '2 단원: 예측 시나리오 구축 (중급 데이터 마이닝 자습서) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- time series [Analysis Services]
- data mining [Analysis Services], tutorials
- tutorials [Data Mining]
ms.assetid: 9a988156-c900-4c22-97fa-f6b0c1aea9e2
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ee814dc0891e70dfeccf2b96383d1d7b5c324aa8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62931525"
---
# <a name="lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial"></a>2단원: 예측 시나리오 구축(중급 데이터 마이닝 자습서)
  [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]의 판매 분석가가 제품의 내년 판매액을 예측해 달라는 요청을 받았습니다. 특히 지역 및 제품 라인별 예측을 비교해야 합니다. 또한 시간에 따라 여러 제품의 판매 방식이 달라지는지 확인해야 합니다.  
  
 요청된 정보를 찾기 위해 이 단원에서 월별 수준으로 회사의 판매 데이터를 요약하고 판매 수치를 유럽, 북아메리카 및 태평양 세 지역으로 요약합니다.  
  
 이 단원의 태스크를 완료하면 다음 질문에 대답할 수 있습니다.  
  
-   시간에 따라 여러 자전거 모델의 판매가 어떻게 변경됩니까?  
  
-   세 지역의 판매 패턴 간에 차이가 있습니까?  
  
-   최고 매출을 예측할 수 있습니까?  
  
 이 단원을 두 부분으로 완료할 수 있습니다.  
  
-   1부에서는 시계열 모델을 만들고 사용하는 방법에 대한 기본 사항을 소개합니다.  
  
-   2부에서는 모든 지역을 기반으로 일반 시계열 모델을 만드는 과정을 안내합니다. 이 일반 모델을 *교차 예측*에 사용할 수 있습니다.  
  
 아래에 나열 된이 단원의 태스크를 완료 하려면 1 단원: 중급 데이터 마이닝 솔루션 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] &#40;중급 데이터 [마이닝 자습서&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)에서 만든 데이터 원본을 사용 합니다.  
  
> [!WARNING]  
>  [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 예제 데이터베이스에서의 날짜가 이 릴리스에 맞게 업데이트되었습니다. 이전 버전의 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]를 사용하는 경우 다음 단계에 따라 모델을 작성할 수 있지만 나타나는 결과가 달라질 수 있습니다.  
  
 **간단한 예측 모델 만들기**  
  
-   [예측을 위한 데이터 원본 뷰 추가 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/adding-a-data-source-view-for-forecasting-intermediate-data-mining-tutorial.md)  
  
-   [&#40;중급 데이터 마이닝 자습서&#41;예측 구조 및 모델 만들기](../../2014/tutorials/creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial.md)  
  
-   [&#40;중급 데이터 마이닝 자습서&#41;예측 구조 수정](../../2014/tutorials/modifying-the-forecasting-structure-intermediate-data-mining-tutorial.md)  
  
-   [&#40;중급 데이터 마이닝 자습서를 통해 예측 모델 사용자 지정 및 처리&#41;](../../2014/tutorials/customize-process-forecasting-model-intermediate-data-mining-tutorial.md)  
  
-   [예측 모델 탐색 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/exploring-the-forecasting-model-intermediate-data-mining-tutorial.md)  
  
-   [&#40;중급 데이터 마이닝 자습서&#41;시계열 예측 만들기](../../2014/tutorials/creating-time-series-predictions-intermediate-data-mining-tutorial.md)  
  
 **교차 예측을 위한 일반 예측 모델 만들기**  
  
-   [고급 시계열 예측 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/advanced-time-series-predictions-intermediate-data-mining-tutorial.md)  
  
-   [업데이트 된 데이터를 사용한 시계열 예측 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/time-series-predictions-using-updated-data-intermediate-data-mining-tutorial.md)  
  
-   [대체 데이터를 사용한 시계열 예측 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
-   [예측 모델에 대 한 예측 비교 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [예측을 위한 데이터 원본 뷰 추가 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/adding-a-data-source-view-for-forecasting-intermediate-data-mining-tutorial.md)  
  
 [시계열 모델에 대 한 요구 사항 이해 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/time-series-model-requirements-intermediate-data-mining-tutorial.md)  
  
## <a name="all-lessons"></a>모든 단원  
 [1 단원: 중급 데이터 마이닝 자습서를 &#40;중급 데이터 마이닝 솔루션 만들기&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 2단원: 예측 시나리오 구축(중급 데이터 마이닝 자습서)  
  
 [3단원: 시장 바구니 시나리오 구축&#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
 [4 단원: 중간 데이터 마이닝 자습서 &#40;시퀀스 클러스터링 시나리오 빌드&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
  
 [5단원: 신경망 및 로지스틱 회귀 모델 작성&#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>참고 항목  
 [기본 데이터 마이닝 자습서](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [Analysis Services 데이터 마이닝&#41;&#40;중급 데이터 마이닝 자습서](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [Microsoft Time Series 알고리즘](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
