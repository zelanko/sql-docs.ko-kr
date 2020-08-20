---
description: Lag(DMX)
title: Lag (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4e7aa504c3afd236ddd748a7ee81cbbb6cf90b7c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466576"
---
# <a name="lag-dmx"></a>Lag(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  현재 사례의 날짜와 학습 집합의 마지막 날짜 간의 시간 조각을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Lag()  
```  
  
## <a name="return-type"></a>반환 형식  
 정수 형식의 스칼라 값  
  
## <a name="remarks"></a>설명  
 KEY TIME 열이 중첩 테이블 내에 있는 모델에서 **Lag** 함수를 사용 하는 경우이 함수는 문의 하위 select 내에 위치 해야 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 모델의 학습에 사용된 데이터에 대한 지난 12개월 간 사례를 반환합니다.  
  
```  
SELECT * FROM [Forecasting].CASES  
WHERE Lag() < 12  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX &#40;함수&#41;](../dmx/functions-dmx.md)   
 [DMX&#41;일반 예측 함수 &#40;](../dmx/general-prediction-functions-dmx.md)  
  
  
