---
title: 시퀀스 클러스터링 클러스터 프로필 탭 (마이닝 모델 뷰어 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.profiles.f1
ms.assetid: 44230895-0a42-4032-8d6c-0cdb8a2dbb8c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4f277abea585715f6a3656fffe7672f347233507
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66069102"
---
# <a name="sequence-clustering-cluster-profiles-tab-mining-model-viewer"></a>시퀀스 클러스터링 클러스터 프로필 탭(마이닝 모델 뷰어
  **Microsoft 시퀀스 클러스터링 뷰어**의 **클러스터 프로필** 탭에는 각 클러스터에 포함된 시퀀스가 색으로 지정되어 표시됩니다.  
  
 이 시퀀스 클러스터링 모델 뷰를 사용하여 모델이 검색한 시퀀스가 그룹화되는 방법을 신속하게 확인할 수 있습니다. 긴 시퀀스의 수와 짧은 시퀀스의 수를 한눈에 볼 수 있습니다. 또한 클러스터를 클릭하고 **마이닝 범례** 를 표시하여 각 시퀀스의 색이 나타내는 상태를 정확히 확인할 수 있습니다.  
  
 **참조 항목:**  [Microsoft 시퀀스 클러스터링 알고리즘](data-mining/microsoft-sequence-clustering-algorithm.md), [Microsoft 시퀀스 클러스터 뷰어를 사용 하 여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>변수  
 **뷰어 내용 새로 고침**  
 뷰어에서 마이닝 모델을 다시 로드합니다.  
  
 **마이닝 모델**  
 현재 마이닝 구조에서 볼 마이닝 모델을 선택합니다. 관련 뷰어에서 마이닝 모델이 열립니다.  
  
 **Viewer**  
 선택한 마이닝 모델을 탐색하는 데 사용할 뷰어를 선택합니다. 사용자 지정 뷰어 또는 **Microsoft 일반 콘텐츠 트리 뷰어**를 사용할 수 있습니다. 또한 사용 가능한 경우 플러그 인 뷰어를 사용할 수 있습니다.  
  
 **범례 표시**  
 상태의 텍스트 값과 클러스터 프로필에 표시된 색 간의 상관 관계를 보여 주는 범례를 표시하려면 이 옵션을 선택합니다.  
  
 **히스토그램 막대**  
 히스토그램에 포함된 색이 지정된 막대의 수를 변경하려면 이 옵션을 사용합니다. 선택한 것보다 많은 막대가 있는 경우 가장 중요한 막대만 유지되고 나머지 막대는 모두 **기타**로 그룹화됩니다.  
  
 **특성** 및 **클러스터 프로필**  
 그래프 차트의 이 섹션에는 모델에서 발견된 시퀀스의 클러스터가 나열됩니다.  
  
 각 시퀀스 클러스터는 **히스토그램 막대**옵션에서 선택한 상태 수를 사용하여 표시됩니다.  
  
 두 히스토그램 집합은 모델의 각 클러스터에 대해 표시되며 각각 그래프의 다른 행에 있습니다.  
  
-   **\<특성 이름 >.samples**: 이 행의 히스토그램은 각 클러스터의 특징을 나타내는 항목의 시퀀스를 보여 줍니다. DMX 측면에서 이러한 항목은 각 클러스터에 대한 샘플 사례입니다.  
  
-   **\<특성 이름 >** : 이 행의 히스토그램은 클러스터에 포함 된 모든 항목 및 전체적인 분포를 설명 합니다. **마이닝 범례** 가 표시될 때 히스토그램을 클릭하면 각각의 숫자 값을 볼 수 있습니다.  
  
 **상태**  
 차트의 이 열은 선택 사항이며 **범례 표시** 옵션을 선택하여 표시하거나 제거할 수 있습니다. **상태** 열은 해당 클러스터 히스토그램에서 어떤 색이 어떤 상태를 나타내는지를 안내합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Microsoft Sequence Clustering Algorithm](data-mining/microsoft-sequence-clustering-algorithm.md)   
 [마이닝 모델 뷰어&#40;데이터 마이닝 모델 디자이너&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [데이터 마이닝 모델 뷰어](data-mining/data-mining-model-viewers.md)   
 [Microsoft 시퀀스 클러스터 뷰어를 사용하여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
  
