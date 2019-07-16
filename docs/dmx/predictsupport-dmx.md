---
title: PredictSupport (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: efe9fb0222dc745e48c248214c42ce706ea18d89
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041876"
---
# <a name="predictsupport-dmx"></a>PredictSupport(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 상태에 대한 지원 값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
PredictSupport(<scalar column reference>, [<predicted state>])  
```  
  
## <a name="applies-to"></a>적용 대상  
 스칼라 열  
  
## <a name="return-type"></a>반환 형식  
 지정 된 유형의 스칼라 값을 *\<* 스칼라 열 참조 *>* 합니다.  
  
## <a name="remarks"></a>설명  
 예측 상태를 생략하면 누락된 상태 버킷을 제외하고 예측 가능성이 가장 높은 상태가 사용됩니다. 누락 된 상태 버킷을 포함 하려면 설정 합니다 \<예측 상태별 > 하 **INCLUDE_NULL**합니다.  
  
 누락 된 상태에 대 한 지원을 반환 된 \<예측 상태별 > NULL로 합니다.  
  
> [!NOTE]  
>  쿼리하는 모델 유형에 따라 지원 값이 다르게 계산되거나 다르게 해석될 수 있습니다. 특정 모델 유형에 지원 계산 되는 방식에 대 한 자세한 내용은 개별 알고리즘에서 입력을 참조 하세요 [마이닝 모델 콘텐츠 &#40;Analysis Services-데이터 마이닝&#41;](../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 단일 쿼리를 사용하여 개별 고객이 자전거를 구입할 가능성이 있는지 여부를 예측하고 TM Decision Tree 마이닝 모델을 기반으로 하는 예측을 지원하는지 여부를 확인합니다.  
  
```  
SELECT  
  [Bike Buyer],  
  PredictSupport([Bike Buyer]) AS [Support],  
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
  
  
