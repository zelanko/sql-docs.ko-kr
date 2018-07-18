---
title: PredictSequence (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 813641b7fa72405a0ba5a026e255f03feb94bd05
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37992475"
---
# <a name="predictsequence-dmx"></a>PredictSequence(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 시퀀스 데이터 집합에 대한 미래의 시퀀스 값을 예측합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
PredictSequence(<table column reference>)  
PredictSequence(\<table column reference, n>)  
PredictSequence(\<table column reference, n-start, n-end>)  
```  
  
## <a name="return-type"></a>반환 형식  
 \<테이블 식 >.  
  
## <a name="remarks"></a>Remarks  
 경우는 *n* 매개 변수가 지정 된 다음 값을 반환 합니다.  
  
-   하는 경우 *n* 가능성이 가장 높은 시퀀스 값 다음에 0 보다 크면 *n* 단계입니다.  
  
-   둘 다 *n 시작* 및 *n 엔드* 지정 된 시퀀스에서 값 *n 시작* 하 *n 엔드*합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Sequence Clustering 마이닝 모델을 기반으로 하는 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] 데이터베이스에서 고객이 구매할 가능성이 가장 높은 다섯 개의 제품 시퀀스를 반환합니다.  
  
```  
SELECT  
  PredictSequence([Sequence Clustering].[v Assoc Seq Line Items],5)  
From  
  [Sequence Clustering]  
```  
  
## <a name="see-also"></a>관련 항목  
 [Data Mining Extensions &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [함수 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [일반 예측 함수 &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
