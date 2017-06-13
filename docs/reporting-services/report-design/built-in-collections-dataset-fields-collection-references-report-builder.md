---
title: "데이터 집합 필드 컬렉션 참조 (보고서 작성기 및 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 006c6bd3-d776-4c20-9092-32e40688ac49
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: df288358b8fd8b209adda5c52af5f23f878541e9
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="built-in-collections---dataset-fields-collection-references-report-builder"></a>기본 제공 컬렉션-데이터 집합 필드 컬렉션 참조 (보고서 작성기)
  보고서의 각 데이터 집합에는 Fields 컬렉션이 하나씩 있습니다. Fields 컬렉션은 데이터 집합 쿼리에서 지정하는 필드와 사용자가 만드는 모든 추가 계산 필드의 집합입니다. 데이터 집합을 만든 후 필드 컬렉션이 **보고서 데이터** 창에 표시됩니다.  
  
 식의 단순 필드 참조가 디자인 화면에 단순 식으로 표시됩니다. 예를 들어 보고서 데이터 창의 `Sales` 필드를 디자인 화면의 테이블 셀로 끌어 오면 `[Sales]` 가 표시됩니다. 이는 Value 입력란 속성에 설정된 `=Fields!Sales.Value` 기본 식을 나타냅니다. 보고서를 실행하면 보고서 처리기에서 이 식을 계산하고 테이블 셀의 입력란에 있는 데이터 원본의 실제 데이터를 표시합니다. 자세한 내용은 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md) 및 [데이터 집합 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="displaying-the-field-collection-for-a-dataset"></a>데이터 집합에 대한 필드 컬렉션 표시  
 필드 컬렉션에 대한 개별 값을 표시하려면 각 필드를 테이블 정보 행으로 끌고 보고서를 실행합니다. 테이블 또는 목록 데이터 영역에 대한 정보 행의 참조가 데이터 집합의 각 행에 대한 값을 표시합니다.  
  
 필드의 요약된 값을 표시하려면 각 숫자 필드를 행렬의 데이터 영역으로 끕니다. 합계 행에 대한 기본 집계 함수는 Sum입니다. 예를 들어 `=Sum(Fields!Sales.Value)`입니다. 다른 합계를 계산하기 위해 기본 함수를 변경할 수 있습니다. 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)를 참조하세요.  
  
 입력란의 필드 컬렉션에 대한 요약된 값을 데이터 영역의 일부가 아닌 디자인 화면에 직접 표시하려면 데이터 집합 이름을 집계 함수에 대한 범위로 지정해야 합니다. 예를 들어 `SalesData`라는 데이터 집합에 대해 다음 식은 `Sales`필드에 대한 모든 값의 합계를 지정합니다. `=Sum(Fields!Sales,"SalesData")`  
  
 **식** 대화 상자를 사용하여 단순 필드 참조를 정의하는 경우 범주 창에서 Fields 컬렉션을 선택하고 **필드** 창에서 사용 가능한 필드 목록을 볼 수 있습니다. 각 필드에는 Value 및 IsMissing을 비롯한 여러 속성이 포함됩니다. 나머지 속성은 데이터 원본 유형에 따라 데이터 집합에 사용할 수 있는 미리 정의된 확장 필드 속성입니다.  
  
### <a name="detecting-nulls-for-a-dataset-field"></a>데이터 집합 필드에 대한 Null 검색  
 Null(**에서** Nothing [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)])인 필드 값을 검색하려면 **IsNothing**함수를 사용합니다. 테이블 정보 행의 입력란에 다음 식이 배치되면 `MiddleName` 필드를 테스트하여 값이 Null인 경우 "No Middle Name" 텍스트를 대체하고, 값이 Null이 아닌 경우 필드 값 자체를 대체합니다.  
  
 `=IIF(IsNothing(Fields!MiddleName.Value),"No Middle Name",Fields!MiddleName.Value)`  
  
### <a name="detecting-missing-fields-for-dynamic-queries-at-run-time"></a>런타임에 동적 쿼리에 대해 누락된 필드 검색  
 Fields 컬렉션의 항목에는 기본적으로 Value 및 IsMissing 속성이 있습니다. IsMissing 속성은 디자인 타임에 데이터 집합에 대해 정의된 필드가 런타임에 검색되는 필드에 포함되어 있는지 여부를 나타냅니다. 쿼리 수는 입력 매개 변수에 따라 결과 집합이 달라 또는 쿼리 수 저장된 프로시저를 호출 하는 예를 들어 `SELECT * FROM`  *\<테이블 >* 테이블 정의 변경 합니다.  
  
