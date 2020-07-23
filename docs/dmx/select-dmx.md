---
title: SELECT (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: bf4164308b0fdc9e6ba3fabb756c18214757cde5
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970622"
---
# <a name="select-dmx"></a>SELECT(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  DMX (데이터 마이닝 확장)의 **SELECT** 문은 데이터 마이닝의 다음 태스크에 사용 됩니다.  
  
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
  
 쿼리 결과를 평면화 하려면 다음 예제와 같이 **평면화** 된 옵션과 함께 **SELECT** 구문을 사용 합니다.  
  
```  
SELECT FLATTENED <select list> FROM ...  
```  
  
## <a name="top-n-and-order-by"></a>TOP \<n> 및 ORDER by  
 식을 사용 하 여 쿼리 결과를 정렬 한 다음 **ORDER by** 및 **TOP** 절의 조합을 사용 하 여 결과의 하위 집합을 반환할 수 있습니다. 이 함수는 응답할 가능성이 높은 사람에게만 결과를 보내도록 메일 대상을 지정하는 시나리오 등에서 유용합니다. 예측 확률을 기준으로 대상 메일 예측 쿼리의 결과를 정렬 한 다음 상위 결과만 반환할 수 있습니다 \<n> .  
  
## <a name="select-list"></a>select list  
 에는 *\<select list>* 스칼라 열 참조, 예측 함수 및 식이 포함 될 수 있습니다. 사용 가능한 옵션은 알고리즘과 다음 컨텍스트에 따라 달라집니다.  
  
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
 **WHERE** 절을 사용 하 여 쿼리에서 반환 되는 사례를 제한할 수 있습니다. **Where** 절은 **where** 식의 열 참조가 SELECT 문의에 있는 열 참조와 동일한 의미 체계를 가져야 하 *\<select list>* 고 부울 **SELECT** 식만 반환할 수 있도록 지정 합니다. **Where** 절의 구문은 다음과 같습니다.  
  
```  
WHERE < condition expression >  
```  
  
 **Select** 문의 select 목록 및 **WHERE** 절은 다음 규칙을 따라야 합니다.  
  
-   select list에는 부울 결과를 반환하지 않는 식이 포함되어야 합니다. 식을 수정할 수는 있지만 이 식은 부울이 아닌 결과를 반환해야 합니다.  
  
-   **Where** 절에는 부울 결과를 반환 하는 식이 포함 되어야 합니다. 절을 수정할 수는 있지만 이 절은 부울 결과를 반환해야 합니다.  
  
## <a name="predictions"></a>예측  
 예측을 만들 때 사용할 수 있는 구문에는 두 가지 유형이 있습니다.  
  
-   [&#60;모델&#62; 예측 조인 &#40;DMX에서 선택&#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
-   [&#60;모델&#62; &#40;DMX에서 선택&#41;](../dmx/select-from-model-dmx.md)  
  
 첫 번째 예측 유형을 사용하면 실시간 또는 일괄 처리로 복잡한 예측을 만들 수 있습니다.  
  
 두 번째 예측 유형은 마이닝 모델에서 예측 가능한 열에 빈 예측 조인을 만들고 가장 가능성이 높은 열 상태를 반환합니다. 이 쿼리 결과는 전적으로 마이닝 모델의 내용을 기준으로 합니다.  
  
 다음 구문을 사용 하 여 select FROM 예측 조인 문의 원본 쿼리에 select 문을 삽입할 수 있습니다.  
  
```  
SELECT FROM PREDICTION JOIN (<SELECT statement>) AS t, WHERE <SELECT statement>  
```  
  
 예측 쿼리를 만드는 방법에 대 한 자세한 내용은 [DMX 예측 쿼리의 구조 및 사용](../dmx/structure-and-usage-of-dmx-prediction-queries.md)을 참조 하세요.  
  
## <a name="clause-syntax"></a>절 구문  
 **SELECT** 문을 사용 하 여 검색 하는 복잡성 때문에 자세한 구문 요소와 인수는 절에 설명 되어 있습니다. 각 절에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
 [&#60;모델 &#62; &#40;DMX&#41;에서 고유를 선택 합니다.](../dmx/select-distinct-from-model-dmx.md)  
  
 [&#60;모델&#62;에서 선택 합니다. 콘텐츠 &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)  
  
 [&#60;모델&#62;에서 선택 합니다. 사례 &#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md)  
  
 [&#60;모델&#62;에서 선택 합니다. DMX&#41;SAMPLE_CASES &#40;](../dmx/select-from-model-sample-cases-dmx.md)  
  
 [&#60;모델&#62;에서 선택 합니다. DMX&#41;DIMENSION_CONTENT &#40;](../dmx/select-from-model-dimension-content-dmx.md)  
  
 [&#60;모델&#62; 예측 조인 &#40;DMX에서 선택&#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
 [&#60;모델&#62; &#40;DMX에서 선택&#41;](../dmx/select-from-model-dmx.md)  
  
 [&#60;구조&#62;에서 선택 합니다. 경우](../dmx/select-from-structure-cases.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)  
  
  
