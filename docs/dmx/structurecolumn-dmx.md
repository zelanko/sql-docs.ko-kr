---
description: StructureColumn(DMX)
title: StructureColumn (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 43e02efd8594497ad4f3c02679a475531489141c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500790"
---
# <a name="structurecolumn-dmx"></a>StructureColumn(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  지정된 사례에 해당하는 구조 열의 값이나 지정된 사례의 중첩 테이블에 대한 테이블 값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
StructureColumn('structure column name')  
```  
  
## <a name="arguments"></a>인수  
 structure-column-name  
 사례 또는 중첩 테이블 마이닝 구조 열의 이름입니다.  
  
## <a name="result-type"></a>결과 형식  
 반환 되는 형식은 매개 변수에서 참조 되는 열의 형식에 따라 달라 집니다 \<structure column name> . 예를 들어 참조되는 마이닝 구조 열에 스칼라 값이 포함되어 있으면 스칼라 값이 반환됩니다.  
  
 참조되는 마이닝 구조 열이 중첩 테이블이면 테이블 값이 반환됩니다. 반환된 테이블 값은 하위 SELECT 문의 FROM 절에 사용할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 이 함수는 다형성을 갖고 있으며 SELECT 식 목록, WHERE 조건 식, ORDER BY 식 등의 식을 허용하는 문의 어디에서나 사용할 수 있습니다.  
  
 마이닝 구조의 열 이름은 문자열 값 이며 작은따옴표로 묶어야 합니다. 예를 들어 `StructureColumn('` **열 1** `')` 입니다. 동일한 이름의 열이 여러 개 있으면 이름이 바깥쪽 SELECT 문의 컨텍스트에서 확인됩니다.  
  
 **StructureColumn** 함수를 사용 하 여 쿼리에서 반환 되는 결과는 모델에 필터가 있는 경우에 영향을 받습니다. 즉, 모델 필터에 의해 마이닝 모델에 포함되어 있는 사례가 제어됩니다. 따라서 구조 열에 대한 쿼리는 마이닝 모델에 사용된 사례만 반환할 수 있습니다. 마이닝 모델 필터가 사례 테이블과 중첩 테이블에 미치는 영향을 보여 주는 코드 예는 이 항목의 예 섹션을 참조하십시오.  
  
 DMX SELECT 문에서이 함수를 사용 하는 방법에 대 한 자세한 내용은 [SELECT FROM &#60;model&#62;을 참조 하세요. 사례는 DMX&#41;&#40;](../dmx/select-from-model-cases-dmx.md) [&#60;구조&#62;에서 선택 합니다. 사례](../dmx/select-from-structure-cases.md).  
  
## <a name="error-messages"></a>오류 메시지  
 사용자에게 부모 마이닝 구조에 대한 드릴스루 권한이 없는 경우 다음과 같은 보안 오류 메시지가 나타납니다.  
  
 '%{user/}' 사용자에게 '%{model/}' 마이닝 모델의 부모 마이닝 구조로 드릴스루할 권한이 없습니다.  
  
 잘못된 구조 열 이름을 지정하면 다음과 같은 오류 메시지가 나타납니다.  
  
 현재 컨텍스트(줄 %{line/}, 열 %{column/})의 '%{structure/}' 부모 마이닝 구조에서 '%{structure-column-name/}' 마이닝 구조 열을 찾을 수 없습니다.  
  
## <a name="examples"></a>예제  
 여기에 나오는 예에서는 다음 마이닝 구조를 사용합니다. 이 마이닝 구조에는 두 개의 중첩 테이블 열, `Products`와 `Hobbies`가 있습니다. `Hobbies` 열의 중첩 테이블에는 중첩 테이블의 키로 사용되는 단일 열이 있습니다. `Products` 열의 중첩 테이블은 키 열과 입력에 사용되는 다른 열이 둘 다 있는 복잡한 중첩 테이블입니다. 다음 예에서는 모델에서 모든 열을 사용할 수는 없더라도 다양한 열을 포함하도록 데이터 마이닝 구조를 디자인하는 방법을 보여 줍니다. 이러한 열 중 일부는 패턴을 일반화하는 모델 수준에서는 유용하지 않을 수 있지만 드릴스루 시 매우 유용할 수 있습니다.  
  
```  
CREATE MINING STRUCTURE [MyStructure]   
(  
CustomerName TEXT KEY,  
Occupation TEXT DISCRETE,  
Age LONG CONTINUOUS,  
MaritalStatus TEXT DISCRETE,  
Income LONG CONTINUOUS,  
Products  TABLE  
 (  
    ProductNameTEXT KEY,  
    Quantity LONG CONTINUOUS,  
    OnSale BOOLEAN  DISCRETE  
)  
 Hobbies  TABLE  
 (  
    Hobby KEY  
 ))  
```  
  
 그런 후 다음 예제 코드를 사용하여 방금 만든 구조를 기반으로 마이닝 모델을 만듭니다.  
  
```  
ALTER MINING STRUCTURE [MyStructure] ADD MINING MODEL [MyModel] (  
CustomerName,  
Age,  
MaritalStatus,  
Income PREDICT,  
Products   
(  
ProductName  
) WITH FILTER(NOT OnSale)  
) USING Microsoft_Decision_Trees   
WITH FILTER(EXISTS (Products))  
```  
  
### <a name="sample-query-1-returning-a-column-from-the-mining-structure"></a>예제 쿼리 1: 마이닝 구조에서 열 반환  
 다음 예제 쿼리에서는 마이닝 모델의 일부로 정의되는 `CustomerName` 및 `Age` 열을 반환합니다. 그러나 이 쿼리에서는 구조에만 포함되어 있고 마이닝 모델에는 포함되어 있지 않은 `Age` 열도 반환합니다.  
  
```  
SELECT CustomerName, Age, StructureColumn('Occupation') FROM MyModel.CASES   
WHERE Age > 30  
```  
  
 31세 이상의 고객으로 사례를 제한하는 행 필터링은 모델 수준에서 발생하기 때문에 이 식은 구조 데이터에는 포함되지만 마이닝 모델에서는 사용되지 않는 사례를 반환하지 않을 수 있습니다. 모델을 만드는 데 사용된 필터 조건(`EXISTS (Products)`)이 제품을 구매한 고객으로 사례를 제한하기 때문에 구조에는 이 쿼리에서 반환하지 않는 사례가 있을 수 있습니다.  
  
### <a name="sample-query-2-applying-a-filter-to-the-structure-column"></a>예제 쿼리 2: 구조 열에 필터 적용  
 다음 예제 쿼리에서는 `CustomerName` 및 `Age` 열과 `Products`중첩 테이블을 반환할 뿐만 아니라 모델에 포함되어 있지 않은 중첩 테이블의 `Quantity` 열 값도 반환합니다.  
  
```  
SELECT CustomerName, Age,  
(SELECT ProductName, StructureColumn('Quantity') FROM Products) FROM MA.CASES   
WHERE StructureColumn('Occupation') = 'Architect'  
```  
  
 이 예에서는 직업이 '건축가'인 고객으로 사례를 제한하는 필터(`WHERE StructureColumn('Occupation') = 'Architect'`)가 구조 열에 적용됩니다. 모델을 만들면 모델 필터 조건이 사례에 항상 적용되기 때문에 `Products` 테이블에 한정하는 행이 적어도 하나 이상 있는 사례만 모델 사례에 포함됩니다. 따라서 `Products` 중첩 테이블의 필터와 `('Occupation')` 사례의 필터가 둘 다 적용됩니다.  
  
### <a name="sample-query-3-selecting-columns-from-a-nested-table"></a>예제 쿼리 3: 중첩 테이블에서 열 선택  
 다음 예제 쿼리에서는 모델의 학습 사례로 사용된 고객의 이름을 반환할 뿐만 아니라 각 고객의 구매 정보가 포함된 중첩 테이블도 반환합니다. 모델에 열이 포함 되어 있지만 `ProductName` 모델에서는 열 값을 사용 하지 않습니다 `ProductName` . 모델은 제품이 일반 () 가격으로 구매 되었는지 확인 `NOT``OnSale` 합니다. 이 쿼리에서는 제품 이름을 반환할 뿐만 아니라 모델에 포함되어 있지 않은 구매 수량도 반환합니다.  
  
```  
SELECT CustomerName,    
(SELECT ProductName, StructureColumn('Quantity')FROM Products)   
FROM MyModel.CASES  
```  
  
 마이닝 모델에 드릴스루가 사용되도록 설정되지 않은 경우 `ProductName` 또는 `Quantity` 열을 반환할 수 없습니다.  
  
### <a name="sample-query-4-filtering-on-and-returning-nested-table-columns"></a>예제 쿼리 4: 중첩 테이블 열 필터링 및 반환  
 다음 예제 쿼리에서는 마이닝 구조에만 포함되어 있고 마이닝 모델에는 포함되어 있지 않은 사례와 중첩 테이블 열을 반환합니다. 모델에서 `OnSale` 제품이 있는지 여부를 기준으로 필터링이 이미 수행되었지만 이 쿼리는 `Quantity` 마이닝 구조 열에 필터를 추가합니다.  
  
```  
SELECT CustomerName, Age, StructureColumn('Occupation'),   
(SELECT ProductName, StructureColumn('Quantity') FROM Products)   
FROM MyModel.CASES   
WHERE EXISTS (SELECT * FROM Products WHERE StructureColumn('Quantity')>1)  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX &#40;함수&#41;](../dmx/functions-dmx.md)   
 [DMX&#41;일반 예측 함수 &#40;](../dmx/general-prediction-functions-dmx.md)  
  
  
