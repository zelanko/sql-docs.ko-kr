---
title: "8단원: 핵심 성과 지표 만들기 | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: a6c8ac2b-64ba-456f-b418-7bf0afe145d1
caps.latest.revision: 18
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 8단원: 핵심 성과 지표 만들기
이 단원에서는 KPI(핵심 성과 지표)를 만듭니다. KPI는 *기본* 측정값으로 정의된 값을 측정값이나 절대값으로 정의된 *대상* 값과 비교하여 값 성과를 측정하는 데 사용됩니다. 비즈니스 전문가는 보고 클라이언트 응용 프로그램에서 KPI를 사용하여 비즈니스 성취도에 대한 빠르고 이해하기 쉬운 요약 정보를 얻거나 추세를 확인할 수 있습니다. 자세한 내용은 [KPI&#40;SSAS 테이블 형식&#41;](../analysis-services/tabular-models/kpis-ssas-tabular.md)를 참조하세요.  
  
이 단원에 소요되는 예상 시간: **15분**  
  
## 필수 구성 요소  
이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행하려면 이전 단원인 [7단원: 측정값 만들기](../analysis-services/lesson-7-create-measures.md)를 완료해야 합니다.  
  
## KPI(핵심 성과 지표) 만들기  
  
#### Internet Current Quarter Sales Performance KPI를 만들려면  
  
1.  모델 디자이너에서 **Internet Sales** 테이블(탭)을 클릭합니다.  
  
2.  측정값 표에서 빈 셀을 클릭합니다.  
  
3.  테이블 위의 수식 입력줄에 다음 수식을 입력합니다.  
  
    **Internet Current Quarter Sales Performance :=IFERROR([Internet Current Quarter Sales]/[Internet Previous Quarter Sales Proportion to QTD],BLANK())**  
  
    수식 작성을 마쳤으면 Enter 키를 누릅니다.  
  
    이 측정값은 KPI의 기본 측정값으로 사용됩니다.  
  
4.  측정값 표에서 **Internet Current Quarter Sales Performance** 측정값을 마우스 오른쪽 단추로 클릭하고 **KPI 만들기**를 클릭합니다.  
  
    **핵심 성과 지표** 대화 상자가 열립니다.  
  
5.  **KPI(핵심 성과 지표)** 대화 상자의 **대상**에서 **절대값**선택합니다.  
  
6.  **절대값** 필드에서 **1.1**을 입력하고 Enter 키를 누릅니다.  
  
7.  왼쪽(아래쪽) 슬라이더 필드에서 **1**을 입력한 다음 오른쪽(위쪽) 슬라이더 필드에서 **1.07**을 입력합니다.  
  
8.  **아이콘 스타일 선택**에서 다이아몬드(빨간색), 삼각형(노란색), 원(녹색) 아이콘 유형을 선택합니다.  
  
    > [!TIP]  
    > 사용 가능한 아이콘 스타일 아래에 확장 가능한 **설명** 필드가 표시됩니다. 여러 KPI 요소에 대한 설명을 입력하여 클라이언트 응용 프로그램에서 KPI를 알아보기 쉽게 만들 수 있습니다.  
  
9. **확인**을 클릭하여 KPI를 완성합니다.  
  
    측정값 표에서 **Internet Current Quarter Sales Performance** 측정값 옆의 아이콘을 확인합니다. 이 아이콘은 이 측정값이 KPI의 기본 측정값으로 사용됨을 나타냅니다.  
  
#### Internet Current Quarter Margin Performance KPI를 만들려면  
  
1.  **Internet Sales** 테이블의 측정값 표에서 빈 셀을 클릭합니다.  
  
2.  테이블 위의 수식 입력줄에 다음 수식을 입력합니다.  
  
    **Internet Current Quarter Margin Performance :=IF([Internet Previous Quarter Margin Proportion to QTD]<>0,([Internet Current Quarter Margin]-[Internet Previous Quarter Margin Proportion to QTD])/[Internet Previous Quarter Margin Proportion to QTD],BLANK())**  
  
    수식 작성을 마쳤으면 Enter 키를 누릅니다.  
  
3.  측정값 표에서 **Internet Current Quarter Margin Performance** 측정값을 마우스 오른쪽 단추로 클릭하고 **KPI 만들기**를 클릭합니다.  
  
4.  **핵심 성과 지표** 대화 상자의 **대상 값 정의**에서 **절대값** 옵션을 선택합니다.  
  
5.  **절대값** 필드에서 **1.25**를 입력합니다.  
  
6.  **상태 임계값 정의**에서 왼쪽(아래쪽) 슬라이더 필드에 **0.8**이 표시될 때까지 슬라이더를 이동한 다음 오른쪽(위쪽) 슬라이더 필드에 **1.03**이 표시될 때까지 슬라이더를 이동합니다.  
  
7.  **아이콘 스타일 선택**에서 다이아몬드(빨간색), 삼각형(노란색), 원(녹색) 아이콘 유형을 선택한 다음 **확인**을 클릭합니다.  
  
## 다음 단계  
이 자습서를 계속하려면 다음 단원인 [9단원: 큐브 뷰 만들기](../Topic/Lesson%209:%20Create%20Perspectives.md)로 이동하세요.  
  
  
  
