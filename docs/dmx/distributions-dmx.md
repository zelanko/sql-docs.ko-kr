---
title: 배포 (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 535d1caff3729b552ef0982b056eb516b8f23048
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669769"
---
# <a name="distributions-dmx"></a>배포(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  에서는 마이닝 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 구조의 열 내용을 정의 하 여 마이닝 모델을 만들 때 알고리즘이 이러한 열의 데이터를 처리 하는 방법에 영향을 줄 수 있습니다. 이렇게 하면 공통적인 값 배포가 열에 포함되어 있을 경우 모델을 처리하기 전에 몇몇 알고리즘에서 연속 열 배포를 정의하는 데 도움이 됩니다. 배포를 정의하지 않으면 알고리즘이 데이터를 해석하는 데 사용할 정보가 더 줄어듭니다. 따라서 마이닝 모델에서 얻는 예측의 정확도가 배포를 정의했을 경우보다 낮아질 수 있습니다.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] 데이터 마이닝 알고리즘에서는 다음 배포 유형을 지원합니다.  
  
 **일반적**  
 연속 열에 대한 값은 정규 가우스 분포로 된 히스토그램을 형성합니다.  
  
 **Log Normal**  
 연속 열에 대한 값은 값 로그가 정상적으로 분포된 히스토그램을 형성합니다.  
  
 **균일**  
 연속 열에 대한 값은 모든 값이 균일한 평탄 곡선을 형성합니다.  
  
 데이터 마이닝 알고리즘에 대 한 자세한 내용은 데이터 마이닝 [!INCLUDE[msCoName](../includes/msconame-md.md)] [알고리즘 &#40;Analysis Services 데이터 마이닝&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)을 참조 하십시오. 타사 알고리즘 공급자가 추가 배포 유형을 지원할 수 있습니다. 알고리즘에서 지 원하는 배포 유형을 확인 하려면 **SUPPORTED_DISTRIBUTION_FLAGS** 스키마 행 집합을 사용 합니다.  
  
 배포 유형에 대 한 자세한 내용은 [열 배포 &#40;데이터 마이닝&#41;](https://docs.microsoft.com/analysis-services/data-mining/column-distributions-data-mining)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝&#41;&#40;내용 유형](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining)   
 [DMX&#41; 참조 &#40;데이터 마이닝 확장](../dmx/data-mining-extensions-dmx-reference.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 구문 요소](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 구문 규칙](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [DMX&#41;일반 예측 함수 &#40;](../dmx/general-prediction-functions-dmx.md)   
 [DMX 예측 쿼리의 구조 및 사용법](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX Select 문 이해](../dmx/understanding-the-dmx-select-statement.md)  
  
  
