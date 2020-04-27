---
title: 데이터 마이닝 쿼리 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- prediction queries [Analysis Services]
- queries [DMX], creating
- prediction queries [DMX]
- Prediction Query Builder
- mining models [Analysis Services], querying
ms.assetid: 802806a6-69bb-4c3c-b9aa-d1a1ddfc7fc2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2bfce63f3686f06c0289c818daac82f336fb2b17
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66084966"
---
# <a name="data-mining-queries"></a>데이터 마이닝 쿼리
  데이터 마이닝 쿼리는 다음과 같은 다양한 용도로 다음과 같습니다.  
  
-   새 데이터에 모델을 적용하여 단일 또는 여러 예측을 수행합니다. 매개 변수나 일괄 처리로 입력 값을 제공할 수 있습니다.  
  
-   학습에 사용하는 데이터에 대한 통계 요약을 얻습니다.  
  
-   패턴과 규칙을 추출하거나 모델에서 패턴을 나타내는 일반적인 사례의 프로필을 생성합니다.  
  
-   회귀 수식 및 패턴을 설명하는 다른 계산을 추출합니다.  
  
-   특정 패턴에 맞는 사례를 얻습니다.  
  
-   분석에 사용되지 않는 데이터를 포함하여 모델에 사용되는 개별 사례에 대한 세부 정보를 검색합니다.  
  
