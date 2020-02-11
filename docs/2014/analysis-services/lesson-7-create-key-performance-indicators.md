---
title: '8 단원: 핵심 성과 지표 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a6c8ac2b-64ba-456f-b418-7bf0afe145d1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1d9d3145583670fb849321bac5b57928caacfbc2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66078366"
---
# <a name="lesson-8-create-key-performance-indicators"></a>8단원: 핵심 성과 지표 만들기
  이 단원에서는 KPI(핵심 성과 지표)를 만듭니다. KPI는 *대상* 값에 대해, *기본* 측정값에 정의되고 측정값 또는 절대값으로도 정의된 값의 성과를 측정하는 데 사용됩니다. 보고 클라이언트 애플리케이션에서, 비즈니스 전문가는 KPI를 통해 비즈니스 성공 요약 및 추세 파악을 신속하고 간편하게 파악할 수 있습니다. 자세한 내용은 [KPI&#40;SSAS 테이블 형식&#41;](tabular-models/kpis-ssas-tabular.md)를 참조하세요.  
  
 이 단원을 완료하기 위한 예상 시간: **15분**  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다. 이 단원의 태스크를 수행하려면 이전 단원인 [7단원: 측정값 만들기](lesson-6-create-measures.md)를 완료해야 합니다.  
  
## <a name="create-key-performance-indicators"></a>핵심 성과 지표 만들기  
  
#### <a name="to-create-an-internet-current-quarter-sales-performance-kpi"></a>Internet Current Quarter Sales Performance KPI를 만들려면  
  
1.  모델 디자이너에서 **Internet Sales** 테이블(탭)을 클릭합니다.  
  
2.  측정값 표에서 빈 셀을 클릭합니다.  
  
3.  테이블 위의 수식 입력줄에 다음 수식을 입력합니다.  
  
     `Internet Current Quarter Sales Performance :=IFERROR([Internet Current Quarter Sales]/[Internet Previous Quarter Sales Proportion to QTD],BLANK())`  
  
     수식 작성을 마쳤으면 Enter 키를 누릅니다.  
  
     이 측정값을 KPI에 대한 기본 측정값으로 제공합니다.  
  
4.  측정값 표에서 **Internet Current Quarter Sales Performance** 측정값을 마우스 오른쪽 단추로 클릭하고 **KPI 만들기**를 클릭합니다.  
  
     
  **핵심 성과 지표** 대화 상자가 열립니다.  
  
5.  
  **핵심 성과 지표** 대화 상자의 **대상 값 정의**에서 **절대값** 옵션을 선택합니다.  
  
6.  **절대 값** 필드에를 입력 `1.1`한 다음 enter 키를 누릅니다.  
  
7.  **상태 임계값 정의**의 왼쪽 (낮음) 슬라이더 필드에를 입력 `1`하 고 오른쪽 (높음) 슬라이더 필드에를 입력 `1.07`합니다.  
  
8.  
  **아이콘 스타일 선택**에서 다이아몬드(빨간색), 삼각형(노란색), 원형(녹색) 아이콘 유형을 선택합니다.  
  
    > [!TIP]  
    >  사용 가능한 아이콘 스타일 아래에 확장 가능한 **설명** 필드가 표시됩니다. 여러 KPI 요소에 대한 설명을 입력하여 클라이언트 애플리케이션에서 KPI를 알아보기 쉽게 만들 수 있습니다.  
  
9. 
  **확인**을 클릭하여 KPI를 완료합니다.  
  
     측정값 표에서 **Internet Current Quarter Sales Performance** 측정값 옆의 아이콘을 확인합니다. 이 아이콘은 이 측정값이 KPI에 대한 기본값으로 제공됨을 나타냅니다.  
  
#### <a name="to-create-an-internet-current-quarter-margin-performance-kpi"></a>Internet Current Quarter Margin Performance KPI를 만들려면  
  
1.  
  **Internet Sales** 테이블의 측정값 표에서 빈 셀을 클릭합니다.  
  
2.  테이블 위의 수식 입력줄에 다음 수식을 입력합니다.  
  
     `Internet Current Quarter Margin Performance :=IF([Internet Previous Quarter Margin Proportion to QTD]<>0,([Internet Current Quarter Margin]-[Internet Previous Quarter Margin Proportion to QTD])/[Internet Previous Quarter Margin Proportion to QTD],BLANK())`  
  
     수식 작성을 마쳤으면 Enter 키를 누릅니다.  
  
3.  측정값 표에서 **Internet Current Quarter Margin Performance** 측정값을 마우스 오른쪽 단추로 클릭하고 **KPI 만들기**를 클릭합니다.  
  
4.  
  **핵심 성과 지표** 대화 상자의 **대상 값 정의**에서 **절대값** 옵션을 선택합니다.  
  
5.  **절대 값** 필드에를 입력 `1.25`합니다.  
  
6.  
  **상태 임계값 정의**에서 왼쪽(아래쪽) 슬라이더 필드에 **0.8**이 표시될 때까지 슬라이더를 이동한 다음 오른쪽(위쪽) 슬라이더 필드에 **1.03**이 표시될 때까지 슬라이더를 이동합니다.  
  
7.  
  **아이콘 스타일 선택**에서 다이아몬드(빨간색), 삼각형(노란색), 원형(녹색) 아이콘 유형을 선택하고 **확인**을 클릭합니다.  
  
## <a name="next-step"></a>다음 단계  
 이 자습서를 계속하려면 다음 단원인 [9단원: 큐브 뷰 만들기](lesson-8-create-perspectives.md)로 이동하세요.  
  
  
