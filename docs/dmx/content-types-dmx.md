---
title: 콘텐츠 형식 (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9a0c44e0ea90b253cee5564a327d49c34c1ae78a
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969897"
---
# <a name="content-types-dmx"></a>내용 유형(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  데이터 마이닝 알고리즘에는 데이터 형식이 올바르게 작동하는 것 외에도 내용 유형과 같은 추가 정보가 필요로 합니다. 내용 유형은 알고리즘에서 열의 데이터를 사용하는 방법을 결정하는 데 도움을 줍니다.  
  
 각 알고리즘마다 특정한 내용 유형을 지원합니다. 예를 들어 [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes 알고리즘에서는 연속 열을 사용할 수 없습니다. [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes 모델에서 연속 열을 사용하려면 열의 데이터를 불연속화해야 합니다. 일부 알고리즘이 올바르게 실행되기 위해서는 특정한 내용 유형이 필요합니다. 예를 들어 [!INCLUDE[msCoName](../includes/msconame-md.md)] 시계열 알고리즘에서는 데이터가 수집된 시간을 식별하기 위한 Key Time 열이 필요합니다.  
  
 에서 지 원하는 콘텐츠 형식에 대 한 자세한 설명은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] [데이터 마이닝&#41;&#40;콘텐츠 형식 ](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining)을 참조 하세요.  
  
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
  
  
