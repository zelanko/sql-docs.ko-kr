---
title: "배포 (DMX) | Microsoft Docs"
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
dev_langs: DMX
helpviewer_keywords:
- column distributions [DMX]
- distributions [DMX]
- DMX [Analysis Services], distributions
- Data Mining Extensions [Analysis Services], distributions
ms.assetid: cfbb9f38-ae71-401e-867f-15c6a2b6fb97
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 8d56f7ed56349f57484aa39511b1ab86607f4508
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="distributions-dmx"></a>배포(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], 마이닝 모델을 만들 때 알고리즘의 열 데이터를 처리 하는 방법에 마이닝 구조에 열의 콘텐츠를 정의할 수 있습니다. 이렇게 하면 공통적인 값 배포가 열에 포함되어 있을 경우 모델을 처리하기 전에 몇몇 알고리즘에서 연속 열 배포를 정의하는 데 도움이 됩니다. 배포를 정의하지 않으면 알고리즘이 데이터를 해석하는 데 사용할 정보가 더 줄어듭니다. 따라서 마이닝 모델에서 얻는 예측의 정확도가 배포를 정의했을 경우보다 낮아질 수 있습니다.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] 데이터 마이닝 알고리즘에서는 다음 배포 유형을 지원합니다.  
  
 **보통**  
 연속 열에 대한 값은 정규 가우스 분포로 된 히스토그램을 형성합니다.  
  
 **Log Normal**  
 연속 열에 대한 값은 값 로그가 정상적으로 분포된 히스토그램을 형성합니다.  
  
 **균일 한**  
 연속 열에 대한 값은 모든 값이 균일한 평탄 곡선을 형성합니다.  
  
 에 대 한 자세한 내용은 [!INCLUDE[msCoName](../includes/msconame-md.md)] 데이터 마이닝 알고리즘 참조 [데이터 마이닝 알고리즘 &#40; Analysis Services-데이터 마이닝 &#41; ](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md). 타사 알고리즘 공급자가 추가 배포 유형을 지원할 수 있습니다. 지 원하는 배포 하는 알고리즘 유형을 확인 하려면, 사용 된 **SUPPORTED_DISTRIBUTION_FLAGS** 스키마 행 집합입니다.  
  
 배포 유형에 대 한 자세한 내용은 참조 하십시오. [열 배포 &#40; 데이터 마이닝 속성 &#41;](../analysis-services/data-mining/column-distributions-data-mining.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [콘텐츠 형식 &#40; 데이터 마이닝 &#41;](../analysis-services/data-mining/content-types-data-mining.md)   
 [Data Mining Extensions &#40; DMX &#41; 참조](../dmx/data-mining-extensions-dmx-reference.md)   
 [Data Mining Extensions &#40; DMX &#41; 구문 요소](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Data Mining Extensions &#40; DMX &#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Data Mining Extensions &#40; DMX &#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Data Mining Extensions &#40; DMX &#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [Data Mining Extensions &#40; DMX &#41; 구문 표기 규칙](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [일반 예측 함수 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [구조 및 DMX 예측 쿼리 사용](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX Select 문 이해](../dmx/understanding-the-dmx-select-statement.md)  
  
  
