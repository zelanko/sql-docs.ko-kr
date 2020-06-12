---
title: Lag (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 04b06d1cbe14ee83915bd5626337720acf9bd2a9
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83670345"
---
# <a name="lag-dmx"></a>Lag(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  현재 사례의 날짜와 학습 집합의 마지막 날짜 간의 시간 조각을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Lag()  
```  
  
## <a name="return-type"></a>반환 형식  
 정수 형식의 스칼라 값  
  
## <a name="remarks"></a>설명  
 KEY TIME 열이 중첩 테이블 내에 있는 모델에서 **Lag** 함수를 사용 하는 경우이 함수는 문의 하위 select 내에 위치 해야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 모델의 학습에 사용된 데이터에 대한 지난 12개월 간 사례를 반환합니다.  
  
```  
SELECT * FROM [Forecasting].CASES  
WHERE Lag() < 12  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX &#40;함수&#41;](../dmx/functions-dmx.md)   
 [DMX&#41;일반 예측 함수 &#40;](../dmx/general-prediction-functions-dmx.md)  
  
  
