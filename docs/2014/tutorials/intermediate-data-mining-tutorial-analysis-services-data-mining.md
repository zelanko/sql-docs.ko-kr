---
title: 중급 데이터 마이닝 자습서 (Analysis Services 데이터 마이닝) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 404b31d5-27f4-4875-bd60-7b2b8613eb1b
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4c244701d8a58765061ef3bde1f918c8be5a941d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63017178"
---
# <a name="intermediate-data-mining-tutorial-analysis-services---data-mining"></a>중급 데이터 마이닝 자습서(Analysis Services - 데이터 마이닝)
  [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 는 데이터 마이닝 모델을 만들고 작업 하기 위한 통합 환경을 제공 합니다. 데이터 원본에 쉽게 바인딩하고, 여러 모델을 만들어 같은 데이터에 대해 테스트하고, 예측 분석에 사용할 모델을 배포할 수 있습니다.  
  
 기본 데이터 마이닝 자습서에서는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 를 사용하여 데이터 마이닝 솔루션을 만드는 방법을 학습하고, 고객 구매 행동을 분석하고 잠재적인 구매자를 대상으로 하는 타겟 메일링 캠페인을 지원하는 3개의 모델을 작성했습니다.  
  
 이 중급 자습서는 이러한 기본 자습서를 기반으로 작성되었으며 예측 및 시장 바구니 분석과 같은 일반적인 비즈니스 요구 사항을 포함하여 여러 가지 새로운 시나리오를 소개합니다. 시계열 모델, 연결 모델 및 시퀀스 클러스터링 모델을 만드는 방법에 대해 설명합니다. 마지막으로 신경망을 사용하여 데이터의 상관 관계를 탐색하는 방법과 로지스틱 회귀를 사용하여 예측하는 방법을 배웁니다.  
  
 단원은 독립적이며 별도로 완료할 수 있습니다.  
  
 다음 자습서를 완료하려면 기본 데이터 마이닝 자습서에서 소개한 마이닝 모델 뷰어 및 데이터 마이닝 도구에 익숙해야 합니다.  
  
 모든 시나리오는 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 데이터 원본을 사용하지만 시나리오마다 다른 데이터 원본 뷰를 만듭니다. 데이터 원본을 먼저 만들면 순서에 관계없이 단원을 학습할 수 있습니다.  
  
## <a name="lesson-scenarios"></a>단원 시나리오  
 타겟 메일링 캠페인이 성공하면 비즈니스 계획에 사용하기 위해 여러 새로운 모델을 개발하는 데 학습한 데이터 마이닝 정보를 적용할 것인지 묻는 메시지가 표시됩니다. 다음과 같은 태스크가 있습니다.  
  
-   **예측:** 전세계 여러 지역에서 제품 판매를 예측하는 *시계열* 모델을 만듭니다. 각 지역의 개별 모델을 개발하고 *교차 예측*을 사용하는 방법을 배웁니다.  
  
-   **시장 바구니 분석:***전자 상거래 사이트를 방문하는 동안 구매한 제품 그룹을 분석하는*연결 모델 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 을 만듭니다. 이 시장 바구니 모델을 기반으로 하여 고객에게 제품을 권장할 수 있습니다.  
  
-   **시퀀스 분석:** 고객이 제품을 구매한 순서를 분석하는 *시퀀스 클러스터링 모델*을 작성합니다. 이 모델을 기반으로 하여 웹 사이트 디자인 또는 새 제안의 변경 사항을 계획할 수 있습니다.  
  
-   **요소 분석:***신경망* 모델을 사용하여 콜 센터 데이터에서 서비스 품질 불량의 가능한 원인을 탐색합니다. 예비 모델이 나타내는 정보를 기반으로 사용자 환경을 개선하기 위한 전략을 예측하는 *로지스틱 회귀 모델* 을 만듭니다.  
  
## <a name="what-you-will-learn"></a>학습 내용  
 이 자습서에서는 여러 유형의 데이터 마이닝 알고리즘을 만들고 작업하는 방법에 대해 설명합니다. 이 자습서는 다음 단원으로 이루어져 있습니다.  
  
 [1 단원: 중급 데이터 마이닝 자습서를 &#40;중급 데이터 마이닝 솔루션 만들기&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
 이 단원에서는 여러 가지 새로운 데이터 원본 뷰 및 기타 여러 마이닝 모델을 지원할 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 데이터베이스를 기반으로 새 프로젝트를 만듭니다.  
  
 [2 단원: 중급 데이터 마이닝 자습서 &#40;예측 시나리오 구축&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
 이 단원에서는 예측 시나리오의 일부로 사용할 수 있는 마이닝 모델을 만듭니다. 또한 [!INCLUDE[msCoName](../includes/msconame-md.md)] 시계열 알고리즘으로 작성한 마이닝 모델을 탐색합니다.  
  
 각 지역에 대한 개별 모델과 교차 예측에 사용할 수 있는 일반 모델을 작성합니다.  
  
 [3단원: 시장 바구니 시나리오 구축&#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
 이 단원에서는 새 데이터 원본 뷰를 추가한 다음 중첩 테이블과 키 사용 방법에 대해 설명합니다. 이 데이터를 기반으로 시장 바구니 시나리오의 일부로 사용할 수 있는 마이닝 모델을 만듭니다. 또한 [!INCLUDE[msCoName](../includes/msconame-md.md)] 연결 알고리즘으로 작성한 마이닝 모델을 탐색합니다.  
  
 [4 단원: 중간 데이터 마이닝 자습서 &#40;시퀀스 클러스터링 시나리오 빌드&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
 이 단원에서는 시퀀스 클러스터링 시나리오의 일부로 사용할 수 있는 마이닝 모델을 만듭니다. [!INCLUDE[msCoName](../includes/msconame-md.md)] 시퀀스 클러스터링 알고리즘으로 구축된 마이닝 모델을 탐색하는 방법도 배웁니다.  
  
 [5단원: 신경망 및 로지스틱 회귀 모델 작성&#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
 이 단원에서는 Microsoft 신경망 및 Microsoft 로지스틱 회귀 알고리즘을 사용하여 여러 관련된 마이닝 모델을 만듭니다. 또한 데이터 원본 뷰를 사용하여 모델의 기본이 되는 데이터를 탐색하는 방법도 배웁니다.  
  
## <a name="requirements"></a>요구 사항  
 다음이 설치되어 있어야 합니다.  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스가 있는 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] .  
  
 보안을 위해 예제 데이터베이스는 기본적으로 설치되지 않습니다. [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 공식 데이터베이스를 설치하려면 [Microsoft SQL 예제 데이터베이스](https://go.microsoft.com/fwlink/?LinkId=88417) 페이지를 방문하고 해당 버전의 예제 데이터베이스를 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
 [기본 데이터 마이닝 자습서](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [자전거 구매자 DMX 자습서](../../2014/tutorials/bike-buyer-dmx-tutorial.md)   
 [Market Basket DMX 자습서](../../2014/tutorials/market-basket-dmx-tutorial.md)  
  
  
