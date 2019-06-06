---
title: 레코드 집합 사용 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset object [ADO]
ms.assetid: bdf9a56a-de4a-44de-9111-2f11ab7b16ea
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8e3c3c7ff7d623d3bec0adf60773266bb6e53571
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704435"
---
# <a name="working-with-recordsets"></a>레코드 집합 작업
합니다 **레코드 집합** 개체에 결과 집합의 데이터를 제공 하는 조건에 따라 특정 레코드를 검색 하 고 인덱스를 사용 하 여 해당 검색 작업을 최적화 하기 위해도 순서를 다시 정렬할 수 있는 기본 제공 기능이 있습니다. 이러한 기능에 사용할 수 있는지 여부 등 일부 경우에서 공급자에 따라 달라 집니다 합니다 [인덱스](../../../ado/reference/ado-api/index-property.md) 속성-데이터 원본 자체의 구조입니다.  
  
## <a name="arranging-data"></a>데이터 정렬  
 데이터를 정렬 하는 가장 효율적인 방법은 자주 하 **레코드 집합** SQL 명령에 결과 반환 하는 데에 ORDER BY 절을 지정 하는 것입니다. 그러나 데이터의 순서를 변경 하려면 있을 **레코드 집합** 는 이미 만들었습니다. 사용할 수는 **정렬** 속성을 설정 하는 행의 순서를 **Recordset** 트래버스 됩니다. 또한 합니다 **필터** 속성 결정 어떤 행이 행을 검색할 때에 액세스할 수 있습니다.  
  
 **정렬** 속성을 설정 하거나 반환을 **문자열** 이름 필드를 나타내는 값을 **레코드 집합** 정렬할 합니다. 각 이름을 쉼표로 구분 됩니다 하 고 필요에 따라 뒤 공백 및 키워드 **ASC** (하는 필드를 오름차순으로 정렬) 또는 **DESC** (하는 필드를 내림차순으로 정렬). 기본적으로 키워드를 지정 하지, 필드 오름차순 정렬 됩니다.  
  
 정렬 작업이 데이터는 실제로 다시 정렬 하지만 지정 된 인덱스 순서 대로 액세스 하기 때문에 효율적입니다.  
  
 **정렬** 속성을 입력 해야 합니다 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 설정할 **adUseClient**합니다. 에 지정 된 각 필드에 대 한 임시 인덱스가 생성 됩니다는 **정렬** 속성 인덱스 아직 없는 경우.  
  
 설정 된 **정렬** 속성을 빈 문자열은 원래 순서 대로 행 다시 설정 하 고 임시 인덱스를 삭제 합니다. 기존 인덱스를 삭제 되지 않습니다.  
  
 가정를 **Recordset** 라는 세 개의 필드가 있습니다 *firstName*, *middleInitial*, 및 *lastName*. 설정 합니다 **정렬** 속성 문자열을 "`lastName DESC, firstName ASC`", 순서는 합니다 **레코드 집합** 내림차순으로 정렬 한 다음 이름 오름차순으로 정렬 하 여 성을 기준으로 합니다. 중간 이니셜이 무시 됩니다.  
  
 정렬 조건 문자열에서 참조 되는 필드 이름을 지정할 수 있습니다 "ASC" 또는 "DESC" 키워드를 사용 하 여 명명할 **ASC** 하 고 **DESC**합니다. 사용 하 여 이름이 충돌 하는 별칭을 가진 필드를 제공 합니다 **AS** 쿼리에서 반환 하는 키워드는 **레코드 집합**합니다.  
  
 에 대 한 자세한 내용은 **레코드 집합** 이 항목 뒷부분의 "the 결과 필터링"을 참조 필터링 합니다.  
  
