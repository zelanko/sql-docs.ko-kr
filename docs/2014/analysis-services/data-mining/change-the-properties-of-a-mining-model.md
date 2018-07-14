---
title: 마이닝 모델의 속성 변경 | Microsoft Docs
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
- mining models [Analysis Services], properties
- properties [data mining]
ms.assetid: aefaeb7f-d174-48d1-a188-0987a3b1196b
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ed77c0d87fc6fb62497cc68c52dd3fabeb50d2ab
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37279817"
---
# <a name="change-the-properties-of-a-mining-model"></a>마이닝 모델의 속성 변경
  일부 마이닝 모델 속성은 모델 전체에 적용되고 다른 모델 속성은 개별 열에 적용됩니다. 전체 모델에 적용 되는 속성의 예로 `Drillthrough` 사례 데이터를 쿼리에 사용할지 여부를 지정 하는 속성 및 `Description` 속성입니다. 열에 적용되는 속성으로는 모델 내에서 열의 데이터가 사용되는 방식을 제어하는 `Usage` 및 `ModelingFlags`가 있습니다.  
  
 다음 모델 속성의 경우 식을 만들거나 복잡한 모델 속성을 구성하는 데 사용할 수 있는 고급 편집기가 제공됩니다.  
  
-   `Filter` 속성: 엽니다는 [데이터 집합 필터 또는 모델 필터 대화 상자](../data-set-filter-or-model-filter-dialog-box.md)합니다.  
  
-   `AlgorithmParameters` 속성: 엽니다는 [알고리즘 매개 변수 대화 상자 &#40;마이닝 모델 뷰&#41;](../algorithm-parameters-dialog-box-mining-models-view.md)합니다.  
  
 마이닝 모델의 속성을 설정하는 방법은 [마이닝 모델 열](mining-model-columns.md)을 참조하세요.  
  
### <a name="to-change-the-properties-of-a-mining-model"></a>마이닝 모델의 속성을 변경하려면  
  
1.  데이터 마이닝 디자이너의 **마이닝 모델** 탭에서 마이닝 모델의 이름이 포함된 열 머리글 또는 마이닝 알고리즘의 이름이 포함된 표의 행을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
2.  화면 오른쪽에 있는 **속성** 창에서 변경할 속성에 해당하는 값을 강조 표시하고 새 값을 입력합니다.  
  
     디자이너에서 다른 요소를 선택하면 새 값이 적용됩니다.  
  
### <a name="to-change-the-properties-of-a-mining-model-column"></a>마이닝 모델 열의 속성을 변경하려면  
  
1.  데이터 마이닝 디자이너의 **마이닝 모델** 탭에서 마이닝 구조 열과 마이닝 모델이 교차하는 지점에 있는 표의 셀을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
2.  화면 오른쪽에 있는 **속성** 창에서 변경할 속성에 해당하는 값을 강조 표시하고 새 값을 입력합니다.  
  
    > [!NOTE]  
    >  열 사용법으로 설정 되어 있으면 `Ignore`는 **속성** 열 창은 비어 있습니다.  
  
     디자이너에서 다른 요소를 선택하면 새 값이 적용됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [마이닝 모델 태스크 및 방법](mining-model-tasks-and-how-tos.md)  
  
  
