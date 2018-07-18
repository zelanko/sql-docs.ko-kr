---
title: SELECT FROM &lt;모델&gt; (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: aac800e225eb5323b1bffeafda77d059f0a837e2
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37989905"
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
  
## <a name="remarks"></a>Remarks  
 열에는 *식 목록* 예측 또는 예측 전용으로 정의 하거나 관련 예측 가능한 열을 해야 합니다.  
  
## <a name="naive-bayes-example"></a>Naive Bayes 예  
 다음 예에서는 Bike Buyer 열에 빈 예측 조인을 수행하고 TM Naive Bayes 마이닝 모델에서 가장 가능성이 높은 상태를 반환합니다.  
  
```  
SELECT ([Bike Buyer]) FROM [TM_Naive_Bayes]  
```  
  
## <a name="time-series-example"></a>시계열 예  
 다음 예에서는 Forecasting 모델의 Amount 열에 예측을 수행하고 다음 네 단계를 반환합니다. Model Region 열은 자전거 모델과 지역을 단일 식별자로 결합합니다. 쿼리를 사용 합니다 [PredictTimeSeries &#40;DMX&#41; ](../dmx/predicttimeseries-dmx.md) 예측을 수행 하는 함수입니다.  
  
```  
SELECT [Model Region], PredictTimeSeries(Amount, 4)   
FROM Forecasting  
```  
  
## <a name="see-also"></a>관련 항목  
 [선택 &AMP;#40;DMX&AMP;#41;](../dmx/select-dmx.md)   
 [Data Mining Extensions &#40;DMX&#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [Data Mining Extensions &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [DMX&#40;Data Mining Extensions&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
