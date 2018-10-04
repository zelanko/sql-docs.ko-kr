---
title: 결정 트리 탭 (마이닝 모델 뷰어) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.decisiontree.f1
ms.assetid: dc88606f-ba7c-4f8d-af65-bfa17ec16e2b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dbb34719b79ba5a12249cdb96187b178450d5802
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48194493"
---
# <a name="decision-tree-tab-mining-model-viewer"></a>의사 결정 트리 탭(마이닝 모델 뷰어)
  **의사 결정 트리** 창에서는 의사 결정 트리 모델에서 만들어진 의사 결정 규칙을 시각적으로 표현합니다. 의사 결정 규칙은 특정 결과로 가는 경로를 설명합니다.  
  
 **자세한 내용:** [Microsoft 의사 결정 트리 알고리즘](data-mining/microsoft-decision-trees-algorithm.md), [Microsoft 트리 뷰어를 사용하여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)  
  
## <a name="options"></a>변수  
 **뷰어 내용 새로 고침**  
 뷰어에서 마이닝 모델을 다시 로드합니다.  
  
 **마이닝 모델**  
 현재 마이닝 구조에서 마이닝 모델을 선택합니다. 관련 뷰어에서 마이닝 모델이 열립니다.  
  
 **뷰어**  
 선택한 마이닝 모델을 탐색하는 데 사용할 뷰어를 선택합니다. 사용자 지정 뷰어나 [!INCLUDE[msCoName](../includes/msconame-md.md)] 마이닝 콘텐츠 뷰어를 사용할 수 있습니다. 또한 사용 가능한 경우 플러그 인 뷰어를 사용할 수 있습니다.  
  
 **확대/축소**  
 의사 결정 트리의 노드와 분기를 자세하게 표시하려면 확대합니다. 복잡한 모델에서는 의사 결정 트리에 많은 수준의 분기가 있을 수 있습니다.  
  
 **축소**  
 트리 구조를 개괄적으로 표시하려면 축소합니다.  
  
 **그래프 뷰 복사**  
 다이어그램에서 표시되는 섹션을 클립보드로 복사합니다.  
  
 **전체 그래프 복사**  
 전체 다이어그램을 클립보드로 복사합니다.  
  
 **창에 맞게 다이어그램 크기 조정**  
 전체 트리 구조가 화면에 표시될 때까지 다이어그램을 축소합니다.  
  
 **히스토그램**  
 각 노드에 대해 히스토그램에 표시될 수 있는 상태 수를 선택합니다. 모델의 상태 수가 선택한 값보다 적으면 추가 막대가 표시되지 않습니다.  
  
 **트리**  
 뷰어에 표시할 트리를 선택합니다. 예측 가능한 여러 특성이 있는 모델을 만드는 경우 알고리즘은 각각의 예측 가능한 특성에 대해 별도의 트리를 만듭니다.  
  
 **배경**  
 각 노드의 배경색을 나타내는 데 사용할 예측 가능한 특성의 값을 선택합니다. 예를 들어 AdventureWorks 예제 모델에서 **배경** 을 1로 설정하는 경우([Bike Buyer] = Yes) 자전거 구매자 비율이 더 높은 노드에 더 짙은 음영이 표시됩니다. 이 옵션은 트리에 있는 분기와 노드의 의미에 대한 시각적 표시를 추가로 제공합니다.  
  
 **기본 확장**  
 트리 그래프에 표시되는 수준 수의 기본값을 설정하려면 목록에서 값을 선택합니다.  
  
 **수준 표시**  
 트리 그래프에 표시되는 수준 수를 조정하려면 슬라이더 막대를 오른쪽이나 왼쪽으로 이동합니다. 모델의 모든 노드를 보려면 막대를 맨 오른쪽으로 이동합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 알고리즘 &#40;Analysis Services-데이터 마이닝&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [마이닝 모델 뷰어 &#40;데이터 마이닝 모델 디자이너&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [데이터 마이닝 모델 뷰어](data-mining/data-mining-model-viewers.md)  
  
  
