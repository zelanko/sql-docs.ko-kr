---
title: Previous 함수(보고서 작성기 및 SSRS) | Microsoft Docs
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
ms.assetid: 403a9384-6ca4-42e8-97ca-ac3f6fe4316b
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f5ce25413eb30996ed6003f33801800a9a132fea
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33025520"
---
# <a name="report-builder-functions---previous-function"></a>보고서 작성기 함수 - Previous 함수
  지정된 범위 내에서 항목의 이전 인스턴스에 대한 지정된 집계 값 또는 값을 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>구문  
  
```  
  
Previous(expression, scope)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *expression*  
 (**Variant** 또는 **이진**) 데이터를 식별하거나 이전 값을 검색하기 위한 식입니다(예: `Fields!Fieldname.Value` 또는 `Sum(Fields!Fieldname.Value)`).  
  
 *범위*  
 (**문자열**) 선택 사항입니다. **expression** 에서 지정된 이전 값을 검색할 범위를 지정하는 그룹 또는 데이터 영역의 이름이거나 Null( [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]의 경우 *Nothing*)입니다.  
  
## <a name="return-type"></a>반환 형식  
 **Variant** 또는 **Binary**를 반환합니다.  
  
## <a name="remarks"></a>Remarks  
 **Previous** 함수는 모든 정렬 및 필터링이 적용된 다음 지정된 범위에서 계산된 식의 이전 값을 반환합니다.  
  
 *expression* 에 집계가 포함되지 않은 경우 **Previous** 함수의 기본값은 보고서 항목에 대한 현재 범위입니다.  
  
 세부 정보 그룹에서 **Previous** 를 사용하여 세부 행의 이전 인스턴스에 필드 참조 값을 지정합니다.  
  
> [!NOTE]  
>  **Previous** 함수는 세부 정보 그룹의 필드 참조만 지원합니다. 예를 들어 세부 정보 그룹의 입력란에서 `=Previous(Fields!Quantity.Value)` 는 이전 행의 `Quantity` 필드에 대한 데이터를 반환합니다. 첫 번째 행에서 이 식은 Null(**의 경우** Nothing [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)])을 반환합니다.  
  
 *expression* 에 기본 범위를 사용하는 집계 함수가 포함된 경우 **Previous** 는 집계 함수 호출에서 지정된 범위의 이전 인스턴스 내에서 데이터를 집계합니다.  
  
 *expression* 에 기본값 이외의 범위를 지정하는 집계 함수가 포함된 경우 *Previous* 함수의 **scope** 매개 변수는 집계 함수 호출에 지정된 범위에 대해 포함하는 범위여야 합니다.  
  
 **Level**, **InScope**, **Aggregate** 및 **Previous** 함수는 *expression*매개 변수에 사용할 수 없습니다. 집계 함수에 대해 *recursive* 매개 변수를 지정할 수 없습니다.  
  
 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) 및 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)를 참조하세요.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [보고서에 사용되는 식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
