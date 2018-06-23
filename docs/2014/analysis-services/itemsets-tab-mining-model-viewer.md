---
title: 항목 집합 탭 (마이닝 모델 뷰어) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dm.miningmodeleditor.associationrules.itemsets.f1
ms.assetid: 95b2b805-b142-4064-9c80-4b1b3fe2fe63
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 4fb7491a8c9fd4a3ee4656bac9c45f0f8a365b74
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092286"
---
# <a name="itemsets-tab-mining-model-viewer"></a>항목 집합 탭(마이닝 모델 뷰어)
  **항목 집합** 창을 사용하여 연결 규칙 마이닝 모델에 자주 포함되는 항목 집합을 볼 수 있습니다. 연결 모델에 많은 항목 집합이 포함될 수 있기 때문에 뷰어에 표시되는 항목 집합을 필터링하는 데 도움이 되는 컨트롤이 뷰어에서 제공됩니다.  
  
 **관련 항목:** [Microsoft 연결 알고리즘](data-mining/microsoft-association-algorithm.md), [Microsoft 연결 규칙 뷰어를 사용하여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)  
  
## <a name="options"></a>변수  
 **뷰어 내용 새로 고침**  
 뷰어에서 마이닝 모델을 다시 로드합니다.  
  
 **마이닝 모델**  
 현재 마이닝 구조에서 볼 마이닝 모델을 선택합니다. 관련 뷰어에서 마이닝 모델이 열립니다.  
  
 **뷰어**  
 선택한 마이닝 모델을 보는 데 사용할 뷰어를 선택합니다. 연결 모델에 대한 사용자 지정 뷰어 또는 [!INCLUDE[msCoName](../includes/msconame-md.md)] 일반 콘텐츠 트리 뷰어를 사용할 수 있습니다. 또한 사용 가능한 경우 플러그 인 뷰어를 사용할 수 있습니다.  
  
 **최소 지지도**  
 뷰어에 나타나기 위해 항목 집합이 포함해야 할 최소 지지도를 설정하려면 이 값을 변경합니다. 처음에 모델을 열 때 표시되는 기본값은 모델에서 계산되지만 이 값을 변경하여 더 많거나 적은 항목 집합을 표시할 수 있습니다.  
  
 **최소 항목 집합 크기**  
 항목 집합이 뷰어에 표시되기 위해 항목 집합에 포함되어야 하는 최소 항목 수를 설정하려면 이 값을 변경합니다.  
  
 **항목 집합 필터**  
 뷰어에 나타나는 항목 집합 수를 필터링할 문자열 값을 입력합니다.  
  
 .NET 정규식을 필터 조건으로 입력할 수도 있습니다. 예를 들어 다음 식은 'Road Bottle Cage'가 포함된 모든 항목 집합을 반환합니다.  
  
 `\bRoad\b.\bBottle\b.\bCage\b.*`  
  
 필터 조건이 적용되는 것을 확인하려면 뷰를 새로 고쳐야 할 수 있습니다. **긴 이름 표시** 옵션을 설정하거나 해제하여 목록을 새로 고칠 수도 있습니다.  
  
 기본적으로 필터 조건은 특성-값 조합의 전체 이름에 적용되므로 특성 이름만 보는 경우에는 필터 조건이 올바르게 적용되었는지가 명확하지 않을 수도 있습니다. **표시** 드롭다운 목록을 사용하여 **특성 이름 및 값 표시**를 선택하고 항목 집합의 목록이 올바르게 필터링되었는지 확인할 수 있습니다.  
  
 **표시**  
 뷰어에 항목 집합이 표시되는 방법을 조정합니다. 다음 3가지 옵션 중 하나를 선택할 수 있습니다.  
  
-   특성 이름 및 값 표시  
  
-   특성 값만 표시  
  
-   특성 이름만 표시  
  
 이 옵션은 모델을 다시 쿼리하지 않으며, 표시되는 특성 또는 값만 필터링합니다.  
  
 **긴 이름 표시**  
 마이닝 모델 콘텐츠에 나타나는 항목 집합의 전체 이름을 표시하려면 이 옵션을 선택합니다.  
  
 **최대 행 수**  
 뷰어에 표시되는 항목 집합 수를 제한합니다. 기본적으로 항목 집합은 지지도를 기준으로 내림차순으로 정렬되므로 이 값을 낮추면 가장 일반적인 항목 집합으로 목록이 제한됩니다.  
  
 **지원**  
 각 항목 집합에 대한 지지도를 표시합니다.  
  
 **크기**  
 각 항목 집합에 있는 항목 수를 표시합니다.  
  
 **항목 집합**  
 각 항목 집합에 대한 설명을 표시합니다. 기본적으로 항목 집합은 특성 및 값의 쉼표로 구분된 목록으로 표시됩니다. **표시** 옵션을 사용하여 이러한 항목이 표시되는 방법을 변경할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 알고리즘 &#40;Analysis Services-데이터 마이닝&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [마이닝 모델 뷰어 &#40;데이터 마이닝 모델 디자이너&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [데이터 마이닝 모델 뷰어](data-mining/data-mining-model-viewers.md)  
  
  