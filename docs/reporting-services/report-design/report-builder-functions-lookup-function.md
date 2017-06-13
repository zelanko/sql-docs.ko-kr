---
title: "Lookup 함수 (보고서 작성기 및 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e60e5bab-b286-4897-9685-9ff12703517d
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4426bffe23295c623d0bba5592c1488cb0ede770
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="report-builder-functions---lookup-function"></a>보고서 작성기 함수-Lookup 함수
  이름/값 쌍을 포함하는 데이터 집합에서 지정된 이름과 일치하는 첫 번째 값을 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>구문  
  
```  
  
Lookup(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *source_expression*  
 (**Variant**) 현재 범위에서 평가되고, 조회할 키 또는 이름을 지정하는 식입니다. `=Fields!ProdID.Value`)을 입력합니다.  
  
 *destination_expression*  
 (**Variant**) 데이터 집합의 각 행에 대해 평가되고, 일치시킬 키 또는 이름을 지정하는 식입니다. `=Fields!ProductID.Value`)을 입력합니다.  
  
 *result_expression*  
 (**Variant**) *source_expression* = *destination_expression*인 데이터 집합의 행에 대해 계산되고 검색할 값을 지정하는 식입니다. `=Fields!ProductName.Value`)을 입력합니다.  
  
 *데이터 집합(dataset)*  
 보고서의 데이터 집합 이름을 지정하는 상수입니다. 예를 들면 "Products"입니다.  
  
## <a name="return"></a>반환 값  
 **Variant**를 반환하거나, 일치하는 항목이 없으면 **Nothing** 을 반환합니다.  
  
## <a name="remarks"></a>주의  
 **Lookup** 을 사용하여 일 대 일 관계의 이름/값 쌍에 대한 지정된 데이터 집합에서 값을 검색할 수 있습니다. 예를 들어 테이블에 있는 ID 필드의 경우 **Lookup** 을 사용하여 데이터 영역에 바인딩되지 않은 데이터 집합에서 해당하는 이름 필드를 검색할 수 있습니다.  
  
 **Lookup** 은 다음을 수행합니다.  
  
-   현재 범위에서 원본 식을 평가합니다.  
  
-   지정된 데이터 집합의 데이터 정렬을 기반으로 필터가 적용된 후 지정된 데이터 집합의 각 행에 대해 대상 식을 평가합니다.  
  
-   원본 식과 대상 식의 첫 번째 일치 항목이 발견되면 데이터 집합의 해당 행에 대해 결과 식을 평가합니다.  
  
-   결과 식 값을 반환합니다.  
  
 일 대 다 관계가 있는 경우 단일 이름 또는 키 필드에 대해 여러 값을 검색하려면 [LookupSet 함수&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-lookupset-function.md)를 사용합니다. 값 집합에 대한 **Lookup**을 호출하려면 [Multilookup 함수&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-multilookup-function.md)를 참조하세요.  
  
 다음과 같은 제한 사항이 있습니다.  
  
-   **Lookup** 은 모든 필터 식이 적용된 후 평가됩니다.  
  
-   조회 수준이 하나만 지원됩니다. 원본, 대상 또는 결과 식에는 조회 함수에 대한 참조가 포함될 수 없습니다.  
  
-   원본 식과 대상 식의 데이터 형식이 같아야 합니다. 반환 형식은 평가된 결과 식의 데이터 형식과 같습니다.  
  
-   원본, 대상 및 결과 식에는 보고서 또는 그룹 변수에 대한 참조가 포함될 수 없습니다.  
  
-   **Lookup** 은 다음 보고서 항목에 대한 식으로 사용할 수 없습니다.  
  
    -   데이터 원본에 대한 동적 연결 문자열  
  
    -   데이터 집합의 계산된 필드  
  
    -   데이터 집합의 쿼리 매개 변수  
  
    -   데이터 집합의 필터  
  
    -   보고서 매개 변수  
  
    -   Report.Language 속성입니다.  
  
 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) 및 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 다음 예에서는 제품 식별자 ProductID에 대한 필드를 포함하는 데이터 집합에 테이블이 바인딩되어 있다고 가정합니다. "Product"라는 별도의 데이터 집합에는 해당하는 제품 식별자 ID와 제품 이름 Name이 포함되어 있습니다.  
  
 다음 식에서 **Lookup** 은 ProductID 값을 "Product" 데이터 집합의 각 행에 있는 ID와 비교한 다음, 일치하는 항목이 있으면 해당 행의 Name 필드 값을 반환합니다.  
  
```  
=Lookup(Fields!ProductID.Value, Fields!ID.Value, Fields!Name.Value, "Product")  
```  
  
## <a name="see-also"></a>관련 항목:  
 [보고서에 사용되는 식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
