---
title: 마이닝 모델의 속성 변경 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models [Analysis Services], properties
- properties [data mining]
ms.assetid: aefaeb7f-d174-48d1-a188-0987a3b1196b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4c34cbfd2ea88d863239c068300c65531fd19f5f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66085876"
---
# <a name="change-the-properties-of-a-mining-model"></a>마이닝 모델의 속성 변경
  일부 마이닝 모델 속성은 모델 전체에 적용되고 다른 모델 속성은 개별 열에 적용됩니다. 모델 전체에 적용되는 속성의 예로는 사례 데이터를 쿼리에 사용할지 여부를 지정하는 `Drillthrough` 속성과 `Description` 속성이 있습니다. 열에 적용되는 속성으로는 모델 내에서 열의 데이터가 사용되는 방식을 제어하는 `Usage` 및 `ModelingFlags`가 있습니다.  
  
 다음 모델 속성의 경우 식을 만들거나 복잡한 모델 속성을 구성하는 데 사용할 수 있는 고급 편집기가 제공됩니다.  
  
-   `Filter`속성: [데이터 집합 필터 또는 모델 필터 대화 상자](../data-set-filter-or-model-filter-dialog-box.md)를 엽니다.  
  
-   `AlgorithmParameters`속성: [마이닝 모델 뷰&#41;&#40;알고리즘 매개 변수 대화 상자 ](../algorithm-parameters-dialog-box-mining-models-view.md)를 엽니다.  
  
 마이닝 모델의 속성을 설정하는 방법은 [마이닝 모델 열](mining-model-columns.md)을 참조하세요.  
  
### <a name="to-change-the-properties-of-a-mining-model"></a>마이닝 모델의 속성을 변경하려면  
  
1.  데이터 마이닝 디자이너의 **마이닝 모델** 탭에서 마이닝 모델의 이름이 포함된 열 머리글 또는 마이닝 알고리즘의 이름이 포함된 표의 행을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
2.  화면 오른쪽에 있는 **속성** 창에서 변경할 속성에 해당하는 값을 강조 표시하고 새 값을 입력합니다.  
  
     디자이너에서 다른 요소를 선택하면 새 값이 적용됩니다.  
  
### <a name="to-change-the-properties-of-a-mining-model-column"></a>마이닝 모델 열의 속성을 변경하려면  
  
1.  데이터 마이닝 디자이너의 **마이닝 모델** 탭에서 마이닝 구조 열과 마이닝 모델이 교차하는 지점에 있는 표의 셀을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
2.  화면 오른쪽에 있는 **속성** 창에서 변경할 속성에 해당하는 값을 강조 표시하고 새 값을 입력합니다.  
  
    > [!NOTE]  
    >  열 사용법을로 `Ignore`설정 하면 해당 열에 대 한 **속성** 창이 비어 있습니다.  
  
     디자이너에서 다른 요소를 선택하면 새 값이 적용됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [마이닝 모델 태스크 및 방법](mining-model-tasks-and-how-tos.md)  
  
  
