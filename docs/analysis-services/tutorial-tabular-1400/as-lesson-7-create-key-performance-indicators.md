---
title: "Analysis Services tutorial 7 단원: 핵심 성과 지표 만들기 | Microsoft Docs"
description: "Analysis Services tutorial 프로젝트에서 핵심 성과 지표를 만드는 방법을 설명 합니다."
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
ms.openlocfilehash: d4036297bdfc8d2c75061951ff329d20378a57a2
ms.sourcegitcommit: 7ed8c61fb54e3963e451bfb7f80c6a3899d93322
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/20/2018
---
# <a name="create-key-performance-indicators"></a>KPI(핵심 성과 지표) 만들기

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

이 단원에서는 핵심 성과 지표 (Kpi)를 만듭니다. Kpi는 정의 된 값의 성능을 측정 하는 데 사용 되는 *자료* 측정값에 대해는 *대상* 측정값으로 또는 절대값으로 정의 된 값입니다. 비즈니스 전문가는 보고 클라이언트 응용 프로그램에서 KPI를 사용하여 비즈니스 성취도에 대한 빠르고 이해하기 쉬운 요약 정보를 얻거나 추세를 확인할 수 있습니다. 자세한 내용은 참고 [Kpi](../tabular-models/kpis-ssas-tabular.md)
  
이 단원에 소요되는 예상 시간: **15분**  
  
## <a name="prerequisites"></a>필수 구성 요소  

이 문서는 순서 대로 완료 해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 완료 해야 이전 단원: [6 단원: 측정값 만들기](../tutorial-tabular-1400/as-lesson-6-create-measures.md)합니다.   
  
## <a name="create-key-performance-indicators"></a>KPI(핵심 성과 지표) 만들기  
  
#### <a name="to-create-an-internetcurrentquartersalesperformance-kpi"></a>InternetCurrentQuarterSalesPerformance KPI를 만들려면  
  
1.  모델 디자이너에서 클릭 된 **FactInternetSales** 테이블입니다.  
  
2.  측정값 표에서 빈 셀을 클릭합니다.  
  
3.  테이블 위의 수식 입력줄에 다음 수식을 입력합니다. 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    이 측정값은 KPI에 대 한 기본 측정값으로 사용 됩니다.  
  
4.  측정값 표에서 마우스 오른쪽 단추로 클릭 **InternetCurrentQuarterSalesPerformance** > **KPI 만들기**합니다.   
  
5.  KPI 핵심 성과 지표 () 대화 상자에서에 **대상** 선택 **절대값**, 한 다음 입력 **1.1**합니다.  
  
7.  왼쪽(아래쪽) 슬라이더 필드에서 **1**을 입력한 다음 오른쪽(위쪽) 슬라이더 필드에서 **1.07**을 입력합니다.  
  
8.  **아이콘 스타일 선택**에서 다이아몬드(빨간색), 삼각형(노란색), 원(녹색) 아이콘 유형을 선택합니다.
  
    ![as-lesson7-kpi](../tutorial-tabular-1400/media/as-lesson7-kpi.png)
    
    > [!TIP]  
    > 확장 가능한 확인 **설명** 가능한 아이콘 스타일 아래에 레이블을 합니다. 여러 KPI 요소에 대 한 설명을 사용 하 여 클라이언트 응용 프로그램에서 쉽게 식별할 수 있도록 합니다.  
  
9. **확인** 을 클릭하여 KPI를 완성합니다.  
  
    측정값 표에서 아이콘을 옆에 확인 된 **InternetCurrentQuarterSalesPerformance** 측정값입니다. 이 아이콘은 이 측정값이 KPI의 기본 측정값으로 사용됨을 나타냅니다.  
  
#### <a name="to-create-an-internetcurrentquartermarginperformance-kpi"></a>InternetCurrentQuarterMarginPerformance KPI를 만들려면  
  
1.  에 대 한 측정값 표에서 **FactInternetSales** 테이블에서 빈 셀을 클릭 합니다.  
  
2.  테이블 위의 수식 입력줄에 다음 수식을 입력합니다.  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  마우스 오른쪽 단추로 클릭 **InternetCurrentQuarterMarginPerformance** > **KPI를 만들려면**합니다.  
  
4.  KPI 핵심 성과 지표 () 대화 상자에서에 **대상** 선택 **절대값**, 한 다음 입력 **1.25**합니다.   
  
5.  필드에 표시 될 때까지 슬라이드 왼쪽된 (아래쪽) 슬라이더 필드에서 **0.8**, 이동한 다음 오른쪽 (위쪽) 슬라이더 필드를 필드에 표시 될 때까지 **1.03**합니다.  
  
6.  **아이콘 스타일 선택**에서 다이아몬드(빨간색), 삼각형(노란색), 원(녹색) 아이콘 유형을 선택한 다음 **확인**을 클릭합니다.  
  
## <a name="whats-next"></a>다음 단계

[8 단원: 큐브 뷰 만들기](../tutorial-tabular-1400/as-lesson-8-create-perspectives.md)합니다.
  
  
