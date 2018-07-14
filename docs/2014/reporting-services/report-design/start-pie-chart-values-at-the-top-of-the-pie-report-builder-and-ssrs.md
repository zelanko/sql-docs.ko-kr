---
title: 원형 차트 값을 원형의 위쪽에서 시작(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d0e6fb59-ca4e-4d70-97cb-0ad183da21d3
caps.latest.revision: 5
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 2da5ccaf0fe846a26959970bd9bf3e939b5a2558
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37256262"
---
# <a name="start-pie-chart-values-at-the-top-of-the-pie-report-builder-and-ssrs"></a>원형 차트를 원형의 위쪽에서 시작(보고서 작성기 및 SSRS)
  기본적으로 원형 차트에서는 데이터 집합의 첫 번째 값이 원형의 위쪽으로부터 90도가 되는 지점에서 시작됩니다. 첫 번째 값이 위쪽에서 시작되게 할 수도 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-start-the-pie-chart-at-the-top-of-the-pie"></a>원형 차트가 원형의 위쪽에서 시작되게 하려면  
  
1.  원형 자체를 클릭합니다.  
  
2.  **속성** 창이 열려 있지 않으면 **보기** 탭에서 **속성**을 클릭합니다.  
  
3.  **속성** 창의 **사용자 정의 특성**에서 **PieStartAngle** 을 **0** 에서 **270**으로 변경합니다.  
  
4.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
 이제 첫 번째 값이 원형 차트의 위쪽에서 시작됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [차트 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [원형 차트 &#40;보고서 작성기 및 SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
