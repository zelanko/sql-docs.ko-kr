---
title: "Microsoft 트리 뷰어를 사용 하 여 모델 찾아보기 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Tree Viewer [Analysis Services]
- predictions [Analysis Services], discrete attributes
- mining model content, viewing
- predictions [Analysis Services], continuous attributes
- mining legend [Analysis Services]
- discrete attributes [Analysis Services]
- Microsoft Decision Trees algorithm [Analysis Services]
- decision tree algorithms [Analysis Services]
- Microsoft Tree Viewer
- decision trees [Analysis Services]
- dependencies [Analysis Services]
- continuous attributes
ms.assetid: 0c96d518-ed20-40b7-8d62-b26ad6244287
caps.latest.revision: 46
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cf93bd7a9be8f6de5e4f807730fcaa4bcb60ab5c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="browse-a-model-using-the-microsoft-tree-viewer"></a>Microsoft 트리 뷰어를 사용하여 모델 찾아보기
  [!INCLUDE[msCoName](../../includes/msconame-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 트리 뷰어는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 알고리즘을 사용하여 작성된 의사 결정 트리를 표시합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 알고리즘은 분류와 회귀를 둘 다 지원하는 하이브리드 의사 결정 트리 알고리즘입니다. 따라서 이 뷰어를 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 선형 회귀 알고리즘을 기반으로 모델을 볼 수도 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 알고리즘은 불연속 및 연속 특성 모두의 예측 모델링에 사용됩니다. 이 알고리즘에 대한 자세한 내용은 [Microsoft Decision Trees Algorithm](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)를 참조하십시오.  
  
> [!NOTE]  
>  발견된 패턴 및 모델에 사용된 수식에 대한 자세한 정보를 보려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 일반 콘텐츠 트리 뷰어를 사용하십시오. 자세한 내용은 [Microsoft 일반 콘텐츠 트리 뷰어를 사용하여 모델 찾아보기](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) 또는 [Microsoft 일반 콘텐츠 트리 뷰어&#40;데이터 마이닝&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)를 참조하세요.  
  
##  <a name="BKMK_TabsPanes"></a> 뷰어 탭  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 마이닝 모델을 찾으면 해당 모델의 적절한 뷰어에서 데이터 마이닝 디자이너의 **마이닝 모델 뷰어** 탭에 해당 모델이 표시됩니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 트리 뷰어에는 다음과 같은 탭과 창이 있습니다.  
  
-   [의사 결정 트리](#BKMK_DecisionTree)  
  
-   [종속성 네트워크](#BKMK_DependencyNetwork)  
  
-   [마이닝 범례](#BKMK_MiningLegend)  
  
###  <a name="BKMK_DecisionTree"></a> 의사 결정 트리  
 의사 결정 트리 모델을 생성할 때 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 예측 가능한 각 특성에 대해 별도의 트리를 생성합니다. 뷰어의 **의사 결정 트리** 탭에 있는 **트리** 목록에서 개별 트리를 선택하여 볼 수 있습니다.  
  
 의사 결정 트리는 일련의 분할로 구성되며 알고리즘의 결정에 따라 가장 중요한 분할이 **모두** 노드의 뷰어 왼쪽에 표시됩니다. 추가 분할은 오른쪽에 나타납니다. **모두** 노드의 분할은 데이터 집합에서 분할을 유발하는 가장 큰 조건을 포함하므로 가장 중요하며, 이로 인해 첫 번째 분할이 발생했습니다.  
  
 트리의 개별 노드를 확장하거나 축소하여 각 노드 다음에 발생하는 분할을 표시하거나 숨길 수 있습니다. **의사 결정 트리** 탭의 옵션을 사용하여 트리 표시 방법을 변경할 수도 있습니다. **수준 표시** 슬라이더를 사용하여 트리에 표시되는 수준의 개수를 조정할 수 있습니다. **기본 확장** 을 사용하여 모델의 모든 트리에 표시되는 기본 수준 개수를 설정할 수 있습니다.  
  
#### <a name="predicting-discrete-attributes"></a>불연속 특성 예측  
 예측 가능한 불연속 특성을 사용하여 트리를 작성할 때 뷰어는 트리의 각 노드에 대해 다음을 표시합니다.  
  
-   분할 발생 조건  
  
-   인기도 순서로 예측 가능한 특성의 상태 분포를 나타내는 히스토그램  
  
 **히스토그램** 옵션을 사용하여 트리의 히스토그램에 나타나는 상태 수를 변경할 수 있습니다. 이 옵션은 예측 가능한 특성에 많은 상태가 있는 경우에 유용합니다. 상태는 왼쪽에서 오른쪽으로 히스토그램에 인기도 순서로 나타납니다. 표시할 상태 수가 특성의 전체 상태 수보다 적으면 가장 인기 없는 상태는 전체가 회색으로 표시됩니다. 노드에 대한 각 상태의 정확한 수를 확인하려면 노드 위에 포인터를 올려 놓고 잠시 기다리면 나타나는 정보 팁을 보거나 노드를 선택하여 **마이닝 범례**에서 세부 정보를 봅니다.  
  
 각 노드의 배경색은 **배경** 옵션을 사용하여 선택한 특성 상태의 사례 집중을 나타냅니다. 이 옵션을 사용하여 관심 있는 특정 대상이 포함된 노드를 강조 표시할 수 있습니다.  
  
#### <a name="predicting-continuous-attributes"></a>연속 특성 예측  
 예측 가능한 연속 특성을 사용하여 트리를 작성할 때 뷰어는 트리의 각 노드에 대해 히스토그램 대신 다이아몬드 차트를 표시합니다. 다이아몬드 차트에는 특성의 범위를 나타내는 선이 있습니다. 다이아몬드는 노드의 평균에 있고 다이아몬드 너비는 해당 노드에서 특성의 분산을 나타냅니다. 다이아몬드가 가늘수록 노드에서 보다 더 정확한 예측을 도출할 수 있음을 나타냅니다. 뷰어는 노드의 분할을 결정하는 데 사용되는 회귀 수식도 표시합니다.  
  
#### <a name="additional-decision-tree-display-options"></a>추가 의사 결정 트리 표시 옵션  
 의사 결정 트리 모델에 대해 드릴스루를 사용하면 트리에서 노드를 마우스 오른쪽 단추로 클릭하고 **드릴스루**를 선택하여 해당 노드를 지원하는 학습 사례에 액세스할 수 있습니다. **마이닝 모델** 탭에서 마이닝 모델에 대한 드릴스루 속성을 조정하거나 데이터 마이닝 마법사 내에서 드릴스루를 설정할 수 있습니다.  
  
 **의사 결정 트리** 탭의 확대/축소 옵션을 사용하여 트리를 확대 또는 축소하거나 **크기 조정** 을 사용하여 전체 모델을 뷰어 화면에 맞출 수 있습니다. 트리가 너무 커서 화면에 맞게 크기를 조정할 수 없으면 **탐색**옵션을 사용하여 트리를 이동할 수 있습니다. **탐색** 을 클릭하면 표시할 모델 섹션을 선택하는 데 사용할 수 있는 별도의 탐색 창이 열립니다.  
  
 트리 뷰 이미지를 클립보드로 복사하여 문서 또는 이미지 조작 소프트웨어에 붙여 넣을 수도 있습니다. **그래프 뷰 복사** 를 사용하여 뷰어에 표시된 트리 섹션만 복사하거나 **전체 그래프 복사** 를 사용하여 트리에서 확장된 모든 노드를 복사할 수 있습니다.  
  
 [맨 위로 이동](#BKMK_TabsPanes)  
  
###  <a name="BKMK_DependencyNetwork"></a> 종속성 네트워크  
 **종속성 네트워크** 는 모델의 입력 특성과 예측 가능한 특성 간의 종속성을 표시합니다. 뷰어의 왼쪽에 있는 슬라이더는 종속성 수준에 연결된 필터 역할을 합니다. 슬라이더를 아래로 이동하면 가장 강력한 링크만 뷰어에 표시됩니다.  
  
 노드를 선택하면 뷰어는 해당 노드와 관련된 종속성을 강조 표시합니다. 예를 들어 예측 가능한 노드를 선택하면 뷰어는 예측 가능한 노드를 예측하는 데 도움을 주는 각 노드도 강조 표시합니다.  
  
 뷰어에 많은 노드가 포함되어 있으면 **노드 찾기** 단추를 사용하여 특정 노드를 검색할 수 있습니다. **노드 찾기** 를 클릭하면 **노드 찾기** 대화 상자가 열리며 여기서 필터를 사용하여 특정 노드를 검색하고 선택할 수 있습니다.  
  
 뷰어의 아래쪽에 있는 범례는 색 코드를 그래프에 있는 종속성 유형에 연결합니다. 예를 들어 예측 가능한 노드를 선택하면 예측 가능한 노드는 옥색으로 표시되며 선택한 노드를 예측하는 노드는 주황색으로 표시됩니다.  
  
 [맨 위로 이동](#BKMK_TabsPanes)  
  
###  <a name="BKMK_MiningLegend"></a> 마이닝 범례  
 의사 결정 트리 모델에서 노드를 선택하면 **마이닝 범례** 에 다음 정보가 표시됩니다.  
  
-   예측 가능한 특성 상태로 분류된 노드의 사례 수  
  
-   노드의 예측 가능한 특성에 대한 각 사례의 확률  
  
-   예측 가능한 특성의 각 상태 수가 포함된 히스토그램  
  
-   특정 노드에 도달하는 데 필요한 조건( *노드 경로*라고도 함)  
  
-   선형 회귀 모델의 경우 회귀 수식  
  
 솔루션 탐색기와 유사한 방식으로 **마이닝 범례** 를 도킹하고 사용할 수 있습니다.  
  
 [맨 위로 이동](#BKMK_TabsPanes)  
  
## <a name="see-also"></a>관련 항목:  
 [Microsoft Decision Trees Algorithm](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)   
 [마이닝 모델 뷰어 &#40; 데이터 마이닝 모델 디자이너 &#41;](http://msdn.microsoft.com/library/4ba391d5-c97b-4848-ba7c-7d096fa4b7dd)   
 [마이닝 모델 뷰어 태스크 및 방법](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [데이터 마이닝 도구](../../analysis-services/data-mining/data-mining-tools.md)   
 [데이터 마이닝 모델 뷰어](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
  
