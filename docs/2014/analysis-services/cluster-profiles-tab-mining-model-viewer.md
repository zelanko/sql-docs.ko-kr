---
title: 클러스터 프로필 탭 (마이닝 모델 뷰어) | Microsoft Docs
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
- sql12.dm.miningmodeleditor.clustering.profiles.f1
ms.assetid: 1ebafa1f-74e9-4c05-b278-a690fa8543bd
caps.latest.revision: 22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e1b3e9bc36c75e0786f0e7de4799fd54f13120ec
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37267605"
---
# <a name="cluster-profiles-tab-mining-model-viewer"></a>클러스터 프로필 탭(마이닝 모델 뷰어)
  **클러스터 프로필** 탭을 사용하여 알고리즘이 클러스터링 모델 내에서 발견한 클러스터를 전체적으로 볼 수 있습니다. 이 탭에는 각 클러스터에서의 특성 분포와 함께 각 특성이 표시됩니다.  
  
 **자세한 내용:** [Microsoft 클러스터링 알고리즘](data-mining/microsoft-clustering-algorithm.md), [Microsoft 클러스터 뷰어를 사용하여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
## <a name="options"></a>변수  
 **뷰어 내용 새로 고침**  
 뷰어에서 마이닝 모델을 다시 로드합니다.  
  
 **마이닝 모델**  
 현재 마이닝 구조에서 마이닝 모델을 선택합니다. 관련 뷰어에서 마이닝 모델이 열립니다.  
  
 **뷰어**  
 선택한 마이닝 모델을 보는 데 사용할 뷰어를 선택합니다. 마이닝 모델에 대해 제공되는 사용자 지정 뷰어나 [!INCLUDE[msCoName](../includes/msconame-md.md)] 마이닝 콘텐츠 뷰어를 사용할 수 있습니다. 또한 사용 가능한 경우 플러그 인 뷰어를 사용할 수 있습니다.  
  
 **범례 표시**  
 **상태** 열의 값에 대한 뷰어 색의 매핑을 보여 주는 키를 표시하려면 이 옵션을 선택합니다.  
  
 **히스토그램 막대**  
 각 히스토그램에 포함되는 상태 수를 제어하려면 이 값을 변경합니다. 표시하도록 선택한 것보다 많은 상태가 있는 경우 확률이 가장 높은 상태가 히스토그램에 표시되고 나머지 상태는 모두 **기타**로 그룹화됩니다.  
  
 **특성**  
 클러스터링 모델에 있는 열을 나열합니다. 각 특성의 히스토그램에는 알고리즘으로 식별된 클러스터 간에 특성이 어떻게 분포되어 있는지 표시됩니다.  
  
 **상태**  
 클러스터의 해당 행에서 각 상태를 나타내는 색을 지정하는 키를 제공하거나 연속 숫자 값의 분포를 나타내는 다이아몬드가 있는 슬라이더를 제공합니다. **범례 표시** 확인란을 사용하여 이 열을 표시하거나 숨길 수 있습니다.  
  
 **클러스터 프로필**  
 이 섹션에는 모델의 각 클러스터에 대한 열이 포함됩니다. 각 특성에 대해 히스토그램에 해당 클러스터에 대한 특성의 값 분포가 표시됩니다. 히스토그램을 사용하여 모델의 모든 사례가 아니라 각 특성에 대한 값의 분포를 표시하는 **모집단**에 대한 열도 차트에 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 알고리즘 &#40;Analysis Services-데이터 마이닝&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [마이닝 모델 뷰어 &#40;데이터 마이닝 모델 디자이너&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [데이터 마이닝 모델 뷰어](data-mining/data-mining-model-viewers.md)  
  
  
