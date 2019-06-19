---
title: 규칙 탭 (마이닝 모델 뷰어) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.associationrules.rules.f1
ms.assetid: 705d5492-b58f-45d9-94d7-ed57b7025823
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fca78578046122a1598df096e45965367b7880ad
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070096"
---
# <a name="rules-tab-mining-model-viewer"></a>규칙 탭(마이닝 모델 뷰어)
  연결 모델의 **규칙** 창을 사용하여 알고리즘이 데이터에서 추출한 규칙을 볼 수 있습니다. 규칙은 항목이 어떻게 서로 관련되어 있는지를 설명하며 권장 항목을 만드는 데 사용할 수 있습니다.  
  
 이 뷰어의 옵션을 사용하여 뷰어에 표시되는 규칙 수를 필터링할 수 있습니다.  
  
> [!WARNING]  
>  기본적으로 **최소 확률** 에 정의된 확률 임계값을 초과하는 규칙만 뷰어에 표시됩니다. 규칙 출력의 확률 임계값은 모델이 만들어질 때 결정되기 때문에 뷰어를 사용하여 이 값을 작게 만들 수 없습니다. 자세한 내용은 [Microsoft 연결 알고리즘 기술 참조](data-mining/microsoft-association-algorithm-technical-reference.md)를 참조하세요.  
  
 **참조 항목:** [Microsoft 연결 알고리즘](data-mining/microsoft-association-algorithm.md), [Microsoft 연결 규칙 뷰어를 사용 하 여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)  
  
## <a name="options"></a>변수  
 **뷰어 내용 새로 고침**  
 뷰어에서 마이닝 모델을 다시 로드합니다.  
  
 **마이닝 모델**  
 현재 마이닝 구조에서 볼 마이닝 모델을 선택합니다. 관련 뷰어에서 마이닝 모델이 열립니다.  
  
 **Viewer**  
 선택한 마이닝 모델을 보는 데 사용할 뷰어를 선택합니다. 각 마이닝 모델에 대한 사용자 지정 뷰어 또는 **Microsoft 일반 콘텐츠 트리 뷰어**를 사용할 수 있습니다. 또한 사용 가능한 경우 플러그 인 뷰어를 사용할 수 있습니다.  
  
 **최소 확률**  
 뷰어에 표시될 규칙에 필요한 최소 확률을 설정하려면 이 값을 변경합니다. 확률 값을 늘리면 표시되는 규칙 수가 줄어듭니다.  
  
 **최소 중요도**  
 뷰어에 표시될 규칙에 필요한 최소 중요도를 설정하려면 이 값을 변경합니다. 중요도 값을 늘리면 표시되는 규칙 수가 줄어듭니다.  
  
 **규칙 필터**  
 뷰어에 나타나는 규칙 수를 필터링할 문자열 값을 입력합니다.  
  
 .NET 정규식을 필터 조건으로 입력할 수도 있습니다. 예를 들어 다음 식은 규칙의 왼쪽에 'Road Bottle Cage'가 포함된 모든 규칙을 반환합니다.  
  
 `\bRoad\b.\bBottle\b.\bCage\b.*->.*`  
  
 필터 조건이 적용되는 것을 확인하려면 뷰를 새로 고쳐야 할 수 있습니다. **긴 이름 표시** 옵션을 설정하거나 해제하여 목록을 새로 고칠 수도 있습니다.  
  
 기본적으로 필터 조건은 특성-값 조합의 전체 이름에 적용되므로 특성 이름만 보는 경우에는 필터 조건이 올바르게 적용되었는지가 명확하지 않을 수도 있습니다. **표시** 드롭다운 목록을 사용하여 **특성 이름 및 값 표시**를 선택하고 항목 집합의 목록이 올바르게 필터링되었는지 확인할 수 있습니다.  
  
 **표시**  
 규칙이 뷰어에 표시되는 방법을 조정합니다. 다음 3가지 옵션 중 하나를 선택할 수 있습니다.  
  
-   특성 이름 및 값 표시  
  
-   특성 값만 표시  
  
-   특성 이름만 표시  
  
 **긴 이름 표시**  
 마이닝 모델 콘텐츠에 나타나는 규칙의 전체 이름을 표시합니다.  
  
 **최대 행 수**  
 뷰어에 표시되는 규칙 수를 제한합니다.  
  
 **확률**  
 차트의 이 열에 각 규칙에 대한 확률이 표시됩니다.  
  
 열 머리글을 클릭하여 확률별로 정렬할 수 있습니다.  
  
 **중요도**  
 차트의 이 열에 각 규칙에 대한 중요도가 표시됩니다.  
  
 열 머리글을 클릭하여 중요도별로 정렬할 수 있습니다.  
  
 **규칙**  
 차트의 이 열에 **표시** 및 **긴 이름 표시**옵션을 사용하여 지정된 형식에 따라 각 규칙에 대한 텍스트 설명이 표시됩니다.  
  
 열 머리글을 클릭하여 규칙의 텍스트별로 정렬할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [마이닝 모델 뷰어&#40;데이터 마이닝 모델 디자이너&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [데이터 마이닝 모델 뷰어](data-mining/data-mining-model-viewers.md)  
  
  
