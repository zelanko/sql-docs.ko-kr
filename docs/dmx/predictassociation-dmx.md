---
title: PredictAssociation (DMX) | Microsoft Docs
ms.custom: ''
ms.date: 09/14/2016
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
- PredictAssociation
dev_langs:
- DMX
helpviewer_keywords:
- PredictAssociation function
ms.assetid: 33eb66b5-84c6-449f-aaae-316345bc4ad5
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 09933a65f19ca025c8a681b068bf31c6fe0e9d7b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="predictassociation-dmx"></a>PredictAssociation(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  연관된 멤버 자격을 예측합니다.  
  
예를 들어 PredictAssociation 함수는 집합의 고객의 시장 바구니의 현재 상태를 제공 된 권장 사항 사용할 수 있습니다. 
  
## <a name="syntax"></a>구문  
  
```  
  
PredictAssociation(<table column reference>, option1, option2, n ...)  
```  
  
## <a name="applies-to"></a>적용 대상  
 연결 및 일부 분류 알고리즘을 포함 하 여 예측 가능한 중첩된 테이블을 포함 하는 알고리즘입니다. 분류 알고리즘을 지 원하는 중첩된 테이블이 포함 된 [!INCLUDE[msCoName](../includes/msconame-md.md)] 의사 결정 트리 [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes 및 [!INCLUDE[msCoName](../includes/msconame-md.md)] 신경망 알고리즘입니다.  
  
## <a name="return-type"></a>반환 형식  
 \<테이블 식 >  
  
## <a name="remarks"></a>주의  
 에 대 한 옵션은 **PredictAssociation** EXCLUDE_NULL, INCLUDE_NULL, INCLUSIVE, EXCLUSIVE (기본값), INPUT_ONLY, INCLUDE_STATISTICS 및 INCLUDE_NODE_ID 함수를 포함 합니다.  
  
> [!NOTE]  
>  INCLUSIVE, EXCLUSIVE, INPUT_ONLY 및 INCLUDE_STATISTICS는 테이블 열 참조에만 적용되고 EXCLUDE_NULL 및 INCLUDE_NULL은 스칼라 열 참조에만 적용됩니다.  
  
 INCLUDE_STATISTICS 반환 **$Probability** 및 **$AdjustedProbability**합니다.  
  
 경우 숫자 매개 변수가  *n*  지정는 **PredictAssociation** 확률을 기반으로 상위 n 가능성이 가장 높은 값을 반환 하는 함수:  
  
```  
PredictAssociation(colref, [$AdjustedProbability], n)  
```  
  
 포함 하는 경우 **$AdjustedProbability**, 위쪽 반환  *n*  값에 따라는 **$AdjustedProbability**합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 **PredictAssociation** 네 개의 제품을 Adventure works에서 데이터베이스를 반환 하도록 함수 되 함께 판매 될 가능성이 큽니다.  
  
```  
SELECT  
  PredictAssociation([Association].[v Assoc Seq Line Items],4)  
From  
  [Association]  
```  
다음 예제에서는 여 방법이 중첩된 테이블이 예측 함수에 대 한 입력으로는 SHAPE 절을 사용 하 여 보여 줍니다. SHAPE 쿼리의 하나의 열으로 customerId 및 고객에 이미 가져온 제품 목록이 포함 된 두 번째 열으로 중첩된 테이블 행 집합을 만듭니다. 

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

  
## <a name="see-also"></a>관련 항목:  
 [Data Mining Extensions &#40; DMX &#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [함수 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [일반 예측 함수 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
