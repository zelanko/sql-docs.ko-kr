---
title: "데이터 형식 (데이터 마이닝) | Microsoft Docs"
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
ms.topic: article
helpviewer_keywords:
- data types [data mining]
- columns [data mining], data types
- data mining [Analysis Services], data types
ms.assetid: 4af5b7db-790b-459c-b2b4-00f0cf6b5ce4
caps.latest.revision: "47"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 275fddacc7d5d24be9581613863e81d2a061c92d
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="data-types-data-mining"></a>데이터 형식(데이터 마이닝)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]마이닝 모델 또는 마이닝 구조에 만들 때 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], 마이닝 구조에 열이 각각에 대 한 데이터 형식을 정의 해야 합니다. 데이터 형식은 분석 엔진에 데이터 원본의 데이터가 숫자인지 또는 텍스트인지 여부와 데이터 처리 방법을 알려 줍니다. 예를 들어 원본 데이터에 숫자 데이터가 포함되어 있는 경우 숫자를 정수로 처리할지, 아니면 소수 자릿수를 사용하여 처리할지 여부를 지정할 수 있습니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 마이닝 구조 열에 대해 다음과 같은 데이터 형식을 지원합니다.  
  
|데이터 형식|지원하는 내용 유형|  
|---------------|-----------------------------|  
|**텍스트**|Cyclical, Discrete, Discretized, Key Sequence, Ordered, Sequence|  
|**Long**|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Key Time, Ordered, Sequence, Time<br /><br /> Classified|  
|**Boolean**|Cyclical, Discrete, Ordered|  
|**Double**|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Key Time, Ordered, Sequence, Time<br /><br /> Classified|  
|**날짜**|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Key Time, Ordered|  
  
> [!NOTE]  
>  Time 및 Sequence 내용 유형은 타사 알고리즘에서만 지원됩니다. Cyclical 및 Ordered 내용 유형이 지원되기는 하지만 대부분의 알고리즘은 해당 유형을 불연속 값으로 처리하고 특수한 처리를 수행하지 않습니다.  
  
 표에서는 각 데이터 형식에 대해 지원되는 *콘텐츠 형식* 도 보여 줍니다.  
  
 콘텐츠 형식은 데이터 마이닝과 관련이 있으며, 마이닝 모델에서 데이터가 처리 또는 계산되는 방식을 사용자 지정할 수 있게 합니다. 예를 들어 열에 숫자가 들어 있는 경우 불연속 값으로 모델링해야 할 수도 있습니다. 열에 숫자가 들어 있는 경우 범주화 또는 불연속화되도록 지정하거나 모델에서 연속 값으로 처리되도록 지정할 수도 있습니다. 따라서 콘텐츠 형식은 모델에 큰 영향을 미칠 수 있습니다. 모든 콘텐츠 형식의 목록을 보려면 [콘텐츠 형식&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/content-types-data-mining.md)을 참조하세요.  
  
> [!NOTE]  
>  다른 기계 학습 시스템에서 *명목 데이터*, *요인* 또는 *범주*, *순차적 데이터*또는 *시퀀스 데이터*등의 용어를 발견할 수도 있습니다. 일반적으로 이러한 용어는 콘텐츠 형식에 해당합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터 형식은 저장을 위한 값 형식만 지정하고 모델에서의 사용법을 지정하지 않습니다.  
  
## <a name="specifying-a-data-type"></a>데이터 형식 지정  
 DMX(Data Mining Extensions)를 사용하여 직접 마이닝 모델을 만드는 경우 모델을 정의할 때 각 열에 대한 데이터 형식을 정의할 수 있으며 동시에 Analysis Services가 지정된 데이터 형식을 사용하여 해당되는 마이닝 구조를 만듭니다. 마법사를 사용하여 마이닝 모델 또는 마이닝 구조를 만드는 경우 Analysis Services에서 데이터 형식을 제안하거나 사용자가 목록에서 데이터 형식을 선택할 수 있습니다.  
  
## <a name="changing-a-data-type"></a>데이터 형식 변경  
 열의 데이터 형식을 변경하는 경우 항상 마이닝 구조 및 이 구조를 기반으로 하는 모든 마이닝 모델을 다시 처리해야 합니다. 데이터 형식을 변경하는 경우 특정 모델에서 해당 열을 더 이상 사용할 수 없는 경우가 있습니다. 이 경우 Analysis Services에서는 사용자가 모델을 다시 처리할 때 오류를 발생시키거나 모델을 처리하지만 해당 특정 열을 제외합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [콘텐츠 형식&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/content-types-data-mining.md)   
 [콘텐츠 형식&#40;DMX&#41;](../../dmx/content-types-dmx.md)   
 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [마이닝 구조&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [데이터 형식 &#40; DMX &#41;](../../dmx/data-types-dmx.md)   
 [마이닝 모델 열](../../analysis-services/data-mining/mining-model-columns.md)   
 [마이닝 구조 열](../../analysis-services/data-mining/mining-structure-columns.md)  
  
  
