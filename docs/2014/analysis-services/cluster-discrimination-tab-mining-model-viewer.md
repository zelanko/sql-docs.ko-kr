---
title: 클러스터 판별 탭 (마이닝 모델 뷰어) | Microsoft Docs
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
- sql12.dm.miningmodeleditor.clustering.discrimination.f1
ms.assetid: ae7cfff7-ab1c-4cf5-9a91-97b21d15d85f
caps.latest.revision: 22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 992ef4a9145a3137975220ac2febdab3028507c1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37179042"
---
# <a name="cluster-discrimination-tab-mining-model-viewer"></a>클러스터 판별 탭(마이닝 모델 뷰어)
  **클러스터 판별** 탭을 사용하여 클러스터링 모델에 있는 두 클러스터를 비교할 수 있습니다. 특성 및 값의 여러 가지 조합이 클러스터 내에서 표시되는 방식을 볼 수 있습니다.  
  
 **자세한 내용:** [Microsoft 클러스터링 알고리즘](data-mining/microsoft-clustering-algorithm.md), [Microsoft 클러스터 뷰어를 사용하여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
## <a name="options"></a>변수  
 **뷰어 내용 새로 고침**  
 뷰어에서 마이닝 모델을 다시 로드합니다.  
  
 **마이닝 모델**  
 현재 마이닝 구조에서 마이닝 모델을 선택합니다. 관련 뷰어에서 마이닝 모델이 열립니다.  
  
 **뷰어**  
 선택한 마이닝 모델을 탐색하는 데 사용할 뷰어를 선택합니다. 클러스터링 모델의 사용자 지정 뷰어나 [!INCLUDE[msCoName](../includes/msconame-md.md)] 마이닝 콘텐츠 뷰어를 사용할 수 있습니다. 또한 사용 가능한 경우 플러그 인 뷰어를 사용할 수 있습니다.  
  
 **클러스터 1**  
 다른 클러스터와 비교할 수 있도록 클러스터를 선택합니다.  
  
 **클러스터 2**  
 마이닝 모델의 클러스터 목록에서 **클러스터 1**과 비교할 두 번째 클러스터를 선택합니다. 클러스터를 해당 보수와 비교할 수도 있습니다. 즉, 선택한 클러스터에 없는 모델의 모든 사례와 비교할 수 있습니다.  
  
 **에 대 한 판별 점수 \<클러스터 1 > 및 \<2 클러스터 >**  
 그래프의 열에서는 각 특성-값 쌍과 선택한 두 클러스터의 관련성에 대한 정보를 제공합니다.  
  
|||  
|-|-|  
|**변수**|마이닝 모델의 특성입니다.|  
|**값**|**변수**에서 선택한 특성의 값입니다.|  
|**유사성 \<1 클러스터 >**|왼쪽의 막대 그래프는 선택한 특성-값 쌍이 **클러스터 1**에서 선택한 클러스터의 특징을 나타낼 확률을 나타냅니다. 막대 위에 마우스를 놓으면 백분율로 표시된 값을 볼 수 있습니다. 값이 0인 경우라도 특성-값이 반드시 클러스터에 없는 것을 의미하지는 않으며, 분포가 다른 클러스터보다 한 클러스터와 크게 유사함을 의미할 뿐입니다.|  
|**유사성 \<2 클러스터 >**|오른쪽의 막대 그래프는 선택한 특성-값 쌍이 **클러스터 2**에서 선택한 클러스터의 특징을 나타낼 확률을 나타냅니다.|  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 알고리즘 &#40;Analysis Services-데이터 마이닝&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [마이닝 모델 뷰어 &#40;데이터 마이닝 모델 디자이너&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [데이터 마이닝 모델 뷰어](data-mining/data-mining-model-viewers.md)  
  
  
