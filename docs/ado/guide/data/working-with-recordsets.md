---
title: "레코드 집합으로 작업할 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Recordset object [ADO]
ms.assetid: bdf9a56a-de4a-44de-9111-2f11ab7b16ea
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cf54089c037d972649d3acc872a38eed21d02507
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="working-with-recordsets"></a>레코드 집합 사용
**레코드 집합** 개체에는 제공 하는 기준에 따라 특정 레코드를 검색 하 고 인덱스를 사용 하 여 해당 검색 작업을 최적화 하기 위해도 결과 집합에 있는 데이터의 순서를 다시 정렬할 수 있는 기본 제공 기능입니다. 일부 경우 공급자에 따라 이러한 기능을 사용 하기 위해 사용할 수 있는지 여부 — 등는 [인덱스](../../../ado/reference/ado-api/index-property.md) 속성 — 자체 데이터 원본의 구조입니다.  
  
## <a name="arranging-data"></a>데이터 정렬  
 데이터를 정렬 하는 가장 효율적인 방법은 대부분의 경우 프로그램 **레코드 집합** SQL 명령에 결과 반환 하는 데에 ORDER BY 절을 지정 하는 것입니다. 그러나,에 있는 데이터의 순서를 변경 해야 할 수도 있습니다는 **레코드 집합** 를 이미 만들었습니다. 사용할 수는 **정렬** 의 어떤 행의 순서를 설정 하려면 속성은 **레코드 집합** 통과 됩니다. 또한는 **필터** 속성 결정 어떤 행이 행을 검색할 때에 액세스할 수 있습니다.  
  
 **정렬** 속성을 설정 하거나 반환는 **문자열** 에서 이름을 필드를 나타내는 값의 **레코드 집합** 을 정렬할 합니다. 각 이름은 쉼표로 구분 하 고 필요에 따라 뒤에 공백을 키워드 **ASC** (필드를 오름차순 정렬) 또는 **DESC** (필드를 내림차순 정렬). 기본적으로 없는 키워드가 지정 된 필드를 오름차순 정렬 됩니다.  
  
 데이터는 실제로 다시 정렬 되지만 인덱스에 의해 지정 된 순서 대로 액세스 하는 정렬 작업이 효율적입니다.  
  
 **정렬** 속성 필요는 [앞](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성에 설정할을 **adUseClient**합니다. 임시 인덱스에 지정 된 각 필드에 대해 생성 됩니다는 **정렬** 인덱스가 아직 없는 경우 속성을 사용 합니다.  
  
 설정의 **정렬** 속성을 빈 문자열로 원래 순서 행이 재설정 되 고 임시 인덱스를 삭제 합니다. 기존 인덱스를 삭제 되지 않습니다.  
  
 가정는 **레코드 집합** 라는 세 개의 필드가 포함 *firstName*, *middleInitial*, 및 *lastName*합니다. 설정의 **정렬** 속성 문자열을 "`lastName DESC, firstName ASC`", 않습니다는 **레코드 집합** 내림차순으로 정렬 한 다음 오름차순 첫 번째 이름으로 성을 기준으로 합니다. 중간 이니셜이 무시 됩니다.  
  
 정렬 조건 문자열에서 참조 되는 필드 이름을 지정할 수 있습니다 "ASC" 또는 "DESC" 명명할 키워드와 함께 **ASC** 및 **DESC**합니다. 지정 된 필드 이름이 충돌 하는 별칭 사용 하 여 제공는 **AS** 키워드를 반환 하는 쿼리에서 **레코드 집합**합니다.  
  
 에 대 한 자세한 내용은 **레코드 집합** 이 항목의 뒷부분에 나오는 "결과 필터링"을 참조 필터링 합니다.  
  
## <a name="finding-a-specific-record"></a>특정 레코드 찾기  
 ADO에서는 제공는 [찾을](../../../ado/reference/ado-api/find-method-ado.md) 및 [Seek](../../../ado/reference/ado-api/seek-method.md) 특정 레코드를 찾기 위한 메서드는 **레코드 집합**합니다. **찾을** 메서드는 다양 한 공급자에서 지원 하지만 단일 검색 조건으로 제한 됩니다. **Seek** 메서드 여러 조건에 검색 기능을 지원 하지만 대부분의 공급자에서 지원 되지 않습니다.  
  
 필드에 인덱스의 성능을 크게 향상 시킬 수는 **찾을** 메서드 및 **정렬** 및 **필터** 의 속성은 **레코드 집합** 개체입니다. 에 대 한 내부 인덱스를 만들 수는 **필드** 해당 동적 설정 하 여 개체 [최적화](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) 속성입니다. 이 동적 속성에 추가 되는 **속성** 의 컬렉션은 **필드** 설정 하는 경우 개체는 [앞](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient**. 이 인덱스는 ADO 내부 기억-에 액세스 하거나 다른 용도로 사용할 수 없습니다. 이 인덱스를 구별 하는 또한는 [인덱스](../../../ado/reference/ado-api/index-property.md) 의 속성은 **레코드 집합** 개체입니다.  
  
 **찾을** 메서드 (필드)의 열 내에서 값을 신속 하 게 찾습니다는 **레코드 집합**합니다. 대체로의 속도 향상 시킬 수 있습니다는 **찾을** 메서드를 사용 하 여 열에는 **최적화** 에 인덱스를 만들 속성입니다.  
  
 **찾을** 한 필드의 내용 범위를 검색 하는 방법 제한 합니다. **Seek** 인덱스 있고 다른 제한 사항도 메서드에 필요 합니다. 인덱스를 여러 필드를 검색 해야 하는 경우 또는 사용 하 여 결과 제한할 수 공급자 인덱스를 지원 하지 않습니다는 **필터** 의 속성은 **레코드 집합** 개체입니다.  
  
### <a name="find"></a>찾기  
 **찾을** 메서드를 검색 한 **레코드 집합** 지정 된 조건을 만족 하는 행에 대 한 합니다. 필요에 따라 검색, 시작 행 및 행 시작에서 오프셋의 방향을 지정할 수 있습니다. 검색 된 레코드로; 현재 행의 위치가 설정 되어 조건을 충족 하는 경우 그렇지 위치의 끝 (또는 시작)으로 설정 되 고 **레코드 집합**검색 방향에 따라 합니다.  
  
 조건에 대 한 단일 열 이름만 지정할 수 있습니다. 즉,이 메서드는 여러 열 검색을 지원 하지 않습니다.  
  
 조건에 대 한 비교 연산자가 될 수 있습니다"**>**"(보다 큼),"**\<**" (보다 작음), "=" (같음), "> =" (보다 크거나 같음), "< =" (작거나 같음), " <> "(같지 않음), 또는"좋아요"(패턴 일치).  
  
 조건 값은 문자열, 부동 소수점 숫자 또는 날짜 수 있습니다. 문자열 값은 작은따옴표 또는 "#" (숫자 기호)로 구분 (예를 들어 "상태 = '서울'" 또는 "상태 = WA # #"). 날짜 값 표시 "#" (숫자 기호)로 구분 됩니다 (예를 들어 "start_date > #7/22/&#97;").  
  
 비교 연산자가 있는 경우 "좋아요", 문자열 값에 별표 (*) 문자 또는 부분 문자열의 하나 이상의 항목을 찾을를 포함할 수 있습니다. 예를 들어 "와 같은 상태 중\*'", Maine 등이 검색 합니다. 선행 및 후행 별표를 사용 하 여 값 내에 포함 된 부분 문자열을 찾을 수 있습니다. 예를 들어 "와 같은 상태 '\*으로\*'" Alaska, 사스, 등이 검색 합니다.  
  
 별표 수 조건 문자열의 끝에만 또는 함께 사용할 시작과 조건 문자열의 끝에 앞에서 보았듯이 합니다. 와일드 카드 앞으로 별표를 사용할 수 없습니다 ('* str'), 아니면 포함 와일드 카드 문\*r'). 이 인해 오류가 발생 합니다.  
  
### <a name="seek-and-index"></a>검색 및 색인  
 사용 하 여는 **Seek** 와 함께 메서드는 **인덱스** 기본 공급자에서 인덱스를 지 원하는 경우 속성은 **레코드 집합** 개체입니다. 사용 하 여는 [지원](../../../ado/reference/ado-api/supports-method.md)**(adSeek)** 기본 공급자에서 지원 하는지 여부를 확인할 수 있는 방법은 **Seek**, 및 **Supports(adIndex)** 공급자 인덱스를 지원 하는지 여부를 결정 하는 방법입니다. (예를 들어는 [OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) 지원 **Seek** 및 **인덱스**.)  
  
 경우 **Seek** 않습니다 찾을 원하는 행을 오류가 발생 하 고 행의 끝에 배치 되는 **레코드 집합**합니다. 설정의 **인덱스** 속성을이 메서드를 실행 하기 전에 원하는 인덱스입니다.  
  
 이 메서드는 서버 쪽 커서에만 지원 됩니다. Seek 때 지원 되지 않습니다는 [앞](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 의 속성 값은 **레코드 집합** 개체가 **adUseClient**합니다.  
  
 이 메서드를 사용할 수 있습니다 경우에만 **레코드 집합** 개체도 연는 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 값 **adCmdTableDirect**합니다.  
  
## <a name="filtering-the-results"></a>결과 필터링  
 **찾을** 한 필드의 내용 범위를 검색 하는 방법 제한 합니다. **Seek** 인덱스 있고 다른 제한 사항도 메서드에 필요 합니다. 인덱스 여러 필드를 검색 해야 하는 경우 또는 사용 하 여 결과 제한할 수 공급자 인덱스를 지원 하지 않습니다는 **필터** 의 속성은 **레코드 집합** 개체입니다.  
  
 사용 하 여는 **필터** 속성을 선택적으로의 레코드 숨기는 **레코드 집합** 개체입니다. 필터링 된 **레코드 집합** 현재 커서를 기록 하는 수단을 충족 하지 않는 되는 **필터** 조건에서 사용할 수 없는 **레코드 집합** 될 때까지 **필터** 제거 됩니다. 현재 커서에 따라 값을 반환 하는 다른 속성에는 영향을 같은 **AbsolutePosition**, **AbsolutePage**, **RecordCount**, 및  **PageCount**합니다. 설정 때문에 이것이 **필터** 속성을 특정 값으로 새 값을 충족 하는 첫 번째 레코드를 현재 레코드를 이동 합니다.  
  
 **필터** 속성은 variant 인수를 사용 합니다. 이 값은 사용 하기 위한 세 가지 방법 중 하나를 나타냅니다는 **필터** 속성: 조건 문자열을 **FilterGroupEnum** 상수 또는 책갈피의 배열입니다. 자세한 내용은이 항목의 뒷부분에 나오는 필터링 조건 문자열로,을 상수와 필터링 및 책갈피와 필터링을 참조 합니다.  
  
> [!NOTE]
>  일반적으로 보다 효과적으로 열은 선택 하려는 데이터를 알고 있는 경우는 **레코드 집합** 효과적으로에 의존 하지 않고 결과 집합을 필터링 하는 SQL 문으로 **필터** 속성입니다.  
  
 필터를 제거 하는 **레코드 집합**를 사용 하 여는 **adFilterNone** 상수입니다. 설정의 **필터** 속성을 빈 문자열 ("")를 사용 하 여 것과 동일한 결과가 **adFilterNone** 상수입니다.  
  
### <a name="filtering-with-a-criteria-string"></a>조건 문자열을 사용 하 여 필터링  
 조건 문자열 형태로 절 이루어져 *FieldName 연산자 값* (예를 들어 `"LastName = 'Smith'"`). 복합 절이 포함 된 개별 절을 연결 하 여 만들 수 있습니다 **AND** (예를 들어 `"LastName = 'Smith' AND FirstName = 'John'"`) 및 **또는** (예를 들어 `"LastName = 'Smith' OR LastName = 'Jones'"`). 빈 문자열에 대 한 다음 지침을 따르세요.  
  
-   *FieldName* 에서 유효한 필드 이름 이어야 합니다는 **레코드 집합**합니다. 필드 이름에 공백이 이름을 대괄호로 묶어야 합니다.  
  
-   *연산자* 다음 중 하나 여야 합니다:  **\<** ,  **>** ,  **\< =** ,  **>=**   **<>** ,  **=** , 또는 **같은**합니다.  
  
-   *값* 된 필드 값을 비교 하 여 값 (예를 들어 `'Smith'`, `#8/24/95#`, `12.345`, 또는 `$50.00`). 작은따옴표 (')를 사용 하 여 문자열 및 파운드 기호 (`#`) 날짜와 함께 합니다. 숫자를 소수점이 하, 달러 기호 및 과학적 표기법을 사용할 수 있습니다. 경우 *연산자* 은 **같은**, *값* 와일드 카드 문자를 사용할 수 있습니다. 별표 (\*) 및 백분율 기호 (%) 와일드 카드 문자는 허용 하며 문자열의 마지막 문자 여야 합니다. *값* null 일 수 없습니다.  
  
    > [!NOTE]
    >  필터에 작은따옴표 (')를 포함 하도록 *값*, 두 개의 작은따옴표를 사용 하 여 하나를 나타냅니다. 예를 들어 필터링 하려면 *O'Malley*, 조건 문자열 이어야 합니다 `"col1 = 'O''Malley'"`합니다. 시작과 끝 필터 값의 작은 따옴표를 포함 하려면 문자열을 숫자 기호 묶습니다 (#). 예를 들어 필터링 하려면 *'1'*, 조건 문자열 이어야 합니다 `"col1 = #'1'#"`합니다.  
  
 간의 선행 규칙이 **AND** 및 **또는**합니다. 괄호 안에 절을 그룹화 할 수 있습니다. 그러나로 조인한 절을 그룹화 수 없습니다는 **또는** 한 후 그룹을 AND로 다른 절은 다음과 같이 조인 합니다.  
  
```  
(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'  
```  
  
 대신, 구성 합니다.이 필터 다음과 같습니다.  
  
```  
(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')  
```  
  
 에 **같은** 절, 시작 및 패턴의 끝 부분에 와일드 카드를 사용할 수 있습니다 (예를 들어 `LastName Like '*mit*'`) 또는 패턴의 끝에만 (예를 들어 `LastName Like 'Smit*'`).  
  
### <a name="filtering-with-a-constant"></a>상수를 사용 하 여 필터링  
 다음 상수는 필터링에 사용할 수 있는 **레코드 집합**합니다.  
  
|상수|Description|  
|--------------|-----------------|  
|**adFilterAffectedRecords**|마지막 영향을 받는 레코드만 보기에 대 한 필터 **삭제**, **Resync**, **UpdateBatch**, 또는 **CancelBatch** 호출 합니다.|  
|**adFilterConflictingRecords**|마지막 일괄 처리 업데이트를 실패 한 레코드를 보기 위한 필터입니다.|  
|**adFilterFetchedRecords**|현재 캐시에서 레코드를 보기 위한 필터-즉, 데이터베이스에서 레코드를 검색 한 마지막 호출의 결과입니다.|  
|**adFilterNone**|현재 필터를 제거 하 고 보기에 대 한 모든 레코드를 복원 합니다.|  
|**그**|레코드에만 보기에 대 한 필터를 변경 되었지만 서버로 아직 보내지 않았습니다. 일괄 업데이트 모드에만 적용할 수 있습니다.|  
  
 필터 상수 보다 쉽게 마지막 하는 동안 해당 레코드를 보고, 예를 들어 허용 하 여 일괄 처리 업데이트 모드에 있는 동안 개별 레코드 충돌 영향을 해결 하려면 **UpdateBatch** 메서드 호출에서와 같이 다음 예제에서는 합니다.  
  
 `Attribute VB_Name = "modExaminingData"`  
  
### <a name="filtering-with-bookmarks"></a>책갈피를 사용 하 여 필터링  
 마지막으로 책갈피를이 인수를 전달할 수 있습니다는 **필터** 속성입니다. 결과 커서 책갈피가 있는 속성에 전달 된 레코드에만 포함 됩니다. 다음 코드 예제에서는의 레코드에서 책갈피의 배열을 만듭니다는 **레코드 집합** "B"를 충족 하는 *ProductName* 필드입니다. 그런 다음에 배열 전달는 **필터** 필터링 된 결과 대 한 속성 및 표시 정보 **레코드 집합**합니다.  
  
```  
'BeginFilterBkmk  
Dim vBkmkArray() As Variant  
Dim i As Integer  
  
'Recordset created using "SELECT * FROM Products" as command.  
'So, we will check to see if ProductName has a capital B, and  
'if so, add to the array.  
i = 0  
Do While Not objRs.EOF  
    If InStr(1, objRs("ProductName"), "B") Then  
        ReDim Preserve vBkmkArray(i)  
        vBkmkArray(i) = objRs.Bookmark  
        i = i + 1  
        Debug.Print objRs("ProductName")  
    End If  
    objRs.MoveNext  
Loop  
  
'Filter using the array of bookmarks.  
objRs.Filter = vBkmkArray  
  
objRs.MoveFirst  
Do While Not objRs.EOF  
    Debug.Print objRs("ProductName")  
    objRs.MoveNext  
Loop  
'EndFilterBkmk  
```  
  
## <a name="creating-a-clone-of-a-recordset"></a>레코드 집합의 복제본 만들기  
 사용 하 여는 **복제** 메서드를 여러 개 만듭니다 중복 **레코드 집합** 개체, 특히 여러 레코드의 지정한 집합의 현재 레코드를 유지 관리 하려는 경우. 사용 하 여는 **복제** 메서드 만들고 새 열 보다 더 효율적입니다. **레코드 집합** 원본과 같은 정의 된 개체입니다.  
  
 새로 만든된 복제본의 현재 레코드 원래 첫 번째 레코드에 설정 되었습니다. 복제 된의 현재 레코드 포인터 **레코드 집합** 원래 하거나 그 반대로 동기화 되지 않습니다. 탐색할 수 있습니다 독립적으로 각 **레코드 집합**합니다.  
  
 하나를 적용 한 변경 내용 **레코드 집합** 개체 모든 커서 유형에 관계 없이 해당 복제 중에 표시 됩니다. 그러나 실행 후 [Requery](../../../ado/reference/ado-api/requery-method.md) 원래에 **레코드 집합**, 클론 원본에 더 이상 동기화 되지 것입니다.  
  
 원래 닫는 **레코드 집합** 복사본 닫히지 않으며 원본이 나 다른 복사본은 닫기 복사본을 닫으면지 않습니다.  
  
 복제할 수 있습니다는 **레코드 집합** 책갈피를 지원 하는 경우에 개체입니다. 책갈피 값은 교환할 수 있습니다. 즉, 하나에서 책갈피 참조 **레코드 집합** 개체 모든 복제본에서 동일한 레코드를 참조 합니다.
