---
title: 원형 차트에서 백분율 값 표시(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: eb905fc1-5235-4773-a27e-b07be9318be5
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: d8c4cc67ad7a3719db277840e4ca535a373e8b44
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37287019"
---
# <a name="display-percentage-values-on-a-pie-chart-report-builder-and-ssrs"></a>원형 차트에서 백분율 값 표시(보고서 작성기 및 SSRS)
  기본적으로 범주는 범례에 표시되어 각 값을 식별합니다. 범주 레이블을 사용하여 원형 차트에 레이블을 적용했다면 범례에 백분율을 표시하기를 원할 것입니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-percentage-values-as-labels-on-a-pie-chart"></a>원형 차트에 레이블로 백분율 값을 표시하려면  
  
1.  보고서에 원형 차트를 추가합니다. 자세한 내용은 [보고서에 차트 추가&#40;보고서 작성기 및 SSRS&#41;](add-a-chart-to-a-report-report-builder-and-ssrs.md)를 참조하세요.  
  
2.  디자인 화면에서 원형을 마우스 오른쪽 단추로 클릭하고 **데이터 레이블 표시**를 선택합니다. 원형 차트의 각 조각 내에 데이터 레이블이 표시됩니다.  
  
3.  디자인 화면에서 레이블을 마우스 오른쪽 단추로 클릭하고 **계열 레이블 속성**을 선택합니다. **계열 레이블 속성** 대화 상자가 표시됩니다.  
  
4.  형식 `#PERCENT` 에 대 한 합니다 **레이블 데이터** 옵션입니다.  
  
5.  (옵션) 레이블을 표시할 때 사용할 소수 자릿수를 지정하려면 "#PERCENT{P*n*}"를 입력합니다. 여기서 *n* 은 표시할 소수 자릿수입니다. 예를 들어 소수 자릿수를 표시하지 않으려면 "#PERCENT{P0}"를 입력합니다.  
  
### <a name="to-display-percentage-values-in-the-legend-of-a-pie-chart"></a>원형 차트의 범례에 백분율 값을 표시하려면  
  
1.  디자인 화면에서 원형 차트를 마우스 오른쪽 단추로 클릭하고 **계열 속성**을 선택합니다. **계열 속성** 대화 상자가 표시됩니다.  
  
2.  **범례**, 형식 `#PERCENT` 에 대 한 합니다 **사용자 지정 범례 텍스트** 속성입니다.  
  
## <a name="see-also"></a>관련 항목  
 [원형 차트 &#40;보고서 작성기 및 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [차트의 범례 서식 지정 &#40;보고서 작성기 및 SSRS&#41;](chart-legend-formatting-report-builder.md)   
 [원형 차트 외부에 표시 데이터 요소 레이블 &#40;보고서 작성기 및 SSRS&#41;](display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 [원형 차트에서 작은 조각 수집 &#40;보고서 작성기 및 SSRS&#41;](collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)  
  
  
