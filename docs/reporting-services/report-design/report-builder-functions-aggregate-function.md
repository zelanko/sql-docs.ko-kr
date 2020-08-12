---
title: Aggregate 함수(보고서 작성기) | Microsoft Docs
description: Aggregate 함수는 데이터 공급자가 정의한 대로 지정된 식의 사용자 지정 집계를 반환합니다.
ms.date: 03/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 16ce643f-bbb3-40a5-ba78-7aed73156f3e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: aef4411334ee9ca345a5b2f2c8b325c6fd2dae70
ms.sourcegitcommit: 6c2232c4d2c1ce5710296ce97b909f5ed9787f66
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2020
ms.locfileid: "84462417"
---
# <a name="report-builder-functions---aggregate-function"></a>보고서 작성기 함수 - 집계 함수
  데이터 공급자가 정의한 대로 지정한 식의 사용자 지정 집계를 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>구문  
  
```  
  
Aggregate(expression, scope)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *expression*  
 집계를 수행할 식입니다. 식은 단순 필드 참조여야 합니다.  
  
 *범위*  
 (**String**) 집계 함수를 적용할 보고서 항목을 포함하는 데이터 세트, 그룹 또는 데이터 영역의 이름입니다. *Scope* 는 문자열 상수여야 하고 식일 수 없습니다. *scope* 를 지정하지 않은 경우 현재 범위가 사용됩니다.  
  
## <a name="return-type"></a>반환 형식  
 반환 형식은 데이터 공급자에 의해 결정됩니다. 데이터 공급자가 이 함수를 지원하지 않거나 데이터를 사용할 수 없는 경우 **Nothing** 을 반환합니다.  
  
## <a name="remarks"></a>설명  
 **Aggregate** 함수를 통해 외부 데이터 원본에서 계산되는 집계를 사용할 수 있습니다. 이 기능에 대한 지원은 데이터 확장 프로그램에 의해 결정됩니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 처리 확장 프로그램은 MDX 쿼리에서 일반 행 세트를 검색합니다. 결과 집합의 일부 행에는 데이터 원본 서버에서 계산된 집계 값이 포함될 수 있습니다. 이를 *서버 집계*라고 합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]용 그래픽 쿼리 디자이너에서 서버 집계를 보려면 도구 모음에서 **집계 표시** 단추를 사용합니다. 자세한 내용은 [Analysis Services MDX 쿼리 디자이너 사용자 인터페이스&#40;보고서 작성기&#41;](https://msdn.microsoft.com/library/7e288eee-2d37-485e-a6a0-dbba5e041e26)를 참조하세요.  
  
 테이블릭스 데이터 영역의 정보 행에 집계 및 정보 데이터 세트 값의 조합을 표시할 때 서버 집계는 정보 데이터가 아니므로 일반적으로 포함되지 않습니다. 하지만 데이터 세트에 대해 검색된 모든 값을 표시하고 집계 데이터가 계산 및 표시되는 방식을 사용자 지정할 수 있습니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 은(는) 세부 정보 행에 서버 집계를 표시할지 여부를 확인하기 위해 보고서 식에서 **Aggregate** 함수의 사용을 검색합니다. 데이터 영역의 식에 **Aggregate** 를 포함할 경우 서버 집계는 그룹 합계 또는 총합계 행에만 표시되며 정보 행에는 표시되지 않습니다. 서버 집계를 정보 행에 표시하려면 **Aggregate** 함수를 사용하지 마십시오.  
  
 이러한 기본 동작은 **데이터 세트 속성** 대화 상자에서 **부분합을 정보 행으로 해석** 옵션의 값을 수정하여 변경할 수 있습니다. 이 옵션이 **True**로 설정된 경우 서버 집계를 포함한 모든 데이터가 정보 데이터로 표시됩니다. **False**로 설정된 경우 서버 집계가 합계로 표시됩니다. 이 속성에 대한 설정은 이 데이터 세트에 연결되어 있는 모든 데이터 영역에 적용됩니다.  
  
> [!NOTE]
>  **Aggregate** 를 참조하는 보고서 항목에 대한 모든 포함 그룹에는 해당 그룹 식에 대한 단순 필드 참조가 있어야 합니다(예: `[FieldName]`). 복잡한 그룹 식을 사용하는 데이터 영역에서는 **Aggregate** 를 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 처리 확장 프로그램의 경우 **Aggregate** 함수를 사용하여 집계를 지원하려면 쿼리에 **MemberProperty**가 아닌 **LevelProperty**형식의 MDX 필드가 포함되어야 합니다.  
  
 *Expression* 에는 다음 예외와 조건이 있는 중첩 집계 함수에 대한 호출이 포함될 수 있습니다.  
  
-   중첩 집계의*Scope* 는 외부 집계의 범위와 동일하거나 외부 집계의 범위에 포함되어야 합니다. 식에 있는 모든 고유 범위의 경우 한 범위는 다른 모든 범위에 대한 자식 관계에 있어야 합니다.  
  
-   중첩 집계의 *Scope*는 데이터 세트의 이름일 수 없습니다.  
  
-   *Expression* 에는 **First**, **Last**, **Previous**또는 **RunningValue** 함수가 포함되지 않아야 합니다.  
  
-   *Expression* 에는 *recursive*를 지정하는 중첩 집계가 포함되지 않아야 합니다.  
  
 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) 및 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)를 참조하세요.  
  
 재귀 집계에 대한 자세한 내용은 [재귀 계층 구조 그룹 만들기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="comparing-the-aggregate-and-sum-functions"></a>Aggregate 함수와 Sum 함수 비교  
 **Aggregate** 함수는 **Sum** 과 같은 숫자 집계 함수와 다릅니다. 즉, **Aggregate** 함수는 데이터 공급자 또는 데이터 처리 확장 프로그램에 의해 계산되는 값을 반환합니다. **Sum**과 같은 숫자 집계 함수는 *scope* 매개 변수로 결정되는 데이터 세트의 일련의 데이터에 대해 보고서 처리기가 계산하는 값을 반환합니다. 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)에 나열된 집계 함수를 참조하세요.  
  
## <a name="example"></a>예제  
 다음 코드 예에서는 `LineTotal`필드에 대한 서버 집계를 검색하는 식을 보여 줍니다. `GroupbyOrder`그룹에 속하는 행의 셀에 식이 추가됩니다.  
  
```  
=Aggregate(Fields!LineTotal.Value, "GroupbyOrder")  
```  
  
## <a name="see-also"></a>참고 항목  
 [보고서에 사용되는 식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
