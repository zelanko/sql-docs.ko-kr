---
title: Select 문 이해 DMX | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- browsing mining model [Analysis Services]
- Data Mining Extensions [Analysis Services], statements
- DMX [Analysis Services], statements
- predictions [DMX]
- queries [DMX], Select statement
- SELECT statement [DMX]
- statements [DMX], SELECT statement
- copying mining models
ms.assetid: 61e97285-4a06-4434-9a40-38cde5af7c3f
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 063b94b4229221c998c42691a1c8832ac42be819
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="understanding-the-dmx-select-statement"></a>DMX Select 문 이해
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  [선택](../dmx/select-dmx.md) 문에와 확장 DMX (Data Mining)에서 만드는 대부분의 쿼리에서 기반 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]합니다. 이 문을 사용하여 데이터 마이닝 모델을 검색하거나 예측하는 등의 여러 가지 태스크를 수행할 수 있습니다.  
  
 사용 하 여 완료할 수 있는 작업은 다음과 같습니다는 **선택** 문:  
  
-   데이터 마이닝 모델을 찾습니다. 스키마 행 집합은 모델 구조를 정의합니다.  
  
-   마이닝 모델 열의 가능한 값을 찾습니다.  
  
-   마이닝 모델에서 노드에 할당된 사례를 찾거나 대표 사례를 가져옵니다.  
  
-   다양한 입력을 사용하여 예측을 만듭니다.  
  
-   마이닝 모델을 복사합니다.  
  
 호출할 데이터 집합이 다른을 사용 하 여 각이 태스크는 *데이터 도메인*합니다. 데이터 도메인을 정의 하는 **FROM** 문의 절.  
  
-   데이터 집합을 정의하는 규칙 등 데이터 마이닝 모델 자체에서 개체 및 예측을 수행하는 데 사용되는 수식을 찾으려고 합니다.  
  
     해당 사례에서 모델 자체에 저장된 메타데이터를 확인해야 합니다. 따라서 데이터 도메인은 데이터 마이닝 스키마 행 집합의 열입니다.  
  
-   사례에서 모델을 만드는 데 사용되는 자세한 정보를 얻을 수 있습니다.  
  
     해당 사례에서 데이터 도메인인 마이닝 구조를 드릴스루하고 Gender, Bike Buyer 등 열의 각 행을 확인해야 합니다.  
  
 **중요:** 또는 식 목록에 포함 되는 모든 항목은 **여기서** 절에서 정의한 데이터 도메인에서 가져와야 합니다.는 **FROM** 절. 데이터 도메인을 혼합할 수 없습니다.  
  
##  <a name="Select_Types"></a>유형 선택  
 구문의 **선택** 문은 여러 다양 한 작업을 지원 합니다. 다음 패턴을 사용하여 이러한 태스크를 수행합니다.  
  
