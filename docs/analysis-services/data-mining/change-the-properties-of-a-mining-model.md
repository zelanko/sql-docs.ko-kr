---
title: "마이닝 모델의 속성 변경 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "마이닝 모델 [Analysis Services], 속성"
  - "속성 [데이터 마이닝]"
ms.assetid: aefaeb7f-d174-48d1-a188-0987a3b1196b
caps.latest.revision: 38
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 38
---
# 마이닝 모델의 속성 변경
  일부 마이닝 모델 속성은 모델 전체에 적용되고 다른 모델 속성은 개별 열에 적용됩니다. 모델 전체에 적용되는 속성의 예로는 사례 데이터를 쿼리에 사용할지 여부를 지정하는 **Drillthrough** 속성과 **Description** 속성이 있습니다. 열에 적용되는 속성으로는 모델 내에서 열의 데이터가 사용되는 방식을 제어하는 **Usage** 및 **ModelingFlags**가 있습니다.  
  
 다음 모델 속성의 경우 식을 만들거나 복잡한 모델 속성을 구성하는 데 사용할 수 있는 고급 편집기가 제공됩니다.  
  
-   **Filter** 속성: [데이터 집합 필터 또는 모델 필터 대화 상자](../Topic/Data%20Set%20Filter%20or%20Model%20Filter%20Dialog%20Box.md)를 엽니다.  
  
-   **AlgorithmParameters** 속성: [알고리즘 매개 변수 대화 상자&#40;마이닝 모델 뷰&#41;](../Topic/Algorithm%20Parameters%20Dialog%20Box%20\(Mining%20Models%20View\).md)를 엽니다.  
  
 마이닝 모델의 속성을 설정하는 방법은 [마이닝 모델 열](../../analysis-services/data-mining/mining-model-columns.md)을 참조하세요.  
  
### 마이닝 모델의 속성을 변경하려면  
  
1.  데이터 마이닝 디자이너의 **마이닝 모델** 탭에서 마이닝 모델의 이름이 포함된 열 머리글 또는 마이닝 알고리즘의 이름이 포함된 표의 행을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
2.  화면 오른쪽에 있는 **속성** 창에서 변경할 속성에 해당하는 값을 강조 표시하고 새 값을 입력합니다.  
  
     디자이너에서 다른 요소를 선택하면 새 값이 적용됩니다.  
  
### 마이닝 모델 열의 속성을 변경하려면  
  
1.  데이터 마이닝 디자이너의 **마이닝 모델** 탭에서 마이닝 구조 열과 마이닝 모델이 교차하는 지점에 있는 표의 셀을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
2.  화면 오른쪽에 있는 **속성** 창에서 변경할 속성에 해당하는 값을 강조 표시하고 새 값을 입력합니다.  
  
    > [!NOTE]  
    >  열 사용법이 **Ignore**로 설정되어 있을 경우 해당 열의 **속성** 창은 비어 있습니다.  
  
     디자이너에서 다른 요소를 선택하면 새 값이 적용됩니다.  
  
## 관련 항목:  
 [마이닝 모델 태스크 및 방법](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  