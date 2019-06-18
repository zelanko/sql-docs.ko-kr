---
title: First 함수(보고서 작성기 및 SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: d0914520-30c5-4d63-9b59-8d9342ed63b9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8d7f2db5b2b212dd529ac800819c5aa58b5d121a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65579525"
---
# <a name="report-builder-functions---first-function"></a>보고서 작성기 함수 - First 함수
  지정된 식의 지정된 범위에서 첫 번째 값을 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>구문  
  
```  
  
First(expression, scope)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *expression*  
 (**Variant** 또는 **Binary**) 집계를 수행할 식의 예는 `=Fields!FieldName.Value`와 같습니다.  
  
 *범위*  
 (**문자열**) 선택 사항입니다. 집계 함수를 적용할 보고서 항목을 포함하는 데이터 세트, 그룹 또는 데이터 영역의 이름입니다. *scope* 를 지정하지 않은 경우 현재 범위가 사용됩니다.  
  
## <a name="return-type"></a>반환 형식  
 식 유형에 따라 결정됩니다.  
  
## <a name="remarks"></a>Remarks  
 **First** 함수는 지정된 범위에 모든 정렬 및 필터링을 적용한 후 데이터 집합에서 첫 번째 값을 반환합니다.  
  
 **First** 함수는 그룹 필터 식에서 현재(기본) 범위 외에는 사용할 수 없습니다.  
  
 페이지의 첫 번째와 마지막 항목을 표시하는 사전 스타일의 머리글을 만들기 위해 페이지 머리글에 **First** 를 사용하여 페이지에 대한 **ReportItems** 컬렉션의 첫 번째 값을 반환할 수도 있습니다.  
  
 *scope* 의 값은 문자열 상수여야 하고 식일 수 없습니다. 외부 집계나 다른 집계를 지정하지 않는 집계의 경우 *scope* 는 현재 범위나 포함하는 범위를 참조해야 합니다. 집계의 집계의 경우 중첩 집계는 자식 범위를 지정할 수 있습니다.  
  
 *Expression* 에는 다음 예외와 조건이 있는 중첩 집계 함수에 대한 호출이 포함될 수 있습니다.  
  
-   중첩 집계의*Scope* 는 외부 집계의 범위와 동일하거나 외부 집계의 범위에 포함되어야 합니다. 식에 있는 모든 고유 범위의 경우 한 범위는 다른 모든 범위에 대한 자식 관계에 있어야 합니다.  
  
-   중첩 집계의 *Scope*는 데이터 세트의 이름일 수 없습니다.  
  
-   *Expression* 에는 **First**, **Last**, **Previous**또는 **RunningValue** 함수가 포함되지 않아야 합니다.  
  
-   *Expression* 에는 *recursive*를 지정하는 중첩 집계가 포함되지 않아야 합니다.  
  
 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) 및 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)를 참조하세요.  
  
 재귀 집계에 대한 자세한 내용은 [재귀 계층 구조 그룹 만들기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 다음 코드 예에서는 데이터 영역의 `Category` 그룹에서 첫 번째 제품 번호를 반환합니다.  
  
```  
=First(Fields!ProductNumber.Value, "Category")  
```  
  
## <a name="see-also"></a>참고 항목  
 [보고서에 사용되는 식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