-   [예측](#Predicting)  
  
-   [검색](#Browsing)  
  
-   [복사](#Copying)  
  
-   [드릴스루](#Drillthrough)  
  
###  <a name="Predicting"></a>예측  
 다음 쿼리 유형을 사용하여 마이닝 모델을 기반으로 예측을 수행할 수 있습니다.  
  
 찾기 또는 예측 중 하나를 포함할 수 있습니다 **선택** 내에 있는 문이 **FROM** 및 **여기서** 예측 조인 절 **선택** 문.  
  
|쿼리 유형|Description|  
|----------------|-----------------|  
|SELECT FROM [NATURAL] PREDICTION JOIN|마이닝 모델의 열을 내부 데이터 원본의 열에 조인하여 만든 예측을 반환합니다.<br /><br /> 이 쿼리 유형에 대한 도메인은 모델의 예측 가능한 열과 입력 데이터 원본의 열입니다.<br /><br /> [SELECT FROM &#60; 모델 &#62; 예측 조인 &#40; DMX &#41;](../dmx/select-from-model-prediction-join-dmx.md)<br /><br /> [예측 쿼리 &#40; 데이터 마이닝 &#41;](../analysis-services/data-mining/prediction-queries-data-mining.md)|  
|SELECT FROM  *\<모델 >*|마이닝 모델만을 기준으로 예측 가능한 열에서 가능성이 가장 높은 상태를 반환합니다. 이 쿼리 유형을 사용하면 더 간단하게 빈 예측 조인을 사용하여 예측을 만들 수 있습니다.<br /><br /> 이 쿼리 유형의 도메인은 모델의 예측 가능한 열입니다.<br /><br /> [SELECT FROM &#60; 모델 &#62; &#40; DMX &#41;](../dmx/select-from-model-dmx.md)<br /><br /> [예측 쿼리 &#40; 데이터 마이닝 &#41;](../analysis-services/data-mining/prediction-queries-data-mining.md)|  
  
 [Select 유형으로 이동](#Select_Types)  
  
###  <a name="Browsing"></a>검색  
 다음 쿼리 유형을 사용하여 마이닝 모델의 내용을 찾을 수 있습니다.  
  
|쿼리 유형|Description|  
|----------------|-----------------|  
|SELECT DISTINCT FROM  *\<모델 >*|지정한 열의 마이닝 모델에 있는 모든 상태 값을 반환합니다.<br /><br /> 이 쿼리 유형의 데이터 도메인은 데이터 마이닝 모델입니다.<br /><br /> [SELECT DISTINCT FROM &#60; 모델 &#62; &#40; DMX &#41;](../dmx/select-distinct-from-model-dmx.md)<br /><br /> [콘텐츠 쿼리 &#40; 데이터 마이닝 &#41;](../analysis-services/data-mining/content-queries-data-mining.md)|  
|SELECT FROM  *\<모델 >*합니다. 콘텐츠|마이닝 모델을 설명하는 내용을 반환합니다.<br /><br /> 이 쿼리 유형의 데이터 도메인은 내용 스키마 행 집합입니다.<br /><br /> [SELECT FROM &#60; 모델 &#62;. 콘텐츠 &#40; DMX &#41;](../dmx/select-from-model-content-dmx.md)<br /><br /> [콘텐츠 쿼리 &#40; 데이터 마이닝 &#41;](../analysis-services/data-mining/content-queries-data-mining.md)|  
|SELECT FROM  *\<모델 >*합니다. DIMENSION_CONTENT|마이닝 모델을 설명하는 내용을 반환합니다.<br /><br /> 이 쿼리 유형의 데이터 도메인은 내용 스키마 행 집합입니다.<br /><br /> [SELECT FROM &#60; 모델 &#62;. DIMENSION_CONTENT &#40; DMX &#41;](../dmx/select-from-model-dimension-content-dmx.md)|  
|SELECT FROM  *\<모델 >*합니다. PMML|이 기능을 지원하는 알고리즘에 대한 마이닝 모델의 PMML(Predictive Model Markup Language) 표현을 반환합니다.<br /><br /> 이 쿼리 유형의 도메인은 PMML 스키마 행 집합입니다.<br /><br /> [DMSCHEMA_MINING_MODEL_CONTENT_PMML 행 집합](../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-pmml-rowset.md)|  
  
 [Select 유형으로 이동](#Select_Types)  
  
###  <a name="Copying"></a>복사  
 새 모델에 마이닝 모델 및 연결된 마이닝 구조를 복사한 다음 문 내에서 모델 이름을 변경할 수 있습니다.  
  
|쿼리 유형|Description|  
|----------------|-----------------|  
|SELECT INTO  *\<새 모델 >*|마이닝 모델의 복사본을 만듭니다.<br /><br /> 이 쿼리 유형의 도메인은 데이터 마이닝 모델입니다.<br /><br /> [SELECT INTO &#40; DMX &#41;](../dmx/select-into-dmx.md)|  
  
 [Select 유형으로 이동](#Select_Types)  
  
###  <a name="Drillthrough"></a>드릴스루  
 다음 쿼리 유형을 사용하여 모델 학습에 사용된 사례 또는 사례의 표현을 찾을 수 있습니다.  
  
|쿼리 유형|Description|  
|----------------|-----------------|  
|SELECT FROM  *\<모델 >*합니다. 경우|마이닝 모델의 학습에 사용된 사례를 반환합니다.<br /><br /> 이 쿼리 유형의 도메인은 데이터 마이닝 모델입니다.<br /><br /> [SELECT FROM &#60; 모델 &#62;. 경우 &#40; DMX &#41;](../dmx/select-from-model-cases-dmx.md)<br /><br /> [DMX를 사용하여 드릴스루 쿼리 만들기](../analysis-services/data-mining/create-drillthrough-queries-using-dmx.md)|  
|SELECT FROM  *\<모델 >*합니다. SAMPLE_CASES|마이닝 모델 학습에 사용된 대표 사례인 샘플 사례를 반환합니다.<br /><br /> 이 쿼리 유형의 도메인은 데이터 마이닝 모델입니다.<br /><br /> [SELECT FROM &#60; 모델 &#62;. SAMPLE_CASES &#40; DMX &#41;](../dmx/select-from-model-sample-cases-dmx.md)|  
|SELECT FROM  *\<구조 >*합니다. 경우|일부 상세 정보가 마이닝 모델 학습에 사용되지 않은 경우에도 기본 마이닝 구조에서 자세한 데이터 행을 반환합니다.<br /><br /> [SELECT FROM &#60; 구조 &#62;. 경우](../dmx/select-from-structure-cases.md)<br /><br /> [드릴스루 쿼리 &#40; 데이터 마이닝 &#41;](../analysis-services/data-mining/drillthrough-queries-data-mining.md)|  
  
 [Select 유형으로 이동](#Select_Types)  
  
## <a name="see-also"></a>관련 항목:  
 [Data Mining Extensions &#40; DMX &#41; 참조](../dmx/data-mining-extensions-dmx-reference.md)   
 [Data Mining Extensions &#40; DMX &#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [Data Mining Extensions &#40; DMX &#41; 구문 표기 규칙](../dmx/data-mining-extensions-dmx-syntax-conventions.md)  
  
  
