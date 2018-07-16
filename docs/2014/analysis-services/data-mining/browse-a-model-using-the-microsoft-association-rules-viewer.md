---
title: Microsoft 연결 규칙 뷰어를 사용 하 여 모델 찾아보기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- itemsets [Analysis Services]
- mining models [Analysis Services], associations
- mining model content, viewing
- rules [Data Mining]
- Association Rules Viewer [Analysis Services]
- market basket analysis [Analysis Services]
- associations [Analysis Services]
- Microsoft Association Rules Viewer
- dependencies [Analysis Services]
ms.assetid: 538fc01b-8eb1-467a-9b66-3cd57cf7489f
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dec01cc20a5863e29b115d0c0225084fdf9ab603
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37192923"
---
# <a name="browse-a-model-using-the-microsoft-association-rules-viewer"></a>Microsoft 연결 규칙 뷰어를 사용하여 모델 찾아보기
   [!INCLUDE[msCoName](../../includes/msconame-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 연결 규칙 뷰어에는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 연결 알고리즘을 사용하여 작성된 마이닝 모델이 표시됩니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 연결 알고리즘은 장바구니 분석에 사용할 수 있는 데이터 마이닝 모델을 만드는 데 사용하는 연결 알고리즘입니다. 이 알고리즘에 대한 자세한 내용은 [Microsoft Association Algorithm](microsoft-association-algorithm.md)를 참조하십시오.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 연결 알고리즘을 사용하는 주된 이유는 다음과 같습니다.  
  
-   트랜잭션에서 일반적으로 함께 발견되는 항목을 설명하는 항목 집합 찾기  
  
-   기존 항목을 기반으로 트랜잭션에 다른 항목이 있는지 여부를 예측하는 규칙 발견  
  
> [!NOTE]  
>  발견된 패턴 및 모델에 사용된 수식에 대한 자세한 정보를 보려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 일반 콘텐츠 트리 뷰어를 사용하십시오. 자세한 내용은 [Microsoft 일반 콘텐츠 트리 뷰어를 사용하여 모델 찾아보기](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) 또는 [Microsoft 일반 콘텐츠 트리 뷰어&#40;데이터 마이닝&#41;](../microsoft-generic-content-tree-viewer-data-mining.md)를 참조하세요.  
  
 연결 마이닝 모델의 생성, 탐색, 사용 방법에 대한 연습은 [3단원: 시장 바구니 시나리오 구축&#40;중급 데이터 마이닝 자습서&#41;](../../tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)을 참조하세요.  
  
##  <a name="BKMK_ViewerTabs"></a> 뷰어 탭  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 마이닝 모델을 찾으면 해당 모델의 적절한 뷰어에서 데이터 마이닝 디자이너의 **마이닝 모델 뷰어** 탭에 해당 모델이 표시됩니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 연결 규칙 뷰어에는 다음과 같은 탭이 있습니다.  
  
-   [항목 집합](#BKMK_Itemsets)  
  
-   [규칙](#BKMK_Rules)  
  
-   [종속성 네트워크](#BKMK_Dependency)  
  
 각 탭에는 **긴 이름 표시** 확인란이 있으며 이 확인란을 사용하여 규칙 또는 항목 집합에서 항목 집합이 만들어진 테이블을 표시 또는 숨길 수 있습니다.  
  
###  <a name="BKMK_Itemsets"></a> 항목 집합  
 **항목 집합** 탭에서는 함께 자주 발견되는 항목 집합 목록을 표시합니다. 이 탭에는 **지원**, **크기**및 **항목 집합**열로 구성된 표가 있습니다. 지원에 대한 자세한 내용은 [Microsoft Association Algorithm](microsoft-association-algorithm.md)을 참조하십시오. **크기** 열에서는 항목 집합에 있는 항목 수를 표시합니다. **항목 집합** 열에서는 모델이 검색한 실제 항목 집합을 표시합니다. **표시** 목록에서 다음 옵션을 설정하여 항목 집합의 형식을 제어할 수 있습니다.  
  
-   **특성 이름 및 값 표시**  
  
-   **특성 값만 표시**  
  
-   **특성 이름만 표시**  
  
 **최소 지원** 및 **최소 항목 집합 크기**를 사용하여 탭에 표시되는 항목 집합 수를 필터링할 수 있습니다. 또한 **항목 집합 필터** 를 통해 필요한 항목 집합 특징을 입력하여 표시되는 항목 집합 수를 더욱 제한할 수 있습니다. 예를 들어 "Water Bottle = existing"을 입력하면 항목 집합을 Water Bottle이 포함된 집합으로 제한할 수 있습니다. **항목 집합 필터** 옵션에서는 이전에 사용한 필터 목록도 표시합니다.  
  
 열 제목을 클릭하여 표에서 행을 정렬할 수 있습니다.  
  
 [맨 위로 이동](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Rules"></a> 규칙  
 **규칙** 탭에서는 연결 알고리즘이 검색한 규칙을 표시합니다. **규칙** 탭에는 **확률**, **중요도**및 **규칙**열로 구성된 표가 있습니다. 확률은 규칙의 결과가 발생할 가능성을 나타내고 중요도는 규칙의 유용성을 측정합니다. 규칙이 발생할 확률은 높아도 규칙 자체의 유용성이 떨어질 수 있습니다. 중요도 열에서는 이러한 측면을 다룹니다. 예를 들어 모든 항목 집합에 특성 상태가 있으면 확률이 매우 높아도 상태를 예측하는 규칙이 중요하지 않습니다. 중요도가 클수록 규칙이 보다 중요해 집니다.  
  
 **항목 집합** 탭에서 수행할 수 있는 필터링과 유사한 방식으로 **최소 확률** 및 **최소 중요도** 를 사용하여 규칙을 필터링할 수 있습니다. **규칙 필터** 를 사용하여 포함된 특성 상태를 기준으로 규칙을 필터링할 수도 있습니다.  
  
 열 제목을 클릭하여 표에서 행을 정렬할 수 있습니다.  
  
 [맨 위로 이동](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Dependency"></a> 종속성 네트워크  
 **종속성 네트워크** 탭에는 종속성 네트워크 뷰어가 있습니다. 뷰어의 각 노드는 "state = WA"와 같은 항목을 나타냅니다. 노드 사이의 화살표는 항목 간의 연결을 나타냅니다. 화살표 방향은 알고리즘이 검색한 규칙에 따른 항목 간의 연결을 표시합니다. 예를 들어 뷰어에 A, B, C라는 항목이 있고 C가 A와 B에 의해 예측된 경우 노드 C를 선택하면 A가 C를 가리키고 B가 C를 가리켜 두 개의 화살표가 노드 C를 가리킵니다.  
  
 뷰어의 왼쪽에 있는 슬라이더는 규칙의 확률에 연결된 필터 역할을 합니다. 슬라이더를 내리면 강력한 링크만 표시됩니다.  
  
 [맨 위로 이동](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft 연결 알고리즘](microsoft-association-algorithm.md)   
 [마이닝 모델 뷰어 태스크 및 방법](mining-model-viewer-tasks-and-how-tos.md)   
 [마이닝 모델 뷰어 태스크 및 방법](mining-model-viewer-tasks-and-how-tos.md)   
 [데이터 마이닝 도구](data-mining-tools.md)   
 [데이터 마이닝 모델 뷰어](data-mining-model-viewers.md)  
  
  