## <a name="finding-a-specific-record"></a>특정 레코드 찾기  
 ADO를 제공 합니다 [찾을](../../../ado/reference/ado-api/find-method-ado.md) 및 [Seek](../../../ado/reference/ado-api/seek-method.md) 의 특정 레코드를 찾기 위한 메서드를 **레코드 집합**합니다. 합니다 **찾을** 메서드는 다양 한 공급자에서 지원 되지만 단일 검색 조건으로 제한 됩니다. 합니다 **Seek** 메서드 여러 조건을 검색을 지원 하지만 대부분의 공급자에서 지원 되지 않습니다.  
  
 필드에 인덱스의 성능을 크게 향상 시킬 수는 **찾을** 메서드 및 **정렬** 및 **필터** 의 속성을 **레코드 집합** 개체입니다. 에 대 한 내부 인덱스를 만들 수는 **필드** 해당 동적을 설정 하 여 개체 [최적화](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) 속성입니다. 이 동적 속성을 추가 합니다 **속성** 컬렉션을 **필드** 설정 하는 경우 개체를 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient**. 이 인덱스는 ADO 내부-액세스할 수 없거나 다른 용도로 사용 해야 합니다. 또한이 인덱스는 다릅니다 합니다 [인덱스](../../../ado/reference/ado-api/index-property.md) 의 속성을 **레코드 집합** 개체.  
  
 합니다 **찾을** 메서드 (필드) 열에 값을 신속 하 게 찾습니다는 **레코드 집합**합니다. 자주의 속도 향상 시킬 수 있습니다는 **찾을** 메서드를 사용 하 여 열에는 **최적화** 인덱스를 만들려면 속성입니다.  
  
 합니다 **찾을** 메서드 제한 한 필드의 내용 검색 합니다. 합니다 **Seek** 메서드 인덱스 있고 다른 제한 사항도 필요 합니다. 인덱스의 기반이 없는 여러 필드에서 검색 해야 하거나 공급자 인덱스를 지원 하지 않으면, 사용 하 여 결과 제한할 수 있습니다는 **필터** 의 속성을 **레코드 집합** 개체.  
  
### <a name="find"></a>찾기  
 합니다 **찾을** 메서드 검색을 **레코드 집합** 지정 된 조건을 만족 하는 행에 대 한 합니다. 필요에 따라 검색, 시작 행 및 오프셋을 시작할 행의 방향을 지정할 수 있습니다. 현재 행 위치가 레코드; 설정 조건이 충족 될 경우 끝 (또는 시작) 위치 설정 되어이 고, 그렇지 합니다 **레코드 집합**검색 방향에 따라 합니다.  
  
 조건에 대 한 단일 열 이름만 지정할 수 있습니다. 즉,이 메서드는 여러 열 검색을 지원 하지 않습니다.  
  
 "조건에 대 한 비교 연산자 할), " **>** "(보다 큼)," **\<** " (보다 작음), "=" (같음), "> =" (보다 크거나 같음), "< =" (작거나 같음), " <> "(같지 않음), 또는"좋아요"(패턴 일치).  
  
 조건 값은 문자열, 부동 소수점 숫자 또는 날짜 수 있습니다. 문자열 값은 작은따옴표 또는 "#" (숫자 기호)를 사용 하 여 구분 기호로 분리 된 (예를 들어, "상태 '서울' =" 또는 "상태 = WA # #"). 날짜 값이 "#" (숫자 기호) 기호를 사용 하 여 구분 됩니다 (예를 들어, "start_date > #7 월 22 일/97 #").  
  
 비교 연산자 "좋아요" 이면 문자열 값을 찾으려면 하나 이상의 원하는 문자나 부분 문자열에 별표 (*)를 포함할 수 있습니다. 예를 들어, "와 같은 상태 저는\*'" Maine, 등이 검색 합니다. 또한 값 내에 포함 된 부분 문자열을 찾으려면 선행 및 후행 별표를 사용할 수 있습니다. 예를 들어, "와 같은 상태 '\*으로\*'" Alaska, 사스, 매사추세츠와 일치 합니다.  
  
 별표 수 조건 문자열의 끝에만 또는 함께 사용할 시작과 조건 문자열의 끝에 앞서 설명한 대로 합니다. 선행 와일드 카드로 별표를 사용할 수 없습니다 ('* str') 또는 와일드 카드 문 포함 된\*r'). 이렇게 하면 오류가 발생 합니다.  
  
### <a name="seek-and-index"></a>검색 및 인덱스  
 사용 하 여는 **Seek** 함께 메서드는 **인덱스** 기본 공급자의 인덱스를 지 원하는 경우 속성을 **레코드 집합** 개체입니다. 사용 된 [지원](../../../ado/reference/ado-api/supports-method.md) **(adSeek)** 기본 공급자를 지원 하는지 여부를 결정 하는 방법 **Seek**, 및 **Supports(adIndex)** 공급자가 인덱스를 지원 하는지 여부를 결정 하는 메서드. (예를 들어 합니다 [OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) 지원 **Seek** 및 **인덱스**.)  
  
 하는 경우 **Seek** 않습니다 찾을 원하는 행에 오류가 발생 하 고 행의 끝에 배치 됩니다 합니다 **레코드 집합**합니다. 설정 된 **인덱스** 이 메서드를 실행 하기 전에 원하는 인덱스에는 속성입니다.  
  
 이 메서드는 서버 쪽 커서에만 지원 됩니다. Seek 때 지원 되지 않습니다는 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성 값을 **레코드 집합** 개체가 **adUseClient**합니다.  
  
 이 메서드를 사용할 수 있습니다 경우에만 합니다 **레코드 집합** 개체를 사용 하 여 열린를 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 의 값 **adCmdTableDirect**합니다.  
  
