---
title: 마이닝 모델 뷰어 (데이터 마이닝 모델 디자이너) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.viewers.f1
ms.assetid: 4ba391d5-c97b-4848-ba7c-7d096fa4b7dd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7890360221f3adae73efef7a58ae1179e19760a1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48152810"
---
# <a name="mining-model-viewers-data-mining-model-designer"></a>마이닝 모델 뷰어(데이터 마이닝 모델 디자이너)
  **마이닝 모델 뷰어** 탭을 사용하여 마이닝 구조에 포함된 마이닝 모델을 탐색할 수 있습니다.  
  
 먼저 마이닝 모델을 선택한 다음 뷰어를 선택합니다. 항상 각 모델에는 여러 탭을 포함할 수 있는 사용자 지정 뷰어와 일반 뷰어라는 두 개의 뷰어가 있습니다.  
  
 각 뷰어를 사용하는 방법을 보여 주는 연습은 [데이터 마이닝 모델 뷰어](data-mining/data-mining-model-viewers.md)를 참조하세요.  
  
## <a name="common-options"></a>일반 옵션  
 **뷰어 내용 새로 고침**  
 뷰어에서 마이닝 모델을 다시 로드합니다.  
  
 **마이닝 모델**  
 현재 마이닝 구조에서 볼 마이닝 모델을 선택합니다. 마이닝 모델은 연결된 사용자 지정 뷰어에서 먼저 열립니다.  
  
 **뷰어**  
 선택한 마이닝 모델을 탐색하는 데 사용할 뷰어를 선택합니다. 이 목록에는 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 가 각 마이닝 모델에 대해 제공하는 뷰어, [!INCLUDE[msCoName](../includes/msconame-md.md)] 마이닝 콘텐츠 뷰어 및 모든 플러그 인 뷰어가 포함되어 있습니다.  
  
 다음 다이어그램에서는 같은 모델에 대해 사용자 지정 뷰어와 일반 뷰어를 보여 줍니다.  
  
-   위쪽 다이어그램은 Microsoft 시계열 알고리즘을 기반으로 하는 마이닝 모델에 대한 뷰어를 보여 줍니다. 이 사용자 지정 뷰어에서는 시계열 그래프를 자동으로 만들고 5개의 예측을 제공합니다.  
  
