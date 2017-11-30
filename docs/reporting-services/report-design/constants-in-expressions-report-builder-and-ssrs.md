---
title: "식의 상수(보고서 작성기 및 SSRS) | Microsoft Docs"
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
ms.assetid: b8ae650b-0f46-4848-b62b-15f8a40751b8
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a8c8fcb95cfc2134b04e77c0fb0fddf3464a706a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="constants-in-expressions-report-builder-and-ssrs"></a>식의 상수(보고서 작성기 및 SSRS)
  상수는 리터럴 텍스트 또는 미리 정의된 텍스트로 구성됩니다. 보고서 처리기는 미리 정의된 상수에 액세스할 수 있으므로 사용자가 식에 상수를 포함하면 이러한 상수가 나타내는 값은 식이 계산되기 전에 대체됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="literal-text"></a>리터럴 텍스트  
 식에서 리터럴 텍스트는 큰따옴표로 묶인 텍스트입니다. 텍스트가 식의 일부가 아닌 경우에는 큰따옴표를 사용하지 않고 입력란에 직접 입력할 수도 있습니다. 입력란 값이 등호(=)로 시작하지 않으면 해당 텍스트는 리터럴 텍스트로 처리됩니다. 다음 표에서는 식에 사용되는 몇 가지 리터럴 텍스트의 예를 보여 줍니다.  
  
|상수|표시 텍스트|식 텍스트|  
|--------------|------------------|---------------------|  
|Report run at:|<\<Expr>>|`="Report run at: " & Globals!ExecutionTime`|  
|Adventure Works Cycles|Adventure Works Cycles|Adventure Works Cycles|  
|[Bracketed display text]|\\[Bracketed display text\\]|[Bracketed display text]|  
  
## <a name="rdl-constants"></a>RDL 상수  
 식에서 RDL(Report Definition Language)로 정의된 상수를 사용할 수 있습니다. **식** 대화 상자에서는 열거 형식이라고도 하는 특정 유효 값만 허용하는 보고서 속성에 대한 식을 만들 경우 상수가 표시됩니다. 다음 표에서는 두 가지 예를 보여 줍니다.  
  
|속성|Description|값|  
|--------------|-----------------|------------|  
|TextAlign|입력란의 텍스트 정렬을 위한 유효한 값|General, Left, Center, Right|  
|BorderStyle|보고서에 추가된 선에 대한 유효한 값|Default, None, Dotted, Dashed, Solid, Double, DashDot, DashDotdot|  
  
## <a name="visual-basic-constants"></a>Visual Basic 상수  
 식에서 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 런타임 라이브러리에 정의된 상수를 사용할 수 있습니다. 예를 들어 **DateInterval.Day**상수를 사용할 수 있습니다. 2008년 1월 10일에 대한 다음 식은 숫자 10을 반환합니다.  
  
 `=DatePart("d",Globals!ExecutionTime)`  
  
## <a name="clr-constants"></a>CLR 상수  
 식에서 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR(공용 언어 런타임)에 정의된 상수를 사용할 수 있습니다. 다음 표에서는 시스템 정의 색의 예를 보여 줍니다.  
  
|상수|Description|  
|--------------|-----------------|  
|MistyRose|배경색을 기반으로 하는 보고서 속성에 대한 식을 만드는 경우 이름으로 색을 지정할 수 있습니다. 유효한 이름은 **식** 대화 상자에 나열됩니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [식 대화 상자](http://msdn.microsoft.com/library/e6c74ccb-4594-4d4f-b958-618d710e34eb)   
 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [식 대화 상자&#40;보고서 작성기&#41;](http://msdn.microsoft.com/library/e89c4d97-5d41-4b55-8695-79329edac15d)  
  
  
