---
title: 레코드 집합 작업 | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 07f970dd557d381280f5a9dbdd52eb015de0df75
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82748337"
---
# <a name="working-with-recordsets"></a>레코드 집합 작업
**레코드 집합** 개체에는 결과 집합의 데이터 순서를 다시 정렬 하 고, 사용자가 제공 하는 조건에 따라 특정 레코드를 검색 하 고, 인덱스를 사용 하 여 해당 검색 작업을 최적화 하는 데 사용할 수 있는 기본 제공 기능이 있습니다. 이러한 기능을 사용할 수 있는지 여부는 공급자에 따라 다르며 [인덱스](../../../ado/reference/ado-api/index-property.md) 속성의 경우, 데이터 원본 자체의 구조와 같은 경우도 있습니다.  
  
## <a name="arranging-data"></a>데이터 정렬  
 **레코드 집합** 의 데이터를 정렬 하는 가장 효율적인 방법은 결과를 반환 하는 데 사용 되는 SQL 명령에 order by 절을 지정 하는 것입니다. 그러나 이미 만들어진 **레코드 집합** 에서 데이터의 순서를 변경 해야 할 수도 있습니다. **Sort** 속성을 사용 하 여 **레코드 집합** 의 행이 트래버스하는 순서를 설정할 수 있습니다. 또한 **Filter** 속성은 행을 트래버스할 때 액세스할 수 있는 행을 결정 합니다.  
  
 **Sort** 속성은 정렬할 **레코드 집합** 의 필드 이름을 나타내는 **문자열** 값을 설정 하거나 반환 합니다. 각 이름은 쉼표로 구분 되며 필요에 따라 공백과 키워드 **ASC** (오름차순으로 필드를 정렬) 또는 **DESC** (내림차순으로 필드를 정렬)로 구분 됩니다. 기본적으로 키워드가 지정 되지 않은 경우 필드는 오름차순으로 정렬 됩니다.  
  
 데이터는 물리적으로 다시 정렬 되지 않지만 인덱스에 지정 된 순서 대로 액세스 되기 때문에 정렬 작업은 효율적입니다.  
  
 **Sort** 속성을 사용 하려면 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient**로 설정 해야 합니다. 인덱스가 아직 없는 경우 **Sort** 속성에 지정 된 각 필드에 대해 임시 인덱스가 생성 됩니다.  
  
 **Sort** 속성을 빈 문자열로 설정 하면 행을 원래 순서로 다시 설정 하 고 임시 인덱스를 삭제 합니다. 기존 인덱스는 삭제 되지 않습니다.  
  
 **레코드 집합** 에 *firstName*, *middleInitial*및 *lastName*이라는 세 개의 필드가 있다고 가정 합니다. **Sort** 속성을 문자열 ""로 설정 합니다 .이 문자열은 성을 기준으로 내림차순으로 정렬 한 다음 이름을 기준으로 오름차순으로 정렬 합니다 `lastName DESC, firstName ASC` . **Recordset** 중간 이니셜은 무시 됩니다.  
  
 정렬 조건 문자열에서 참조 되는 필드는 **asc** 및 **DESC**키워드와 충돌 하므로 "ASC" 또는 "DESC"로 명명할 수 없습니다. **레코드 집합**을 반환 하는 쿼리의 **AS** 키워드를 사용 하 여 이름이 충돌 하는 필드에 별칭을 지정 합니다.  
  
 **레코드 집합** 필터링에 대 한 자세한 내용은이 항목의 뒷부분에 나오는 "결과 필터링"을 참조 하십시오.  
  
