---
title: 열 배포 (데이터 마이닝) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
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
ms.openlocfilehash: 6c7eab32f251b9622c6ac77febf2c004806c024b
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78174629"
---
# <a name="column-distributions-data-mining"></a>열 배포(데이터 마이닝)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]마이닝 구조에서 열 배포를 정의 하 여 마이닝 모델을 만들 때 알고리즘이 이러한 열의 데이터를 처리 하는 방법에 영향을 줄 수 있습니다. 이렇게 하면 공통적인 값 배포가 열에 포함되어 있을 경우 모델을 처리하기 전에 몇몇 알고리즘에서 연속 열 배포를 정의하는 데 도움이 됩니다. 배포를 정의하지 않으면 알고리즘이 데이터를 해석하는 데 사용할 정보가 더 줄어듭니다. 따라서 마이닝 모델에서 얻는 예측의 정확도가 배포를 정의했을 경우보다 낮아질 수 있습니다.

 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 사용 가능한 알고리즘은 다음 배포 유형을 지원합니다.

 `Normal`연속 열에 대 한 값은 정규 분포를 사용 하는 히스토그램을 형성 합니다.

 ![정규 분포를 보여 주는 히스토그램](../media/normal-distribution.gif "정규 분포를 보여 주는 히스토그램")

 `Log Normal`연속 열에 대 한 값은 히스토그램을 형성 합니다. 여기서 곡선이 위쪽 끝에 곡선은 늘어나고 곡선은 아래쪽 끝에 기울어집니다.

 ![로그 정규 분포를 보여 주는 히스토그램](../media/log-normal-distribution.gif "로그 정규 분포를 보여 주는 히스토그램")

 `Uniform`연속 열에 대 한 값은 모든 값이 동일 하 게 될 가능성이 있는 플랫 곡선을 형성 합니다.

 ![균일한 분포를 보여 주는 히스토그램](../media/uniform-distribution.gif "균일한 분포를 보여 주는 히스토그램")

 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 제공하는 알고리즘에 대한 자세한 내용은 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](data-mining-algorithms-analysis-services-data-mining.md)을 참조하세요.

## <a name="see-also"></a>참고 항목
 [콘텐츠 형식 &#40;데이터 마이닝&#41;](content-types-data-mining.md) [마이닝 구조 &#40;Analysis Services 데이터](mining-structures-analysis-services-data-mining.md) 마이닝&#41;분할 메서드 &#40;[DMX](/sql/dmx/distributions-dmx)&#41;[마이닝 구조 열](mining-structure-columns.md) &#40;데이터 마이닝&#41;분할 [방법](discretization-methods-data-mining.md)


