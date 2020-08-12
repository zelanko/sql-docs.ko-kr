---
title: 차트에서 범례 항목 숨기기(보고서 작성기) | Microsoft Docs
description: 보고서 작성기에서 필수 데이터를 표시하기 위해 범례에 표시되는 항목을 선택하는 방법을 알아봅니다.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 92256240-0cd5-4be4-8904-d1e3b93cb6b3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5f745b3eb2c862f4105bcdd872a8915845341942
ms.sourcegitcommit: 02b22274da4a103760a376c4ddf26c4829018454
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2020
ms.locfileid: "84681422"
---
# <a name="chart-legend---hide-items-report-builder"></a>차트 범례 - 항목 숨기기(보고서 작성기)
기본적으로 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 페이지를 매긴 보고서의 셰이프 차트가 아닌 차트에 추가된 모든 계열은 범례에서 항목으로 추가됩니다. 원형, 도넛형, 깔때기형 및 피라미드형 차트의 경우 차트에 계열을 추가하면 범례에 개별 데이터 요소가 추가됩니다.  
  
 범례에서 모든 항목을 숨길 수 있습니다. 범례 항목을 숨기더라도 차트에는 계속 나타납니다. 이 기능은 차트에 추가된 계열에 대한 자세한 정보를 표시하지 않으려는 경우에 유용합니다. 예를 들어 이동 평균과 같은 계산된 계열을 차트에 추가한 경우 원래 계열에 대해서만 자세한 정보가 표시되도록 이 항목을 범례에서 숨길 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-hide-an-item-from-display-in-the-legend"></a>범례에서 항목을 숨기려면  
  
1.  숨기려는 계열을 마우스 오른쪽 단추로 클릭하고 **계열 속성**을 선택합니다.  
  
2.  **범례**를 클릭합니다. **범례에 이 계열 표시 안 함** 옵션을 선택합니다.  
  
    > [!NOTE]  
    >  한 그룹에서 계열을 숨기고 다른 그룹에서는 표시하는 기능은 지원되지 않습니다. **계열 그룹** 영역에 필드를 추가하면 해당 그룹에 속한 모든 계열이 숨겨집니다.  
  
## <a name="see-also"></a>참고 항목  
 [차트의 범례 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)   
 [차트의 데이터 요소에 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [범례 항목의 텍스트 변경&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/chart-legend-change-item-text-report-builder.md)   
 [차트에 이동 평균 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-a-moving-average-to-a-chart-report-builder-and-ssrs.md)   
 [범례 속성 대화 상자, 일반&#40;보고서 작성기 및 SSRS&#41;](https://msdn.microsoft.com/library/db718f8f-f185-422f-871c-96f0749e5893)  
  
  
