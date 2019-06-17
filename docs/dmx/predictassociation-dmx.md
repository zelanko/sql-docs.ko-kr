---
title: PredictAssociation (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7a23407b546bcde2dd1fde81654da4fe861e0719
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62501844"
---
# <a name="predictassociation-dmx"></a>PredictAssociation(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  연관된 멤버 자격을 예측합니다.  
  
예를 들어, 고객의 시장 바구니의 현재 상태를 지정 하는 권장 사항 집합을 가져오는 PredictAssociation 함수를 사용할 수 있습니다. 
  
## <a name="syntax"></a>구문  
  
```  
  
PredictAssociation(<table column reference>, option1, option2, n ...)  
```  
  
## <a name="applies-to"></a>적용 대상  
 연결 및 일부 분류 알고리즘을 포함 하 여 예측 가능한 중첩된 테이블을 포함 하는 알고리즘입니다. 중첩된 테이블을 지 원하는 분류 알고리즘을 포함 합니다 [!INCLUDE[msCoName](../includes/msconame-md.md)] 의사 결정 트리 [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes 및 [!INCLUDE[msCoName](../includes/msconame-md.md)] 신경망 알고리즘입니다.  
  
## <a name="return-type"></a>반환 형식  
 \<테이블 식 >  
  
## <a name="remarks"></a>Remarks  
 에 대 한 옵션을 **PredictAssociation** EXCLUDE_NULL, INCLUDE_NULL, INCLUSIVE, EXCLUSIVE (기본값), INPUT_ONLY, INCLUDE_STATISTICS 및 INCLUDE_NODE_ID 함수를 포함 합니다.  
  
> [!NOTE]  
>  INCLUSIVE, EXCLUSIVE, INPUT_ONLY 및 INCLUDE_STATISTICS는 테이블 열 참조에만 적용되고 EXCLUDE_NULL 및 INCLUDE_NULL은 스칼라 열 참조에만 적용됩니다.  
  
 INCLUDE_STATISTICS 반환 **$Probability** 하 고 **$AdjustedProbability**합니다.  
  
 경우 숫자 매개 변수 *n* 를 지정 합니다 **PredictAssociation** 가능성에 따라 상위 n 가능성이 가장 높은 값을 반환 하는 함수:  
  
```  
PredictAssociation(colref, [$AdjustedProbability], n)  
```  
  
 포함 하는 경우 **$AdjustedProbability**, 맨 위에 반환 *n* 값에 따라 합니다 **$AdjustedProbability**합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 합니다 **PredictAssociation** 네 가지 제품을 Adventure works에서 데이터베이스를 반환 하는 함수를 함께 판매 될 가능성이 가장 높은 합니다.  
  
```  
SELECT  
  PredictAssociation([Association].[v Assoc Seq Line Items],4)  
From  
  [Association]  
```  
다음 예제에서는 어떻게 사용할 수 중첩된 테이블이 예측 함수에 대 한 입력으로 SHAPE 절을 사용 하 여 하는 방법을 보여 줍니다. SHAPE 쿼리의 중첩된 테이블로 고객이 이미 가져왔습니다. 제품의 목록을 포함 하는 두 번째 열을 하나의 열으로 customerId와 행 집합을 만듭니다. 

~~~~
SELECT T.[CustomerId], PredictAssociation(MyNestedTable, 5) // returns top 5 associated items
FROM My Model
PREDICTION JOIN
SHAPE {
    OPENQUERY([Adventure Works DW],'SELECT CustomerID, OrderNumber
    FROM vAssocSeqOrders ORDER BY OrderNumber')
} APPEND (
    {OPENQUERY([Adventure Works DW],'SELECT OrderNumber, model FROM 
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}
  RELATE OrderNumber to OrderNumber) AS T
~~~~  

  
## <a name="see-also"></a>관련 항목  
 [Data Mining Extensions &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [함수 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [일반 예측 함수 &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