-   아래쪽 다이어그램은 **Microsoft 일반 콘텐츠 트리 뷰어**를 사용하여 표시되는 동일한 모델을 보여 줍니다. 이 뷰어에는 표준화된 스키마에 따라 마이닝 모델의 내용이 표시됩니다. 자세한 내용은 [Microsoft 일반 콘텐츠 트리 뷰어&#40;데이터 마이닝&#41;](microsoft-generic-content-tree-viewer-data-mining.md)를 참조하세요.  
  
 ![마이닝 모델 디자이너 개요](media/generic-mining-model-tab1.gif "마이닝 모델 디자이너 개요")  
  
## <a name="viewers-and-their-components"></a>뷰어 및 해당 구성 요소  
 선택한 모델에 따라, 선택된 데이터 마이닝 모델을 만들 때 사용한 알고리즘에 맞게 조정된 각기 다른 사용자 지정 뷰어가 표시됩니다. 각 사용자 지정 뷰어에는 모델의 패턴 및 통계를 탐색하는 데 도움이 되는 다양한 도구 및 대화 상자가 있습니다.  
  
 다음 목록에서는 각 사용자 지정 뷰어에 있는 옵션에 대해 설명합니다.  
  
### <a name="microsoft-association-rules-algorithm"></a>Microsoft 연결 규칙 알고리즘  
  
-   [Microsoft 연결 규칙 뷰어를 사용하여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)  
  
    -   [항목 집합 탭 &#40;마이닝 모델 뷰어&#41;](itemsets-tab-mining-model-viewer.md)  
  
    -   [규칙 탭 &#40;마이닝 모델 뷰어&#41;](rules-tab-mining-model-viewer.md)  
  
    -   [종속성 네트워크 탭 &#40;마이닝 모델 뷰어&#41;](dependency-network-tab-mining-model-viewer.md)  
  
### <a name="microsoft-clustering-algorithm"></a>Microsoft Clustering Algorithm  
  
-   [Microsoft 클러스터 뷰어를 사용하여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
    -   [클러스터 다이어그램 탭 &#40;마이닝 모델 뷰어&#41;](cluster-diagram-tab-mining-model-viewer.md)  
  
    -   [클러스터 프로필 탭 &#40;마이닝 모델 뷰어&#41;](cluster-profiles-tab-mining-model-viewer.md)  
  
    -   [클러스터 특징 탭 &#40;마이닝 모델 뷰어&#41;](cluster-characteristics-tab-mining-model-viewer.md)  
  
    -   [클러스터 판별 탭 &#40;마이닝 모델 뷰어&#41;](cluster-discrimination-tab-mining-model-viewer.md)  
  
    -   [마이닝 범례 대화 상자 &#40;마이닝 모델 뷰어&#41;](mining-legend-dialog-box-mining-model-viewer.md)  
  
### <a name="microsoft-decision-tree-algorithm"></a>Microsoft 의사 결정 트리 알고리즘  
  
-   [Microsoft 트리 뷰어를 사용하여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)  
  
    -   [트리 탭 의사 결정 &#40;마이닝 모델 뷰어&#41;](decision-tree-tab-mining-model-viewer.md)  
  
    -   [종속성 네트워크 탭 &#40;마이닝 모델 뷰어&#41;](dependency-network-tab-mining-model-viewer.md)  
  
    -   [마이닝 범례 대화 상자 &#40;마이닝 모델 뷰어&#41;](mining-legend-dialog-box-mining-model-viewer.md)  
  
### <a name="microsoft-linear-regression-algorithm"></a>Microsoft 선형 회귀 알고리즘  
  
-   [Microsoft 신경망 뷰어를 사용하여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)  
  
    -   [트리 탭 의사 결정 &#40;마이닝 모델 뷰어&#41;](decision-tree-tab-mining-model-viewer.md)  
  
    -   [종속성 네트워크 탭 &#40;마이닝 모델 뷰어&#41;](dependency-network-tab-mining-model-viewer.md)  
  
    -   [마이닝 범례 대화 상자 &#40;마이닝 모델 뷰어&#41;](mining-legend-dialog-box-mining-model-viewer.md)  
  
### <a name="microsoft-logistic-regression-algorithm"></a>Microsoft 로지스틱 회귀 알고리즘  
  
-   [Microsoft 신경망 뷰어를 사용하여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)  
  
### <a name="microsoft-nave-bayes-algorithm"></a>Microsoft Naive Bayes 알고리즘  
  
-   [Microsoft Naive Bayes 뷰어를 사용하여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
    -   [종속성 네트워크 탭 &#40;마이닝 모델 뷰어&#41;](dependency-network-tab-mining-model-viewer.md)  
  
    -   [특성 프로필 탭 &#40;마이닝 모델 뷰어&#41;](attribute-profiles-tab-mining-model-viewer.md)  
  
    -   [특성 특징 탭 &#40;마이닝 모델 뷰어&#41;](attribute-characteristics-tab-mining-model-viewer.md)  
  
    -   [특성 판별 탭 &#40;마이닝 모델 뷰어&#41;](attribute-discrimination-tab-mining-model-viewer.md)  
  
### <a name="microsoft-neural-network-algorithm"></a>Microsoft Neural Network Algorithm  
  
-   [Microsoft 신경망 뷰어를 사용하여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)  
  
    -   [종속성 네트워크 탭 &#40;마이닝 모델 뷰어&#41;](dependency-network-tab-mining-model-viewer.md)  
  
    -   [신경망 &#40;마이닝 모델 뷰어&#41;](neural-network-mining-model-viewer.md)  
  
    -   [노드 찾기 대화 상자 &#40;마이닝 모델 뷰어&#41;](find-node-dialog-box-mining-model-viewer.md)  
  
### <a name="microsoft-sequence-clustering-algorithm"></a>Microsoft 시퀀스 클러스터링 알고리즘  
  
-   [Microsoft 시퀀스 클러스터 뷰어를 사용하여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
    -   [시퀀스 클러스터링 클러스터 다이어그램 탭 &#40;마이닝 모델 뷰어](sequence-clustering-cluster-diagram-tab-mining-model-viewer.md)  
  
    -   [시퀀스 클러스터링 클러스터 프로필 탭 &#40;마이닝 모델 뷰어](sequence-clustering-cluster-profiles-tab-mining-model-viewer.md)  
  
    -   [시퀀스 클러스터링 클러스터 특징 탭 &#40;마이닝 모델 뷰어&#41;](sequence-clustering-cluster-characteristics-tab-mining-model-viewer.md)  
  
    -   [시퀀스 클러스터링 클러스터 판별 탭 &#40;마이닝 모델 뷰어&#41;](sequence-clustering-cluster-discrimination-tab-mining-model-viewer.md)  
  
    -   [시퀀스 클러스터링 클러스터 전환 탭 &#40;마이닝 모델 뷰어&#41;](sequence-clustering-cluster-transition-tab-mining-model-viewer.md)  
  
### <a name="microsoft-time-series-algorithm"></a>Microsoft 시계열 알고리즘  
  
-   [Microsoft 시계열 뷰어를 사용하여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md)  
  
    -   [모델 탭 &#40;마이닝 모델 뷰어&#41;](model-tab-mining-model-viewers.md)  
  
    -   [차트 탭 &#40;마이닝 모델 뷰어&#41;](chart-tab-mining-model-viewers.md)  
  
    -   [마이닝 범례 대화 상자 &#40;마이닝 모델 뷰어&#41;](mining-legend-dialog-box-mining-model-viewer.md)  
  
## <a name="see-also"></a>관련 항목  
 [마이닝 모델 뷰 &#40;데이터 마이닝 모델 디자이너&#41;](mining-models-view-data-mining-model-designer.md)   
 [마이닝 구조 뷰 &#40;데이터 마이닝 모델 디자이너&#41;](mining-structure-view-data-mining-model-designer.md)   
 [마이닝 정확도 차트 디자이너 &#40;데이터 마이닝&#41;](mining-accuracy-chart-designer-data-mining.md)   
 [예측 쿼리 작성기 &#40;데이터 마이닝&#41;](prediction-query-builder-data-mining.md)  
  
  
