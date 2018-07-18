---
title: SELECT (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: def96304f13f57095679056e6eab0a004b5c47d9
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37989882"
---
# <a name="select-dmx"></a>SELECT(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  합니다 **선택** 에서 확장 DMX (Data Mining) 문은 데이터 마이닝에서는 다음과 같은 작업에 사용 됩니다.  
  
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
  
 쿼리 결과 평면화 하려면 사용 합니다 **선택** 구문에는 **FLATTENED** 옵션을 다음 예와에서 같이:  
  
```  
SELECT FLATTENED <select list> FROM ...  
```  
  
## <a name="top-n-and-order-by"></a>상위 \<n > 및 ORDER BY  
 식을 사용 하 여 쿼리 결과 정렬할 수 및 결과의 하위 집합을 함께 사용 하 여 후 반환할 수 있습니다 합니다 **ORDER BY** 하 고 **위쪽** 절. 이 함수는 응답할 가능성이 높은 사람에게만 결과를 보내도록 메일 대상을 지정하는 시나리오 등에서 유용합니다. 예측 확률을 기준으로 예측 쿼리를 메일 대상의 결과 정렬 한 다음 위쪽 반환할 수 있습니다 \<n > 결과입니다.  
  
## <a name="select-list"></a>select list  
 합니다  *\<select 목록 >* 스칼라 열 참조, 예측 함수 또는 식이 포함 될 수 있습니다. 사용 가능한 옵션은 알고리즘과 다음 컨텍스트에 따라 달라집니다.  
  
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
 사용 하 여 쿼리에 의해 반환 되는 사례를 제한할 수 있습니다는 **여기서** 절. **위치** 절에서 참조 하는 해당 열을 지정 합니다 **여기서** 식 열 참조와 동일한 의미 체계 있어야 합니다.를  *\<select 목록 >* 의 합니다 **선택** 문과 반환할 수 있습니다 하는 부울 식입니다. 구문은 합니다 **여기서** 절은 다음과 같습니다  
  
```  
WHERE < condition expression >  
```  
  
 Select 목록 및 **여기서** 절을 **선택** 문은 다음 규칙을 따라야 합니다.:  
  
-   select list에는 부울 결과를 반환하지 않는 식이 포함되어야 합니다. 식을 수정할 수는 있지만 이 식은 부울이 아닌 결과를 반환해야 합니다.  
  
-   합니다 **여기서** 절에 부울 결과 반환 하는 식을 포함 해야 합니다. 절을 수정할 수는 있지만 이 절은 부울 결과를 반환해야 합니다.  
  
## <a name="predictions"></a>예측  
 예측을 만들 때 사용할 수 있는 구문에는 두 가지 유형이 있습니다.  
  
-   [SELECT FROM &#60;모델&#62; PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
-   [SELECT FROM &#60;모델&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)  
  
 첫 번째 예측 유형을 사용하면 실시간 또는 일괄 처리로 복잡한 예측을 만들 수 있습니다.  
  
 두 번째 예측 유형은 마이닝 모델에서 예측 가능한 열에 빈 예측 조인을 만들고 가장 가능성이 높은 열 상태를 반환합니다. 이 쿼리 결과는 전적으로 마이닝 모델의 내용을 기준으로 합니다.  
  
 다음 구문을 사용 하 여 선택 FROM PREDICTION JOIN 문의 원본 쿼리에 select 문을 삽입할 수 있습니다.  
  
```  
SELECT FROM PREDICTION JOIN (<SELECT statement>) AS t, WHERE <SELECT statement>  
```  
  
 예측 쿼리를 만드는 방법에 대 한 자세한 내용은 참조 하세요. [구조와 DMX 예측 쿼리 사용량](../dmx/structure-and-usage-of-dmx-prediction-queries.md)합니다.  
  
## <a name="clause-syntax"></a>절 구문  
 사용 하 여 검색의 복잡성으로 인해 합니다 **선택** 문, 자세한 구문 요소 및 인수는 절로 설명 됩니다. 각 절에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
 [SELECT DISTINCT FROM &#60;모델 &#62; &#40;DMX&#41;](../dmx/select-distinct-from-model-dmx.md)  
  
 [SELECT FROM &#60;모델&#62;합니다. 콘텐츠 &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)  
  
 [SELECT FROM &#60;모델&#62;합니다. 경우 &#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md)  
  
 [SELECT FROM &#60;모델&#62;합니다. SAMPLE_CASES &#40;DMX&#41;](../dmx/select-from-model-sample-cases-dmx.md)  
  
 [SELECT FROM &#60;모델&#62;합니다. DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)  
  
 [SELECT FROM &#60;모델&#62; PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
 [SELECT FROM &#60;모델&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)  
  
 [SELECT FROM &#60;구조&#62;합니다. 경우](../dmx/select-from-structure-cases.md)  
  
## <a name="see-also"></a>관련 항목  
 [Data Mining Extensions &#40;DMX&#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [Data Mining Extensions &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [Data Mining Extensions &#40;DMX&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [Data Mining Extensions &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)  
  
  