## <a name="filtering-the-results"></a>결과 필터링  
 합니다 **찾을** 메서드 제한 한 필드의 내용 검색 합니다. 합니다 **Seek** 메서드 인덱스 있고 다른 제한 사항도 필요 합니다. 인덱스의 기반이 없는 여러 필드에서 검색 해야 하거나 공급자 인덱스를 지원 하지 않으면, 사용 하 여 결과 제한할 수 있습니다는 **필터** 의 속성을 **레코드 집합** 개체.  
  
 사용 하 여는 **필터** 레코드에 선택적으로 화면에 속성을 **레코드 집합** 개체입니다. 필터링 된 **레코드 집합** 되는 기록 즉 충족 하지 않는 현재 커서를 **필터** 조건에서 사용할 수 없는 합니다 **레코드 집합** 될 때까지 **필터** 제거 됩니다. 현재 커서를 기반으로 값을 반환 하는 다른 속성에는 영향을 같은 **AbsolutePosition**, **AbsolutePage**하십시오 **RecordCount**, 및  **PageCount**합니다. 설정 때문에 이것이 합니다 **필터** 속성을 특정 값으로 새 값을 충족 하는 첫 번째 레코드를 현재 레코드를 이동 합니다.  
  
 합니다 **필터** 속성 변형 인수를 사용 합니다. 이 값은 사용 하기 위한 세 가지 방법 중 하나를 나타냅니다 합니다 **필터** 속성: 조건 문자열을 **FilterGroupEnum** 상수 또는 책갈피의 배열입니다. 자세한 내용은이 항목의 뒷부분에 나오는 조건 문자열을 사용 하 여 필터링, 상수를 사용 하 여 필터링 및 책갈피를 사용 하 여 필터링을 참조 합니다.  
  
> [!NOTE]
>  선택 하려는 데이터를 알고 때 일반적으로 더 효과적으로 열을 **레코드 집합** 효과적으로에 의존 하지 않고 결과 집합을 필터링 하는 SQL 문을 사용 하 여 합니다 **필터** 속성입니다.  
  
 필터를 제거 하려면를 **레코드 집합**를 사용 합니다 **adFilterNone** 상수입니다. 설정 된 **필터** 속성을 빈 문자열로 ("") 사용 하는 것과 동일한 효과가 합니다 **adFilterNone** 상수입니다.  
  
### <a name="filtering-with-a-criteria-string"></a>조건 문자열을 사용 하 여 필터링  
 조건 문자열 형태로 절 이루어져 *FieldName 연산자 값* (예를 들어 `"LastName = 'Smith'"`). 복합 절이 포함 된 개별 절을 연결 하 여 만들 수 있습니다 **AND** (예를 들어 `"LastName = 'Smith' AND FirstName = 'John'"`) 및 **하거나** (예를 들어 `"LastName = 'Smith' OR LastName = 'Jones'"`). 기준 문자열에 대 한 다음 지침을 따르세요.  
  
-   *FieldName* 에서 유효한 필드 이름 이어야 합니다 **레코드 집합**합니다. 필드 이름에 공백이 이름을 대괄호로 묶어야 합니다.  
  
-   *연산자* 다음 중 하나 여야 합니다: **\<** 하십시오 **>** 를 **\< =** , **>=** 를 **<>** 를 **=** , 또는 **와 같은**합니다.  
  
