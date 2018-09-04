---
title: CountRows 함수(보고서 작성기 및 SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: 5b1c403d-6afd-44c8-b5f6-5ecff2a29a45
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cfc17d7989ea3f65f7800a83d809c08042bd8bfc
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43279915"
---
# <a name="report-builder-functions---countrows-function"></a>보고서 작성기 함수 - CountRows 함수
  Null 값을 가진 행을 포함하여 지정된 범위의 행 수를 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>구문  
  
```  
  
CountRows(scope, recursive)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *범위*  
 (**String**) 계산할 보고서 항목이 포함된 데이터 집합, 데이터 영역 또는 그룹의 이름입니다.  
  
 *재귀*  
 (**열거 형식**) 선택 사항입니다. **Simple** (기본값) 또는 **RdlRecursive**입니다. 집계를 재귀적으로 수행할지 여부를 지정합니다.  
  
## <a name="return-type"></a>반환 형식  
 **Integer**를 반환합니다.  
  
## <a name="remarks"></a>Remarks  
 **CountRows** 는 Null 값을 가진 행을 포함하여 지정된 범위의 모든 행을 계산합니다.  
  
 *scope* 값은 식이 될 수 없으며 현재 범위 또는 포함하는 범위를 참조해야 합니다.  
  
 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) 및 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)를 참조하세요.  
  
 재귀 집계에 대한 자세한 내용은 [재귀 계층 구조 그룹 만들기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 다음 코드 예에서는 `GroupbyCategory` 라는 행 그룹에 있는 행의 수를 계산하는 식을 보여 줍니다( `[Category]`식 기반).  
  
```  
="Number of rows: " & CountRows("GroupbyCategory")  
```  
  
## <a name="see-also"></a>참고 항목  
 [보고서에 사용되는 식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
