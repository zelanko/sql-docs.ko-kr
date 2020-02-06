---
title: InScope 함수(보고서 작성기 및 SSRS) | Microsoft Docs
ms.date: 03/08/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: a8cd209a-e5d3-4dce-ab2d-f271f6c54955
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8b6891ec497b3100206b812fbc8da7b0463fa4d3
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "65579493"
---
# <a name="report-builder-functions---inscope-function"></a>보고서 작성기 함수 - InScope 함수
  항목의 현재 인스턴스가 지정한 범위 내에 있는지 여부를 나타냅니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>구문  
  
```  
InScope(scope)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *범위*  
 (**문자열**) 범위를 지정하는 데이터 세트, 데이터 영역 또는 그룹의 이름입니다.  
  
## <a name="return-type"></a>반환 형식  
 **Boolean**을 반환합니다.  
  
## <a name="remarks"></a>설명  
 **InScope** 함수는 *scope*매개 변수로 지정된 범위의 멤버 자격에 대해 보고서 항목의 현재 인스턴스 범위를 테스트합니다.  
  
 *Scope* 는 식이 될 수 없습니다.  
  
 **InScope** 함수는 일반적으로 동적으로 범위가 지정되는 데이터 영역에 사용됩니다. 예를 들어 데이터 영역 셀의 드릴스루 링크에 **InScope** 를 사용하여 클릭한 셀에 따라 다양한 보고서 이름과 다양한 매개 변수 집합을 제공할 수 있습니다. 이러한 예는 다음과 같습니다.  
  
-   드릴스루 링크의 보고서 이름으로 사용된 다음 식은 클릭한 셀이 `ProductDetail` 그룹에 있으면 `Month` 보고서를 열고 그렇지 않으면 `ProductSummary` 보고서를 엽니다.  
  
    ```  
    =Iif(InScope("Month"), "ProductDetail", "ProductSummary")  
    ```  
  
-   드릴스루 보고서 매개 변수의 **Omit** 속성에 사용된 다음 식은 클릭한 셀이 `Product` 그룹에 있는 경우에만 대상 보고서에 매개 변수를 전달합니다.  
  
    ```  
    =Not(InScope("Product"))  
    ```  
  
 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) 및 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 다음 코드 예에서는 항목의 현재 인스턴스가 `Product` 데이터 세트, 데이터 영역 또는 그룹 범위 내에 있는지 여부를 나타냅니다.  
  
```  
=InScope("Product")  
```  
  
## <a name="see-also"></a>참고 항목  
 [보고서에 사용되는 식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
