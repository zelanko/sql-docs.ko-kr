---
title: RunningValue 함수(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 6bee2f15-0e69-49c8-9689-b04544063b1d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5176ddc4f06531dcbfea383362bdd195a215fe84
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59941579"
---
# <a name="runningvalue-function-report-builder-and-ssrs"></a>RunningValue 함수(보고서 작성기 및 SSRS)
  식으로 지정되어 정해진 범위에서 계산되는 Null이 아닌 모든 숫자 값의 실행 집계를 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>구문  
  
```  
  
RunningValue(expression, function, scope)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *expression*  
 집계를 수행할 식입니다(예: `[Quantity]`).  
  
 *function*  
 (`Enum`) 식에 적용할 집계 함수의 이름입니다(예: `Sum`). 이 함수는 `RunningValue`, `RowNumber` 또는 `Aggregate`일 수 없습니다.  
  
 *범위*  
 (`String`) 집계를 계산할 컨텍스트를 지정하는 데이터 집합, 데이터 영역, 그룹의 이름인 문자열 상수 또는 Null([!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]의 `Nothing`)입니다. `Nothing`은 가장 바깥쪽 컨텍스트를 지정하며 이는 일반적으로 보고서 데이터 집합입니다.  
  
## <a name="return-type"></a>반환 형식  
 반환 형식은 *function* 매개 변수에 지정된 집계 함수에 의해 결정됩니다.  
  
## <a name="remarks"></a>Remarks  
 `RunningValue` 값은 범위의 각 새로운 인스턴스에 대해 0으로 다시 설정됩니다. 그룹이 지정되어 있는 경우 그룹 식이 변경되면 실행 값이 다시 설정됩니다. 데이터 영역이 지정되어 있는 경우 데이터 영역의 새 인스턴스 각각에 대해 실행 값이 다시 설정됩니다. 데이터 세트가 지정되어 있으면 전체 데이터 세트에서 실행 값이 다시 설정되지 않습니다.  
  
 `RunningValue`는 필터 또는 정렬 식에 사용할 수 없습니다.  
  
 실행 값이 계산되는 데이터 집합의 데이터 형식은 동일해야 합니다. 여러 숫자 데이터 형식이 포함된 데이터를 동일한 데이터 형식으로 변환하려면 `CInt`, `CDbl` 또는 `CDec` 같은 변환 함수를 사용하세요. 자세한 내용은 [형식 변환 함수](https://go.microsoft.com/fwlink/?LinkId=96142)를 참조하세요.  
  
 *Scope* 는 식이 될 수 없습니다.  
  
 *Expression* 에는 다음 예외와 조건이 있는 중첩 집계 함수에 대한 호출이 포함될 수 있습니다.  
  
-   중첩 집계의 범위는 외부 집계의 범위와 동일하거나 외부 집계의 범위에 포함되어야 합니다. 식에 있는 모든 고유 범위의 경우 한 범위는 다른 모든 범위에 대한 자식 관계에 있어야 합니다.  
  
-   중첩 집계의 범위는 데이터 세트의 이름일 수 없습니다.  
  
-   *식을* 없어야 `First`, `Last`, `Previous`, 또는 `RunningValue` 함수입니다.  
  
-   *Expression* 에는 *recursive*를 지정하는 중첩 집계가 포함되지 않아야 합니다.  
  
 행 개수의 실행 값을 계산하려면 `RowNumber`를 사용하세요. 자세한 내용은 [RowNumber 함수&#40;보고서 작성기 및 SSRS&#41;](report-builder-functions-rownumber-function.md)를 참조하세요.  
  
 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) 및 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)를 참조하세요.  
  
 재귀 집계에 대한 자세한 내용은 [재귀 계층 구조 그룹 만들기&#40;보고서 작성기 및 SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="examples"></a>예  
 다음 코드 예에서는 가장 바깥쪽 범위인 데이터 세트에서 `Cost`라는 필드의 실행 합계를 제공합니다.  
  
```  
=RunningValue(Fields!Cost.Value, Sum, Nothing)  
```  
  
 다음 코드 예에서는 `Score` 데이터 세트에서 `DataSet1`라는 필드의 실행 합계를 제공합니다.  
  
```  
=RunningValue(Fields!Score.Value,sum,"DataSet1")  
```  
  
 다음 코드 예에서는 가장 바깥쪽 범위에서 `Traffic Charges` 라는 필드의 실행 합계를 제공합니다.  
  
```  
=RunningValue(Fields!Traffic Charges.Value, Sum, Nothing)  
```  
  
## <a name="see-also"></a>관련 항목  
 [보고서에 사용되는 식&#40;보고서 작성기 및 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
