---
title: 매개 변수 컬렉션 참조(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: c4b47e15-0484-4c13-9182-898db825f01f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c3c9452a9be55c71431a0ed3012769b1f5f6d8eb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106408"
---
# <a name="parameters-collection-references-report-builder-and-ssrs"></a>매개 변수 컬렉션 참조(보고서 작성기 및 SSRS)
  보고서 매개 변수는 식에서 참조할 수 있는 기본 제공 컬렉션 중 하나입니다. 식에 매개 변수를 포함하면 사용자의 선택에 따라 보고서 데이터와 모양을 사용자 지정할 수 있습니다. 식은 (*Fx*) 또는 \<**Expression**> 옵션을 제공하는 모든 보고서 항목 속성 또는 입력란 속성에 사용할 수 있습니다. 식은 보고서의 내용과 모양을 다른 방법으로 제어하는 데도 사용됩니다. 자세한 내용은 [식 예&#40;보고서 작성기 및 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)를 참조하세요.  
  
 런타임에 매개 변수 값을 데이터 세트 필드 값과 비교할 때는 비교하는 두 항목의 데이터 형식이 같아야 합니다. 보고서 매개 변수는 다음 유형 중 하나일 수 있습니다. Boolean, DateTime, Integer, Float 또는 Text(기본 데이터 형식인 String을 나타냄). 필요한 경우에는 데이터 세트 값과 일치하도록 매개 변수 값의 데이터 형식을 변환해야 할 수 있습니다. 자세한 내용은 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)).  
  
 식에 매개 변수 참조를 포함하려면 매개 변수가 단일 값인지 다중값 매개 변수인지에 따라 달라지는 매개 변수 참조의 올바른 구문을 지정하는 방법을 이해해야 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="using-a-single-valued-parameter-in-an-expression"></a><a name="Single"></a> 식에서 단일 값 매개 변수 사용  
 다음 표에서는 식에서 임의 데이터 형식의 단일 값 매개 변수에 대한 참조를 포함할 때 사용할 구문의 예를 보여 줍니다.  
  
|예제|Description|  
|-------------|-----------------|  
|`=Parameters!` *\<ParameterName>* `.IsMultiValue`|`False`를 반환합니다.<br /><br /> 매개 변수가 다중값인지 확인합니다. `True`일 경우 매개 변수는 다중값이며 개체 컬렉션입니다. `False`일 경우 매개 변수는 단일 값이며 단일 개체입니다.|  
|`=Parameters!` *\<ParameterName>* `.Count`|정수 값 1을 반환합니다. 단일 값 매개 변수의 경우 개수는 항상 1입니다.|  
|`=Parameters!` *\<ParameterName>* `.Label`|사용 가능한 값의 드롭다운 목록에서 표시 이름으로 자주 사용되는 매개 변수 레이블을 반환합니다.|  
|`=Parameters!` *\<ParameterName>* `.Value`|매개 변수 값을 반환합니다. Label 속성이 설정되지 않은 경우 이 값은 사용 가능한 값 드롭다운 목록에 표시됩니다.|  
|`=CStr(Parameters!`  *\<ParameterName>* `.Value)`|매개 변수 값을 문자열로 반환합니다.|  
|`=Fields(Parameters!` *\<ParameterName>* `.Value).Value`|매개 변수와 동일한 이름을 갖고 있는 필드에 대해 값을 반환합니다.|  
  
 필터에서 매개 변수를 사용하는 방법은 [데이터 세트 필터, 데이터 영역 필터 및 그룹 필터 추가&#40;보고서 작성기 및 SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)을 참조하세요.  
  
##  <a name="using-a-multivalue-parameter-in-an-expression"></a><a name="Multi"></a> 식에서 다중값 매개 변수 사용  
 다음 표에서는 식에서 임의 데이터 형식의 다중값 매개 변수에 대한 참조를 포함할 때 사용할 구문의 예를 보여 줍니다.  
  
|예제|Description|  
|-------------|-----------------|  
|`=Parameters!` *\<MultivalueParameterName>* `.IsMultiValue`|`True` 또는 `False`를 반환합니다.<br /><br /> 매개 변수가 다중값인지 확인합니다. `True`일 경우 매개 변수는 다중값이며 개체 컬렉션입니다. `False`일 경우 매개 변수는 단일 값이며 단일 개체입니다.|  
|`=Parameters!` *\<MultivalueParameterName>* `.Count`|정수 값을 반환합니다.<br /><br /> 값 개수를 나타냅니다. 단일 값 매개 변수의 경우 개수는 항상 1입니다. 다중값 매개 변수의 경우 개수는 0개 이상입니다.|  
|`=Parameters!` *\<MultivalueParameterName>* `.Value(0)`|다중값 매개 변수의 첫 번째 값을 반환합니다.|  
|`=Parameters!` *\<MultivalueParameterName>* `.Value(Parameters!` *\<MultivalueParameterName>* `.Count-1)`|다중값 매개 변수의 마지막 값을 반환합니다.|  
|`=Split("Value1,Value2,Value3",",")`|값 배열을 반환합니다.<br /><br /> 다중값 `String` 매개 변수에 대한 값 배열을 만듭니다. 분할할 두 번째 매개 변수에서 임의의 구분 기호를 사용할 수 있습니다. 다중값 매개 변수에 대한 기본값을 설정하거나, 하위 보고서 또는 드릴스루 보고서에 전송할 다중값 매개 변수를 만드는 데 이 식을 사용할 수 있습니다.|  
|`=Join(Parameters!` *\<MultivalueParameterName>* `.Value,", ")`|다중값 매개 변수에서 쉼표로 구분된 값 목록으로 구성된 `String`을 반환합니다. 조인할 두 번째 매개 변수에서 임의의 구분 기호를 사용할 수 있습니다.|  
  
 필터에서 매개 변수를 사용하는 방법은 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](report-parameters-report-builder-and-report-designer.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [일반적으로 사용되는 필터&#40;보고서 작성기 및 SSRS&#41;](commonly-used-filters-report-builder-and-ssrs.md)   
 [보고서 매개 변수 추가, 변경 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [자습서: 보고서에 매개 변수 추가&#40;보고서 작성기&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [자습서 &#40;보고서 작성기&#41;](../report-builder-tutorials.md)   
 [식의 기본 제공 컬렉션&#40;보고서 작성기 및 SSRS&#41;](built-in-collections-in-expressions-report-builder.md)  
  
  
