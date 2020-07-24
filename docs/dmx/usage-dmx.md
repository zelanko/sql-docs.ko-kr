---
title: 사용량 (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cdbefcfeb6d638998ec2e0a01b8da5ca40f2aeaf
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86971576"
---
# <a name="usage-dmx"></a>사용법(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  DMX (데이터 마이닝 확장)를 사용 하 여에서 새 데이터 마이닝 모델을 정의 하는 경우 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 모델을 작성 하는 데이터 마이닝 알고리즘에서 각 열을 사용 하는 방법을 지정 해야 합니다. 다음 유형 중 하나로 열을 지정할 수 있습니다.  
  
-   **Key**  
  
-   **키 시퀀스**  
  
-   **Key Time**  
  
-   **예측**  
  
-   **PredictOnly**  
  
 DMX에서 지정되지 않은 상태로 남아 있는 열은 입력 열로 처리됩니다.  
  
 모델을 올바르게 처리하려면 각 행을 고유하게 식별하는 키 열, 예측 가능한 모델을 만드는 경우 예측을 만들 대상 열, 그리고 대상 열을 예측하는 관계를 만들기 위해 입력 열로 사용할 열을 알고리즘에서 파악해야 합니다.  
  
 **Predict** 유형으로 지정 된 열은 입력 및 출력 열 모두로 사용 됩니다. **Predictonly** 로 지정 된 열은 출력 열로만 사용 됩니다. 특정 알고리즘에서는 Predict 열을 다른 방식으로 처리할 수 있습니다.  
  
 에서 지 원하는 열 사용 유형에 대 한 자세한 내용은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] [마이닝 모델 열](https://docs.microsoft.com/analysis-services/data-mining/mining-model-columns)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 알고리즘 &#40;Analysis Services 데이터 마이닝&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [DMX&#41; 참조 &#40;데이터 마이닝 확장](../dmx/data-mining-extensions-dmx-reference.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 구문 요소](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 구문 규칙](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [DMX&#41;일반 예측 함수 &#40;](../dmx/general-prediction-functions-dmx.md)   
 [DMX 예측 쿼리의 구조 및 사용법](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX Select 문 이해](../dmx/understanding-the-dmx-select-statement.md)  
  
  
