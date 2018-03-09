---
title: "예측 쿼리 (데이터 마이닝) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e5e6686c-1360-480e-8c0d-8a56204fbed9
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 89a8d2a3edf4cf3d875f582918d714c2e6dc72e5
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
---
# <a name="prediction-queries-data-mining"></a>예측 쿼리(데이터 마이닝)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
일반적인 데이터 마이닝 프로젝트의 목표는 마이닝 모델을 사용하여 예측을 수행하는 것입니다. 예를 들어 서버의 특정 클러스터에 대해 예상 작동 중단 시간의 양을 예측하거나, 고객의 세그먼트가 광고 캠페인에 응답할 가능성이 있는지 여부를 표시하는 점수를 생성할 수 있습니다. 이러한 작업을 모두 수행하기 위해 예측 쿼리를 만들 수 있습니다.  
  
 기능적으로 쿼리에 대한 입력의 유형에 따라 SQL Server에서 다른 유형의 예측 쿼리가 지원됩니다.  
  
|쿼리 유형|쿼리 옵션|  
|----------------|-------------------|  
|단일 예측 쿼리|새로운 단일 사례 또는 복수 사례에 대한 결과를 예측하려는 경우 단일 쿼리를 사용합니다. 쿼리에서 입력 값을 직접 제공하며 쿼리는 단일 세션으로 실행됩니다.|  
|일괄 처리 예측|예측의 기반으로 사용하기 위해 모델로 피드하려는 외부 데이터가 있는 경우 일괄 처리 예측을 사용합니다. 전체 데이터 집합에 대한 예측을 만들려면 외부 원본의 데이터를 모델의 열에 매핑한 다음 출력할 예측 데이터의 유형을 지정합니다.<br /><br /> 전체 데이터 집합에 대한 쿼리가 단일 세션에서 실행되므로 이 옵션은 반복되는 쿼리를 여러 개 보내는 것보다 훨씬 효율적입니다.|  
|시계열 예측|몇 가지 이후 단계에 대한 값을 예측하려는 경우 시계열 쿼리를 사용합니다. SQL Server 데이터 마이닝은 시계열 쿼리에서 다음 기능도 제공합니다.<br /><br /> 쿼리의 일부로 새 데이터를 추가하여 기존 모델을 확장하고 복합 계열을 기반으로 예측을 만들 수 있습니다.<br /><br /> REPLACE_MODEL_CASES 옵션을 사용하여 새 데이터 계열에 기존 모델을 적용할 수 있습니다.<br /><br /> 교차 예측을 수행할 수 있습니다.|  
  
 다음 섹션에서는 예측 쿼리의 일반 구문, 예측 쿼리의 다양한 유형 및 예측 쿼리의 결과로 작업하는 방법에 대해 설명합니다.  
  
 [기본 예측 쿼리 디자인](#bkmk_PredQuery)  
  
-   [예측 함수 추가](#bkmk_PredFunc)  
  
-   [단일 쿼리](#bkmk_SingletonQuery)  
  
-   [일괄 처리 예측 쿼리](#bkmk_BatchQuery)  
  
-   [시계열 쿼리](#bkmk_TSQuery)  
  
 [쿼리 결과 작업](#bkmk_WorkResults)  
  
##  <a name="bkmk_PredQuery"></a> 기본 예측 쿼리 디자인  
 예측을 만들 때 사용자는 일반적으로 몇 가지 새로운 데이터를 제공한 다음 이 새로운 데이터를 기반으로 모델이 예측을 생성하도록 요청합니다.  
  
-   일괄 처리 예측 쿼리에서는 *예측 조인*을 사용하여 모델을 외부 데이터 원본에 매핑합니다.  
  
-   단일 예측 쿼리에서는 입력으로 사용할 값을 하나 이상 입력합니다. 단일 예측 쿼리를 사용하여 여러 예측을 만들 수 있습니다. 그러나 많은 예측을 만들어야 하는 경우 일괄 처리 쿼리를 사용하면 성능이 향상됩니다.  
  
 단일 및 일괄 처리 예측 쿼리는 모두 PREDICTION JOIN 구문을 사용하여 새 데이터를 정의합니다. 차이점은 예측 조인의 입력 쪽을 지정하는 방법에 있습니다.  
  
-   일괄 처리 예측 쿼리에서 데이터는 OPENQUERY 구문을 사용하여 지정한 외부 데이터 원본에서 가져옵니다.  
  
-   단일 예측 쿼리에서 데이터는 쿼리에 포함되어 인라인으로 제공됩니다.  
  
 시계열 모델의 경우 입력 데이터가 필요하지 않은 경우도 있습니다. 모델에 이미 있는 데이터만 사용하여 예측을 만들 수 있습니다. 하지만 새 입력 데이터를 지정하는 경우에는 새 데이터를 사용하여 모델을 업데이트하고 확장할지 아니면 모델에서 사용된 데이터의 원래 계열을 바꿀지를 결정해야 합니다.  이러한 옵션에 대한 자세한 내용은 [Time Series Model Query Examples](../../analysis-services/data-mining/time-series-model-query-examples.md)를 참조하세요.  
  
###  <a name="bkmk_PredFunc"></a> 예측 함수 추가  
 값을 예측하는 것 외에도 예측 쿼리를 사용자 지정하여 예측과 관련된 여러 종류의 정보를 반환할 수 있습니다. 예를 들어 예측에 따라 고객에게 권장할 제품 목록을 만드는 경우 예측을 평가하여 최상위 권장 사항만 사용자에게 제공할 수 있도록 각 예측에 대한 확률을 반환할 수 있습니다.  
  
 이렇게 하려면 쿼리에 *예측 함수* 를 추가합니다. 지원되는 함수는 모델 또는 쿼리 유형마다 다릅니다. 예를 들어 클러스터링 모델은 모델에서 만들어진 클러스터에 대한 추가 세부 정보를 제공하는 특수한 예측 함수를 지원하지만 시계열 모델에는 시간 경과에 따른 차이를 계산하는 함수가 있습니다. 또한 모든 모델 유형에서 작동하는 일반 예측 함수도 있습니다. 다양한 유형의 쿼리에서 지원되는 예측 함수 목록은 DMX 참조 항목 [일반 예측 함수&#40;DMX&#41;](../../dmx/general-prediction-functions-dmx.md)를 참조하세요.  
  
###  <a name="bkmk_SingletonQuery"></a> 단일 예측 쿼리 만들기  
 단일 예측 쿼리는 빠른 예측을 실시간으로 만들려는 경우에 유용합니다. 일반적인 시나리오는 웹 사이트에서 폼을 사용하는 등의 방법으로 고객으로부터 정보를 얻은 다음 해당 데이터를 단일 예측 쿼리에 입력으로 전송하려는 경우입니다. 예를 들어 고객이 목록에서 제품을 선택하는 경우 추천할 최고의 제품을 예측하는 쿼리에 대한 입력으로 해당 선택을 사용할 수 있습니다.  
  
 단일 예측 쿼리에는 입력을 포함하는 별도의 테이블이 필요하지 않습니다. 대신 하나 또는 여러 행의 값을 모델에 입력으로 제공하면 예측이 실시간으로 반환됩니다.  
  
> [!WARNING]  
>  이름이 의미하는 것과 달리 단일 예측 쿼리는 단일 예측만 만들지는 않으며 각 입력 집합에 대해 여러 예측을 생성할 수 있습니다. 각 입력 사례에 대해 SELECT 문을 만들고 UNION 연산자로 입력 사례를 결합하여 여러 입력 사례를 제공합니다.  
  
 단일 예측 쿼리를 만들 때 PREDICTION JOIN의 형태로 모델에 새 데이터를 제공해야 합니다. 즉, 실제 테이블에 매핑하는 것은 아니지만 새 데이터가 마이닝 모델의 기존 열과 일치하도록 해야 합니다. 새 데이터 열과 새 데이터가 정확하게 일치할 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 자동으로 열을 매핑하는데 이를 *NATURAL PREDICTION JOIN*이라고 합니다. 하지만 열이 일치하지 않거나 모델에 있는 것과 동일한 종류 및 양의 데이터가 새 데이터에 들어 있지 않은 경우 모델의 어떤 열이 새 데이터에 매핑되는지 지정하거나 누락된 값을 지정해야 합니다.  
  
###  <a name="bkmk_BatchQuery"></a> 일괄 처리 예측 쿼리  
 예측을 만드는 데 사용하려는 외부 데이터가 있는 경우 일괄 처리 예측 쿼리가 유용합니다. 예를 들어 온라인 활동과 구매 기록을 기준으로 고객을 범주화하는 모델을 작성했을 수 있습니다. 이 모델을 새로 얻은 잠재 고객의 목록에 적용하여 매출 예상치를 구하거나 제안된 캠페인의 대상을 식별할 수 있습니다.  
  
 예측 조인을 수행하는 경우 모델의 열을 새 데이터 원본의 열에 매핑해야 합니다. 따라서 입력을 위해 선택하는 데이터 원본은 모델의 데이터와 어느 정도 비슷한 데이터여야 합니다. 새 정보는 정확히 일치할 필요가 없으며 불완전할 수 있습니다. 예를 들어 수입 및 연령에 대한 정보를 사용하여 모델을 학습했지만 예측에 사용할 고객 목록에 수입에 대한 정보는 전혀 없고 연령 정보만 있다고 가정합니다. 이 경우 새 데이터를 모델에 매핑하고 각 고객에 대한 예측을 만들 수 있습니다. 그러나 수입은 모델을 예측하는 데 중요한 요소이므로 완전한 정보가 없음으로 인해 예측 품질이 떨어집니다.  
  
 최상의 결과를 얻기 위해서는 새 데이터와 모델 간에 일치하는 열을 가능한 많이 조인해야 합니다. 그러나 일치하는 열이 없더라도 쿼리는 성공합니다. 즉, 조인된 열이 없는 경우 쿼리가 한계 예측을 반환하는데 이는 PREDICTION JOIN 절이 없는 `SELECT <predictable-column> FROM <model>` 문과 같습니다.  
  
 모든 관련 열을 성공적으로 매핑한 후 쿼리를 실행하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 모델의 패턴을 기반으로 새 데이터의 각 행에 대해 예측을 만듭니다. 외부 데이터가 포함된 데이터 원본 뷰의 새 테이블에 결과를 저장하거나, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하는 경우 데이터를 복사하여 붙여넣을 수 있습니다.  
  
> [!WARNING]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 디자이너를 사용하는 경우 먼저 외부 데이터 원본을 데이터 원본 뷰로 정의해야 합니다.  
  
 DMX를 사용하여 예측 조인을 만드는 경우 OPENQUERY, OPENROWSET 또는 SHAPE 명령을 사용하여 외부 데이터 원본을 지정할 수 있습니다. DMX 템플릿의 기본 데이터 액세스 메서드는 OPENQUERY입니다. 이러한 메서드에 대한 자세한 내용은 [&#60;원본 데이터 쿼리&#62;](../../dmx/source-data-query.md)를 참조하세요.  
  
###  <a name="bkmk_TSQuery"></a> 시계열 마이닝 모델의 예측  
 시계열 모델은 다른 모델 유형과 다릅니다. 모델을 있는 그대로 사용하여 예측을 만들 수도 있고, 모델에 새 데이터를 제공하여 최신 추세를 기반으로 모델을 업데이트하고 예측을 만들 수도 있습니다. 새 데이터를 추가하는 경우 새 데이터를 사용할 방법을 지정할 수 있습니다.  
  
-   *모델 사례 확장* 은 시계열 모델의 기존 데이터 계열에 새 데이터를 추가하는 것을 의미합니다. 이후에는 예측이 결합된 새 계열을 기반으로 합니다. 이 옵션은 몇 가지 데이터 요소를 기존 모델에 추가하려는 경우에 유용합니다.  
  
     예를 들어 전년도 판매 데이터에 대해 학습된 기존 시계열 모델이 있다고 가정합니다. 수개월 동안 새로운 판매 데이터를 수집한 후 현재 연도에 대한 예측 판매량을 업데이트하려고 합니다. 이 경우 새 데이터를 추가하여 모델을 업데이트하고 새로운 예측을 만들도록 모델을 확장하는 예측 조인을 만들 수 있습니다.  
  
-   *모델 사례 대체* 는 학습된 모델은 그대로 유지하지만 기본 사례를 새로운 사례 데이터 집합으로 대체하는 것을 의미합니다. 이 옵션은 추세를 모델에 유지하지만 다른 데이터 집합에 적용하려는 경우에 유용합니다.  
  
     예를 들어 원래 모델이 판매량이 매우 많은 데이터 집합에 대해 학습되었을 수도 있습니다. 기본 데이터를 새 계열(판매량이 적은 상점 등에서 제공됨)로 대체할 때 추세를 유지하지만 예측은 대체 계열의 값에서 시작됩니다.  
  
 사용하는 방법에 관계없이 예측은 항상 원래 계열의 끝에서 시작됩니다.  
  
 시계열 모델에 대한 예측 조인을 만드는 방법은 [시계열 모델 쿼리 예제](../../analysis-services/data-mining/time-series-model-query-examples.md) 또는 [PredictTimeSeries&#40;DMX&#41;](../../dmx/predicttimeseries-dmx.md)를 참조하세요.  
  
##  <a name="bkmk_WorkResults"></a> 예측 쿼리 결과 처리  
 데이터 마이닝 예측 쿼리의 결과를 저장하기 위한 옵션은 쿼리를 만드는 방법에 따라 달라집니다.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 예측 쿼리 작성기를 사용하여 쿼리를 작성할 경우 예측 쿼리의 결과를 기존 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 원본에 저장할 수 있습니다. 자세한 내용은 [예측 쿼리 결과 보기 및 저장](../../analysis-services/data-mining/view-and-save-the-results-of-a-prediction-query.md)을 참조하세요.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 쿼리 창에서 DMX를 사용하여 예측 쿼리를 만드는 경우 쿼리 출력 옵션을 사용하여 결과를 파일로 저장하거나 쿼리 결과 창에 텍스트 또는 표로 저장할 수 있습니다. 자세한 내용은 [쿼리 및 텍스트 편집기&#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)를 참조하세요.  
  
-   Integration Services 구성 요소를 사용하여 예측 쿼리를 실행하는 경우 해당 태스크에서 사용 가능한 ADO.NET 연결 관리자나 OLEDB 연결 관리자를 사용하여 데이터베이스에 결과를 쓸 수 있습니다. 자세한 내용은 [Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md)을 참조하세요.  
  
 예측 쿼리의 결과는 항상 관련 값의 단일 행을 반환하는 관계형 데이터베이스에 대한 쿼리 결과와는 다릅니다. 쿼리에 추가된 각 DMX 예측 함수는 고유한 행 집합을 반환합니다. 그러므로 단일 사례에 대한 예측을 만들면 그 결과는 추가 세부 정보를 포함하는 중첩 테이블의 여러 열이 함께 표시되는 예측 값일 수 있습니다.  
  
 여러 개의 함수를 한 개의 쿼리에 결합하면 반환 결과는 계층적 행 집합으로 결합됩니다. 예를 들어 시계열 모델을 사용하여 다음 DMX 문과 같은 쿼리를 통해 판매액 및 판매 수량에 대한 미래 값을 예측한다고 가정합니다.  
  
```  
SELECT  
  PredictTimeSeries([Forecasting].[Amount]) as [PredictedAmount]  
, PredictTimeSeries([Forecasting].[Quantity]) as [PredictedQty]  
FROM  
  [Forecasting]  
  
```  
  
 이 쿼리의 결과는 각 예측 시계열에 대한 두 개의 열이며 열의 각 행에는 예측 값이 있는 중첩 테이블이 포함됩니다.  
  
 **PredictedAmount**  
  
|$TIME|Amount|  
|-----------|------------|  
|201101|172067.11|  
  
|$TIME|Amount|  
|-----------|------------|  
|201102|363390.68|  
  
 **PredictedQty**  
  
|$TIME|수량|  
|-----------|--------------|  
|201101|77|  
  
|$TIME|수량|  
|-----------|--------------|  
|201102|260|  
  
 공급자가 계층적 행 집합을 처리할 수 없는 경우 예측 쿼리에 FLATTEN 키워드를 사용하여 결과를 평면화할 수 있습니다. 일반 행 집합의 예를 비롯한 자세한 내용은 [SELECT&#40;DMX&#41;](../../dmx/select-dmx.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [콘텐츠 쿼리 &#40; 데이터 마이닝 &#41;](../../analysis-services/data-mining/content-queries-data-mining.md)   
 [데이터 정의 쿼리 &#40; 데이터 마이닝 &#41;](../../analysis-services/data-mining/data-definition-queries-data-mining.md)  
  
  
