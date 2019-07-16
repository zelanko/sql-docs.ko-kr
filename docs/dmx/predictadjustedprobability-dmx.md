---
title: PredictAdjustedProbability (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c2ae90886d6469802543f62bf5636ccaafeb32fb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008093"
---
# <a name="predictadjustedprobability-dmx"></a>PredictAdjustedProbability(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 상태에 대한 조정된 확률을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
PredictAdjustedProbability(<scalar column reference>, [<predicted state>])  
```  
  
## <a name="applies-to"></a>적용 대상  
 스칼라 열  
  
## <a name="return-type"></a>반환 형식  
 스칼라 값입니다.  
  
## <a name="remarks"></a>설명  
 예측 상태를 생략하면 누락된 상태 버킷을 제외하고 예측 가능성이 가장 높은 상태가 사용됩니다. 누락 된 상태 버킷을 포함 하려면 설정 합니다 \<예측 상태별 > 하 **INCLUDE_NULL**합니다.  
  
 누락 된 상태에 대 한 조정 된 확률을 반환 합니다 \<예측 상태별 > NULL로 합니다.  
  
 **PredictAdjustedProbability** 함수는를 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 확장을 [!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB for Data Mining 사양 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 자연 예측 조인을 사용하여 TM Decision Tree 마이닝 모델을 기반으로 개별 고객이 자전거를 구입할 가능성이 있는지 여부를 확인하고 예측의 조정된 확률도 확인합니다.  
  
```  
SELECT  
  [Bike Buyer],  
  PredictAdjustedProbability([Bike Buyer]) AS [Adjusted Probability]  
From  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>관련 항목  
 [Data Mining Extensions &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [함수 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [일반 예측 함수 &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
