---
title: Lag (DMX) | Microsoft Docs
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
f1_keywords: LAG
dev_langs: DMX
helpviewer_keywords: Lag function
ms.assetid: 2da6df1a-5506-4871-a0f0-83292f1df41e
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 91c86f45191c9e68774d2a787499a169de8d919c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
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
  
## <a name="remarks"></a>주의  
 경우는 **지연** 함수 사용 되는 KEY TIME 열이 중첩된 테이블 내에 모델에 대해 함수는 문의 sub-select 내에 있어야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 모델의 학습에 사용된 데이터에 대한 지난 12개월 간 사례를 반환합니다.  
  
```  
SELECT * FROM [Forecasting].CASES  
WHERE Lag() < 12  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Data Mining Extensions &#40; DMX &#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [함수 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [일반 예측 함수 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
