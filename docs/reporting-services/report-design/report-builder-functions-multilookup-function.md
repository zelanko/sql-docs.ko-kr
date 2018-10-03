---
title: Multilookup 함수(보고서 작성기 및 SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 1fec079e-33b3-4e4d-92b3-6b4d06a49a77
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9235e945a9733767c2dbf9ca7c507f516b5b0dac
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47850461"
---
# <a name="report-builder-functions---multilookup-function"></a>보고서 작성기 함수 - Multilookup 함수
  이름/값 쌍을 포함하는 데이터 집합에서 지정된 이름 집합과 처음 일치하는 값 집합을 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>구문  
  
```  
  
Multilookup(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *source_expression*  
 (**VariantArray**) 현재 범위에서 평가되고, 조회할 키 또는 이름의 집합을 지정하는 식입니다. 예를 들어 다중값 매개 변수의 경우 `=Parameters!IDs.value`입니다.  
  
 *destination_expression*  
 (**Variant**) 데이터 집합의 각 행에 대해 평가되고, 일치시킬 키 또는 이름을 지정하는 식입니다. `=Fields!ID.Value`).  
  
 *result_expression*  
 (**Variant**) *source_expression* = *destination_expression*인 데이터 집합의 행에 대해 계산되고 검색할 값을 지정하는 식입니다. `=Fields!Name.Value`).  
  
 *데이터 집합(dataset)*  
 보고서의 데이터 집합 이름을 지정하는 상수입니다. 예를 들면 "Colors"입니다.  
  
## <a name="return"></a>반환 값  
 **VariantArray**를 반환하거나, 일치하는 항목이 없으면 **Nothing** 을 반환합니다.  
  
## <a name="remarks"></a>Remarks  
 **Multilookup** 을 사용하여 일 대 일 관계가 있는 이름 값 쌍의 데이터 집합에서 값 집합을 검색할 수 있습니다. **MultiLookup** 은 이름 또는 키 집합에 대해 **Lookup** 을 호출하는 것과 동일합니다. 예를 들어 기본 키 식별자를 기반으로 하는 다중값 매개 변수의 경우 테이블의 입력란에 있는 식에 **Multilookup** 을 사용하여 매개 변수 또는 테이블에 바인딩되지 않은 데이터 집합에서 연결된 값을 검색할 수 있습니다.  
  
 **Multilookup** 은 다음을 수행합니다.  
  
-   현재 범위에서 원본 식을 평가하고 변형 개체의 배열을 생성합니다.  
  
-   배열의 각 개체에 대해 [Lookup 함수&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-lookup-function.md)를 호출하고 결과를 반환 배열에 추가합니다.  
  
-   결과 집합을 반환합니다.  
  
 일 대 일 관계의 이름-값 쌍을 포함하는 데이터 집합에서 지정된 이름에 대한 단일 값을 검색하려면 [Lookup 함수&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-lookup-function.md)를 사용합니다. 일 대 다 관계의 이름-값 쌍을 포함하는 데이터 집합에서 이름에 대한 여러 값을 검색하려면 [LookupSet 함수&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-lookupset-function.md)를 사용합니다.  
  
 다음과 같은 제한 사항이 있습니다.  
  
-   **Multilookup** 은 모든 필터 식이 적용된 후 평가됩니다.  
  
-   조회 수준이 하나만 지원됩니다. 원본, 대상 또는 결과 식에는 조회 함수에 대한 참조가 포함될 수 없습니다.  
  
-   원본 식과 대상 식의 데이터 형식이 같아야 합니다.  
  
-   원본, 대상 및 결과 식에는 보고서 또는 그룹 변수에 대한 참조가 포함될 수 없습니다.  
  
-   **Multilookup** 은 다음 보고서 항목에 대한 식으로 사용할 수 없습니다.  
  
    -   데이터 원본에 대한 동적 연결 문자열  
  
    -   데이터 집합의 계산된 필드  
  
    -   데이터 집합의 쿼리 매개 변수  
  
    -   데이터 집합의 필터  
  
    -   보고서 매개 변수  
  
    -   Report.Language 속성입니다.  
  
 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) 및 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 "Category"라는 데이터 집합에 CategoryList 필드가 포함되어 있다고 가정합니다. 이 필드는 쉼표로 구분된 범주 식별자 목록(예: "2, 4, 2, 1")을 포함합니다.  
  
 CategoryNames 데이터 집합은 다음 표와 같이 범주 식별자와 범주 이름을 포함합니다.  
  
|ID|속성|  
|--------|----------|  
|1|Accessories|  
|2|Bikes|  
|3|Clothing|  
|4|구성 요소|  
  
 식별자 목록에 해당하는 이름을 조회하려면 **Multilookup**을 사용합니다. 먼저 목록을 문자열 배열로 분할한 다음, **Multilookup** 을 호출하여 범주 이름을 검색하고 결과를 문자열로 연결해야 합니다.  
  
 다음 식을 Category 데이터 집합에 바인딩된 데이터 영역의 입력란에 넣으면 "Bikes, Components, Bikes, Accessories"가 표시됩니다.  
  
```  
=Join(MultiLookup(Split(Fields!CategoryList.Value,","),  
   Fields!CategoryID.Value,Fields!CategoryName.Value,"Category")),  
   ", ")  
```  
  
## <a name="example"></a>예제  
 ProductColors 데이터 집합에 다음 표와 같이 색 식별자 필드 ColorID와 색 값 필드 Color가 포함되어 있다고 가정합니다.  
  
|ColorID|색|  
|-------------|-----------|  
|1|빨강|  
|2|파랑|  
|3|녹색|  
  
 다중값 매개 변수 *MyColors* 가 사용 가능한 값에 대한 데이터 집합에 바인딩되어 있지 않다고 가정합니다. 이 매개 변수의 기본값은 2와 3으로 설정되어 있습니다. 다음 식을 테이블의 입력란에 넣으면 매개 변수에 대해 선택된 여러 값을 쉼표로 구분된 목록으로 연결하고 "Blue, Green"이 표시됩니다.  
  
```  
=Join(MultiLookup(Parameters!MyColors.Value,Fields!ColorID.Value,Fields!Color.Value,"ProductColors"),", ")  
```  
  
## <a name="see-also"></a>참고 항목  
 [보고서에 사용되는 식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
