---
title: Lag (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0f984e50b2c6a800a66f689d88b21dfcb487e282
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38042831"
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
  
## <a name="remarks"></a>Remarks  
 경우는 **지연** 함수는 KEY TIME 열이 중첩된 테이블 내에 모델에는 문의 sub-select 내에 있어야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 모델의 학습에 사용된 데이터에 대한 지난 12개월 간 사례를 반환합니다.  
  
```  
SELECT * FROM [Forecasting].CASES  
WHERE Lag() < 12  
```  
  
## <a name="see-also"></a>관련 항목  
 [Data Mining Extensions &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [함수 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [일반 예측 함수 &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
