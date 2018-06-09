---
title: 사용법 (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 459d6a0240ac2588c0924eae7bdae348a71f5946
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34841436"
---
# <a name="usage-dmx"></a>사용법(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  새 데이터 마이닝 모델을 정의 하 확장 DMX (Data Mining)를 사용 하면 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], 모델을 작성 하는 데이터 마이닝 알고리즘은 각 열을 사용 하는 방법을 지정 해야 합니다. 다음 유형 중 하나로 열을 지정할 수 있습니다.  
  
-   **Key**  
  
-   **키 시퀀스**  
  
-   **Key Time**  
  
-   **Predict**  
  
-   **PredictOnly**  
  
 DMX에서 지정되지 않은 상태로 남아 있는 열은 입력 열로 처리됩니다.  
  
 모델을 올바르게 처리하려면 각 행을 고유하게 식별하는 키 열, 예측 가능한 모델을 만드는 경우 예측을 만들 대상 열, 그리고 대상 열을 예측하는 관계를 만들기 위해 입력 열로 사용할 열을 알고리즘에서 파악해야 합니다.  
  
 로 지정 된 열은 **Predict** 유형 입력 및 출력 열으로 사용 됩니다. 로 지정 된 열 **PredictOnly** 출력 열으로만 사용 됩니다. 특정 알고리즘에서는 Predict 열을 다른 방식으로 처리할 수 있습니다.  
  
 열에 대 한 자세한 내용은 사용 하는 유형에 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 지 원하는 참조 [마이닝 모델 열](../analysis-services/data-mining/mining-model-columns.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 알고리즘 &#40;Analysis Services-데이터 마이닝&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Data Mining Extensions &#40;DMX&#41; 참조](../dmx/data-mining-extensions-dmx-reference.md)   
 [Data Mining Extensions &#40;DMX&#41; 구문 요소](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Data Mining Extensions &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Data Mining Extensions &#40;DMX&#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Data Mining Extensions &#40;DMX&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [Data Mining Extensions &#40;DMX&#41; 구문 표기 규칙](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [일반 예측 함수 &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [구조 및 DMX 예측 쿼리 사용](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX Select 문 이해](../dmx/understanding-the-dmx-select-statement.md)  
  
  