## <a name="finding-a-specific-record"></a>특정 레코드 찾기  
 ADO에서는 **레코드 집합**에서 특정 레코드를 찾기 위한 [Find](../../../ado/reference/ado-api/find-method-ado.md) 및 [Seek](../../../ado/reference/ado-api/seek-method.md) 메서드를 제공 합니다. **Find** 메서드는 다양 한 공급자에서 지원 되지만 단일 검색 조건으로 제한 됩니다. **Seek** 메서드는 여러 조건에 대 한 검색을 지원 하지만 많은 공급자가 지원 하지는 않습니다.  
  
 필드의 인덱스는 **레코드 집합** 개체의 **찾기** 메서드 및 **정렬** 및 **필터** 속성의 성능을 크게 향상 시킬 수 있습니다. Dynamic [Optimize](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) 속성을 설정 하 여 **필드** 개체에 대 한 내부 인덱스를 만들 수 있습니다. [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient**로 설정 하면이 동적 속성이 **Field** 개체의 **Properties** 컬렉션에 추가 됩니다. 이 인덱스는 ADO의 내부에 있습니다. 액세스 권한을 얻거나 다른 용도로 사용할 수 없습니다. 또한이 인덱스는 **레코드 집합** 개체의 [index](../../../ado/reference/ado-api/index-property.md) 속성과는 다릅니다.  
  
 **Find** 메서드는 **레코드 집합**의 열 (필드) 내에서 값을 빠르게 찾습니다. **Optimize** 속성을 사용 하 여 열에 대 한 인덱스를 만들면 열에서 **찾기** 방법의 속도를 자주 향상 시킬 수 있습니다.  
  
 **Find** 메서드는 한 필드의 콘텐츠로 검색을 제한 합니다. **Seek** 메서드를 사용 하려면 인덱스가 있어야 하 고 다른 제한도 있어야 합니다. 인덱스의 기반이 아닌 여러 필드를 검색 해야 하거나 공급자가 인덱스를 지원 하지 않는 경우에는 **레코드 집합** 개체의 **Filter** 속성을 사용 하 여 결과를 제한할 수 있습니다.  
  
### <a name="find"></a>찾기  
 **Find** 메서드는 지정 된 조건을 충족 하는 행의 **레코드 집합** 을 검색 합니다. 필요에 따라 검색의 방향, 시작 행 및 시작 행의 오프셋을 지정할 수 있습니다. 조건을 충족 하는 경우에는 현재 행 위치가 찾은 레코드에 대해 설정 됩니다. 그렇지 않으면 검색 방향에 따라 위치가 **레코드 집합**의 끝 (또는 시작)으로 설정 됩니다.  
  
 조건에는 단일 열 이름만 지정할 수 있습니다. 즉,이 메서드는 여러 열 검색을 지원 하지 않습니다.  
  
 조건에 대 한 비교 연산자는 " **>** " (보다 큼), " **\<** " (보다 작음), "=" (같음), ">=" (크거나 같음), "<=" (작거나 같음), "<>" (같지 않음) 또는 "LIKE" (패턴 일치)가 될 수 있습니다.  
  
 조건 값은 문자열, 부동 소수점 숫자 또는 날짜 일 수 있습니다. 문자열 값은 작은따옴표 또는 "#" (숫자 기호) 표시 (예: "state = ' WA '" 또는 "state = #WA #")로 구분 됩니다. 날짜 값은 "#" (숫자 기호) 표시 (예: "start_date > #7/22/97 #")로 구분 됩니다.  
  
 비교 연산자가 "like" 이면 문자열 값에 별표 (*)를 포함 하 여 하나 이상의 문자 또는 하위 문자열을 찾을 수 있습니다. 예를 들어 "m '과 같은 상태는 \* Maine 및 Massachusetts와 일치 합니다. 선행 및 후행 별표를 사용 하 여 값 내에 포함 된 하위 문자열을 찾을 수도 있습니다. 예를 들어 "as '와 같은 ' state '는 \* \* 알래스카, 아칸 사스 및 Massachusetts와 일치 합니다.  
  
 앞에서와 같이 별표는 조건 문자열의 끝 이나 조건 문자열의 시작과 끝 모두에 함께 사용할 수 있습니다. 별표는 선행 와일드 카드 (' * str ') 또는 포함 된 와일드 카드 (' r ')로 사용할 수 없습니다 \* . 그러면 오류가 발생 합니다.  
  
### <a name="seek-and-index"></a>Seek 및 Index  
 기본 공급자가 **레코드 집합** 개체에 대 한 인덱스를 지 원하는 경우에는 **Index** 속성과 함께 **Seek** 메서드를 사용 합니다. [지원](../../../ado/reference/ado-api/supports-method.md)**(adseek)** 메서드를 사용 하 여 기본 공급자가 **Seek**를 지원 하는지 여부를 확인 하 고 **지원 (adseek)** 메서드를 사용 하 여 공급자가 인덱스를 지원 하는지 여부를 확인 합니다. 예를 들어 [Microsoft Jet 용 OLE DB 공급자](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) 는 **검색** 및 **인덱스**를 지원 합니다.  
  
 **검색** 에서 원하는 행을 찾지 못하면 오류가 발생 하지 않으며 **레코드 집합**의 끝에 행이 배치 됩니다. 이 메서드를 실행 하기 전에 **인덱스** 속성을 원하는 인덱스로 설정 합니다.  
  
 이 메서드는 서버 쪽 커서 에서만 지원 됩니다. **레코드 집합** 개체의 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성 값이 **adUseClient**인 경우 검색은 지원 되지 않습니다.  
  
 이 메서드는 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 값 **adCmdTableDirect**를 사용 하 여 **레코드 집합** 개체를 연 경우에만 사용할 수 있습니다.  
  
## <a name="filtering-the-results"></a>결과 필터링  
 **Find** 메서드는 한 필드의 콘텐츠로 검색을 제한 합니다. **Seek** 메서드를 사용 하려면 인덱스가 있어야 하 고 다른 제한도 있어야 합니다. 인덱스의 기반이 아닌 여러 필드를 검색 해야 하거나 공급자가 인덱스를 지원 하지 않는 경우에는 **레코드 집합** 개체의 **Filter** 속성을 사용 하 여 결과를 제한할 수 있습니다.  
  
 **Filter** 속성을 사용 하 여 레코드 **집합** 개체에서 레코드를 선택적으로 화면에 출력 합니다. 필터링 된 **레코드 집합** 은 현재 커서가 됩니다. 즉, **필터 조건을 충족** 하지 않는 레코드는 **필터** 를 제거할 때까지 **레코드 집합** 에서 사용할 수 없습니다. 현재 커서를 기준으로 값을 반환 하는 다른 속성 (예: **AbsolutePosition**, **AbsolutePage**, **RecordCount**및 **PageCount**)이 영향을 받습니다. 이는 **필터** 속성을 특정 값으로 설정 하면 현재 레코드가 새 값을 충족 하는 첫 번째 레코드로 이동 하기 때문입니다.  
  
 **Filter** 속성은 variant 인수를 사용 합니다. 이 값은 **필터** 속성을 사용 하기 위한 세 가지 방법 (조건 문자열, **filtergroupenum** 상수 또는 책갈피 배열) 중 하나를 나타냅니다. 자세한 내용은이 항목의 뒷부분에 나오는 조건 문자열을 사용 하 여 필터링, 상수로 필터링 및 책갈피로 필터링을 참조 하세요.  
  
> [!NOTE]
>  선택할 데이터를 알고 있는 경우 일반적으로 **필터** 속성에 의존 하지 않고 결과 집합을 효과적으로 필터링 하는 SQL 문을 사용 하 여 **레코드 집합** 을 여는 것이 더 효율적입니다.  
  
 **레코드 집합**에서 필터를 제거 하려면 **adfilternone** 상수를 사용 합니다. **Filter** 속성을 길이가 0 인 문자열 ("")로 설정 하면 **adfilternone** 상수를 사용 하는 것과 동일한 효과가 있습니다.  
  
### <a name="filtering-with-a-criteria-string"></a>조건 문자열을 사용 하 여 필터링  
 조건 문자열은 *FieldName 연산자 값* 형식의 절로 구성 됩니다 (예: `"LastName = 'Smith'"` ). 개별 절 **과** (예: `"LastName = 'Smith' AND FirstName = 'John'"` ) 및 **또는** (예:)를 연결 하 여 복합 절을 만들 수 있습니다 `"LastName = 'Smith' OR LastName = 'Jones'"` . 조건 문자열에 대해 다음 지침을 사용 합니다.  
  
-   *FieldName* 은 **레코드 집합**의 올바른 필드 이름 이어야 합니다. 필드 이름에 공백이 포함 된 경우 이름을 대괄호로 묶어야 합니다.  
  
-   *연산자* 는 **\<** , **>** ,,,, **\<=** **>=** **<>** **=** 또는 **와**같은 중 하나 여야 합니다.  
  
-   *Value* 는 필드 값을 비교 하는 데 사용할 값입니다 (예:, `'Smith'` , `#8/24/95#` `12.345` 또는 `$50.00` ). 문자열이 있는 작은따옴표 (')와 날짜를 포함 하는 파운드 기호 ()를 사용 `#` 합니다. 숫자의 경우 소수점, 달러 기호 및 과학적 표기법을 사용할 수 있습니다. *연산자* 가 **LIKE**인 경우 *값* 은 와일드 카드 문자를 사용할 수 있습니다. 별표 ( \* ) 및 백분율 기호 (%)만 와일드 카드 문자를 사용할 수 있으며 문자열에서 마지막 문자 여야 합니다. *값* 은 null 일 수 없습니다.  
  
    > [!NOTE]
    >  필터 *값*에 작은따옴표 (')를 포함 하려면 두 개의 작은따옴표를 사용 하 여 하나를 표시 합니다. 예를 들어 *O'Malley*를 필터링 하려면 조건 문자열이 여야 합니다 `"col1 = 'O''Malley'"` . 필터 값의 시작과 끝에 작은따옴표를 포함 하려면 문자열을 파운드 기호 (#)로 묶습니다. 예를 들어 *' 1 '* 을 필터링 하려면 조건 문자열이 여야 합니다 `"col1 = #'1'#"` .  
  
 **과** 와 **또는**사이에는 우선 순위가 없습니다. 절은 괄호 안에 그룹화 할 수 있습니다. 그러나 다음과 같이 **또는** 에 의해 조인 된 절을 그룹화 한 다음 및를 사용 하 여 그룹을 다른 절에 조인할 수는 없습니다.  
  
```  
(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'  
```  
  
 대신 다음과 같이이 필터를 생성 합니다.  
  
```  
(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')  
```  
  
 **LIKE** 절에서는 패턴의 시작과 끝 (예:) 또는 패턴의 끝에만 와일드 카드를 사용할 수 있습니다 `LastName Like '*mit*'` (예: `LastName Like 'Smit*'` ).  
  
### <a name="filtering-with-a-constant"></a>상수로 필터링  
 다음 상수는 **레코드 집합**을 필터링 하는 데 사용할 수 있습니다.  
  
|상수|설명|  
|--------------|-----------------|  
|**adFilterAffectedRecords**|마지막 **삭제**, 다시 **동기화**, **UpdateBatch**또는 **CancelBatch** 호출의 영향을 받는 레코드만 볼 필터입니다.|  
|**adFilterConflictingRecords**|마지막 일괄 업데이트에 실패 한 레코드를 보기 위한 필터입니다.|  
|**adFilterFetchedRecords**|현재 캐시의 레코드 (즉, 데이터베이스에서 레코드를 검색 하는 마지막 호출의 결과)를 보기 위한 필터입니다.|  
|**adFilterNone**|현재 필터를 제거 하 고 보기 위해 모든 레코드를 복원 합니다.|  
|**adFilterPendingRecords**|변경 되었지만 아직 서버에 전송 되지 않은 레코드만 볼 수 있는 필터입니다. 일괄 처리 업데이트 모드에만 적용할 수 있습니다.|  
  
 필터 상수를 사용 하면 다음 예제와 같이 마지막 **UpdateBatch** 메서드 호출 중에 영향을 받은 레코드만 볼 수 있도록 하 여 일괄 처리 업데이트 모드에서 개별 레코드 충돌을 보다 쉽게 해결할 수 있습니다.  
  
 `Attribute VB_Name = "modExaminingData"`  
  
### <a name="filtering-with-bookmarks"></a>책갈피를 사용 하 여 필터링  
 마지막으로, **필터** 속성에 책갈피의 변형 배열을 전달할 수 있습니다. 결과 커서에는 책갈피가 속성에 전달 된 레코드만 포함 됩니다. 다음 코드 예제에서는 *ProductName* 필드에 "B"가 있는 레코드 **집합** 의 레코드에서 책갈피의 배열을 만듭니다. 그런 다음 배열을 **필터** 속성에 전달 하 고 필터링 된 결과 **레코드 집합**에 대 한 정보를 표시 합니다.  
  
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
 **복제** 메서드를 사용 하 여 여러 중복 **레코드 집합** 개체를 만들 수 있습니다. 특히 지정 된 레코드 집합에서 둘 이상의 현재 레코드를 유지 관리 하려는 경우에 사용 합니다. **Clone** 메서드를 사용 하는 것은 원래와 같은 정의를 사용 하 여 새 **레코드 집합** 개체를 만들고 여는 것 보다 더 효율적입니다.  
  
 새로 만든 클론의 현재 레코드는 원래 첫 번째 레코드로 설정 됩니다. 복제 된 **레코드 집합** 의 현재 레코드 포인터는 원래 또는 그 반대로 동기화 되지 않습니다. 각 **레코드 집합**에서 개별적으로 탐색할 수 있습니다.  
  
 하나의 **레코드 집합** 개체에 대 한 변경 내용은 커서 유형에 관계 없이 모든 클론에 표시 됩니다. 그러나 원래 **레코드 집합**에서 [Requery](../../../ado/reference/ado-api/requery-method.md) 를 실행 한 후에는 복제본이 더 이상 원래와 동기화 되지 않습니다.  
  
 원래 **레코드 집합** 을 닫으면 복사본은 닫히지 않으며 복사본을 닫지 않고 원본 또는 기타 복사본을 닫습니다.  
  
 책갈피를 지 원하는 경우에만 **레코드 집합** 개체를 복제할 수 있습니다. 책갈피 값은 서로 바꿔 사용할 수 있습니다. 즉, 한 **레코드 집합** 개체의 책갈피 참조는 해당 복제본의 동일한 레코드를 참조 합니다.
