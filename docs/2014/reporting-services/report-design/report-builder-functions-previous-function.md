---
title: Previous 함수(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 403a9384-6ca4-42e8-97ca-ac3f6fe4316b
caps.latest.revision: 8
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 65f8f0bdc7db2e58efd27522a93e4edf6c4e0bf3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181514"
---
# <a name="previous-function-report-builder-and-ssrs"></a>Previous 함수(보고서 작성기 및 SSRS)
  지정된 범위 내에서 항목의 이전 인스턴스에 대한 지정된 집계 값 또는 값을 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>구문  
  
```  
  
Previous(expression, scope)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *expression*  
 (`Variant` 또는 `Binary`) 데이터를 식별 하는 데 식 및 예를 들어, 이전 값을 검색할 `Fields!Fieldname.Value` 또는 `Sum(Fields!Fieldname.Value)`합니다.  
  
 *범위*  
 (`String`) 선택 사항입니다. 그룹 또는 데이터 영역 또는 null의 이름 (`Nothing` 에 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)])에 지정 된 이전 값을 검색할 범위를 지정 하는 *식*합니다.  
  
## <a name="return-type"></a>반환 형식  
 반환 된 `Variant` 또는 `Binary`합니다.  
  
## <a name="remarks"></a>Remarks  
 `Previous` 함수는 모든 정렬 및 필터링이 적용된 다음 지정된 범위에서 계산된 식의 이전 값을 반환합니다.  
  
 경우 *식* 집계가 포함 되지 않습니다는 `Previous` 함수의 기본값 보고서 항목에 대 한 현재 범위입니다.  
  
 세부 정보 그룹을 사용 하 여 `Previous` 정보 행의 이전 인스턴스에 필드 참조의 값을 지정할 수 있습니다.  
  
> [!NOTE]  
>  `Previous` 함수 세부 정보 그룹의 필드 참조는 지원 합니다. 예를 들어 세부 정보 그룹의 입력란에서 `=Previous(Fields!Quantity.Value)` 는 이전 행의 `Quantity` 필드에 대한 데이터를 반환합니다. 첫 번째 행에서 이 식은 Null([!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]의 경우 `Nothing`)을 반환합니다.  
  
 경우 *식* 기본 범위를 사용 하는 집계 함수가 포함 된 `Previous` 범위의 이전 인스턴스 내에서 데이터를 집계는 집계를 지정 된 함수 호출 합니다.  
  
 경우 *식* 기본값 이외의 범위를 지정 하는 집계 함수가 포함 된는 *범위* 에 대 한 매개 변수는 `Previous` 함수에 지정 된 범위를 포함 하는 범위 여야 합니다. 집계 함수 호출 합니다.  
  
 함수 `Level`, `InScope`, `Aggregate` 및 `Previous` 에서 사용할 수 없습니다는 *식*매개 변수입니다. 집계 함수에 대해 *recursive* 매개 변수를 지정할 수 없습니다.  
  
 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) 및 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)를 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="description"></a>Description  
 다음 코드 예는 데이터 영역의 기본 데이터 행에 배치될 경우 이전 행의 `LineTotal` 필드에 대한 값을 제공합니다.  
  
### <a name="code"></a>코드  
  
```  
=Previous(Fields!LineTotal.Value)  
```  
  
### <a name="description"></a>Description  
 다음 예에서는 월 중 특정 일에 대한 판매 합계를 계산하고 이전 연도의 해당 월 및 일에 대한 이전 값을 계산하는 식을 보여 줍니다. `GroupbyDay`자식 그룹에 속하는 행의 셀에 식이 추가됩니다. 부모 그룹은 `GroupbyMonth`이며 이 그룹의 부모 그룹은 `GroupbyYear`입니다. 식은 GroupbyDay(기본 범위)에 대한 결과와 `GroupbyYear` ( `GroupbyMonth`부모 그룹의 부모)에 대한 결과를 표시합니다.  
  
 예를 들어 `Year`라는 부모 그룹을 가진 데이터 영역의 경우 자식 그룹의 이름은 `Month`이고 이 그룹의 자식 그룹 이름은 `Day` 가 됩니다(3수준 중첩). `=Previous(Sum(Fields!Sales.Value,"Day"),"Year")` 그룹과 관련된 행에서 `Day` 식을 사용하면 이전 연도의 동일 월 및 일에 대한 판매 값이 반환됩니다.  
  
### <a name="code"></a>코드  
  
```  
=Sum(Fields!Sales.Value) & " " & Previous(Sum(Fields!Sales.Value,"GroupbyDay"),"GroupbyYear")  
```  
  
## <a name="see-also"></a>관련 항목  
 [식은 보고서에서 사용 하 여 &#40;보고서 작성기 및 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [합계, 집계 및 기본 제공 컬렉션의 식 범위 &#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  