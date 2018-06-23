---
title: Count 함수(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7b50b101-daf8-4fb0-ae04-57384755779f
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: e623374290e9620d048d651683a58bfcd3ddf573
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172607"
---
# <a name="count-function-report-builder-and-ssrs"></a>Count 함수(보고서 작성기 및 SSRS)
  식으로 지정되어 정해진 범위의 컨텍스트에서 계산되는 Null이 아닌 값의 개수를 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>구문  
  
```  
  
Count(expression, scope, recursive)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *expression*  
 (`Variant` 또는 `Binary`) 예를 들어 집계를 수행할 식 `=Fields!FieldName.Value`합니다.  
  
 *범위*  
 (`String`) 항목을 집계 함수를 적용할 보고서가 포함 된 데이터 집합, 그룹 또는 데이터 영역의 이름입니다. *scope* 를 지정하지 않은 경우 현재 범위가 사용됩니다.  
  
 *재귀*  
 (**열거 형식**) 선택 사항입니다. `Simple` (기본값) 또는 `RdlRecursive`합니다. 집계를 재귀적으로 수행할지 여부를 지정합니다.  
  
## <a name="return-type"></a>반환 형식  
 반환 된 `Integer`합니다.  
  
## <a name="remarks"></a>Remarks  
 *scope* 의 값은 문자열 상수여야 하고 식일 수 없습니다. 외부 집계나 다른 집계를 지정하지 않는 집계의 경우 *scope* 는 현재 범위나 포함하는 범위를 참조해야 합니다. 집계의 집계의 경우 중첩 집계는 자식 범위를 지정할 수 있습니다.  
  
 *Expression* 에는 다음 예외와 조건이 있는 중첩 집계 함수에 대한 호출이 포함될 수 있습니다.  
  
-   중첩 집계의*Scope* 는 외부 집계의 범위와 동일하거나 외부 집계의 범위에 포함되어야 합니다. 식에 있는 모든 고유 범위의 경우 한 범위는 다른 모든 범위에 대한 자식 관계에 있어야 합니다.  
  
-   중첩 집계의*Scope* 는 데이터 집합의 이름일 수 없습니다.  
  
-   *식* 포함 되지 않아야 `First`, `Last`, `Previous`, 또는 `RunningValue` 함수입니다.  
  
-   *Expression* 에는 *recursive*를 지정하는 중첩 집계가 포함되지 않아야 합니다.  
  
 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) 및 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)를 참조하세요.  
  
 재귀 집계에 대한 자세한 내용은 [재귀 계층 구조 그룹 만들기&#40;보고서 작성기 및 SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)를 참조하세요.  
  
 예제  
  
## <a name="description"></a>Description  
 다음 코드 예에서는 기본 범위 및 부모 그룹 범위에 대해 Null이 아닌 `Size` 값의 수를 계산하는 식을 보여 줍니다. `GroupbySubcategory`자식 그룹에 속하는 행의 셀에 식이 추가됩니다. 부모 그룹은 `GroupbyCategory`입니다. 식은 `GroupbySubcategory` (기본 범위)에 대한 결과를 표시한 후 `GroupbyCategory` (부모 그룹 범위)에 대한 결과를 표시합니다.  
  
> [!NOTE]  
>  식은 실제 캐리지 리턴 및 줄 바꿈을 포함할 수 없습니다. 예의 이러한 항목은 설명서 작성의 편의를 위해 포함되었습니다. 다음 예를 복사할 경우 각 줄에서 캐리지 리턴을 제거하십시오.  
  
## <a name="code"></a>코드  
  
```  
="Count (Subcategory): " & Count(Fields!Size.Value) &   
"Count (Category): " & Count(Fields!Size.Value,"GroupbyCategory")  
```  
  
## <a name="see-also"></a>관련 항목  
 [식은 보고서에서 사용 하 여 &#40;보고서 작성기 및 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [합계, 집계 및 기본 제공 컬렉션의 식 범위 &#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  