-   새 데이터를 추가하여 모델을 다시 학습하거나 교차 예측을 수행합니다.  
  
 이 섹션에서는 데이터 마이닝 쿼리를 시작하는 데 필요한 정보의 개요를 제공합니다. 또한 데이터 마이닝 개체에 대해 만들 수 있는 쿼리의 유형에 대해 설명하고 쿼리 도구와 쿼리 언어를 소개하며 SQL Server 데이터 마이닝에서 제공하는 알고리즘을 사용하여 작성된 모델에 대해 만들 수 있는 쿼리 예의 링크를 제공합니다.  
  
 [데이터 마이닝 쿼리 이해](#bkmk_Understand)  
  
 [쿼리 도구 및 인터페이스](#bkmk_Interfaces)  
  
 [다른 모델 유형에 대 한 쿼리](#bkmk_ModelTypes)  
  
 [요구 사항](#bkmk_Reqs)  
  
##  <a name="understanding-data-mining-queries"></a><a name="bkmk_Understand"></a>데이터 마이닝 쿼리 이해  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 마이닝은 다음과 같은 쿼리 유형을 지원합니다.  
  
-   [예측 쿼리&#40;데이터 마이닝&#41;](prediction-queries-data-mining.md)  
  
     모델의 패턴을 기반으로 입력 데이터에서 추론하는 쿼리입니다.  
  
-   [내용 쿼리&#40;데이터 마이닝&#41;](content-queries-data-mining.md)  
  
     모델 자체에 대한 메타데이터, 통계 및 기타 정보를 반환하는 쿼리입니다.  
  
-   [드릴스루 쿼리&#40;데이터 마이닝&#41;](drillthrough-queries-data-mining.md)  
  
     모델의 기본 사례 데이터나 모델에서 사용되지 않은 구조의 데이터까지 검색할 수 있는 쿼리입니다.  
  
-   [데이터 정의 쿼리&#40;데이터 마이닝&#41;](data-definition-queries-data-mining.md)  
  
     모델에서 정보를 반환하지 않지만 모델과 구조를 작성하거나 모델 또는 구조에서 데이터를 업데이트하는 데 사용되는 쿼리입니다.  
  
 쿼리를 만들기 전에 SQL Server에서 제공하는 각각의 데이터 마이닝 알고리즘으로 만들어진 모델 간의 차이를 잘 알아두는 것이 좋습니다.  
  
-   각 알고리즘 유형에 대해 제공된 사용자 지정 데이터 마이닝 뷰어를 사용하여 각 모델 유형을 찾아보고 탐색합니다. 자세한 내용은 [마이닝 모델 뷰어 태스크 및 방법](mining-model-viewer-tasks-and-how-tos.md)을 참조하세요.  
  
-   **Microsoft 일반 콘텐츠 트리 뷰어**를 사용하여 각 모델 유형의 모델 콘텐츠를 검토합니다. 이 정보를 해석하려면 [마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](mining-model-content-analysis-services-data-mining.md)을 참조하세요.  
  
##  <a name="query-tools-and-interfaces"></a><a name="bkmk_Interfaces"></a>쿼리 도구 및 인터페이스  
 SQL Server에서 제공하는 쿼리 도구 중 하나를 사용하여 대화식으로 데이터 마이닝 쿼리를 작성할 수 있습니다. 그래픽 예측 쿼리 작성기는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 와 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 제공됩니다. 예측 쿼리 작성기를 사용해보지 않은 경우 [Basic Data Mining Tutorial](../../tutorials/basic-data-mining-tutorial.md) 의 단계를 수행하여 인터페이스에 대해 잘 알아두는 것이 좋습니다. 단계를 간단히 살펴보려면 [예측 쿼리 작성기를 사용하여 예측 쿼리 만들기](create-a-prediction-query-using-the-prediction-query-builder.md)를 사용하여 쿼리 만들기를 참조하세요.  
  
 예측 쿼리 작성기는 나중에 사용자 지정할 쿼리를 시작하는 데 유용합니다. 쉽게 데이터 원본을 추가하고 열에 매핑한 다음 DMX 뷰로 전환하고 WHERE 절이나 다른 함수를 추가하여 쿼리를 사용자 지정할 수 있습니다.  
  
 데이터 마이닝 모델과 쿼리 작성 방법을 익히면 DMX(Data Mining Extensions)를 사용하여 쿼리를 직접 작성할 수도 있습니다. DMX는 Transact-SQL과 유사하며 다양한 여러 클라이언트에서 사용할 수 있는 쿼리 언어입니다. DMX는 사용자 지정 예측과 복잡한 쿼리를 만들 수 있는 최상의 도구입니다. DMX에 대한 소개는 [DMX를 사용하여 데이터 마이닝 모델 만들기 및 쿼리: 자습서&#40;Analysis Services - 데이터 마이닝&#41;](../../tutorials/create-query-data-mining-models-dmx-tutorials.md)를 참조하세요.  
  
 DMX 편집기는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 및 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 제공됩니다. 예측 쿼리 작성기를 사용하여 쿼리를 시작한 다음 뷰를 텍스트 편집기로 변경하고 DMX 문을 다른 클라이언트에 복사할 수도 있습니다. 자세한 내용은 [데이터 마이닝 쿼리 인터페이스](data-mining-query-tools.md)를 참조 하세요.  
  
 프로그래밍 방식으로 DMX 문을 작성하고 AMO 또는 XMLA를 사용하여 클라이언트에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버로 보낼 수 있습니다. 그러나 DMX는 마이닝 모델에 대해 쿼리를 만드는 데 사용해야 하는 언어입니다.  
  
 또한 데이터 마이닝 스키마 행 집합을 기반으로 하는 DMV(동적 관리 뷰)를 사용하여 모델의 메타데이터, 통계 및 콘텐츠를 쿼리할 수도 있습니다. 이러한 DMV에서는 SELECT 문을 입력하여 모델에 대한 정보를 쉽게 검색할 수 있지만 예측을 수행할 수는 없습니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 지원하는 DMV에 대한 자세한 내용은 [DMV&#40;동적 관리 뷰&#41;를 사용하여 Analysis Services 모니터링](../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)을 참조하세요.  
  
 마지막으로 [Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md)또는 [Data Mining Query Transformation](../../integration-services/data-flow/transformations/data-mining-query-transformation.md)을 사용하여 Integration Services 패키지에서 사용하기 위한 데이터 마이닝 쿼리를 만들 수 있습니다. 제어 흐름 태스크는 여러 유형의 DMX 쿼리를 지원하는 반면에 데이터 흐름 변환은 데이터 흐름의 데이터로 작업하는 쿼리(즉, PREDICTION JOIN 구문을 사용하는 쿼리)만 지원합니다.  
  
##  <a name="queries-for-different-model-types"></a><a name="bkmk_ModelTypes"></a> 여러 가지 모델 유형에 대한 쿼리  
 모델을 만들 때 사용한 알고리즘은 데이터 마이닝 쿼리에서 얻을 수 있는 정보의 유형에 큰 영향을 줍니다. 이는 각 알고리즘이 고유한 방법으로 데이터를 처리하고 다양한 유형의 패턴을 저장하기 때문입니다. 예를 들어 어떤 알고리즘은 클러스터를 만들고 다른 알고리즘은 트리를 만듭니다. 따라서 작업하고 있는 모델의 유형에 따라 특수한 예측 및 쿼리 함수를 사용해야 할 수도 있습니다.  
  
 다음 목록에서는 쿼리에서 사용할 수 있는 함수에 대한 요약을 제공합니다.  
  
-   **일반 예측 함수:** 함수 `Predict` 는 다형성 이며 모든 모델 형식에서 작동 합니다. 이 함수는 작업하고 있는 모델의 유형을 자동으로 검색하고 추가 매개 변수를 묻는 메시지를 표시합니다. 자세한 내용은 [예측&#40;DMX&#41;](/sql/dmx/predict-dmx)을 참조하세요.  
  
    > [!WARNING]  
    >  일부 모델만 예측을 수행하는 데 사용됩니다. 예를 들어 예측 가능한 특성이 없는 클러스터링 모델을 만들 수 있습니다. 그러나 모델에 예측 가능한 특성이 없는 경우에도 모델에서 다른 유형의 유용한 정보를 반환하는 예측 쿼리를 만들 수 있습니다.  
  
-   **사용자 지정 예측 함수:** 각 모델 유형은 해당 알고리즘으로 만들어진 패턴으로 작업하도록 설계된 예측 함수의 집합을 제공합니다.  
  
     예를 들어 `Lag` 함수는 시계열 모델에 사용되는 기록 데이터를 볼 수 있도록 시계열 모델에 제공됩니다. 클러스터링 모델의 경우 `ClusterDistance`와 같은 함수가 더 중요합니다.  
  
     각 모델 유형에 대해 지원되는 함수에 대한 자세한 내용은 다음 링크를 참조하십시오.  
  
    |||  
    |-|-|  
    |[연결 모델 쿼리 예제](association-model-query-examples.md)|[Microsoft Naive Bayes Algorithm](microsoft-naive-bayes-algorithm.md)|  
    |[클러스터링 모델 쿼리 예제](clustering-model-query-examples.md)|[신경망 모델 쿼리 예제](neural-network-model-query-examples.md)|  
    |[의사 결정 트리 모델 쿼리 예제](decision-trees-model-query-examples.md)|[시퀀스 클러스터링 모델 쿼리 예제](sequence-clustering-model-query-examples.md)|  
    |[선형 회귀 모델 쿼리 예제](linear-regression-model-query-examples.md)|[시계열 모델 쿼리 예제](time-series-model-query-examples.md)|  
    |[로지스틱 회귀 모델 쿼리 예제](logistic-regression-model-query-examples.md)||  
  
     또한 VBA 함수를 호출하거나 함수를 직접 만들 수도 있습니다. 자세한 내용은 [함수&#40;DMX&#41;](/sql/dmx/functions-dmx)를 참조하세요.  
  
-   **일반 통계:** 표준 편차와 같은 기술 통계의 표준 집합을 반환하는, 거의 모든 모델 유형과 함께 사용할 수 있는 다양한 함수가 있습니다.  
  
     예를 들어 `PredictHistogram` 함수는 지정된 열의 모든 상태를 나열하는 테이블을 반환합니다.  
  
     자세한 내용은 [일반 예측 함수&#40;DMX&#41;](/sql/dmx/general-prediction-functions-dmx)를 참조하세요.  
  
-   **사용자 지정 통계:** 특정 분석 태스크와 관련된 통계를 생성하기 위한 추가 지원 함수가 각 모델 유형에 제공됩니다.  
  
     예를 들어 클러스터링 모델로 작업하는 경우 `PredictCaseLikelihood` 함수를 사용하여 특정 사례 및 클러스터와 연결된 유사도 점수를 반환할 수 있습니다. 그러나 선형 회귀 모델을 만든 경우 내용 쿼리를 사용하여 수행할 수 있는 계수 및 절편 검색에 더 관심이 있을 수 있습니다.  
  
-   **모델 콘텐츠 함수:** 모든 모델의 *콘텐츠* 는 단순 쿼리로 정보를 검색할 수 있는 표준화된 형식으로 표시됩니다. DMX를 사용하여 모델 콘텐츠에 대한 쿼리를 만듭니다. 또한 데이터 마이닝 스키마 행 집합을 사용하여 일부 유형의 모델 콘텐츠를 가져올 수도 있습니다.  
  
     모델 콘텐츠에서 반환되는 테이블의 각 행 또는 노드의 의미는 모델을 작성하는 데 사용된 알고리즘의 유형과 열의 데이터 형식에 따라 달라집니다. 자세한 내용은 [내용 쿼리&#40;데이터 마이닝&#41;](content-queries-data-mining.md)을 참조하세요.  
  
##  <a name="requirements"></a><a name="bkmk_Reqs"></a> 요구 사항  
 모델에 대해 쿼리를 만들려면 먼저 데이터 마이닝 모델을 처리해야 합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체를 처리하려면 특별한 권한이 있어야 합니다. 마이닝 모델 처리에 대한 자세한 내용은 [처리 요구 사항 및 고려 사항&#40;데이터 마이닝&#41;](processing-requirements-and-considerations-data-mining.md)을 참조하세요.  
  
 데이터 마이닝 모델에 대해 쿼리를 실행하려면 실행하는 쿼리 유형에 따라 다양한 권한 수준이 필요합니다. 예를 들어 사례 또는 구조 데이터로 드릴스루하려면 마이닝 구조 개체 또는 마이닝 모델 개체에 대해 설정할 수 있는 추가 권한이 일반적으로 필요합니다.  
  
 그러나 쿼리에서 외부 데이터를 사용하고 OPENROWSET 또는 OPENQUERY와 같은 문을 포함하는 경우 쿼리할 데이터베이스에서 이러한 문을 사용할 수 있어야 하고 기본 데이터베이스 개체에 대한 권한이 있어야 합니다.  
  
 데이터 마이닝 쿼리를 실행하는 데 필요한 보안 컨텍스트에 대한 자세한 내용은 [보안 개요&#40;데이터 마이닝&#41;](security-overview-data-mining.md)를 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 이 섹션의 항목에서는 데이터 마이닝 쿼리의 각 유형에 대해 자세히 소개하고 데이터 마이닝 모델에 대한 쿼리를 만드는 방법을 보여 주는 자세한 예의 링크를 제공합니다.  
  
 [예측 쿼리&#40;데이터 마이닝&#41;](prediction-queries-data-mining.md)  
  
 [내용 쿼리&#40;데이터 마이닝&#41;](content-queries-data-mining.md)  
  
 [드릴스루 쿼리&#40;데이터 마이닝&#41;](drillthrough-queries-data-mining.md)  
  
 [데이터 정의 쿼리&#40;데이터 마이닝&#41;](data-definition-queries-data-mining.md)  
  
 [데이터 마이닝 쿼리 인터페이스](data-mining-query-tools.md)  
  
## <a name="related-tasks"></a>관련 작업  
 다음 링크를 사용하여 데이터 마이닝 쿼리를 만들고 작업하는 방법을 알아봅니다.  
  
|작업|링크|  
|-----------|-----------|  
|자습서 및 연습 데이터 마이닝 쿼리 보기|[6단원: 예측 만들기 및 작업&#40;기본 데이터 마이닝 자습서&#41;](../../tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)<br /><br /> [시계열 예측 DMX 자습서](../../tutorials/time-series-prediction-dmx-tutorial.md)|  
|SQL Server Management Studio 및 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]|[SQL Server Management Studio에서 DMX 쿼리 만들기](create-a-dmx-query-in-sql-server-management-studio.md)<br /><br /> [예측 쿼리 작성기를 사용하여 예측 쿼리 만들기](create-a-prediction-query-using-the-prediction-query-builder.md)<br /><br /> [모델에 예측 함수 적용](apply-prediction-functions-to-a-model.md)<br /><br /> [예측 쿼리 수동 편집](manually-edit-a-prediction-query.md)|  
|예측 쿼리에 사용하는 외부 데이터 작업|[예측 쿼리에 대한 입력 데이터 선택 및 매핑](choose-and-map-input-data-for-a-prediction-query.md)<br /><br /> [예측 쿼리에 대한 입력 데이터 선택 및 매핑](choose-and-map-input-data-for-a-prediction-query.md)|  
|쿼리 결과 사용|[예측 쿼리 결과 보기 및 저장](view-and-save-the-results-of-a-prediction-query.md)|  
|Management Studio에서 제공하는 DMX 및 XMLA 쿼리 템플릿 사용|[템플릿에서 단일 예측 쿼리 작성](create-a-singleton-prediction-query-from-a-template.md)<br /><br /> [XMLA를 사용하여 데이터 마이닝 쿼리 만들기](create-a-data-mining-query-by-using-xmla.md)<br /><br /> [SQL Server Management Studio에서 Analysis Services 템플릿 사용](../instances/use-analysis-services-templates-in-sql-server-management-studio.md)|  
|내용 쿼리에 대한 자세한 정보 및 예제 참조|[마이닝 모델에 내용 쿼리 만들기](create-a-content-query-on-a-mining-model.md)<br /><br /> [마이닝 모델을 만드는 데 사용한 매개 변수 쿼리](query-the-parameters-used-to-create-a-mining-model.md)<br /><br /> [내용 쿼리&#40;데이터 마이닝&#41;](content-queries-data-mining.md)|  
|쿼리 옵션 설정과 쿼리 권한 및 문제 해결|[데이터 마이닝 쿼리에 대한 제한 시간 값 변경](data-mining-queries.md)|  
|Integration Services에서 데이터 마이닝 구성 요소 사용|[Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md)<br /><br /> [데이터 마이닝 쿼리 변환](../../integration-services/data-flow/transformations/data-mining-query-transformation.md)|  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 알고리즘 &#40;Analysis Services 데이터 마이닝&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](mining-model-content-analysis-services-data-mining.md)  
  
  
