---
title: 모델 필터 구문 및 예 (Analysis Services-데이터 마이닝) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- model filter [data mining]
- filter syntax [data mining]
- filters [data mining]
- filters [Analysis Services]
ms.assetid: c729d9b3-8fda-405e-9497-52b2d7493eae
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 881b62a2e013d9e01a21272d3adeaf6819b2abb6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079395"
---
# <a name="model-filter-syntax-and-examples-analysis-services---data-mining"></a>모델 필터 구문 및 예(Analysis Services - 데이터 마이닝)
  이 섹션에서는 샘플 식과 함께 모델 필터 구문에 대한 자세한 정보를 제공합니다.  
  
 
  
##  <a name="bkmk_Syntax"></a> Filter Syntax  
 일반적으로 필터 식은 WHERE 절의 내용에 해당합니다. 논리 연산자 `AND`, `OR` 및 `NOT`을 사용하여 여러 조건을 연결할 수 있습니다.  
  
 중첩된 테이블에서 사용할 수도 있습니다는 `EXISTS` 및 `NOT EXISTS` 연산자입니다. `EXISTS` 조건은 하위 쿼리가 하나 이상의 행을 반환하는 경우 `true`로 평가됩니다. 이는 중첩 테이블에 특정 값을 포함하는 사례로 모델을 제한하려는 경우 유용합니다. 특정 제품을 한 번 이상 구매한 고객으로 모델을 제한하려는 경우를 예로 들 수 있습니다.  
  
 `NOT EXISTS` 조건은 하위 쿼리에 지정된 조건이 없는 경우 `true`로 평가됩니다. 특정 제품을 구매한 적이 없는 고객으로 모델을 제한하려는 경우를 예로 들 수 있습니다.  
  
 일반 구문은 다음과 같습니다.  
  
```  
<filter>::=<predicate list>  | ( <predicate list> )  
<predicate list>::= <predicate> | [<logical_operator> <predicate list>]   
<logical_operator::= AND| OR  
<predicate>::= NOT <predicate>|( <predicate> ) <avPredicate> | <nestedTablePredicate> | ( <predicate> )   
<avPredicate>::= <columnName> <operator> <scalar> | <columnName> IS [NOT] NULL  
<operator>::= = | != | <> | > | >= | < | <=  
<nestedTablePredicate>::= EXISTS (<subquery>)  
<subquery>::=SELECT * FROM <columnName>[ WHERE  <predicate list> ]  
```  
  
 *filter*  
 논리 연산자로 연결된 하나 이상의 조건자를 포함합니다.  
  
 *predicate list*  
 논리 연산자로 구분된 하나 이상의 올바른 필터 식입니다.  
  
 *columnName*  
 마이닝 구조 열의 이름입니다.  
  
 logical_operator  
 `AND`, `OR`, `NOT`  
  
 *avPredicate*  
 스칼라 마이닝 구조 열에만 적용할 수 있는 필터 식입니다. *avPredicate* 식은 모델 필터나 중첩 테이블 필터 모두에 사용할 수 있습니다.  
  
 다음 연산자를 사용하는 식은 연속 열에만 적용할 수 있습니다. 으로 디코딩된 문자입니다.  
  
-   **\<** (보다 작음)  
  
-   **>** (보다 큼)  
  
-   **>=** (크거나 같음)  
  
-   **\<=** (작거나 같음)  
  
> [!NOTE]  
>  데이터 형식에 관계 없이 이러한 연산자에 적용할 수 없습니다는 형식이 있는 열 `Discrete`, `Discretized`, 또는 `Key`합니다.  
  
 다음 연산자를 사용하는 식은 연속 열, 불연속 열, 분할된 열 또는 키 열에 적용할 수 있습니다.  
  
-   **=** (같음)  
  
-   **!=** (같지 않음)  
  
