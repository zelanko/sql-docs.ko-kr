---
title: 로그 눈금 간격 지정(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f3092c1c-b128-433d-9a95-983508b2a8d4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0910888603528d899f0180bf96c66cfbea045aa4
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66104953"
---
# <a name="specify-a-logarithmic-scale-report-builder-and-ssrs"></a>로그 눈금 간격 지정(보고서 작성기 및 SSRS)
  로그 비례하는 데이터가 있는 경우 차트에서 로그 눈금 간격을 사용할 수 있습니다. 이렇게 하면 데이터를 관리하기가 쉬워지므로 차트의 모양이 개선됩니다. 대부분의 로그 눈금 간격은 기준으로 10을 사용합니다.  
  
 이 기능은 값 축에서만 사용할 수 있습니다. 값 축은 일반적으로 세로 축 또는 Y축이지만 가로 막대형 차트에서는 가로 축 또는 X축입니다.  
  
 축이 로그로 표현된 경우 해당 축과 관련된 다른 모든 속성에도 로그 눈금 간격이 사용됩니다. 예를 들어 축에 상용 로그 눈금 간격을 지정한 경우 축 간격을 2로 설정하면 10의 2제곱, 즉 100 크기로 간격이 생성됩니다. 즉, 축 값은 기본 결과인 1, 10, 100, 1000, 10000 대신 1, 100, 10000으로 표시됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-a-logarithmic-scale"></a>로그 눈금 간격을 지정하려면  
  
1.  차트의 Y축을 마우스 오른쪽 단추로 클릭하고 **세로 축 속성**을 클릭합니다. **VerticalAxis 속성** 대화 상자가 나타납니다.  
  
2.  **축 옵션**에서 **로그 눈금 간격 사용**을 선택합니다.  
  
3.  **로그 밑** 입력란에 로그 밑으로 사용할 양수 값을 입력합니다. 값을 지정하지 않으면 로그 밑에는 기본값인 10이 사용됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [차트의 축 레이블 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [차트 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [축 레이블의 서식을 날짜 또는 통화로 지정&#40;보고서 작성기 및 SSRS&#41;](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [차트&#40;보고서 작성기 및 SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
