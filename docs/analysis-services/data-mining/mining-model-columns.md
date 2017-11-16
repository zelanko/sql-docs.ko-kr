---
title: "마이닝 모델 열 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- columns [data mining], mining model columns
- columns [data mining]
- REGRESSOR column
- columns [data mining], modeling flags
- modeling flags [data mining]
- MODEL_EXISTENCE_ONLY column
- usage property [data mining]
ms.assetid: fab47643-5bfd-424e-a0f7-69e665db6bab
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e2691f87c4ded8d2e9f00e4390681c936591bc83
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="mining-model-columns"></a>마이닝 모델 열
  데이터 마이닝 모델은 마이닝 구조가 나타나는 데이터에 마이닝 모델 알고리즘을 적용합니다. 마이닝 구조와 마찬가지로 마이닝 모델에는 열이 포함됩니다. 마이닝 모델은 마이닝 구조 내에 포함되며 마이닝 구조에서 정의한 속성의 모든 값을 상속받습니다. 모델은 마이닝 구조에 포함된 모든 열이나 이 열의 하위 집합을 사용할 수 있습니다.  
  
 마이닝 모델 열에는 사용법 및 모델링 플래그 정보를 추가로 정의할 수 있습니다.  
  
-   **사용법** 은 모델이 열을 사용하는 방법을 정의하는 속성입니다. 열은 입력 열, 키 열 또는 예측 가능한 열로 사용될 수 있습니다.  
  
-   **모델링 플래그** 는 사례 테이블에 정의된 데이터에 대한 추가 정보를 알고리즘에 제공하므로 알고리즘이 보다 정확한 모델을 작성할 수 있습니다. 모델링 플래그는 DMX(Data Mining Extensions) 언어를 사용하여 프로그래밍 방식으로 정의하거나 **의** 데이터 마이닝 디자이너 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 정의할 수 있습니다.  
  
 다음 목록에서는 마이닝 모델 열에 정의할 수 있는 모델링 플래그를 설명합니다.  
  
 **MODEL_EXISTENCE_ONLY**  
 특성의 존재 여부가 특성 열에 있는 값보다 더 중요함을 나타냅니다. 예를 들어 특정 고객과 관련된 주문 항목 목록이 포함된 사례 테이블이 있다고 가정해 봅니다. 이 테이블 데이터에는 제품 종류, ID 및 각 항목의 값이 포함되어 있습니다. 모델링을 위해서는 고객이 특정 주문 항목을 구입했다는 사실이 주문 항목의 값 자체보다 더 중요할 수 있습니다. 이 경우 값 열을 **MODEL_EXISTENCE_ONLY**로 표시해야 합니다.  
  
 **REGRESSOR**  
 회귀 알고리즘의 회귀 수식에 지정된 열을 사용할 수 있음을 나타냅니다. 이 플래그는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시계열 알고리즘에 사용할 수 있습니다.  
  
 사용법 속성을 설정하고 DMX를 사용하여 프로그래밍 방식으로 모델링 플래그를 정의하는 방법은 [CREATE MINING MODEL&#40;DMX&#41;](../../dmx/create-mining-model-dmx.md)을 참조하세요. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 사용법 속성을 설정하고 모델링 플래그를 정의하는 방법은 [데이터 마이닝 개체 이동](../../analysis-services/data-mining/moving-data-mining-objects.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [마이닝 구조&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [마이닝 모델의 속성 변경](../../analysis-services/data-mining/change-the-properties-of-a-mining-model.md)   
 [마이닝 모델에서 열 제외](../../analysis-services/data-mining/exclude-a-column-from-a-mining-model.md)   
 [마이닝 구조 열](../../analysis-services/data-mining/mining-structure-columns.md)  
  
  