-   **IS NULL**  
  
 *avPredicate*인수가 불연속 열에 적용되는 경우 필터에 사용되는 값은 특정 버킷의 임의 값이 될 수 있습니다.  
  
 즉, 조건을 `AgeDisc = ’25-35’`로 정의하지 않고 해당 구간에서 값을 계산하여 사용합니다.  
  
 예를 들어  `AgeDisc = 27`  은 27과 같은 구간(이 경우 25-35)에 있는 임의의 값을 의미합니다.  
  
 *nestedTablePredicate*  
 중첩 테이블에 적용되는 필터 식입니다. 모델 필터에만 사용할 수 있습니다.  
  
 *nestedTablePredicate*의 하위 쿼리 인수는 테이블 마이닝 구조 열에만 적용할 수 있습니다.  
  
 하위 쿼리  
 올바른 조건자 또는 조건자 목록 앞에 오는 SELECT 문입니다.  
  
 모든 조건자는 *avPredicates*에 설명된 형식이어야 합니다. 또한 조건자는 현재 중첩 테이블에 포함되어 있으며 *columnName*인수로 식별되는 열만 참조할 수 있습니다.  
  
### <a name="limitations-on-filter-syntax"></a>필터 구문의 제한 사항  
 필터에는 다음 제한 사항이 적용됩니다.  
  
-   필터는 간단한 조건자만 포함할 수 있습니다. 여기에는 수치 연산자, 스칼라 및 열 이름이 포함됩니다.  
  
-   사용자 정의 함수는 필터 구문에서 지원되지 않습니다.  
  
-   더하기 기호나 빼기 기호 같이 부울이 아닌 연산자는 필터 구문에서 지원되지 않습니다.  
  
## <a name="examples-of-filters"></a>필터 예  
 다음 예에서는 마이닝 모델에 적용되는 필터의 사용을 보여 줍니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]를 사용하여 **속성** 창 및 필터 대화 상자의 **식** 창에서 필터 식을 만드는 경우 WITH FILTER 키워드 뒤에 나타나는 문자열만 표시됩니다. 여기서는 열 유형 및 사용법을 더 쉽게 이해할 수 있도록 마이닝 구조의 정의를 포함했습니다.  
  
###  <a name="bkmk_Ex1"></a> 예 1: 일반적인 사례 수준 필터링  
 이 예에서는 직업이 건축가이고 나이가 31세 이상인 고객으로 모델에 사용되는 사례를 제한하는 간단한 필터를 보여 줍니다.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_1  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT  
)  
WITH FILTER (Age > 30 AND Occupation=’Architect’)  
```  
  

  
###  <a name="bkmk_Ex2"></a> 예 2: 중첩 테이블 특성을 사용한 사례 수준 필터링  
 마이닝 구조에 중첩 테이블이 포함되어 있는 경우 중첩 테이블에서 값의 존재 여부를 필터링하거나 특정 값이 포함된 중첩 테이블 행을 필터링할 수 있습니다. 이 예에서는 우유를 포함한 제품을 한 번 이상 구매한 31세 이상의 고객으로 모델에 사용되는 사례를 제한합니다.  
  
 이 예에서 볼 수 있듯이 모델에 포함된 열만 필터에 사용할 필요는 없습니다. 중첩 테이블 **Products** 는 마이닝 구조의 일부이지만 마이닝 모델에는 포함되지 않습니다. 그럼에도 불구하고 중첩 테이블의 값 및 특성을 필터링할 수 있습니다. 이러한 사례에 대한 세부 정보를 보려면 드릴스루를 사용해야 합니다.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_2  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT  
)  
WITH DRILLTHROUGH,   
FILTER (Age > 30 AND EXISTS (SELECT * FROM Products WHERE ProductName=’Milk’)  
)  
```  
  
 
  
