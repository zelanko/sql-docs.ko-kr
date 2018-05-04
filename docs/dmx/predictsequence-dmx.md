---
title: PredictSequence (DMX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PredictSequence
dev_langs:
- DMX
helpviewer_keywords:
- PredictSequence function
ms.assetid: c2992dfc-b99d-4430-8dcd-21ad3ffd4590
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: b8ef0b3f0ba361e368695b31d15b26cd013ed6e8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
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
 A \<테이블 식 > 합니다.  
  
## <a name="remarks"></a>주의  
 경우는 *n* 매개 변수가 지정 된, 다음 값을 반환 합니다.  
  
-   경우 *n* 0, 다음의 가장 가능성이 높은 시퀀스 값 보다 크면 *n* 단계입니다.  
  
-   두 *n 시작* 및 *n 간* 지정 된 시퀀스에서 값 *n 시작* 를 *n 엔드*합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Sequence Clustering 마이닝 모델을 기반으로 하는 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] 데이터베이스에서 고객이 구매할 가능성이 가장 높은 다섯 개의 제품 시퀀스를 반환합니다.  
  
```  
SELECT  
  PredictSequence([Sequence Clustering].[v Assoc Seq Line Items],5)  
From  
  [Sequence Clustering]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Data Mining Extensions &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [함수 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [일반 예측 함수 &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
