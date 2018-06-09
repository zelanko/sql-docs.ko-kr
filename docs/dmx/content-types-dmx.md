---
title: 콘텐츠 형식 (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 002dfef00f428f7fe87f3de06eb174e0566282c7
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34842896"
---
# <a name="content-types-dmx"></a>내용 유형(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  데이터 마이닝 알고리즘에는 데이터 형식이 올바르게 작동하는 것 외에도 내용 유형과 같은 추가 정보가 필요로 합니다. 내용 유형은 알고리즘에서 열의 데이터를 사용하는 방법을 결정하는 데 도움을 줍니다.  
  
 각 알고리즘마다 특정한 내용 유형을 지원합니다. 예를 들어 [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes 알고리즘에서는 연속 열을 사용할 수 없습니다. [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes 모델에서 연속 열을 사용하려면 열의 데이터를 불연속화해야 합니다. 일부 알고리즘이 올바르게 실행되기 위해서는 특정한 내용 유형이 필요합니다. 예를 들어 [!INCLUDE[msCoName](../includes/msconame-md.md)] 시계열 알고리즘에서는 데이터가 수집된 시간을 식별하기 위한 Key Time 열이 필요합니다.  
  
 전체 설명은 콘텐츠 형식에 대해 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 지 원하는 참조 [콘텐츠 형식 &#40;데이터 마이닝&#41;](../analysis-services/data-mining/content-types-data-mining.md)합니다.  
  
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
  
  