###  <a name="bkmk_Ex3"></a> 예 3: 여러 중첩 테이블 특성을 사용한 사례 수준 필터링  
 이 예에서는 사례 테이블에 적용되는 조건, 중첩 테이블의 특성에 적용되는 조건 및 중첩 테이블 열 중 하나의 특정 값에 적용되는 조건이라는 세 부분으로 이루어진 필터를 보여 줍니다.  
  
 필터의 첫 번째 조건인 `Age > 30`은 사례 테이블의 열에 적용됩니다. 나머지 조건은 중첩 테이블에 적용됩니다.  
  
 두 번째 조건인 `EXISTS (SELECT * FROM Products WHERE ProductName=’Milk’`는 중첩 테이블에 우유를 포함한 한 번 이상의 구매가 있는지 확인합니다. 세 번째 조건인 `Quantity>=2`는 고객이 한 번의 거래 과정에서 두 팩 이상의 우유를 구매했음을 의미합니다.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_3  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName KEY,  
Quantity        
)  
)  
FILTER (Age > 30 AND EXISTS (SELECT * FROM Products WHERE ProductName=’Milk’  AND Quantity >= 2)   
)  
```  
  

  
###  <a name="bkmk_Ex4"></a> 예 4: 중첩 테이블 특성의 부재를 사용한 사례 수준 필터링  
 이 예에서는 중첩 테이블에서 특성의 부재를 필터링하여 특정 제품을 구매하지 않은 고객으로 사례를 제한하는 방법을 보여 줍니다. 이 예에서는 우유를 구입한 적이 없는 31세 이상의 고객을 사용하여 모델을 학습합니다.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_4  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName  
)  
)  
FILTER (Age > 30 AND NOT EXISTS (SELECT * FROM Products WHERE ProductName=’Milk’) )  
```  
  

  
###  <a name="bkmk_Ex5"></a> 예 5: 여러 중첩 테이블 값을 사용한 필터링  
 이 예는 중첩 테이블 필터링을 보여 주기 위한 것입니다. 중첩 테이블 필터는 사례 필터 다음에 적용되며 중첩 테이블 행만 제한합니다.  
  
 이 모델에서는 EXISTS를 지정하지 않았으므로 빈 중첩 테이블이 있는 여러 사례가 모델에 포함될 수 있습니다.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_5  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName KEY,  
Quantity        
) WITH FILTER(ProductName=’Milk’ OR ProductName=’bottled water’)  
)  
WITH DRILLTHROUGH  
```  
  

  
###  <a name="bkmk_Ex6"></a> 예 6: 중첩 테이블 특성 및 EXISTS를 사용한 필터링  
 이 예에서 중첩 테이블에 대한 필터는 우유 또는 생수를 포함하는 항목으로만 행을 제한합니다. 그런 다음 `EXISTS` 문을 사용하여 모델의 사례를 제한합니다. 이렇게 하면 중첩 테이블이 비어 있지 않게 됩니다.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_6  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName KEY,  
Quantity        
) WITH FILTER(ProductName=’Milk’ OR ProductName=’bottled water’)  
)  
FILTER (EXISTS (Products))  
```  
  

  
###  <a name="bkmk_Ex7"></a> 예 7: 복잡한 필터 조합  
 이 모델의 시나리오는 예 4의 시나리오와 비슷하지만 훨씬 더 복잡합니다. 중첩된 테이블 **ProductsOnSale**, 필터 조건이 `(OnSale)` 의 값 즉 **OnSale** 해야 `true` 에 나열 된 제품에 대 한 **ProductName**. 여기서 **OnSale** 은 구조 열입니다.  
  
 필터의 두 번째 부분에 대 한 **ProductsNotOnSale**,이 구문이 반복 되지만 필터링 인 제품을 값 **OnSale** 은 `not true``(!OnSale)`합니다.  
  
 마지막으로 조건을 조합하고 하나의 추가 제한 사항을 사례 테이블에 추가합니다. 그 결과 26세 이상의 모든 고객에 대해 **ProductsNotOnSale** 목록에 포함된 사례를 기반으로 **ProductsOnSale** 목록의 제품 구매를 예측할 수 있습니다.  
  
 `ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_7`  
  
 `(`  
  
 `CustomerId,`  
  
 `Age,`  
  
 `Occupation,`  
  
 `MaritalStatus,`  
  
 `ProductsOnSale`  
  
 `(`  
  
 `ProductName KEY`  
  
 `) WITH FILTER(OnSale),`  
  
 `ProductsNotOnSale PREDICT ONLY`  
  
 `(`  
  
 `ProductName KEY`  
  
 `) WITH FILTER(!OnSale)`  
  
 `)`  
  
 `WITH DRILLTHROUGH,`  
  
 `FILTER (EXISTS (ProductsOnSale) AND EXISTS(ProductsNotOnSale) AND Age > 25)`  
  
  
  
