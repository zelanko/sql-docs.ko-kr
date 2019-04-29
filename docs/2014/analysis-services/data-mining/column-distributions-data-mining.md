---
title: 열 배포 (데이터 마이닝) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- normal distribution type [data mining]
- uniform distribution type [data mining]
- columns [data mining], distributions
- log normal distribution type [data mining]
- continuous columns
- distributions [data mining]
ms.assetid: 87e700de-32be-4bc8-b01d-ba4ee1ab48de
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0a4969e3665aca4ed5aef588fa9595e96b846e98
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62715429"
---
# <a name="column-distributions-data-mining"></a>열 배포(데이터 마이닝)
   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 마이닝 구조의 열 배포를 정의한 다음 마이닝 모델을 만들 때 알고리즘의 열 데이터 처리 방법에 정의 내용을 적용할 수 있습니다. 이렇게 하면 공통적인 값 배포가 열에 포함되어 있을 경우 모델을 처리하기 전에 몇몇 알고리즘에서 연속 열 배포를 정의하는 데 도움이 됩니다. 배포를 정의하지 않으면 알고리즘이 데이터를 해석하는 데 사용할 정보가 더 줄어듭니다. 따라서 마이닝 모델에서 얻는 예측의 정확도가 배포를 정의했을 경우보다 낮아질 수 있습니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 사용 가능한 알고리즘은 다음 배포 유형을 지원합니다.  
  
 `Normal`  
 연속 열 값이 정규 분포로 된 히스토그램을 형성합니다.  
  
 ![정규 분포를 보여 주는 히스토그램](../media/normal-distribution.gif "정규 분포를 보여 주는 히스토그램")  
  
 `Log Normal`  
 연속 열 값이 위쪽 끝 곡선은 늘어나고 아래쪽 끝 곡선은 기울어진 히스토그램을 형성합니다.  
  
 ![로그 정규 분포를 보여 주는 히스토그램](../media/log-normal-distribution.gif "로그 정규 분포를 보여 주는 히스토그램")  
  
 `Uniform`  
 연속 열에 대한 값은 모든 값이 균일한 평탄 곡선을 형성합니다.  
  
 ![균일 한 분포를 보여 주는 히스토그램](../media/uniform-distribution.gif "균일 한 분포를 보여 주는 히스토그램")  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 제공하는 알고리즘에 대한 자세한 내용은 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](data-mining-algorithms-analysis-services-data-mining.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [콘텐츠 형식&#40;데이터 마이닝&#41;](content-types-data-mining.md)   
 [마이닝 구조&#40;Analysis Services - 데이터 마이닝&#41;](mining-structures-analysis-services-data-mining.md)   
 [분할 메서드&#40;데이터 마이닝&#41;](discretization-methods-data-mining.md)   
 [배포&#40;DMX&#41;](/sql/dmx/distributions-dmx)   
 [마이닝 구조 열](mining-structure-columns.md)  
  
  
