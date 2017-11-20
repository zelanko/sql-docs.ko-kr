---
title: "SELECT FROM &lt;모델&gt; (DMX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SELECT
- FROM
dev_langs:
- DMX
helpviewer_keywords:
- empty prediction joins [DMX]
- SELECT FROM <model> statement
ms.assetid: dc5b9a01-e308-4ee8-84fc-ba4b991c60aa
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c51d5d3f3a5a1c8e9b94f72367739d592f1918c8
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="select-from-ltmodelgt-dmx"></a>SELECT FROM &lt;모델&gt; (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  빈 예측 조인을 수행하며 지정한 열에 대해 가장 가능성이 높은 값을 반환합니다. 예측을 만드는 데는 마이닝 모델의 콘텐츠만 사용됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SELECT <expression list> [TOP <n>] FROM <model>   
[WHERE <condition list>]   
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>인수  
 *식 목록*  
 식, 예측 열 또는 예측 전용 열의 쉼표로 구분된 목록입니다.  
  
 *n*  
 (선택 사항) 반환할 행의 수를 지정하는 정수입니다.  
  
 *모델*  
 모델 식별자입니다.  
  
 *조건 목록*  
 (선택 사항) 열 목록에서 반환되는 값을 제한하는 조건입니다.  
  
 *expression*  
 (선택 사항) 스칼라 값을 반환하는 식입니다.  
  
## <a name="remarks"></a>주의  
 열에는 *식 목록* 예측 또는 예측 전용으로 정의 된 또는 예측 가능한 열에 관련 해야 합니다.  
  
## <a name="naive-bayes-example"></a>Naive Bayes 예  
 다음 예에서는 Bike Buyer 열에 빈 예측 조인을 수행하고 TM Naive Bayes 마이닝 모델에서 가장 가능성이 높은 상태를 반환합니다.  
  
```  
SELECT ([Bike Buyer]) FROM [TM_Naive_Bayes]  
```  
  
## <a name="time-series-example"></a>시계열 예  
 다음 예에서는 Forecasting 모델의 Amount 열에 예측을 수행하고 다음 네 단계를 반환합니다. Model Region 열은 자전거 모델과 지역을 단일 식별자로 결합합니다. 쿼리에서 [PredictTimeSeries &#40; DMX &#41;](../dmx/predicttimeseries-dmx.md) 예측을 수행 하는 함수입니다.  
  
```  
SELECT [Model Region], PredictTimeSeries(Amount, 4)   
FROM Forecasting  
```  
  
## <a name="see-also"></a>참고 항목  
 [SELECT&#40; DMX &#41;](../dmx/select-dmx.md)   
 [Data Mining Extensions &#40; DMX &#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [Data Mining Extensions &#40; DMX &#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [Data Mining Extensions &#40; DMX &#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

