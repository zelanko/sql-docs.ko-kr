---
title: LookupSet 함수(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 7685acfd-1c8d-420c-993c-903236fbe1ff
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: d84ee2971ca430d87220d07ec461180f5c31f759
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48166403"
---
# <a name="lookupset-function-report-builder-and-ssrs"></a>LookupSet 함수(보고서 작성기 및 SSRS)
  이름/값 쌍을 포함하는 데이터 세트에서 지정된 이름과 일치하는 값 집합을 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>구문  
  
```  
  
LookupSet(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *source_expression*  
 (`Variant`) 현재 범위에서 평가되고, 조회할 키 또는 이름을 지정하는 식입니다.  `=Fields!ID.Value`) 을 입력합니다.  
  
 *destination_expression*  
 (`Variant`) 데이터 집합의 각 행에 대해 평가되고, 일치시킬 키 또는 이름을 지정하는 식입니다.  `=Fields!CustomerID.Value`) 을 입력합니다.  
  
 *result_expression*  
 (`Variant`) 데이터 집합의 행에 대해 평가 되는 식을 위치 *source_expression* = *destination_expression*, 검색할 값을 지정 하 고 있습니다.  `=Fields!PhoneNumber.Value`) 을 입력합니다.  
  
 *데이터 집합(dataset)*  
 보고서의 데이터 세트 이름을 지정하는 상수입니다. 예를 들면 "ContactInformation"입니다.  
  
## <a name="return"></a>반환 값  
 반환 된 `VariantArray`, 또는 `Nothing` 일치 항목이 없는 경우.  
  
## <a name="remarks"></a>Remarks  
 사용 하 여 `LookupSet` 이름/값 쌍에 대해 지정된 된 데이터 집합에서 값의 집합을 검색 하는 1 대 다 관계가 있는 합니다. 예를 들어 테이블의 고객 식별자를 사용할 수 있습니다 `LookupSet` 를 데이터 영역에 바인딩되지 않은 데이터 집합에서 해당 고객에 대 한 모든 연결 된 전화 번호를 검색 합니다.  
  
 `LookupSet` 다음을 수행합니다.  
  
-   현재 범위에서 원본 식을 평가합니다.  
  
-   지정된 데이터 세트의 데이터 정렬을 기반으로 필터가 적용된 후 지정된 데이터 세트의 각 행에 대해 대상 식을 평가합니다.  
  
-   원본 식과 대상 식의 일치 항목을 찾을 때마다 데이터 세트의 해당 행에 대해 결과 식을 평가합니다.  
  
-   결과 식 값의 집합을 반환합니다.  
  
 일 대 일 관계의 이름/값 쌍을 포함하는 데이터 집합에서 지정된 이름에 대한 단일 값을 검색하려면 [Lookup 함수&#40;보고서 작성기 및 SSRS&#41;](report-builder-functions-lookup-function.md)를 사용합니다. 호출할 `Lookup` 값의 집합을 사용 하 여 [Multilookup 함수 &#40;보고서 작성기 및 SSRS&#41;](report-builder-functions-multilookup-function.md)합니다.  
  
 다음과 같은 제한 사항이 있습니다.  
  
-   `LookupSet`은 모든 필터 식이 적용된 후 평가됩니다.  
  
-   조회 수준이 하나만 지원됩니다. 원본, 대상 또는 결과 식에는 조회 함수에 대한 참조가 포함될 수 없습니다.  
  
-   원본 식과 대상 식의 데이터 형식이 같아야 합니다.  
  
-   원본, 대상 및 결과 식에는 보고서 또는 그룹 변수에 대한 참조가 포함될 수 없습니다.  
  
-   `LookupSet` 다음 보고서 항목에 대 한 식으로 사용할 수 없습니다.  
  
    -   데이터 원본에 대한 동적 연결 문자열  
  
    -   데이터 세트의 계산된 필드.  
  
    -   데이터 세트의 쿼리 매개 변수.  
  
    -   데이터 세트의 필터.  
  
    -   보고서 매개 변수  
  
    -   Report.Language 속성입니다.  
  
 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) 및 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 다음 예에서는 영업 지역 식별자 TerritoryGroupID를 포함하는 데이터 세트에 테이블이 바인딩되어 있다고 가정합니다. "Stores"라는 별도의 데이터 세트에는 지역의 모든 매장 목록과 지역 식별자 ID 및 매장 이름 StoreName이 포함되어 있습니다.  
  
 다음 식에서 `LookupSet`은 TerritoryGroupID 값을 "Stores" 데이터 집합에 있는 각 행의 ID와 비교합니다. 일치 항목을 찾을 때마다 해당 행에 대한 StoreName 필드의 값이 결과 집합에 추가됩니다.  
  
```  
=LookupSet(Fields!TerritoryGroupID.Value, Fields!ID.Value, Fields!StoreName.Value, "Stores")  
```  
  
## <a name="example"></a>예제  
 때문에 `LookupSet` 컬렉션을 반환 개체의 텍스트 상자에 직접 결과 식에서 표시할 수 없습니다. 컬렉션에 있는 각 개체의 값을 문자열로 연결할 수 있습니다.  
  
 사용 된 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 함수 `Join` 개체 집합에서 구분 기호로 분리 된 문자열을 만듭니다. 개체를 한 줄로 결합하려면 쉼표를 구분 기호로 사용합니다. 일부 렌더러에서는 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 줄 바꿈(`vbCrLF`)을 구분 기호로 사용하여 각 값을 새 줄에 나열할 수 있습니다.  
  
 텍스트 상자에 대 한 Value 속성으로 사용할 경우 다음 식을 사용 하 여 `Join` 목록을 만듭니다.  
  
```  
=Join(LookupSet(Fields!TerritoryGroupID.Value, Fields!ID.Value, Fields!StoreName.Value, "Stores"),",")  
```  
  
## <a name="example"></a>예제  
 몇 번만 렌더링되는 입력란의 경우 입력란에 값을 표시하는 HTML을 생성하기 위해 사용자 지정 코드를 추가하도록 선택할 수도 있습니다. 입력란에 HTML을 표시하려면 추가 처리 작업이 필요하므로 수천 번 렌더링되는 입력란의 경우에는 이러한 선택이 적합하지 않습니다.  
  
 다음 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 함수를 보고서 정의의 Code 블록에 복사합니다. **MakeList** 는 *result_expression* 에서 반환되는 개체 배열을 사용하고 HTML 태그를 사용하여 정렬되지 않은 목록을 만듭니다. **Length** 는 개체 배열의 항목 수를 반환합니다.  
  
```  
Function MakeList(ByVal items As Object()) As String  
   If items Is Nothing Then  
      Return Nothing  
   End If  
  
   Dim builder As System.Text.StringBuilder =   
      New System.Text.StringBuilder()  
   builder.Append("<ul>")  
  
   For Each item As Object In items  
      builder.Append("<li>")  
      builder.Append(item)  
   Next  
   builder.Append("</ul>")  
  
   Return builder.ToString()  
End Function  
  
Function Length(ByVal items as Object()) as Integer  
   If items is Nothing Then  
      Return 0  
   End If  
   Return items.Length  
End Function  
```  
  
## <a name="example"></a>예제  
 HTML을 생성하려면 함수를 호출해야 합니다. 다음 식을 입력란의 Value 속성에 붙여넣고 텍스트의 태그 형식을 HTML로 설정합니다. 자세한 내용은 [보고서에 HTML 추가&#40;보고서 작성기 및 SSRS&#41;](add-html-into-a-report-report-builder-and-ssrs.md)를 참조하세요.  
  
```  
=Code.MakeList(LookupSet(Fields!TerritoryGroupID.Value, Fields!ID.Value, Fields!StoreName.Value, "Stores"))  
```  
  
## <a name="see-also"></a>관련 항목  
 [보고서에 사용 되는 식 &#40;보고서 작성기 및 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [합계, 집계 및 기본 제공 컬렉션의 식 범위 &#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
