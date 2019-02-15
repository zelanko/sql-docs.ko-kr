---
title: 축 간격 지정(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: ae46712d-a5bf-44c0-9929-e30ccc1e7e33
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: fd2b4d8d8b883fd5cb4dd22aca9d64537d1bcd79
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56291841"
---
# <a name="specify-an-axis-interval-report-builder-and-ssrs"></a>축 간격 지정(보고서 작성기 및 SSRS)
  축 간격은 축에 있는 레이블 및 해당 눈금 표시의 수를 정의합니다. 값 축에서 축 간격은 차트의 데이터 요소를 일정하게 측정할 수 있도록 합니다. 그러나 범주 축에서는 이 기능 때문에 범주가 축 레이블 없이 표시될 수 있습니다. 축 Interval 속성에서 원하는 간격 수를 지정할 수 있습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 결과 집합의 데이터를 기반으로 런타임에 간격 수를 계산합니다. 축 간격을 계산하는 방법에 대한 자세한 내용은 [차트의 축 레이블 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)을 참조하세요.  
  
 이 항목은 범주 축의 날짜 또는 시간 값에는 적용되지 않습니다. 기본적으로 `DateTime` 값은 일로 표시됩니다. 월 또는 시간 간격과 같은 다른 날짜 또는 시간 간격을 지정하려면 축 레이블의 서식을 지정하고 `DateTime` 형식 대신 `String` 형식의 인스턴스를 표시하도록 축을 설정해야 합니다. 또한 Interval 속성을 설정해야 합니다. 자세한 내용은 [축 레이블의 서식을 날짜 또는 통화로 지정&#40;보고서 작성기 및 SSRS&#41;](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)을 참조하세요.  
  
 이 항목은 축이 없는 원형, 도넛형, 깔때기형 또는 피라미드형 차트에는 적용되지 않습니다.  
  
> [!NOTE]  
>  일반적으로 범주 축은 가로 축 또는 x축이지만 가로 막대형 차트에서는 범주 축이 세로 축 또는 y축입니다.  
  
 다른 축 간격을 지정하는 차트의 예는 예제 보고서로 제공됩니다. 이 샘플 보고서 및 기타 보고서를 다운로드하는 방법은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][보고서 작성기 및 보고서 디자이너 샘플 보고서](https://go.microsoft.com/fwlink/?LinkId=198283).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-show-all-category-labels-on-the-x-axis"></a>X축에 모든 범주 레이블을 표시하려면  
  
1.  범주 축을 마우스 오른쪽 단추로 클릭하고 **축 속성**을 클릭합니다. **축 속성** 대화 상자가 열립니다.  
  
2.  **축 옵션**설정 `Interval` 하려면 **1**합니다. 모든 범주 그룹 레이블이 표시됩니다. x축에 다른 모든 범주 그룹 레이블을 표시하려면 **2**를 입력합니다.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  축 간격이 설정되면 모든 자동 레이블 지정이 비활성화됩니다. 축 간격에 대한 값을 지정할 경우 범주 축의 범주 수에 따라 예측할 수 없는 레이블 동작이 발생할 수 있습니다.  
  
### <a name="to-enable-a-variable-interval-calculation-on-an-axis"></a>축에서 가변 간격 계산을 사용하려면  
  
1.  변경할 차트 축을 마우스 오른쪽 단추로 클릭한 다음 **축 속성**을 클릭합니다. **축 속성** 대화 상자가 열립니다.  
  
2.  **축 옵션**설정 `Interval` 하려면 **자동**합니다. 차트에 축을 따라 배치할 수 있는 최적의 범주 레이블 수가 표시됩니다.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [차트 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [차트의 데이터 요소에 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [데이터 영역의 데이터 정렬&#40;보고서 작성기 및 SSRS&#41;](sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [축 속성 대화 상자, 축 옵션&#40;보고서 작성기 및 SSRS&#41;](../axis-properties-dialog-box-axis-options-report-builder-and-ssrs.md)   
 [로그 눈금 간격 지정&#40;보고서 작성기 및 SSRS&#41;](specify-a-logarithmic-scale-report-builder-and-ssrs.md)   
 [보조 축에 데이터 표시&#40;보고서 작성기 및 SSRS&#41;](plot-data-on-a-secondary-axis-report-builder-and-ssrs.md)  
  
  
