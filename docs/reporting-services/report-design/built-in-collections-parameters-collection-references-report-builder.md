---
title: "매개 변수 컬렉션 참조 (보고서 작성기 및 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c4b47e15-0484-4c13-9182-898db825f01f
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 17698a3c268e824d2f638042b71b3ec21f994e86
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="built-in-collections---parameters-collection-references-report-builder"></a>기본 제공 컬렉션-매개 변수 컬렉션 참조 (보고서 작성기)
  보고서 매개 변수는 식에서 참조할 수 있는 기본 제공 컬렉션 중 하나입니다. 식에 매개 변수를 포함하면 사용자의 선택에 따라 보고서 데이터와 모양을 사용자 지정할 수 있습니다. 모든 보고서 항목 속성 또는 제공 하는 텍스트 상자 속성에 대 한 식을 사용할 수 있습니다는 (*Fx*) 또는 \< **식**> 옵션입니다. 식은 보고서의 내용과 모양을 다른 방법으로 제어하는 데도 사용됩니다. 자세한 내용은 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)를 참조하세요.  
  
 런타임에 매개 변수 값을 데이터 집합 필드 값과 비교할 때는 비교하는 두 항목의 데이터 형식이 같아야 합니다. 보고서 매개 변수는 다음 유형 중 하나일 수 있습니다. Boolean, DateTime, Integer, Float 또는 Text(기본 데이터 형식인 String을 나타냄). 필요한 경우에는 데이터 집합 값과 일치하도록 매개 변수 값의 데이터 형식을 변환해야 할 수 있습니다. 자세한 내용은 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)을 참조하세요.  
  
 식에 매개 변수 참조를 포함하려면 매개 변수가 단일 값인지 다중값 매개 변수인지에 따라 달라지는 매개 변수 참조의 올바른 구문을 지정하는 방법을 이해해야 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Single"></a> 식에서 단일 값 매개 변수 사용  
 다음 표에서는 식에서 임의 데이터 형식의 단일 값 매개 변수에 대한 참조를 포함할 때 사용할 구문의 예를 보여 줍니다.  
  
|예제|Description|  
|-------------|-----------------|  
|`=Parameters!`* \<ParameterName >*`.IsMultiValue`|**False**를 반환합니다.<br /><br /> 매개 변수가 다중값인지 확인합니다. **True**일 경우 매개 변수는 다중값이며 개체 컬렉션입니다. **False**일 경우 매개 변수는 단일 값이며 단일 개체입니다.|  
|`=Parameters!`* \<ParameterName >*`.Count`|정수 값 1을 반환합니다. 단일 값 매개 변수의 경우 개수는 항상 1입니다.|  
|`=Parameters!`* \<ParameterName >*`.Label`|사용 가능한 값의 드롭다운 목록에서 표시 이름으로 자주 사용되는 매개 변수 레이블을 반환합니다.|  
|`=Parameters!`* \<ParameterName >*`.Value`|매개 변수 값을 반환합니다. Label 속성이 설정되지 않은 경우 이 값은 사용 가능한 값 드롭다운 목록에 표시됩니다.|  
|`=CStr(Parameters!`  *\<ParameterName >*`.Value)`|매개 변수 값을 문자열로 반환합니다.|  
|`=Fields(Parameters!`* \<ParameterName >*`.Value).Value`|매개 변수와 동일한 이름을 갖고 있는 필드에 대해 값을 반환합니다.|  
  
 필터에서 매개 변수를 사용하는 방법은 [데이터 집합 필터, 데이터 영역 필터 및 그룹 필터 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)를 참조하세요.  
  
##  <a name="Multi"></a> 식에서 다중값 매개 변수 사용  
 다음 표에서는 식에서 임의 데이터 형식의 다중값 매개 변수에 대한 참조를 포함할 때 사용할 구문의 예를 보여 줍니다.  
  
|예제|Description|  
|-------------|-----------------|  
|`=Parameters!`* \<MultivalueParameterName >*`.IsMultiValue`|**True** 또는 **False**를 반환합니다.<br /><br /> 매개 변수가 다중값인지 확인합니다. **True**일 경우 매개 변수는 다중값이며 개체 컬렉션입니다. **False**일 경우 매개 변수는 단일 값이며 단일 개체입니다.|  
|`=Parameters!`* \<MultivalueParameterName >*`.Count`|정수 값을 반환합니다.<br /><br /> 값 개수를 나타냅니다. 단일 값 매개 변수의 경우 개수는 항상 1입니다. 다중값 매개 변수의 경우 개수는 0개 이상입니다.|  
|`=Parameters!`* \<MultivalueParameterName >*`.Value(0)`|다중값 매개 변수의 첫 번째 값을 반환합니다.|  
|`=Parameters!`* \<MultivalueParameterName >* `.Value(Parameters!` * \<MultivalueParameterName >*`.Count-1)`|다중값 매개 변수의 마지막 값을 반환합니다.|  
|`=Split("Value1,Value2,Value3",",")`|값 배열을 반환합니다.<br /><br /> 다중값 **String** 매개 변수에 대한 값 배열을 만듭니다. 분할할 두 번째 매개 변수에서 임의의 구분 기호를 사용할 수 있습니다. 다중값 매개 변수에 대한 기본값을 설정하거나, 하위 보고서 또는 드릴스루 보고서에 전송할 다중값 매개 변수를 만드는 데 이 식을 사용할 수 있습니다.|  
|`=Join(Parameters!`* \<MultivalueParameterName >*`.Value,", ")`|다중값 매개 변수에서 쉼표로 구분된 값 목록으로 구성된 **String** 을 반환합니다. 조인할 두 번째 매개 변수에서 임의의 구분 기호를 사용할 수 있습니다.|  
  
 필터에서 매개 변수를 사용하는 방법은 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [일반적으로 사용되는 필터&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/commonly-used-filters-report-builder-and-ssrs.md)   
 [보고서 매개 변수 추가, 변경 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [자습서: 보고서에 매개 변수 추가&#40;보고서 작성기&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [보고서 작성기 자습서](../../reporting-services/report-builder-tutorials.md)   
 [식의 기본 제공 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)  
  
  
