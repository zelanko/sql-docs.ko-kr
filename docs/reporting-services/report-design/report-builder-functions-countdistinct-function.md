---
title: CountDistinct 함수(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 902c251e-e1e8-41d2-ac20-5bb6138ac410
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8c0d4ee82f130b7b6db732814ebe33483921b80b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33024360"
---
# <a name="report-builder-functions---countdistinct-function"></a>보고서 작성기 함수 - CountDistinct 함수
  식으로 지정되어 정해진 범위의 컨텍스트에서 계산되는 Null이 아닌 모든 고유 값의 수를 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>구문  
  
```  
  
CountDistinct(expression, scope, recursive)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *expression*  
 (**Variant**) 집계를 수행할 식입니다.  
  
 *범위*  
 (**문자열**) 선택 사항입니다. 집계 함수를 적용할 보고서 항목을 포함하는 데이터 집합, 그룹 또는 데이터 영역의 이름입니다. *scope* 를 지정하지 않은 경우 현재 범위가 사용됩니다.  
  
 *재귀*  
 (**열거 형식**) 선택 사항입니다. **Simple** (기본값) 또는 **RdlRecursive**입니다. 집계를 재귀적으로 수행할지 여부를 지정합니다.  
  
## <a name="return-type"></a>반환 형식  
 **Integer**를 반환합니다.  
  
## <a name="remarks"></a>Remarks  
 *scope* 의 값은 문자열 상수여야 하고 식일 수 없습니다. 외부 집계나 다른 집계를 지정하지 않는 집계의 경우 *scope* 는 현재 범위나 포함하는 범위를 참조해야 합니다. 집계의 집계의 경우 중첩 집계는 자식 범위를 지정할 수 있습니다.  
  
 *Expression* 에는 다음 예외와 조건이 있는 중첩 집계 함수에 대한 호출이 포함될 수 있습니다.  
  
-   중첩 집계의*Scope* 는 외부 집계의 범위와 동일하거나 외부 집계의 범위에 포함되어야 합니다. 식에 있는 모든 고유 범위의 경우 한 범위는 다른 모든 범위에 대한 자식 관계에 있어야 합니다.  
  
-   중첩 집계의*Scope* 는 데이터 집합의 이름일 수 없습니다.  
  
-   *Expression* 에는 **First**, **Last**, **Previous**또는 **RunningValue** 함수가 포함되지 않아야 합니다.  
  
-   *Expression* 에는 *recursive*를 지정하는 중첩 집계가 포함되지 않아야 합니다.  
  
 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) 및 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)를 참조하세요.  
  
 재귀 집계에 대한 자세한 내용은 [재귀 계층 구조 그룹 만들기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 다음 코드 예에서는 기본 범위 및 부모 그룹 범위에 대해 Null이 아닌 고유한 `Size` 값의 수를 계산하는 식을 보여 줍니다. `GroupbySubcategory`자식 그룹에 속하는 행의 셀에 식이 추가됩니다. 부모 그룹은 `GroupbyCategory`입니다. 식은 `GroupbySubcategory` (기본 범위)에 대한 결과를 표시한 후 `GroupbyCategory` (부모 그룹 범위)에 대한 결과를 표시합니다.  
  
> [!NOTE]  
>  식은 실제 캐리지 리턴 및 줄 바꿈을 포함할 수 없습니다. 코드 예의 이러한 항목은 설명서 작성의 편의를 위해 포함되었습니다. 다음 예를 복사할 경우 각 줄에서 캐리지 리턴을 제거하십시오.  
  
```  
="Distinct count (Subcategory): " & CountDistinct(Fields!Size.Value) &   
"Distinct count (Category): " & CountDistinct(Fields!Size.Value,"GroupbyCategory")  
```  
  
## <a name="see-also"></a>참고 항목  
 [보고서에 사용되는 식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
