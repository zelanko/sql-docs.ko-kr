---
title: "식 (보고서 작성기 및 SSRS)를 사용 하 여 표시기 크기 지정 | Microsoft Docs"
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
ms.assetid: ab0b86f1-4882-4258-a2b6-c612faecfa4b
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 50bf03c9ad36de5e98451705aaae5c0afa79c70b
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="specify-the-size-of-an-indicator-using-an-expression-report-builder-and-ssrs"></a>식을 사용하여 표시기 크기 지정(보고서 작성기 및 SSRS)
  색, 방향 및 모양 외에 크기도 표시기의 시각적 효과를 최대화하는 데 사용할 수 있습니다.  
  
 표시기에는 IndicatorStates라는 표시기 상태 컬렉션이 있습니다. 일반적으로 IndicatorStates 컬렉션에는 여러 상태가 있습니다. 각 상태는 컬렉션의 멤버이며 아이콘으로 표시됩니다. 이러한 상태가 함께 IndicatorsStates 컬렉션을 구성합니다.  
  
 아이콘 크기를 동적으로 구성하려면 보고서 작성기의 속성 창에서 IndicatorsStates 컬렉션 멤버의 속성을 설정합니다. **속성** 창이 표시되지 않으면 **보기** 탭을 클릭하고 **속성**을 선택합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서는 **속성** 창을 사용하여 멤버 속성을 설정합니다. **속성** 창이 열리지 않으면 F4 키를 누릅니다.  
  
 **속성** 창에서 표시기의 IndicatorStates 컬렉션 속성에 액세스할 수 있습니다. 아이콘을 다양한 크기로 구성하려면 식을 사용하여 IndicatorStates 컬렉션 멤버의 ScaleFactor 속성을 설정합니다. 자세한 내용은 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)을 참조하세요.  
  
 이 절차에서 사용된 식이 [표시기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)에 표시된 다양한 크기의 표시기가 포함된 보고서를 생성하는 데도 사용되었습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-the-indicator-icon-size-using-an-expression"></a>식을 사용하여 표시기 아이콘 크기를 지정하려면  
  
1.  변경할 표시기를 클릭합니다.  
  
2.  속성 창에서 IndicatorStates 속성을 찾습니다.  
  
     속성 창이 범주별로 구성된 경우 IndicatorStates는 **상태** 범주에 있습니다.  
  
3.  IndicatorStates 옆에 있는 줄임표 **(...)** 단추를 클릭합니다. **IndicatorState 컬렉션 편집기** 대화 상자가 열립니다.  
  
     컬렉션 멤버를 모두 선택합니다.  
  
4.  **다중 선택 속성** 목록에서 ScaleFactor 옆의 아래쪽 화살표를 클릭하고 **식**을 클릭합니다.  
  
5.  **식** 대화 상자에서 식을 작성합니다.  
  
     다음 예제 식은 **SalesYTD** 필드의 값을 기준으로 아이콘을 다른 크기로 만듭니다.  
  
     `=IIF(Fields!SalesYTD.value = 0,0,Fields!SalesYTD.value/Max(Fields!SalesYTD.value,"Indicator"))`  
  
     자세한 내용은 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)를 참조하세요.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>관련 항목:  
 [표시기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  
