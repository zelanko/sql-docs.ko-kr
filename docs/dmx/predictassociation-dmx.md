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
ms.openlocfilehash: ea0a9915e062d7b6f15b63e18976e88cc339202d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "76939501"
---
# <a name="predictassociation-dmx"></a>PredictAssociation(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  연관된 멤버 자격을 예측합니다.  
  
예를 들어 PredictAssociation 함수를 사용 하 여 고객에 대 한 쇼핑 바구니의 현재 상태에 대 한 권장 사항 집합을 얻을 수 있습니다. 
  
## <a name="syntax"></a>구문  
  
```  
  
PredictAssociation(<table column reference>, option1, option2, n ...)  
```  
  
## <a name="applies-to"></a>적용 대상  
 연결 및 일부 분류 알고리즘을 포함 하 여 예측 가능한 중첩 테이블을 포함 하는 알고리즘입니다. 중첩 테이블을 지 원하는 분류 알고리즘에 [!INCLUDE[msCoName](../includes/msconame-md.md)] 는 의사 결정 [!INCLUDE[msCoName](../includes/msconame-md.md)] 트리, Naive Bayes [!INCLUDE[msCoName](../includes/msconame-md.md)] 및 신경망 알고리즘이 포함 됩니다.  
  
## <a name="return-type"></a>반환 형식  
 \<테이블 식>  
  
## <a name="remarks"></a>설명  
 **PredictAssociation** 함수에 대 한 옵션에는 EXCLUDE_NULL, INCLUDE_NULL, 포함, 배타 (기본값), INPUT_ONLY, INCLUDE_STATISTICS 및 INCLUDE_NODE_ID가 포함 됩니다.  
  
> [!NOTE]  
>  INCLUSIVE, EXCLUSIVE, INPUT_ONLY 및 INCLUDE_STATISTICS는 테이블 열 참조에만 적용되고 EXCLUDE_NULL 및 INCLUDE_NULL은 스칼라 열 참조에만 적용됩니다.  
  
 INCLUDE_STATISTICS는 **$Probability** 및 **$AdjustedProbability**만 반환 합니다.  
  
 숫자 매개 변수 *n* 이 지정 된 경우 **PredictAssociation** 함수는 확률에 따라 가장 가능성이 높은 n 개의 상위 n 개 값을 반환 합니다.  
  
```  
PredictAssociation(colref, [$AdjustedProbability], n)  
```  
  
 **$AdjustedProbability**를 포함 하는 경우 문은 **$AdjustedProbability**를 기반으로 상위 *n* 개의 값을 반환 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 **PredictAssociation** 함수를 사용 하 여 함께 판매 될 가능성이 가장 높은 놀이 Works 데이터베이스의 4 개 제품을 반환 합니다.  
  
```  
SELECT  
  PredictAssociation([Association].[v Assoc Seq Line Items],4)  
From  
  [Association]  
```  
다음 예에서는 SHAPE 절을 사용 하 여 중첩 테이블을 예측 함수의 입력으로 사용할 수 있는 방법을 보여 줍니다. 셰이프 쿼리는 customerId가 있는 행 집합을 하나의 열로, 중첩 테이블을 두 번째 열로 만듭니다. 여기에는 고객이 이미 가져온 제품의 목록이 포함 됩니다. 

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

  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX &#40;함수&#41;](../dmx/functions-dmx.md)   
 [DMX&#41;일반 예측 함수 &#40;](../dmx/general-prediction-functions-dmx.md)  
  
  
