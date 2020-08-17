---
description: Exists(DMX)
title: Exists (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a0fa41dfff8edc6ddddeb420027a436f235e54a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88353339"
---
# <a name="exists-dmx"></a>Exists(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  지정 된 하위 쿼리가 하나 이상의 행을 반환 하는 경우 **true** 를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
EXISTS(<subquery>)  
```  
  
## <a name="arguments"></a>인수  
 *subquery*  
 Select * FROM [WHERE] 형식의 SELECT 문입니다 \<column name> \<predicate list> .  
  
## <a name="result-type"></a>결과 형식  
 하위 쿼리에서 반환 된 결과 집합에 하나 이상의 행이 포함 된 경우 **true** 를 반환 합니다. 그렇지 않으면 **false**를 반환 합니다.  
  
## <a name="remarks"></a>설명  
 EXISTS 앞에 NOT 키워드를 사용할 수 있습니다. 예를 들면 `WHERE NOT EXISTS (<subquery>)`와 같습니다.  
  
 EXISTS의 하위 쿼리 인수에 추가하는 열 목록은 상관이 없습니다. 함수는 조건에 맞는 행의 존재 여부만 확인합니다.  
  
## <a name="examples"></a>예제  
 EXISTS 및 NOT EXISTS를 사용하여 중첩 테이블의 조건을 확인할 수 있습니다. 이는 데이터 마이닝 모델을 학습 또는 테스트하는 데 사용되는 데이터를 제어하는 필터를 만들 때 유용합니다. 자세한 내용은 [마이닝 모델에 대한 필터&#40;Analysis Services - 데이터 마이닝&#41;](https://docs.microsoft.com/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining)를 참조하세요.  
  
 다음 예는 `[Association]` [기본 데이터 마이닝 자습서](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)에서 만든 마이닝 구조 및 마이닝 모델을 기반으로 합니다. 쿼리는 고객이 하나 이상의 Patch kit을 구매한 사례만 반환합니다.  
  
```  
SELECT * FROM [Association].CASES  
WHERE EXISTS  
(  
SELECT * FROM [v Assoc Seq Line Numbers]  
WHERE [[Model] = 'Patch kit'  
)  
```  
  
 이 쿼리에서 반환 되는 것과 동일한 데이터를 볼 수 있는 다른 방법은 연결 뷰어에서 모델을 열고, 항목 집합 **패치 키트 = 기존**을 마우스 오른쪽 단추로 클릭 하 고, **드릴스루** 옵션을 선택한 다음, **모델 사례만**을 선택 하는 것입니다.  
  
## <a name="see-also"></a>참고 항목  
 [DMX &#40;함수&#41;](../dmx/functions-dmx.md)   
 [모델 필터 구문 및 예&#40;Analysis Services - 데이터 마이닝&#41;](https://docs.microsoft.com/analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining)  
  
  
