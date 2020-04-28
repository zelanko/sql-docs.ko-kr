---
title: 모델&gt; 에서 &lt;선택 (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5611ce3da4f12bca5cb271cabe8af3e149dcbf35
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67928322"
---
# <a name="select-from-ltmodelgt-dmx"></a>모델&gt; 에서 &lt;선택 (DMX)
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
 선택 사항입니다. 반환할 행의 수를 지정하는 정수입니다.  
  
 *모델링*  
 모델 식별자입니다.  
  
 *조건 목록*  
 선택 사항입니다. 열 목록에서 반환되는 값을 제한하는 조건입니다.  
  
 *expression*  
 선택 사항입니다. 스칼라 값을 반환하는 식입니다.  
  
## <a name="remarks"></a>설명  
 *식 목록의* 열은 예측 또는 예측 전용으로 정의 하거나 예측 가능한 열과 관련 되어야 합니다.  
  
## <a name="naive-bayes-example"></a>Naive Bayes 예  
 다음 예에서는 Bike Buyer 열에 빈 예측 조인을 수행하고 TM Naive Bayes 마이닝 모델에서 가장 가능성이 높은 상태를 반환합니다.  
  
```  
SELECT ([Bike Buyer]) FROM [TM_Naive_Bayes]  
```  
  
## <a name="time-series-example"></a>시계열 예  
 다음 예에서는 Forecasting 모델의 Amount 열에 예측을 수행하고 다음 네 단계를 반환합니다. Model Region 열은 자전거 모델과 지역을 단일 식별자로 결합합니다. 이 쿼리에서는 [PredictTimeSeries &#40;DMX&#41;](../dmx/predicttimeseries-dmx.md) 함수를 사용 하 여 예측을 수행 합니다.  
  
```  
SELECT [Model Region], PredictTimeSeries(Amount, 4)   
FROM Forecasting  
```  
  
## <a name="see-also"></a>참고 항목  
 [DMX &#40;선택&#41;](../dmx/select-dmx.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [DMX&#40;Data Mining Extensions&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
