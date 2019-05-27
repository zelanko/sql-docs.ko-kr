---
title: 시퀀스 클러스터링 클러스터 다이어그램 탭 (마이닝 모델 뷰어 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.diagrams.f1
ms.assetid: 4b705397-9af4-4678-9eda-149bc5d762fa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d8cff96e3ed2d36db93abb3583a08b5c9d8153d8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66069109"
---
# <a name="sequence-clustering-cluster-diagram-tab-mining-model-viewer"></a>시퀀스 클러스터링 클러스터 다이어그램 탭(마이닝 모델 뷰어)
  **Microsoft 시퀀스 클러스터링 뷰어** 의 **클러스터 다이어그램** 탭에는 시퀀스 클러스터링 모델에 포함된 모든 클러스터가 그래픽으로 표시됩니다.  
  
 드릴스루가 사용하도록 설정된 경우 이 시퀀스 클러스터링 모델 뷰를 사용하여 각 클러스터에서 지원하는 사례로 드릴스루할 수 있습니다. 또한 클러스터에 설명이 포함된 이름을 할당하고 음영 변수를 변경하여 값의 분포를 한눈에 평가할 수 있습니다.  
  
 **참조 항목:** [Microsoft 시퀀스 클러스터링 알고리즘](data-mining/microsoft-sequence-clustering-algorithm.md), [Microsoft 시퀀스 클러스터 뷰어를 사용 하 여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>변수  
 **뷰어 내용 새로 고침**  
 뷰어에서 마이닝 모델을 다시 로드합니다.  
  
 **마이닝 모델**  
 현재 마이닝 구조에서 볼 마이닝 모델을 선택합니다. 관련 뷰어에서 마이닝 모델이 열립니다.  
  
 **Viewer**  
 선택한 마이닝 모델을 탐색하는 데 사용할 뷰어를 선택합니다. 사용자 지정 뷰어 또는 **Microsoft 일반 콘텐츠 트리 뷰어**를 사용할 수 있습니다. 또한 사용 가능한 경우 플러그 인 뷰어를 사용할 수 있습니다.  
  
 **확대/축소**  
 클러스터를 보다 자세하게 표시하려면 다이어그램을 확대합니다.  
  
 **축소**  
 모델의 모든 클러스터를 표시하려면 다이어그램을 축소합니다.  
  
 **그래프 뷰 복사**  
 다이어그램에서 표시되는 섹션을 클립보드로 복사합니다.  
  
 **전체 그래프 복사**  
 전체 다이어그램을 클립보드로 복사합니다.  
  
 **창에 맞게 다이어그램 크기 조정**  
 전체 다이어그램이 화면에 표시될 때까지 다이어그램을 축소합니다.  
  
 **노드 찾기**  
 **노드 찾기** 대화 상자를 사용하여 그래프의 클러스터를 필터링하고 특정 클러스터를 보다 찾기 쉽게 만들 수 있습니다. 자세한 내용은 [노드 찾기 대화 상자&#40;마이닝 모델 뷰어&#41;](find-node-dialog-box-mining-model-viewer.md)를 참조하세요.  
  
 이 컨텍스트에서는 클러스터 내의 특성이 아니라 클러스터의 이름만 검색하므로 이 옵션은 클러스터에 설명이 포함된 이름을 할당한 경우 가장 유용합니다. 각 클러스터를 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 선택하여 뷰어에서 클러스터에 이름을 할당할 수 있습니다.  
  
 **레이아웃 개선**  
 다이어그램에서 클러스터를 다시 정렬하여 레이아웃을 개선합니다.  
  
 **밀도**  
 밀도 막대 그래프의 모양과 값은 **음영 변수**에서 선택하는 특성에 따라 달라집니다.  
  
-   음영 변수로 특성 상태를 선택하지 않은 경우 기본적으로 각 클러스터에 적용된 밀도 음영은 사례의 전체 모집단과 비교되는 클러스터에 대한 지지도를 나타냅니다.  
  
-   **음영 변수**의 특성을 선택하는 경우 **상태** 의 값도 선택해야 합니다. 이렇게 하면 밀도 막대 그래프가 업데이트되어 이 상태의 확률이 표시됩니다. 개별 클러스터 위에 마우스를 놓으면 클러스터의 선택된 상태에 대한 확률을 볼 수 있습니다.  
  
 **음영 변수**  
 클러스터 다이어그램에 음영을 지정하는 데 사용할 특성을 마이닝 모델에서 선택합니다.  
  
 **State**  
 **음영 변수**에 해당하는 상태를 선택합니다. 예를 들어 특정 제품이 포함된 시퀀스를 보려면 [Product] 열을 **음영 변수**의 특성으로 선택하고 특정 제품 이름을 **상태** 값으로 선택할 수 있습니다.  
  
 **링크**  
 다이어그램의 선은 시퀀스 클러스터 간의 연결을 나타냅니다. 클러스터의 오른쪽에 있는 슬라이더를 조정하여 뷰어에 표시되는 링크의 수를 조정할 수 있습니다. 슬라이더를 내리면 강력한 링크만 표시됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [마이닝 모델 뷰어&#40;데이터 마이닝 모델 디자이너&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [데이터 마이닝 모델 뷰어](data-mining/data-mining-model-viewers.md)  
  
  
