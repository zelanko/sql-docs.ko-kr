---
title: "축 간격 지정(보고서 작성기 및 SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "09/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ae46712d-a5bf-44c0-9929-e30ccc1e7e33
caps.latest.revision: 14
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 12
---
# 축 간격 지정(보고서 작성기 및 SSRS)
[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]의 페이지를 매긴 보고서에서 축 간격을 설정하여 차트에서 범주(x) 축에 레이블 수와 눈금 수를 변경하는 방법을 알아 봅니다.
 
값 축(일반적으로 y축)에서 축 간격은 차트의 데이터 요소를 일정하게 측정할 수 있도록 합니다. 

하지만 범주 축(일반적으로 x축)에서는 자동 축 간격으로 인해 축 레이블이 없는 범주가 만들어지기도 합니다. 축 Interval 속성에서 원하는 간격 수를 지정할 수 있습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 결과 집합의 데이터를 기반으로 런타임에 간격 수를 계산합니다. 축 간격을 계산하는 방법에 대한 자세한 내용은 [차트의 축 레이블 서식 지정](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)을 참조하세요.  

샘플 데이터로 축 간격을 설정해 보려면 [자습서: 보고서에 세로 막대형 차트 추가](Tutorial:%20Add%20a%20Column%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)를 참조하세요.
  
> [!NOTE]  
>  일반적으로 범주 축은 가로 축 또는 x축이지만 가로 막대형 차트에서는 범주 축이 세로 축 또는 y축입니다.  
>
> 이 항목은 다음에 적용되지 않습니다.
>-   범주 축에서 날짜나 시간 값. 기본적으로 **DateTime** 값은 일로 표시됩니다. 월 또는 시간 간격과 같은 다른 날짜 또는 시간 간격을 지정할 수 있습니다. 자세한 내용은 [축 레이블의 서식을 날짜 또는 통화로 지정](../../reporting-services/report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)을 참조하세요.  
>-  축이 없는 원형, 도넛형, 깔때기형 또는 피라미드형 차트. 
  
## X축에 모든 범주 레이블을 표시하려면  

이 세로 막대형 차트에서 가로 레이블 간격은 자동으로 설정됩니다.

![report-builder-column-chart-preview-x-axis-interval-auto](../../reporting-services/report-design/media/report-builder-column-chart-preview-x-axis-interval-auto.png)
  
1.  범주 축을 마우스 오른쪽 단추로 클릭한 다음 **가로 축 속성**을 클릭합니다.   

    ![report-builder-column-chart-x-axis-labels](../../reporting-services/report-design/media/report-builder-column-chart-x-axis-labels.png)
  
2.  **가로 축 속성** 대화 상자 > **축 옵션** 탭에서 **간격**을 **1**로 설정하여 모든 범주 그룹 레이블을 표시합니다. x축에 다른 모든 범주 그룹 레이블을 표시하려면 **2**를 입력합니다. 

     ![report-builder-column-chart-x-axis-interval-one](../../reporting-services/report-design/media/report-builder-column-chart-x-axis-interval-one.png)
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

    이제 세로 막대형 차트에 가로 축 레이블이 모두 표시됩니다.

    ![report-builder-column-chart-preview-x-axis-interval-one](../../reporting-services/report-design/media/report-builder-column-chart-preview-x-axis-interval-one.png)
  
    > [!NOTE]  
    >  축 간격이 설정되면 모든 자동 레이블 지정이 비활성화됩니다. 축 간격에 대한 값을 지정할 경우 범주 축의 범주 수에 따라 예측할 수 없는 레이블 동작이 발생할 수 있습니다.  

## 속성 창에서 레이블 간격을 변경합니다.

또한 속성 창에서 레이블 간격을 설정할 수 있습니다.

1.  보고서 디자인 뷰에서 차트를 클릭한 다음 가로 축 레이블을 선택합니다.

3. 속성 창에서 LabelInterval을 **1**로 설정합니다.

    ![report-builder-column-chart-set-label-interval](../../reporting-services/media/report-builder-column-chart-set-label-interval.png)

    차트는 디자인 뷰에서 동일하게 보입니다. 
    
5.  **실행** 을 클릭하여 보고서를 미리 봅니다.

    ![report-builder-column-chart-label-interval-one-preview](../../reporting-services/media/report-builder-column-chart-label-interval-one-preview.png)
    
    이제 차트에 해당하는 모든 레이블이 표시됩니다.
  
## 축에서 가변 간격 계산을 사용하려면  

기본적으로 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서는 축 간격을 자동으로 설정합니다. 다음 절차에서는 기본값으로 다시 설정하는 방법을 설명합니다. 
  
1.  변경할 차트 축을 마우스 오른쪽 단추로 클릭한 다음 **축 속성**을 클릭합니다. 
  
2.  **가로 축 속성** 대화 상자 > **축 옵션** 탭에서 **간격**을 **자동**으로 설정합니다. 차트에 축을 따라 배치할 수 있는 최적의 범주 레이블 수가 표시됩니다.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## 관련 항목:  
 [차트 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [차트의 데이터 요소에 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [데이터 영역의 데이터 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [축 속성 대화 상자, 축 옵션&#40;보고서 작성기 및 SSRS&#41;](../Topic/Axis%20Properties%20Dialog%20Box,%20Axis%20Options%20\(Report%20Builder%20and%20SSRS\).md)   
 [로그 눈금 간격 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/specify-a-logarithmic-scale-report-builder-and-ssrs.md)   
 [보조 축에 데이터 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/plot-data-on-a-secondary-axis-report-builder-and-ssrs.md)  
  
  