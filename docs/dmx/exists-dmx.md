---
title: Exists (DMX) | Microsoft Docs
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
f1_keywords:
- Exists
dev_langs:
- DMX
helpviewer_keywords:
- Exists function
ms.assetid: 3b54dd93-f0a8-4f9a-96ae-a38bf977dda1
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 9e741b37b167fcb4568fd38fe069224e669cda0f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="exists-dmx"></a>Exists(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  반환 **true** 지정된 된 하위 쿼리가 하나 이상의 행을 반환 하는 경우.  
  
## <a name="syntax"></a>구문  
  
```  
  
EXISTS(<subquery>)  
```  
  
## <a name="arguments"></a>인수  
 *subquery*  
 SELECT 문의 폼 선택의 * FROM \<열 이름 > [여기서 \<조건자 목록 >].  
  
## <a name="result-type"></a>결과 유형  
 반환 **true** 하위 쿼리에서 반환 된 결과 집합 하나 이상의 행을 포함 하는 경우는 그렇지 않으면 반환 **false**합니다.  
  
## <a name="remarks"></a>주의  
 EXISTS 앞에 NOT 키워드를 사용할 수 있습니다. 예를 들면 `WHERE NOT EXISTS (<subquery>)`와 같습니다.  
  
 EXISTS의 하위 쿼리 인수에 추가하는 열 목록은 상관이 없습니다. 함수는 조건에 맞는 행의 존재 여부만 확인합니다.  
  
## <a name="examples"></a>예  
 EXISTS 및 NOT EXISTS를 사용하여 중첩 테이블의 조건을 확인할 수 있습니다. 이는 데이터 마이닝 모델을 학습 또는 테스트하는 데 사용되는 데이터를 제어하는 필터를 만들 때 유용합니다. 자세한 내용은 [마이닝 모델에 대한 필터&#40;Analysis Services - 데이터 마이닝&#41;](../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)를 참조하세요.  
  
 다음 예제에서는 기반는 `[Association]` 마이닝 구조와 마이닝 모델에서 만든는 [기본 데이터 마이닝 자습서](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)합니다. 쿼리는 고객이 하나 이상의 Patch kit을 구매한 사례만 반환합니다.  
  
```  
SELECT * FROM [Association].CASES  
WHERE EXISTS  
(  
SELECT * FROM [v Assoc Seq Line Numbers]  
WHERE [[Model] = 'Patch kit'  
)  
```  
  
 이 쿼리에서 반환 되는 동일한 데이터를 보려면 또 다른 방법은 연결 뷰어에서 모델을 열고, 항목 집합을 마우스 오른쪽 단추로 클릭 하는 것 **Patch kit = Existing**, 선택는 **드릴스루** 옵션을 선택한 다음 선택 **모델 사례만**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [함수 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [모델 필터 구문 및 예 &#40;Analysis Services-데이터 마이닝&#41;](../analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md)  
  
  
