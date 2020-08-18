---
description: DMX Select 문 이해
title: DMX Select 문 이해 | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 93744da59ad7149203da8fd14179045b63dc798f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88395219"
---
# <a name="understanding-the-dmx-select-statement"></a>DMX Select 문 이해
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  [SELECT](../dmx/select-dmx.md) 문은에서 DMX (데이터 마이닝 확장)를 사용 하 여 만드는 대부분의 쿼리에 대 한 기본입니다 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . 이 문을 사용하여 데이터 마이닝 모델을 검색하거나 예측하는 등의 여러 가지 태스크를 수행할 수 있습니다.  
  
 **SELECT** 문을 사용 하 여 완료할 수 있는 작업은 다음과 같습니다.  
  
-   데이터 마이닝 모델을 찾습니다. 스키마 행 집합은 모델 구조를 정의합니다.  
  
-   마이닝 모델 열의 가능한 값을 찾습니다.  
  
-   마이닝 모델에서 노드에 할당된 사례를 찾거나 대표 사례를 가져옵니다.  
  
-   다양한 입력을 사용하여 예측을 만듭니다.  
  
-   마이닝 모델을 복사합니다.  
  
 이러한 각 작업은 서로 다른 데이터 집합을 사용 하 여 *데이터 도메인*을 호출 합니다. 문의 **FROM** 절에서 데이터 도메인을 정의 합니다.  
  
-   데이터 집합을 정의하는 규칙 등 데이터 마이닝 모델 자체에서 개체 및 예측을 수행하는 데 사용되는 수식을 찾으려고 합니다.  
  
     해당 사례에서 모델 자체에 저장된 메타데이터를 확인해야 합니다. 따라서 데이터 도메인은 데이터 마이닝 스키마 행 집합의 열입니다.  
  
-   사례에서 모델을 만드는 데 사용되는 자세한 정보를 얻을 수 있습니다.  
  
     해당 사례에서 데이터 도메인인 마이닝 구조를 드릴스루하고 Gender, Bike Buyer 등 열의 각 행을 확인해야 합니다.  
  
 **중요:** 식 목록 또는 **WHERE** 절에 포함 된 모든 항목은 **from** 절에서 정의한 데이터 도메인에서 가져와야 합니다. 데이터 도메인을 혼합할 수 없습니다.  
  
##  <a name="select-types"></a><a name="Select_Types"></a> 유형 선택  
 **SELECT** 문의 구문은 다양 한 작업을 지원 합니다. 다음 패턴을 사용하여 이러한 태스크를 수행합니다.  
  
