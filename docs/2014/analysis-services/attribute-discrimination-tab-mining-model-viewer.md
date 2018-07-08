---
title: 특성 판별 탭 (마이닝 모델 뷰어) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.naivebayse.discrimination.f1
ms.assetid: 68323f23-121e-44fc-be85-6f9915d6d3c7
caps.latest.revision: 22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2e661e6a993639d3eac86bd5fb45f607ba8d346f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37161524"
---
# <a name="attribute-discrimination-tab-mining-model-viewer"></a>특성 판별 탭(마이닝 모델 뷰어)
  **특성 판별** 탭을 사용하여 입력 특성의 상태를 비교하고 결과 특성과의 관련성을 확인할 수 있습니다. 선택한 두 예측 가능한 특성 간의 가장 큰 차이를 나타내는 특성 값이 먼저 나열됩니다.  
  
 **자세한 내용:** [Microsoft Naive Bayes 알고리즘](data-mining/microsoft-naive-bayes-algorithm.md), [Microsoft Naive Bayes 뷰어를 사용하여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
## <a name="options"></a>변수  
 **뷰어 내용 새로 고침**  
 뷰어에서 마이닝 모델을 다시 로드합니다.  
  
 **마이닝 모델**  
 현재 마이닝 구조에서 마이닝 모델을 선택합니다. 마이닝 모델이 올바른 사용자 지정 뷰어에서 자동으로 열립니다.  
  
 **뷰어**  
 선택한 마이닝 모델을 탐색하는 데 사용할 뷰어를 선택합니다. 각 모델에 대해 사용자 지정 뷰어나 [!INCLUDE[msCoName](../includes/msconame-md.md)] 마이닝 콘텐츠 뷰어를 선택할 수 있습니다. 또한 사용 가능한 경우 플러그 인 뷰어를 사용할 수 있습니다.  
  
 **Attribute**  
 예측 가능한 특성을 선택합니다.  
  
 **값 1**  
 **값 2**에 포함된 상태와 비교할 예측 가능한 특성의 상태를 선택합니다.  
  
 **값 2**  
 **값 1**에 포함된 상태와 비교할 예측 가능한 특성의 상태를 선택합니다. **다른 모든 상태** 를 선택하여 **값 1** 의 값을 보수, 즉 값 1을 제외한 다른 모든 값과 비교할 수도 있습니다.  
  
 **에 대 한 판별 점수 \<값 1 > 및 \<값 2 >**  
 그래프에는 대상 특성이 입력 특성의 특정 상태와 어떠한 관련이 있는지를 설명하는 다음 열이 포함되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**특성**|마이닝 모델의 입력 특성입니다.|  
|**값**|**특성**에 나열된 특성의 상태입니다.|  
|**유사성 \<1 값 >**|막대는 현재 특성과 값이 **값 1**에서 선택한 대상 결과와 유사한지 여부를 나타냅니다.|  
|**유사성 \<2 값 >**|막대는 현재 특성과 값이 **값 2**에서 선택한 대상 결과와 유사한지 여부를 나타냅니다.|  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 알고리즘 &#40;Analysis Services-데이터 마이닝&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [마이닝 모델 뷰어 &#40;데이터 마이닝 모델 디자이너&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [데이터 마이닝 모델 뷰어](data-mining/data-mining-model-viewers.md)  
  
  
