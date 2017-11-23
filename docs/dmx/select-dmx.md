---
title: SELECT (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: SELECT
dev_langs: DMX
helpviewer_keywords:
- browsing mining model [Analysis Services]
- TOP clause, SELECT
- FLATTENED option
- predictions [DMX]
- ORDER BY clause [DMX]
- SELECT statement [DMX]
- mining models [Analysis Services], browsing
- statements [DMX], SELECT statement
- WHERE clause, DMX
ms.assetid: 32d9e8fd-796b-4e1c-ae59-73cd6f645485
caps.latest.revision: "43"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 79fb3f8ce7766130ced9a8353a83e34bbbf007d1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="select-dmx"></a>SELECT(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  **선택** 문은에 확장 DMX (Data Mining) 데이터 마이닝에는 다음 작업에 사용 됩니다.  
  
-   기존 마이닝 모델의 내용 탐색  
  
-   기존 마이닝 모델을 사용하여 예측 만들기  
  
-   기존 마이닝 모델의 복사본 만들기  
  
-   마이닝 구조 탐색  
  
 이 문의 전체 구문은 복잡하지만 모델과 해당 기본 구조를 찾는 데 사용되는 기본 절을 요약하면 다음과 같습니다.  
  
```  
SELECT [FLATTENED] [TOP <n>] <select list>  
FROM <model/structure>[.aspect]  
[WHERE <condition expression>]  
[ORDER BY <expression>[DESC|ASC]]  
```  
  
## <a name="flattened"></a>FLATTENED  
 일부 데이터 마이닝 클라이언트에서는 데이터 마이닝 공급자로부터 계층 구조 형식의 결과 집합을 받을 수 없습니다. 해당 클라이언트에서 계층 구조를 처리할 수 없는 경우도 있고 결과를 정규화되지 않은 단일 테이블에 저장해야 하는 경우도 있습니다. 중첩 테이블에서 일반 테이블로 데이터를 변환하려면 쿼리 결과가 일반 형식으로 나오도록 요청해야 합니다.  
  
 사용 하 여 쿼리 결과 평면화 하는 **선택** 구문에는 **FLATTENED** 다음 예제에 표시 된 대로 옵션:  
  
```  
SELECT FLATTENED <select list> FROM ...  
```  
  
## <a name="top-n-and-order-by"></a>TOP \<n > 및 ORDER BY  
 식을 사용 하 여 쿼리 결과 정렬할 수 및의 조합을 사용 하 여 결과의 하위 집합을 반환한 다음 수는 **ORDER BY** 및 **TOP** 절. 이 함수는 응답할 가능성이 높은 사람에게만 결과를 보내도록 메일 대상을 지정하는 시나리오 등에서 유용합니다. 예측 확률에 따라 예측 쿼리를 발송 대상의 결과 정렬 하 고 다음 반환할 상위 수 \<n > 결과입니다.  
  
## <a name="select-list"></a>select list  
 *\<select 목록 >* 스칼라 열 참조, 예측 함수 및 식을 포함할 수 있습니다. 사용 가능한 옵션은 알고리즘과 다음 컨텍스트에 따라 달라집니다.  
  
-   마이닝 구조를 쿼리하는지 아니면 마이닝 모델을 쿼리하는지 여부  
  
-   내용을 쿼리하는지 아니면 사례를 쿼리하는지 여부  
  
-   원본 데이터가 관계형 테이블인지 아니면 큐브인지 여부  
  
-   예측을 만드는 경우  
  
 대부분의 경우 별칭을 사용하거나 select list의 항목을 기반으로 단순 식을 만들 수 있습니다. 예를 들어 다음 예에서는 모델 열의 단순 식을 보여 줍니다.  
  
```  
SELECT [CustomerID], [Last Name] + ', ' + [FirstName] AS FullName  
FROM <model>.CASES  
```  
  
 다음 예에서는 예측 함수의 결과가 들어 있는 열의 별칭을 만듭니다.  
  
```  
SELECT Predict([Column1], 'Value') as Column1Prediction  
FROM MyModel  
JOIN <source data query>  
```  
  
## <a name="where"></a>WHERE  
 사용 하 여 쿼리에 의해 반환 되는 사례를 제한할 수 있습니다는 **여기서** 절. **여기서** 절 지정 해당 열에서 참조는 **여기서** 식에는 열 참조와 동일한 의미 체계를 사용 해야 합니다.는  *\<select 목록 >* 의 **선택** 문과 반환할 수 있습니다는 부울 식입니다. 에 대 한 구문에서 **여기서** 절은 다음과 같습니다  
  
```  
WHERE < condition expression >  
```  
  
 Select 목록 및 **여기서** 절은 **선택** 문은 다음 규칙을 따라야 합니다.  
  
-   select list에는 부울 결과를 반환하지 않는 식이 포함되어야 합니다. 식을 수정할 수는 있지만 이 식은 부울이 아닌 결과를 반환해야 합니다.  
  
-   **여기서** 절 부울 결과 반환 하는 식을 포함 해야 합니다. 절을 수정할 수는 있지만 이 절은 부울 결과를 반환해야 합니다.  
  
## <a name="predictions"></a>예측  
 예측을 만들 때 사용할 수 있는 구문에는 두 가지 유형이 있습니다.  
  
-   [SELECT FROM &#60; 모델 &#62; 예측 조인 &#40; DMX &#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
-   [SELECT FROM &#60; 모델 &#62; &#40; DMX &#41;](../dmx/select-from-model-dmx.md)  
  
 첫 번째 예측 유형을 사용하면 실시간 또는 일괄 처리로 복잡한 예측을 만들 수 있습니다.  
  
 두 번째 예측 유형은 마이닝 모델에서 예측 가능한 열에 빈 예측 조인을 만들고 가장 가능성이 높은 열 상태를 반환합니다. 이 쿼리 결과는 전적으로 마이닝 모델의 내용을 기준으로 합니다.  
  
 다음 구문을 사용 하 여 선택 FROM PREDICTION JOIN 문의 원본 쿼리에 select 문을 삽입할 수 있습니다.  
  
```  
SELECT FROM PREDICTION JOIN (<SELECT statement>) AS t, WHERE <SELECT statement>  
```  
  
 예측 쿼리를 만드는 방법에 대 한 자세한 내용은 참조 [구조와 DMX 예측 쿼리 사용](../dmx/structure-and-usage-of-dmx-prediction-queries.md)합니다.  
  
## <a name="clause-syntax"></a>절 구문  
 찾는 복잡성으로 인해는 **선택** 문, 자세한 구문 요소 및 인수는 절로 설명 됩니다. 각 절에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
 [SELECT DISTINCT FROM &#60; 모델 &#62; &#40; DMX &#41;](../dmx/select-distinct-from-model-dmx.md)  
  
 [SELECT FROM &#60; 모델 &#62;. 콘텐츠 &#40; DMX &#41;](../dmx/select-from-model-content-dmx.md)  
  
 [SELECT FROM &#60; 모델 &#62;. 경우 &#40; DMX &#41;](../dmx/select-from-model-cases-dmx.md)  
  
 [SELECT FROM &#60; 모델 &#62;. SAMPLE_CASES &#40; DMX &#41;](../dmx/select-from-model-sample-cases-dmx.md)  
  
 [SELECT FROM &#60; 모델 &#62;. DIMENSION_CONTENT &#40; DMX &#41;](../dmx/select-from-model-dimension-content-dmx.md)  
  
 [SELECT FROM &#60; 모델 &#62; 예측 조인 &#40; DMX &#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
 [SELECT FROM &#60; 모델 &#62; &#40; DMX &#41;](../dmx/select-from-model-dmx.md)  
  
 [SELECT FROM &#60; 구조 &#62;. 경우](../dmx/select-from-structure-cases.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Data Mining Extensions &#40; DMX &#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [Data Mining Extensions &#40; DMX &#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [Data Mining Extensions &#40; DMX &#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [Data Mining Extensions &#40; DMX &#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)  
  
  