-   [예측](#Predicting)  
  
-   [검색](#Browsing)  
  
-   [복사](#Copying)  
  
-   [드릴스루](#Drillthrough)  
  
###  <a name="predicting"></a><a name="Predicting"></a> 예측  
 다음 쿼리 유형을 사용하여 마이닝 모델을 기반으로 예측을 수행할 수 있습니다.  
  
 예측 조인 **select** 문의 **FROM** 및 **WHERE** 절 내에서 찾아보기 또는 예측 **select** 문 중 하나를 포함할 수 있습니다.  
  
|쿼리 유형|설명|  
|----------------|-----------------|  
|SELECT FROM [자연] 예측 조인|마이닝 모델의 열을 내부 데이터 원본의 열에 조인하여 만든 예측을 반환합니다.<br /><br /> 이 쿼리 유형에 대한 도메인은 모델의 예측 가능한 열과 입력 데이터 원본의 열입니다.<br /><br /> [&#60;모델&#62; 예측 조인 &#40;DMX에서 선택&#41;](../dmx/select-from-model-prediction-join-dmx.md)<br /><br /> [예측 쿼리&#40;데이터 마이닝&#41;](https://docs.microsoft.com/analysis-services/data-mining/prediction-queries-data-mining)|  
|SELECT FROM *\<model>*|마이닝 모델만을 기준으로 예측 가능한 열에서 가능성이 가장 높은 상태를 반환합니다. 이 쿼리 유형을 사용하면 더 간단하게 빈 예측 조인을 사용하여 예측을 만들 수 있습니다.<br /><br /> 이 쿼리 유형의 도메인은 모델의 예측 가능한 열입니다.<br /><br /> [&#60;모델&#62; &#40;DMX에서 선택&#41;](../dmx/select-from-model-dmx.md)<br /><br /> [예측 쿼리&#40;데이터 마이닝&#41;](https://docs.microsoft.com/analysis-services/data-mining/prediction-queries-data-mining)|  
  
 [SELECT 유형으로 이동](#Select_Types)  
  
###  <a name="browsing"></a><a name="Browsing"></a> 보는  
 다음 쿼리 유형을 사용하여 마이닝 모델의 내용을 찾을 수 있습니다.  
  
|쿼리 유형|설명|  
|----------------|-----------------|  
|다음에서 고유 선택 *\<model>*|지정한 열의 마이닝 모델에 있는 모든 상태 값을 반환합니다.<br /><br /> 이 쿼리 유형의 데이터 도메인은 데이터 마이닝 모델입니다.<br /><br /> [&#60;모델 &#62; &#40;DMX&#41;에서 고유를 선택 합니다. ](../dmx/select-distinct-from-model-dmx.md)<br /><br /> [내용 쿼리&#40;데이터 마이닝&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-queries-data-mining)|  
|선택에서 선택 *\<model>* 합니다. 콘텐트가|마이닝 모델을 설명하는 내용을 반환합니다.<br /><br /> 이 쿼리 유형의 데이터 도메인은 내용 스키마 행 집합입니다.<br /><br /> [&#60;모델&#62;에서 선택 합니다. 콘텐츠 &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)<br /><br /> [내용 쿼리&#40;데이터 마이닝&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-queries-data-mining)|  
|선택에서 선택 *\<model>* 합니다. DIMENSION_CONTENT|마이닝 모델을 설명하는 내용을 반환합니다.<br /><br /> 이 쿼리 유형의 데이터 도메인은 내용 스키마 행 집합입니다.<br /><br /> [&#60;모델&#62;에서 선택 합니다. DMX&#41;DIMENSION_CONTENT &#40;](../dmx/select-from-model-dimension-content-dmx.md)|  
|선택에서 선택 *\<model>* 합니다. PMML|이 기능을 지원하는 알고리즘에 대한 마이닝 모델의 PMML(Predictive Model Markup Language) 표현을 반환합니다.<br /><br /> 이 쿼리 유형의 도메인은 PMML 스키마 행 집합입니다.<br /><br /> [DMSCHEMA_MINING_MODEL_CONTENT_PMML 행 집합](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/ms126283(v=sql.110))|  
  
 [SELECT 유형으로 이동](#Select_Types)  
  
###  <a name="copying"></a><a name="Copying"></a> 복사  
 새 모델에 마이닝 모델 및 연결된 마이닝 구조를 복사한 다음 문 내에서 모델 이름을 변경할 수 있습니다.  
  
|쿼리 유형|설명|  
|----------------|-----------------|  
|SELECT INTO *\<new model>*|마이닝 모델의 복사본을 만듭니다.<br /><br /> 이 쿼리 유형의 도메인은 데이터 마이닝 모델입니다.<br /><br /> [&#40;DMX&#41;를 선택 합니다. ](../dmx/select-into-dmx.md)|  
  
 [SELECT 유형으로 이동](#Select_Types)  
  
###  <a name="drillthrough"></a><a name="Drillthrough"></a> 드릴스루  
 다음 쿼리 유형을 사용하여 모델 학습에 사용된 사례 또는 사례의 표현을 찾을 수 있습니다.  
  
|쿼리 유형|설명|  
|----------------|-----------------|  
|선택에서 선택 *\<model>* 합니다. 경우|마이닝 모델의 학습에 사용된 사례를 반환합니다.<br /><br /> 이 쿼리 유형의 도메인은 데이터 마이닝 모델입니다.<br /><br /> [&#60;모델&#62;에서 선택 합니다. 사례 &#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md)<br /><br /> [DMX를 사용하여 드릴스루 쿼리 만들기](https://docs.microsoft.com/analysis-services/data-mining/create-drillthrough-queries-using-dmx)|  
|선택에서 선택 *\<model>* 합니다. SAMPLE_CASES|마이닝 모델 학습에 사용된 대표 사례인 샘플 사례를 반환합니다.<br /><br /> 이 쿼리 유형의 도메인은 데이터 마이닝 모델입니다.<br /><br /> [&#60;모델&#62;에서 선택 합니다. DMX&#41;SAMPLE_CASES &#40;](../dmx/select-from-model-sample-cases-dmx.md)|  
|선택에서 선택 *\<structure>* 합니다. 경우|일부 상세 정보가 마이닝 모델 학습에 사용되지 않은 경우에도 기본 마이닝 구조에서 자세한 데이터 행을 반환합니다.<br /><br /> [&#60;구조&#62;에서 선택 합니다. 경우](../dmx/select-from-structure-cases.md)<br /><br /> [드릴스루 쿼리&#40;데이터 마이닝&#41;](https://docs.microsoft.com/analysis-services/data-mining/drillthrough-queries-data-mining)|  
  
 [SELECT 유형으로 이동](#Select_Types)  
  
## <a name="see-also"></a>참고 항목  
 [DMX&#41; 참조 &#40;데이터 마이닝 확장](../dmx/data-mining-extensions-dmx-reference.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 구문 규칙](../dmx/data-mining-extensions-dmx-syntax-conventions.md)  
  
  
