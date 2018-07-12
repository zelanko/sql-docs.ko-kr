---
title: Multilookup 함수(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1fec079e-33b3-4e4d-92b3-6b4d06a49a77
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 3022c5d802da527dc1c1bfb062f8a5dca267f50e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37157744"
---
# <a name="multilookup-function-report-builder-and-ssrs"></a>Multilookup 함수(보고서 작성기 및 SSRS)
  이름/값 쌍을 포함하는 데이터 집합에서 지정된 이름 집합과 처음 일치하는 값 집합을 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>구문  
  
```  
  
Multilookup(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *source_expression*  
 (`VariantArray`)는 현재 범위에서 평가 되 고, 조회할 키 또는 이름의 집합을 지정 하는 식입니다. 예를 들어 다중값 매개 변수의 경우 `=Parameters!IDs.value`입니다.  
  
 *destination_expression*  
 (`Variant`) 데이터 집합의 각 행에 대해 평가되고, 일치시킬 키 또는 이름을 지정하는 식입니다. `=Fields!ID.Value`).  
  
 *result_expression*  
 (`Variant`) 데이터 집합의 행에 대해 평가 되는 식을 위치 *source_expression* = *destination_expression*, 검색할 값을 지정 하 고 있습니다. `=Fields!Name.Value`).  
  
 *데이터 집합(dataset)*  
 보고서의 데이터 집합 이름을 지정하는 상수입니다. 예를 들면 "Colors"입니다.  
  
## <a name="return"></a>반환 값  
 반환 된 `VariantArray`, 또는 `Nothing` 일치 항목이 없는 경우.  
  
## <a name="remarks"></a>Remarks  
 사용 하 여 `Multilookup` 를 각 쌍의 1 대 일 관계에 있는 이름-값 쌍에 대 한 데이터 집합에서 값의 집합을 검색 합니다. `MultiLookup` 호출 하는 것과 같습니다 `Lookup` 이름 또는 키 집합에 대 한 합니다. 예를 들어, 기본 키 식별자를 기반으로 하는 다중값 매개 변수를 사용할 수 있습니다 `Multilookup` 매개 변수 또는 테이블에 바인딩되지 않은 데이터 집합에서 연결된 값을 검색할 테이블의 입력란의 식에 있습니다.  
  
 `Multilookup` 다음을 수행합니다.  
  
-   현재 범위에서 원본 식을 평가하고 변형 개체의 배열을 생성합니다.  
  
-   배열의 각 개체에 대해 [Lookup 함수&#40;보고서 작성기 및 SSRS&#41;](report-builder-functions-lookup-function.md)를 호출하고 결과를 반환 배열에 추가합니다.  
  
-   결과 집합을 반환합니다.  
  
 일 대 일 관계의 이름-값 쌍을 포함하는 데이터 집합에서 지정된 이름에 대한 단일 값을 검색하려면 [Lookup 함수&#40;보고서 작성기 및 SSRS&#41;](report-builder-functions-lookup-function.md)를 사용합니다. 일 대 다 관계의 이름-값 쌍을 포함하는 데이터 집합에서 이름에 대한 여러 값을 검색하려면 [LookupSet 함수&#40;보고서 작성기 및 SSRS&#41;](report-builder-functions-lookupset-function.md)를 사용합니다.  
  
 다음과 같은 제한 사항이 있습니다.  
  
-   `Multilookup` 모든 필터 식이 적용 된 후 평가 됩니다.  
  
-   조회 수준이 하나만 지원됩니다. 원본, 대상 또는 결과 식에는 조회 함수에 대한 참조가 포함될 수 없습니다.  
  
-   원본 식과 대상 식의 데이터 형식이 같아야 합니다.  
  
-   원본, 대상 및 결과 식에는 보고서 또는 그룹 변수에 대한 참조가 포함될 수 없습니다.  
  
-   `Multilookup` 다음 보고서 항목에 대 한 식으로 사용할 수 없습니다.  
  
    -   데이터 원본에 대한 동적 연결 문자열  
  
    -   데이터 집합의 계산된 필드  
  
    -   데이터 집합의 쿼리 매개 변수  
  
    -   데이터 집합의 필터  
  
    -   보고서 매개 변수  
  
    -   Report.Language 속성입니다.  
  
 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) 및 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 "Category"라는 데이터 집합에 CategoryList 필드가 포함되어 있다고 가정합니다. 이 필드는 쉼표로 구분된 범주 식별자 목록(예: "2, 4, 2, 1")을 포함합니다.  
  
 CategoryNames 데이터 집합은 다음 표와 같이 범주 식별자와 범주 이름을 포함합니다.  
  
|ID|속성|  
|--------|----------|  
|1|Accessories|  
|2|Bikes|  
|3|Clothing|  
|4|구성 요소|  
  
 식별자 목록에 해당하는 이름을 조회하려면 `Multilookup`을 사용합니다. 먼저 목록 호출을 문자열 배열로 분할 해야 `Multilookup` 하 여 범주 이름을 검색 하 고 결과 문자열에 연결 합니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [보고서에 사용 되는 식 &#40;보고서 작성기 및 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [합계, 집계 및 기본 제공 컬렉션의 식 범위 &#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
