---
title: "차트 (보고서 작성기 및 SSRS)에서 범례 항목 숨기기 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 92256240-0cd5-4be4-8904-d1e3b93cb6b3
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 06f1cf8cde2eb9a9c9aa261188e64aa2fc7afe4b
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="chart-legend---hide-items-report-builder"></a>차트 범례-항목 숨기기 (보고서 작성기)
기본적으로 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 페이지를 매긴 보고서의 셰이프 차트가 아닌 차트에 추가된 모든 계열은 범례에서 항목으로 추가됩니다. 원형, 도넛형, 깔때기형 및 피라미드형 차트의 경우 차트에 계열을 추가하면 범례에 개별 데이터 요소가 추가됩니다.  
  
 범례에서 모든 항목을 숨길 수 있습니다. 범례 항목을 숨기더라도 차트에는 계속 나타납니다. 이 기능은 차트에 추가된 계열에 대한 자세한 정보를 표시하지 않으려는 경우에 유용합니다. 예를 들어 이동 평균과 같은 계산된 계열을 차트에 추가한 경우 원래 계열에 대해서만 자세한 정보가 표시되도록 이 항목을 범례에서 숨길 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-hide-an-item-from-display-in-the-legend"></a>범례에서 항목을 숨기려면  
  
1.  숨기려는 계열을 마우스 오른쪽 단추로 클릭하고 **계열 속성**을 선택합니다.  
  
2.  **범례**를 클릭합니다. **범례에 이 계열 표시 안 함** 옵션을 선택합니다.  
  
    > [!NOTE]  
    >  한 그룹에서 계열을 숨기고 다른 그룹에서는 표시하는 기능은 지원되지 않습니다. **계열 그룹** 영역에 필드를 추가하면 해당 그룹에 속한 모든 계열이 숨겨집니다.  
  
## <a name="see-also"></a>관련 항목:  
 [차트 &#40;의 범례 서식 지정 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)   
 [차트 &#40;의 데이터 요소에 서식 지정 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [범례 항목 &#40;의 텍스트 변경 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/chart-legend-change-item-text-report-builder.md)   
 [차트 &#40; 이동 평균 추가 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/add-a-moving-average-to-a-chart-report-builder-and-ssrs.md)   
 [범례 속성 대화 상자, 일반 &#40; 보고서 작성기 및 SSRS &#41;](http://msdn.microsoft.com/library/db718f8f-f185-422f-871c-96f0749e5893)  
  
  

