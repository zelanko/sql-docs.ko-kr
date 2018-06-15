---
title: 그룹 식 예(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data [Reporting Services], grouping
- grouping data
- expressions [Reporting Services], adding
- groups [Reporting Services], expressions
ms.assetid: 34cd0249-fc74-4cf2-ba11-7b072992bfd2
caps.latest.revision: 24
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 60639da2f409f6468c909cc341c0880150ba144c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33023390"
---
# <a name="group-expression-examples-report-builder-and-ssrs"></a>그룹 식 예(보고서 작성기 및 SSRS)
  데이터 영역에서 단일 필드를 기준으로 데이터를 그룹화하거나 그룹화할 데이터를 식별하는 보다 복잡한 식을 만들 수 있습니다. 복잡한 식에는 여러 필드 또는 매개 변수에 대한 참조, 조건문 또는 사용자 지정 코드가 포함됩니다. 데이터 영역에 대해 그룹을 정의할 때 이러한 식을 **그룹** 속성에 추가합니다. 자세한 내용은 [데이터 영역에서 그룹 추가 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)를 참조하세요.  
  
 간단한 필드 식을 기반으로 하는 둘 이상의 그룹을 병합하려면 각 필드를 그룹 정의의 그룹 식 목록에 추가합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="examples-of-group-expressions"></a>그룹 식 예  
 다음 표에서는 그룹을 정의하는 데 사용할 수 있는 그룹 식의 예를 보여 줍니다.  
  
|Description|식|  
|-----------------|----------------|  
|`Region` 필드를 기준으로 그룹화합니다.|`=Fields!Region.Value`|  
|성 및 이름을 기준으로 그룹화합니다.|`=Fields!LastName.Value`<br /><br /> `=Fields!FirstName.Value`|  
|성의 첫 문자를 기준으로 그룹화합니다.|`=Fields!LastName.Value.Substring(0,1)`|  
|매개 변수를 기준으로 그룹화합니다(사용자 선택 기반).<br /><br /> 이 예에서 매개 변수 `GroupBy` 는 그룹화할 유효 선택 항목을 제공하는 사용 가능한 값 목록을 기반으로 해야 합니다.|`=Fields(Parameters!GroupBy.Value).Value`|  
|다음과 같은 세 나이 범위를 기준으로 그룹화합니다.<br /><br /> "21세 미만", "21-50세", "51세 이상"|`=IIF(First(Fields!Age.Value)<21,"Under 21",(IIF(First(Fields!Age.Value)>=21 AND First(Fields!Age.Value)<=50,"Between 21 and 50","Over 50")))`|  
|많은 나이 범위를 기준으로 그룹화합니다. 이 예에서는 다음 범위에 대한 문자열을 반환하는 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET으로 작성된 사용자 지정 코드를 보여 줍니다.<br /><br /> 25세 이하<br /><br /> 26-50세<br /><br /> 51 ~ 75<br /><br /> 76세 이상|`=Code.GetRangeValueByAge(Fields!Age.Value)`<br /><br /> 사용자 지정 코드:<br /><br /> `Function GetRangeValueByAge(ByVal age As Integer) As String`<br /><br /> `Select Case age`<br /><br /> `Case 0 To 25`<br /><br /> `GetRangeValueByByAge = "25 or Under"`<br /><br /> `Case 26 To 50`<br /><br /> `GetRangeValueByByAge = "26 to 50"`<br /><br /> `Case 51 to 75`<br /><br /> `GetRangeValueByByAge = "51 to 75"`<br /><br /> `Case Else`<br /><br /> `GetRangeValueByByAge = "Over 75"`<br /><br /> `End Select`<br /><br /> `Return GetRangeValueByByAge`<br /><br /> `End Function`|  
  
## <a name="see-also"></a>참고 항목  
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [보고서 디자이너의 식에 포함된 사용자 지정 코드 및 어셈블리 참조&#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)  
  
  