###  <a name="bkmk_Ex8"></a> 예 8: 날짜로 필터링  
 다른 데이터와 마찬가지로 날짜로 입력 열을 필터링할 수 있습니다. 날짜/시간 형식의 열에 포함된 날짜는 연속 값입니다. 따라서 보다 큼(>) 또는 보다 작음(<)과 같은 연산자를 사용하여 날짜 범위를 지정할 수 있습니다. 데이터 원본에서 날짜를 연속 데이터 형식이 아니라 불연속 또는 텍스트 값으로 나타낼 경우 날짜 범위를 필터링할 수 없고 개별 불연속 값을 지정해야 합니다.  
  
 그러나 필터에 사용된 날짜 열이 또한 모델의 키 열인 경우 시계열 모델에서 날짜 열에 대한 필터를 만들 수 없습니다. 시계열 모델 및 시퀀스 클러스터링 모델에서 날짜 열 형식으로 처리 수 때문 `KeyTime` 또는 `KeySequence`합니다.  
  
 시계열 모델에서 연속 날짜를 필터링해야 하는 경우 마이닝 구조에서 열의 복사본을 만들고 새 열에서 모델을 필터링할 수 있습니다.  
  
 예를 들어 다음 식은 예측 모델에 추가된 `Continuous` 형식의 날짜 열에 대한 필터를 나타냅니다.  
  
 `=[DateCopy] > '12:31:2003:00:00:00'`  
  
> [!NOTE]  
>  모델에 추가하는 모든 추가 열은 결과에 영향을 줄 수 있습니다. 따라서 계열의 계산에 열을 사용하지 않으려면 열을 모델이 아니라 마이닝 구조에만 추가해야 합니다. 열을 모델 플래그를 설정할 수도 있습니다 `PredictOnly` 또는 `Ignore`합니다. 자세한 내용은 [모델링 플래그&#40;데이터 마이닝&#41;](modeling-flags-data-mining.md)를 참조하세요.  
  
 다른 모델 유형의 경우 다른 열과 마찬가지로 입력 조건이나 필터 조건으로 날짜를 사용할 수 있습니다. 그러나 특정 수준의 세분성에서 지원 되지 않는 사용 해야 하는 경우는 `Continuous` 데이터 형식을 만들 수 있습니다 파생 된 값을 데이터 소스에서 필터링 및 분석에 사용할 단위를 추출 하는 식을 사용 하 여 합니다.  
  
> [!WARNING]  
>  필터 조건으로 날짜를 지정하는 경우에는 현재 운영 체제의 날짜 형식에 관계없이 다음 형식을 사용해야 합니다. `mm/dd/yyyy` 다른 형식을 사용하면 오류가 발생합니다.  
  
 예를 들어 콜 센터 결과를 필터링하여 주말만 표시하려면 각 날짜의 평일 이름을 추출한 다음 해당 평일 이름 값을 입력에 사용하거나 필터링에서 불연속 값으로 사용하는 식을 데이터 원본 뷰에서 만들 수 있습니다. 반복 값은 모델에 영향을 줄 수 있으므로 파생 값과 함께 날짜 열을 사용하는 대신에 열 중에서 하나만 사용해야 합니다.  
  
 
  
## <a name="see-also"></a>관련 항목  
 [마이닝 모델에 대 한 필터 &#40;Analysis Services-데이터 마이닝&#41;](mining-models-analysis-services-data-mining.md)   
 [테스트 및 유효성 검사 &#40;데이터 마이닝&#41;](testing-and-validation-data-mining.md)  
  
  