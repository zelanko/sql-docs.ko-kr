---
title: 데이터 형식 (데이터 마이닝) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data types [data mining]
- columns [data mining], data types
- data mining [Analysis Services], data types
ms.assetid: 4af5b7db-790b-459c-b2b4-00f0cf6b5ce4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 77a0c6f2f0100e7e0c0e73ee70bc8705135d259f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62722815"
---
# <a name="data-types-data-mining"></a>데이터 형식(데이터 마이닝)
   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 마이닝 모델 또는 마이닝 구조를 만들 때는 마이닝 구조의 각 열에 대한 데이터 형식을 정의해야 합니다. 데이터 형식은 데이터 마이닝 엔진에게 데이터 원본의 데이터가 숫자인지, 아니면 텍스트인지 여부와 데이터 처리 방법을 알려 줍니다. 예를 들어 원본 데이터에 숫자 데이터가 포함되어 있는 경우 숫자를 정수로 처리할지, 아니면 소수 자릿수를 사용하여 처리할지 여부를 지정할 수 있습니다.  
  
 각 데이터 형식은 하나 이상의 내용 유형을 지원합니다. 내용 유형을 설정하여 마이닝 모델에서 열의 데이터를 처리하거나 계산하는 방법을 사용자 지정할 수 있습니다.  
  
 예를 들어 열에 숫자 데이터가 있는 경우 해당 데이터를 숫자 데이터 형식 또는 텍스트 데이터 형식으로 처리하도록 선택할 수 있습니다. 숫자 데이터 형식을 선택하는 경우 여러 개의 서로 다른 내용 유형을 설정할 수 있습니다. 즉, 숫자를 분할하거나 숫자를 연속 값으로 처리할 수 있습니다. 모든 콘텐츠 형식의 목록을 보려면 [콘텐츠 형식&#40;데이터 마이닝&#41;](content-types-data-mining.md)을 참조하세요.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 마이닝 구조 열에 대해 다음과 같은 데이터 형식을 지원합니다.  
  
|데이터 형식|지원하는 내용 유형|  
|---------------|-----------------------------|  
|`Text`|Cyclical, Discrete, Discretized, Key Sequence, Ordered, Sequence|  
|`Long`|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Key Time, Ordered, Sequence, Time<br /><br /> Classified|  
|`Boolean`|Cyclical, Discrete, Ordered|  
|`Double`|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Key Time, Ordered, Sequence, Time<br /><br /> Classified|  
|`Date`|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Key Time, Ordered|  
  
> [!NOTE]  
>  Time 및 Sequence 내용 유형은 타사 알고리즘에서만 지원됩니다. Cyclical 및 Ordered 내용 유형이 지원되기는 하지만 대부분의 알고리즘은 해당 유형을 불연속 값으로 처리하고 특수한 처리를 수행하지 않습니다.  
  
## <a name="specifying-a-data-type"></a>데이터 형식 지정  
 DMX(Data Mining Extensions)를 사용하여 직접 마이닝 모델을 만드는 경우 모델을 정의할 때 각 열에 대한 데이터 형식을 정의할 수 있으며 동시에 Analysis Services가 지정된 데이터 형식을 사용하여 해당되는 마이닝 구조를 만듭니다. 마법사를 사용하여 마이닝 모델 또는 마이닝 구조를 만드는 경우 Analysis Services에서 데이터 형식을 제안하거나 사용자가 목록에서 데이터 형식을 선택할 수 있습니다.  
  
## <a name="changing-a-data-type"></a>데이터 형식 변경  
 열의 데이터 형식을 변경하는 경우 항상 마이닝 구조 및 이 구조를 기반으로 하는 모든 마이닝 모델을 다시 처리해야 합니다. 데이터 형식을 변경하는 경우 특정 모델에서 해당 열을 더 이상 사용할 수 없는 경우가 있습니다. 이 경우 Analysis Services에서는 사용자가 모델을 다시 처리할 때 오류를 발생시키거나 모델을 처리하지만 해당 특정 열을 제외합니다.  
  
## <a name="see-also"></a>관련 항목  
 [콘텐츠 형식&#40;데이터 마이닝&#41;](content-types-data-mining.md)   
 [콘텐츠 형식&#40;DMX&#41;](/sql/dmx/content-types-dmx)   
 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [마이닝 구조 & #40; Analysis Services-데이터 마이닝 & #41;](mining-structures-analysis-services-data-mining.md)   
 [데이터 형식&#40;DMX&#41;](/sql/dmx/data-types-dmx)   
 [마이닝 모델 열](mining-model-columns.md)   
 [마이닝 구조 열](mining-structure-columns.md)  
  
  
