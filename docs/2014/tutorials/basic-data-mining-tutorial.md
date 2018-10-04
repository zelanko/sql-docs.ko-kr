---
title: 기본 데이터 마이닝 자습서 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- databases [Analysis Services], tutorials
- data mining [Analysis Services], tutorials
- tutorials [Data Mining]
ms.assetid: 6602edb6-d160-43fb-83c8-9df5dddfeb9c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: db5b4fcded48a711fc1c8e8c8ffdebdd36562282
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48150303"
---
# <a name="basic-data-mining-tutorial"></a>기본 데이터 마이닝 자습서
  시작 합니다 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 기본 데이터 마이닝 자습서입니다. [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터 마이닝 모델을 만들고 예측 하기 위한 통합된 환경을 제공 합니다. 이 자습서에서는 시스템 학습을 사용하여 고객 구매 행동을 분석하고 예측하는 타겟 메일링 캠페인 시나리오를 완료합니다. 이 자습서에서는 가장 중요한 세 가지 데이터 마이닝 알고리즘인 클러스터링, 의사 결정 트리 및 Naive Bayes를 사용하는 방법을 보여 줍니다. 또한 마이닝 모델 뷰어를 사용 하 여 결과 분석 및 예측과 정확도 차트에 포함 된 데이터 마이닝 도구를 사용 하 여를 만드는 방법을 배웁니다 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]합니다. 모든 예에 가상 회사인 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]가 사용됩니다.  
  
 데이터 마이닝 도구를 사용 하 여 편리 하 게 되 면도 완료 하는 것이 좋습니다 합니다 [중급 데이터 마이닝 자습서 &#40;Analysis Services-데이터 마이닝&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)합니다. 해당 단원에서는 예측, 시장 바구니 분석, 시계열, 연결 모델, 중첩 테이블 및 시퀀스 클러스터링을 사용하는 방법을 보여 줍니다.  
  
## <a name="tutorial-scenario"></a>자습서 시나리오  
 직원은이 자습서에서는 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 수행한 사용자가 구매 기록이 기반된으로 회사의 고객에 대해 자세히 알아보기 및 다음 해당 기록 데이터를 사용 하 여 마케팅에 사용할 수 있는 예측을 수행 합니다. 이 회사는 이전에 데이터 마이닝을 수행한 적이 없기 때문에 사용자는 특히 데이터 마이닝을 위한 새 데이터베이스를 만들고 여러 데이터 마이닝 모델을 설정해야 합니다.  
  
## <a name="what-you-will-learn"></a>학습 내용  
 이 자습서에서는 여러 종류의 시스템 학습 방법을 만들고 작업하는 방법을 배웁니다. 또한 마이닝 모델의 복사본을 만들고 입력 데이터에 필터를 적용하여 여러 가지 결과를 얻는 방법도 알아봅니다. 이후에 리프트 차트를 사용하여 두 모델의 결과를 비교할 수 있습니다. 마지막으로 드릴스루를 사용하여 기본 마이닝 구조에서 추가 데이터를 검색합니다.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 다음을 포함 하는 데이터 마이닝 기능을 쉽게 개발 여러 예측 모델을 비교 및 결과 대해 다음 동작을 수행 합니다.  
  
-   *홀드아웃 테스트 집합 -* 마이닝 구조를 만들 때 이제는 마이닝 구조의 데이터를 학습 집합과 테스트 집합으로 나눌 수 있습니다. 이렇게 하면 비슷한 데이터 집합에서 모델을 테스트하고 관련 모델의 정확도를 비교할 수 있습니다.  
  
-   *마이닝 모델 필터 -* 이제 마이닝 모델에 필터를 연결하고 학습 및 테스트 중에 해당 필터를 적용할 수 있습니다. 이렇게 하면 데이터의 여러 하위 집합을 기반으로 관련 모델을 쉽게 작성할 수 있습니다.  
  
-   *구조 사례 및 구조 열로 드릴스루 -* 이제 마이닝 모델의 일반적인 패턴에서 데이터 원본의 후속 조치 가능한 세부 정보로 쉽게 전환할 수 있습니다.  
  
 이 자습서는 다음 단원으로 이루어져 있습니다.  
  
 [1 단원: 데이터베이스 서비스는 분석을 준비 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-1-preparing-the-analysis-services-database-basic-data-mining-tutorial.md)  
 이 단원에서는 새 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스를 만들고 데이터 원본과 데이터 원본 뷰를 추가하며 데이터 마이닝에 사용할 새 데이터베이스를 준비하는 방법을 배웁니다.  
  
 [2 단원: 타겟된 메일링 구조 구축 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-2-building-a-targeted-mailing-structure-basic-data-mining-tutorial.md)  
 이 단원에서는 대상 메일 시나리오의 일부로 사용할 수 있는 마이닝 모델 구조를 만드는 방법을 배웁니다.  
  
 [3단원: 모델 추가 및 처리](../../2014/tutorials/lesson-3-adding-and-processing-models.md)  
 이 단원에서는 구조에 모델을 추가하는 방법을 배웁니다. 사용자가 만드는 모델은 다음 알고리즘을 사용하여 생성됩니다.  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] 의사 결정 트리  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] 클러스터링  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes  
  
 [4 단원: 타겟된 메일링 모델 탐색 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-4-exploring-the-targeted-mailing-models-basic-data-mining-tutorial.md)  
 이 단원에서는 뷰어를 사용하여 각 모델의 결과를 탐색하고 해석하는 방법을 배웁니다.  
  
 [5 단원: 모델을 테스트 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
 이 단원에서는 대상 메일 모델 중 하나의 복사본을 만들고, 마이닝 모델 필터를 추가하여 학습 데이터를 특정 고객 집합으로 제한한 다음 모델의 실행 가능성을 평가합니다.  
  
 [6 단원: 만들기 및 예측 작업 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)  
 기본 데이터 마이닝 자습서의 이 마지막 단원에서는 모델을 사용하여 자전거를 구매할 가능성이 가장 높은 고객을 예측합니다. 그런 다음 기본 사례로 드릴스루하여 연락처 정보를 얻습니다.  
  
## <a name="requirements"></a>요구 사항  
 다음이 설치되어 있어야 합니다.  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 다차원 모드의  
  
-   [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 데이터베이스.  
  
 보안을 위해 예제 데이터베이스는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]과 함께 설치되지 않습니다. 공식 데이터베이스를 설치 하려면 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 방문 합니다 [Microsoft SQL Sample Databases](http://go.microsoft.com/fwlink/?LinkId=88417) 페이지를 선택 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]합니다.  
  
> [!NOTE]  
>  문서 뷰어 도구 모음에 **다음 항목** 단추 및 **이전 항목** 단추를 추가하면 단계의 앞뒤로 편리하게 이동할 수 있어 자습서를 더 쉽게 진행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 솔루션](../../2014/analysis-services/data-mining/data-mining-solutions.md)   
 [마이닝 모델 태스크 및 방법](../../2014/analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [DMX 사용 하 여 데이터 마이닝 모델 만들기 및 쿼리: 자습서 &#40;Analysis Services-데이터 마이닝&#41;](../../2014/tutorials/create-query-data-mining-models-dmx-tutorials.md)  
  
  
