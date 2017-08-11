---
title: "원형 차트 (보고서 작성기 및 SSRS) 원형의 위쪽에서 시작 | Microsoft Docs"
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
ms.assetid: d0e6fb59-ca4e-4d70-97cb-0ad183da21d3
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8a12864064849ffc3bb0fa6937833ffee57e0df5
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="start-pie-chart-values-at-the-top-of-the-pie-report-builder-and-ssrs"></a>원형 차트를 원형의 위쪽에서 시작(보고서 작성기 및 SSRS)
[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 페이지를 매긴 보고서의 원형 차트에서는 기본적으로 데이터 집합의 첫 번째 값이 원형의 위쪽으로부터 90도에서 시작합니다. 

![report-builder-pie-chart-start-at-90](../../reporting-services/media/report-builder-pie-chart-start-at-90.png)

*차트 값이 90도에서 시작합니다.*

첫 번째 값이 맨 위에서 시작하도록 설정할 수 있습니다. 

![report-builder-pie-chart-start-at-top](../../reporting-services/media/report-builder-pie-chart-start-at-top.png)

*차트 값이 차트의 맨 위에서 시작합니다.*
  
## <a name="to-start-the-pie-chart-at-the-top-of-the-pie"></a>원형 차트가 원형의 위쪽에서 시작되게 하려면  
  
1.  원형 자체를 클릭합니다.  
  
2.  **속성** 창이 열려 있지 않으면 **보기** 탭에서 **속성**을 클릭합니다.  
  
3.  **속성** 창의 **사용자 정의 특성**에서 **PieStartAngle** 을 **0** 에서 **270**으로 변경합니다.  
  
4.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
 이제 첫 번째 값이 원형 차트의 위쪽에서 시작됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [차트 &#40; 서식 지정 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [원형 차트 &#40; 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)  
  
  
