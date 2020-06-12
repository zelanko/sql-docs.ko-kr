---
title: 종속성 네트워크 탭 (마이닝 모델 뷰어) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.dependencynetwork.f1
ms.assetid: e58ce1b7-20d6-42cb-ade5-916da8471e09
author: minewiskan
ms.author: owend
ms.openlocfilehash: dde94a8d08bba3ea529c9edf3fde12ee0260a3f0
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528739"
---
# <a name="dependency-network-tab-mining-model-viewer"></a>종속성 네트워크 탭(마이닝 모델 뷰어)
  **종속성 네트워크** 탭에서는 마이닝 모델에 포함된 모든 특성에 대한 그래픽 뷰를 제공하고 특성의 관계를 보여 줍니다.  
  
 **종속성 네트워크**  탭은 Naïve Bayes 모델, 의사 결정 트리 모델 및 연결 모델을 비롯한 몇 가지 유형의 마이닝 모델에 사용됩니다. 이러한 모델의 컨텍스트에서 **종속성 네트워크**  탭의 내용을 해석하는 방법은 다음 링크를 참조하십시오.  
  
 [Microsoft 트리 뷰어를 사용하여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)  
  
 [Microsoft Naive Bayes 뷰어를 사용하여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
 [Microsoft 연결 규칙 뷰어를 사용하여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)  
  
## <a name="options"></a>옵션  
 **뷰어 내용 새로 고침**  
 뷰어에서 마이닝 모델을 다시 로드합니다.  
  
 **마이닝 모델**  
 현재 마이닝 구조에서 보려는 마이닝 모델을 선택합니다. 사용자 지정 뷰어에서 마이닝 모델이 열립니다. 각 모델에 사용되는 사용자 지정 뷰어의 유형은 모델을 만드는 데 사용한 알고리즘에 따라 결정됩니다.  
  
 **뷰어**  
 선택한 마이닝 모델을 탐색하는 데 사용할 뷰어를 선택합니다. 각 마이닝 모델에 대해 제공되는 사용자 지정 뷰어나 [!INCLUDE[msCoName](../includes/msconame-md.md)] 마이닝 콘텐츠 뷰어를 사용할 수 있습니다. 또한 사용 가능한 경우 플러그 인 뷰어를 사용할 수 있습니다. Microsoft 콘텐츠 트리 뷰어는 모든 모델에서 사용할 수 있으며 HTML 테이블로 모델 콘텐츠를 나타냅니다.  
  
 **확대**  
 특성을 자세히 볼 수 있도록 다이어그램을 확대합니다.  
  
 **축소**  
 특성을 더 보고 특성 간의 링크를 볼 수 있도록 다이어그램을 축소합니다.  
  
 **그래프 뷰 복사**  
 다이어그램에서 표시되는 섹션을 클립보드로 복사합니다.  
  
 **전체 그래프 복사**  
 전체 다이어그램을 클립보드로 복사합니다.  
  
 **링크**  
 특성의 오른쪽에 있는 슬라이더를 조정하여 뷰어에 표시되는 링크(가장자리) 및 노드의 수를 조정합니다. 슬라이더 막대를 아래로 끌면 임계값이 증가하므로 가장 강력한 링크만 표시됩니다. 각 모델 유형에 대해 약간 다른 값이 그래프의 링크를 나타내는 데 사용됩니다.  
  
-   **의사 결정 트리** 모델에서 가장자리는 분할 점수에 의해 부분적으로 결정되는 연결의 예측 강도를 나타냅니다.  
  
-   **Naïve Bayes** 모델에서 두 노드 간의 링크는 양방향으로 이동할 수 있습니다. 즉, 노드 A는 노드 B를 예측할 수 있고 노드 B는 노드 A를 예측할 수 있습니다. 가장자리와 연결된 점수는 연결의 예측 강도를 나타냅니다.  
  
-   **연결 모델**에서 노드 간의 가장자리는 두 항목 집합을 연결하는 규칙의 중요도 점수를 나타냅니다.  
  
 모든 모델 유형에 대한 일반 규칙은 링크가 강력할수록 두 특성 간의 예측 관계도 강력하다는 것입니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 알고리즘 &#40;Analysis Services 데이터 마이닝&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [마이닝 모델 뷰어 &#40;데이터 마이닝 모델 디자이너&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [데이터 마이닝 모델 뷰어](data-mining/data-mining-model-viewers.md)  
  
  
