---
title: "분류 열 (데이터 마이닝) | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- content types [data mining]
- STDEV column
- VARIANCE column
- PROBABLILITY column
- PROBABILITY_STDEV column
- columns [data mining], classified
- classified columns [data mining]
- PROBABILITY_VARIANCE column
- SUPPORT column
ms.assetid: 68bf3b78-dc12-497c-898f-b43a45646123
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d114c3495c213e5493e3ccb87c1201d0517e4edf
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="classified-columns-data-mining"></a>분류된 열(데이터 마이닝)
  분류된 열을 정의할 경우 마이닝 구조의 현재 열과 다른 열 간에 관계를 생성하게 됩니다. 분류된 열로 지정한 마이닝 구조 열의 데이터에는 마이닝 구조의 다른 열의 값을 설명하는 범주 정보가 포함됩니다.  
  
 예를 들어 숫자 데이터를 포함하는 두 개의 열이 있다고 가정합니다. [Yearly Purchases] 열에는 특정 달력 연도의 고객당 연간 총 구매액에 들어 있고, 다른 열인 [Standard Deviations] 열에는 그러한 값에 대한 표준 편차가 들어 있습니다. 이 경우 [Yearly Purchases] 열을 분류된 열로 지정할 수 있으며 그러면 모델에서 분석에 이 관계를 사용할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 제공하는 알고리즘은 분류된 열의 사용을 지원하지 않습니다. 이 기능은 사용자 지정 알고리즘을 만드는 데 사용하기 위해 제공됩니다.  
  
## <a name="defining-a-classified-column"></a>분류된 열 정의  
 분류된 열의 데이터 형식은 **Long** 또는 **Double**중 하나여야 합니다.  
  
 다음 목록에서는 분류된 열에 대해 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 지원하는 내용 유형을 설명합니다.  
  
 **PROBABILITY**  
 이 열의 값은 관련 값의 확률이며 0에서 1 사이의 수입니다.  
  
 **VARIANCE**  
 이 열의 값은 관련 값의 분산입니다.  
  
 **STDEV**  
 이 열의 값은 관련 값의 표준 편차입니다.  
  
 **PROBABILITY_VARIANCE**  
 이 열의 값은 관련 값에 대한 확률의 분산입니다.  
  
 **PROBABILITY_STDEV**  
 이 열의 값은 관련 값에 대한 확률의 표준 편차입니다.  
  
 **별칭**  
 이 열의 값은 관련 값의 가중치 또는 사례 복제 요소입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [콘텐츠 형식&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/content-types-data-mining.md)   
 [마이닝 구조&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [데이터 형식&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/data-types-data-mining.md)  
  
  