-   *값* 값인 있는 필드 값을 비교 합니다 (예를 들어 `'Smith'`를 `#8/24/95#`합니다 `12.345`, 또는 `$50.00`). 문자열이 포함 된 작은따옴표 (')를 사용 하 고 파운드 기호 (`#`) 날짜를 사용 합니다. 숫자의 경우 소수점이 하, 달러 기호 및 과학적 표기법을 사용할 수 있습니다. 경우 *연산자* 됩니다 **와 같은**, *값* 와일드 카드 문자를 사용할 수 있습니다. 만 별표 (\*) 및 백분율 기호 (%) 와일드 카드 문자 허용 하며 문자열의 마지막 문자 여야 합니다. *값* null 일 수 없습니다.  
  
    > [!NOTE]
    >  필터에 작은따옴표 (')를 포함 하도록 *값*, 두 개의 작은따옴표 하나를 나타내는 데 사용 합니다. 예를 들어 기준으로 필터링 할 *O'Malley*, 조건 문자열 이어야 합니다 `"col1 = 'O''Malley'"`합니다. 시작 및 필터 값의 끝에 작은따옴표를 포함 하려면 묶어야 문자열 파운드 기호 (#). 예를 들어 기준으로 필터링 할 *'1'* , 조건 문자열 이어야 합니다 `"col1 = #'1'#"`합니다.  
  
 사이는 우선 순위가 **AND** 하 고 **또는**합니다. 괄호 안에 절을 그룹화 할 수 있습니다. 그러나 조인할 절을 그룹화 할 수 없습니다를 **또는** 한 후 그룹 AND 사용 하 여 다른 절을 다음과 같이 조인 합니다.  
  
```  
(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'  
```  
  
 대신 생성 하는이 필터 다음과 같습니다.  
  
```  
(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')  
```  
  
 에 **와 같은** 절 패턴의 시작과 끝에 와일드 카드를 사용할 수 있습니다 (예를 들어 `LastName Like '*mit*'`) 또는 패턴의 끝에만 (예를 들어 `LastName Like 'Smit*'`).  
  
### <a name="filtering-with-a-constant"></a>상수를 사용 하 여 필터링  
 다음 상수는 필터링에 사용 가능한 **레코드 집합**합니다.  
  
|상수|Description|  
|--------------|-----------------|  
|**adFilterAffectedRecords**|마지막 영향을 받는 레코드만 보기에 대 한 필터 **삭제**, **Resync**를 **UpdateBatch**, 또는 **CancelBatch** 호출 합니다.|  
|**adFilterConflictingRecords**|마지막 일괄 처리 업데이트를 실패 한 레코드를 보기 위한 필터입니다.|  
|**adFilterFetchedRecords**|필터 현재 캐시 기능에서 레코드를 보기 위한 즉, 데이터베이스에서 레코드를 검색에 대 한 마지막 호출 결과입니다.|  
|**adFilterNone**|현재 필터를 제거 하 고 보기에 대 한 모든 레코드를 복원 합니다.|  
|**adFilterPendingRecords**|레코드만 보기에 대 한 필터는 변경 되었지만 서버에 아직 보내지 않았습니다. 일괄 업데이트 모드에만 적용 됩니다.|  
  
 필터 상수 쉽게 마지막 영향을 받은 일괄 업데이트 모드를 보고, 예를 들어, 해당 레코드에 허용 하 여 개별 레코드 충돌 해결 **UpdateBatch** 메서드 호출에서와 같이 다음 예입니다.  
  
 `Attribute VB_Name = "modExaminingData"`  
  
### <a name="filtering-with-bookmarks"></a>책갈피를 사용 하 여 필터링  
 마지막으로 책갈피를이 인수를 전달할 수 있습니다 합니다 **필터** 속성입니다. 결과 커서를 책갈피가 있는 속성에 전달 된 레코드만 포함 됩니다. 다음 코드 예제에서 레코드에서 책갈피의 배열을 만듭니다는 **Recordset** "B" 있는 합니다 *ProductName* 필드. 그런 다음 배열에 전달 된 **필터** 필터링 된 결과 대 한 속성 및 표시 정보 **레코드 집합**합니다.  
  
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
  
## <a name="creating-a-clone-of-a-recordset"></a>레코드 집합의 클론을 만드는  
 사용 합니다 **복제** 메서드를 여러 중복 **레코드 집합** 개체에 지정된 된 레코드 집합에서 현재 둘 이상의 레코드를 유지 하려는 경우에 특히 합니다. 사용 하는 **복제** 메서드를 만들고 새 열 보다 더 효율적입니다 **레코드 집합** 원본과 동일한 정의 사용 하 여 개체입니다.  
  
 새로 만든된 복제본의 현재 레코드 첫 번째 레코드를 원래 설정 됩니다. 복제 된에서 현재 레코드 포인터 **레코드 집합** 원본 또는 그 반대로 동기화 되지 않습니다. 탐색할 수 있습니다 독립적으로 각 **레코드 집합**합니다.  
  
 하나를 변경한 **레코드 집합** 개체 모든 커서 유형에 관계 없이 해당 복제 중에 표시 됩니다. 그러나 실행 후 [Requery](../../../ado/reference/ado-api/requery-method.md) 원본에서 **레코드 집합**, 복제본 원래 더 이상 동기화 되지 것입니다.  
  
 원래 닫는 **레코드 집합** 해당 복사본을 닫히지 않으며 원본 또는 다른 복사본은 닫기 복사본을 닫지 않습니다.  
  
 복제할 수 있습니다는 **레코드 집합** 책갈피를 지원 하는 경우에 개체입니다. 책갈피 값은 교환할 수 있습니다. 즉, 책갈피에서 참조를 하나 **레코드 집합** 개체의 모든 해당 복제본에 동일한 레코드를 가리킵니다.
