---
title: 클러스터 특징 탭 (마이닝 모델 뷰어) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.clustering.characteristics.f1
ms.assetid: 8e33ed1d-1ce4-405d-895b-7e995b2c910d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c0b4a798f9a395741ae831d3b22fc06a71f55607
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66087985"
---
# <a name="cluster-characteristics-tab-mining-model-viewer"></a>클러스터 특징 탭(마이닝 모델 뷰어)
  **클러스터 특징** 탭에서는 클러스터링 모델에 있는 클러스터의 특징이나 모델에 있는 모든 사례 집합의 특징을 탐색할 수 있습니다. 이 그래프에는 다른 클러스터와 비교한 각 특성-값 쌍의 중요도가 클러스터를 정의하는 특징으로 표시됩니다.  
  
 **참조 항목:** [Microsoft 클러스터링 알고리즘](data-mining/microsoft-clustering-algorithm.md), [Microsoft 클러스터 뷰어를 사용 하 여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
## <a name="options"></a>변수  
 **뷰어 내용 새로 고침**  
 뷰어에서 마이닝 모델을 다시 로드합니다.  
  
 **마이닝 모델**  
 현재 마이닝 구조에서 마이닝 모델을 선택합니다. 사용자 지정 뷰어에서 마이닝 모델이 열립니다.  
  
 **Viewer**  
 선택한 마이닝 모델을 탐색하는 데 사용할 뷰어를 선택합니다. 이 모델 유형과 연결된 사용자 지정 뷰어 또는 [!INCLUDE[msCoName](../includes/msconame-md.md)] 마이닝 콘텐츠 뷰어를 사용할 수 있습니다. 또한 사용 가능한 플러그 인 뷰어를 사용할 수 있습니다.  
  
 **Cluster**  
 보려는 클러스터를 선택하거나 모델의 특성 분포를 전체적으로 보려면 **채우기(모두)** 를 선택합니다.  
  
 **에 대 한 특성 \<클러스터 >**  
 이 그래프에는 선택한 클러스터의 특징을 설명하는 다음 열이 포함됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|**변수**|선택한 클러스터에 있는 마이닝 모델의 특성을 나열합니다.|  
|**값**|현재 선택한 클러스터에 있는 현재 특성 값을 나열합니다.|  
|**확률**|이 막대는 이 클러스터의 특징적인 기능으로 특성-값 쌍의 강도를 나타냅니다. 막대를 마우스로 가리키면 백분율로 표시된 확률 값을 볼 수 있습니다. 이는 특정 사례에서 이 특성 및 값 조합이 제공된 경우 해당 사례가 이 클러스터에 속할 확률을 나타냅니다.|  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [마이닝 모델 뷰어&#40;데이터 마이닝 모델 디자이너&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [데이터 마이닝 모델 뷰어](data-mining/data-mining-model-viewers.md)  
  
  