> [!NOTE]  
>  IsMissing은 모든 유형의 데이터 원본에 대해 디자인 타임과 런타임 간의 데이터 집합 스키마 변경을 검색합니다. IsMissing은 다차원 큐브의 빈 멤버를 검색하는 데 사용할 수 없으며 **EMPTY** 및 **NON EMPTY**의 MDX 쿼리 언어 개념과 관련이 없습니다.  
  
 사용자 지정 코드에서 IsMissing 속성을 테스트하여 결과 집합에 필드가 있는지 여부를 확인할 수 있습니다. [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] IIF **또는** SWITCH **와 같은**함수 호출을 포함하는 식을 사용하여 필드의 존재 여부를 테스트할 수 없습니다. [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 에서는 함수 호출에서 모든 매개 변수를 평가하므로 누락된 필드에 대한 참조가 평가될 때 오류가 발생하기 때문입니다.  
  
#### <a name="example-for-controlling-the-visibility-of-a-dynamic-column-for-a-missing-field"></a>누락된 필드에 대한 동적 열의 표시 유형을 제어하는 작업의 예  
 데이터 집합에 필드를 표시하는 열의 표시 유형을 제어하는 식을 설정하려면 먼저 필드의 누락 여부에 따라 부울 값을 반환하는 사용자 지정 코드 함수를 정의해야 합니다. 예를 들어 다음 사용자 지정 코드 함수에서는 필드가 누락되면 True를 반환하고 필드가 존재하면 False를 반환합니다.  
  
```  
Public Function IsFieldMissing(field as Field) as Boolean  
 If (field.IsMissing) Then  
 Return True  
  Else   
  Return False  
 End If  
End Function  
```  
  
 이 함수를 사용하여 열의 표시 유형을 제어하려면 열의 Hidden 속성을 다음 식으로 설정합니다.  
  
 `=Code.IsFieldMissing(Fields!FieldName)`  
  
 필드가 없는 경우 열이 숨겨집니다.  
  
#### <a name="example-for-controlling-the-text-box-value-for-a-missing-field"></a>누락된 필드에 대한 입력란 값을 제어하는 작업의 예  
 누락된 필드 값 대신 작성할 텍스트를 대체하려면 필드가 누락된 경우 필드 값 대신 사용할 수 있는 텍스트를 반환하는 사용자 지정 코드를 작성해야 합니다. 예를 들어 다음 사용자 지정 코드 함수에서는 필드가 있으면 필드 값을 반환하고 필드가 없으면 두 번째 매개 변수로 지정하는 메시지를 반환합니다.  
  
```  
Public Function IsFieldMissingThenString(field as Field, strMessage as String) as String  
 If (field.IsMissing) Then  
  Return strMessage  
 Else   
  Return field.Value  
  End If  
End Function  
```  
  
 입력란에 이 함수를 사용하려면 Value 속성에 다음 식을 추가합니다.  
  
 `=Code.IsFieldMissingThenString(Fields!FieldName,"Missing")`  
  
 입력란에 지정한 필드 값 또는 텍스트가 표시됩니다.  
  
### <a name="using-extended-field-properties"></a>확장 필드 속성 사용  
 확장 필드 속성은 데이터 집합에 대한 데이터 원본 유형에 의해 결정되는 데이터 처리 확장 프로그램에서 필드에 대해 정의하는 추가 속성입니다. 확장 필드 속성은 미리 정의되거나 데이터 원본 유형 관련 속성입니다. 자세한 내용은 [Analysis Services 데이터베이스에 대한 확장 필드 속성&#40;SSRS&#41;](../../reporting-services/report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md)을 참조하세요.  
  
 해당 필드에 지원되지 않는 속성을 지정하는 경우 식이 **null**([!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]에서 **Nothing**)로 계산됩니다. 데이터 공급자가 확장 필드 속성을 지원하지 않거나 쿼리가 실행될 때 해당 필드가 없으면 속성 값은 **String** 및**Object** 형식 속성의 경우 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]null **(** 에서 **Nothing**)이 되고 **Integer**형식 속성의 경우 0이 됩니다. 데이터 처리 확장 프로그램에서는 이 구문이 포함된 쿼리를 최적화하여 미리 정의된 속성을 이용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [보고서 데이터 집합&#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
  
  
