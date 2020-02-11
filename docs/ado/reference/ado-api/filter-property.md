---
title: 필터 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Filter
helpviewer_keywords:
- Filter property
ms.assetid: 80263a7a-5d21-45d1-84fc-34b7a9be4c22
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ff06bc27e765945d1cca74b5f8401e0caadf6b17
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67918632"
---
# <a name="filter-property"></a>Filter 속성
[레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)의 데이터에 대 한 필터를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값

다음 항목 중 하나를 포함할 수 있는 **Variant** 값을 설정 하거나 반환 합니다.  
  
-   **조건 문자열:** **AND** 또는 **or** 연산자와 연결 된 하나 이상의 개별 절로 구성 된 문자열입니다.  
  
-   **책갈피의 배열:** **레코드 집합** 개체의 레코드를 가리키는 고유한 책갈피 값의 배열입니다.  
  
-   [Filtergroupenum](../../../ado/reference/ado-api/filtergroupenum.md) 값입니다.  
  
## <a name="remarks"></a>설명

**Filter** 속성을 사용 하 여 레코드 **집합** 개체에서 레코드를 선택적으로 화면에 출력 합니다. 필터링 된 **레코드 집합** 은 현재 커서가 됩니다. 현재 **커서** 를 기준으로 값을 반환 하는 다른 속성 (예: [ado](../../../ado/reference/ado-api/absoluteposition-property-ado.md)), [AbsolutePage Property (](../../../ado/reference/ado-api/absolutepage-property-ado.md)ado), AbsolutePosition 속성 [(](../../../ado/reference/ado-api/recordcount-property-ado.md)ado) 및 [PageCount 속성 (ado))](../../../ado/reference/ado-api/pagecount-property-ado.md)이 영향을 받습니다. **필터** 속성을 특정 새 값으로 설정 하면 현재 레코드가 새 값을 충족 하는 첫 번째 레코드로 이동 합니다.
  
조건 문자열은 *FieldName-Operator-Value* 형식의 절로 구성 됩니다 (예: `"LastName = 'Smith'"`). 개별 절을 **AND** (예: `"LastName = 'Smith' AND FirstName = 'John'"`) 또는 **또는** (예: `"LastName = 'Smith' OR LastName = 'Jones'"`)와 연결 하 여 복합 절을 만들 수 있습니다. 조건 문자열의 경우 다음 지침을 사용 합니다.

-   *FieldName* 은 **레코드 집합**의 올바른 필드 이름 이어야 합니다. 필드 이름에 공백이 포함 된 경우 이름을 대괄호로 묶어야 합니다.  
  
-   연산자는, >, \< \<=, >=,  <>, = 또는 **와**같은 중 하나 여야 합니다.  
  
-   Value는 필드 값을 비교 하는 데 사용할 값입니다 (예: ' Smith ', #8/24/95 #, 12.345 또는 $50.00). 날짜에 문자열 및 파운드 기호 (#)와 함께 작은따옴표를 사용 합니다. 숫자의 경우 소수점, 달러 기호 및 과학적 표기법을 사용할 수 있습니다. 연산자가 **LIKE**인 경우 값은 와일드 카드를 사용할 수 있습니다. 별표 (*) 및 백분율 기호 (%)만 와일드 카드는 사용할 수 있으며 문자열에서 마지막 문자 여야 합니다. 값은 null 일 수 없습니다.  
  
> [!NOTE]
>  필터 값에 작은따옴표 (')를 포함 하려면 두 개의 작은따옴표를 사용 하 여 하나를 표시 합니다. 예를 들어 O'Malley를 필터링 하려면 조건 문자열이 여야 `"col1 = 'O''Malley'"`합니다. 필터 값의 시작과 끝에 작은따옴표를 포함 하려면 문자열을 파운드 기호 (#)로 묶습니다. 예를 들어 ' 1 '을 필터링 하려면 조건 문자열이 여야 `"col1 = #'1'#"`합니다.  
  
-   과와 또는 사이에는 우선 순위가 없습니다. 절은 괄호 안에 그룹화 할 수 있습니다. 그러나 다음 코드 조각과 같이 또는에 의해 조인 된 절을 그룹화 한 다음 및를 사용 하 여 그룹을 다른 절에 조인할 수는 없습니다.  
 `(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'`  
  
-   대신이 필터를 다음과 같이 생성 합니다.  
 `(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')`  
  
-   **LIKE** 절에서는 패턴의 시작과 끝에 와일드 카드를 사용할 수 있습니다. 예를 들어를 사용할 `LastName Like '*mit*'`수 있습니다. 또는 **LIKE** 를 사용 하는 경우 패턴의 끝에만 와일드 카드를 사용할 수 있습니다. `LastName Like 'Smit*'`)을 입력합니다.  
  
 필터 상수를 사용 하면 예를 들어, 마지막 [UpdateBatch 메서드](../../../ado/reference/ado-api/updatebatch-method.md) 호출 중에 영향을 받은 레코드만 볼 수 있으므로 일괄 업데이트 모드에서 개별 레코드 충돌을 쉽게 해결할 수 있습니다.  
  
기본 데이터와의 충돌로 인해 **필터** 속성 자체를 설정 하지 못할 수 있습니다. 예를 들어 다른 사용자가 이미 레코드를 삭제 한 경우이 오류가 발생할 수 있습니다. 이 경우 공급자는 [오류 컬렉션 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md) 컬렉션에 대 한 경고를 반환 하지만 프로그램 실행을 중단 하지는 않습니다. 런타임에 발생 한 오류는 요청 된 모든 레코드에 충돌이 있는 경우에만 발생 합니다. [Status 속성 (ADO 레코드 집합)](../../../ado/reference/ado-api/status-property-ado-recordset.md) 속성을 사용 하 여 충돌이 발생 한 레코드를 찾을 수 있습니다.  
  
**Filter** 속성을 길이가 0 인 문자열 ("")로 설정 하면 **adfilternone** 상수를 사용 하는 것과 동일한 효과가 있습니다.
  
**Filter** 속성이 설정 될 때마다 현재 레코드 위치가 레코드 **집합**에 있는 레코드의 필터링 된 하위 집합에 있는 첫 번째 레코드로 이동 합니다. 마찬가지로 **필터** 속성을 선택 취소 하면 현재 레코드 위치가 **레코드 집합**의 첫 번째 레코드로 이동 합니다.

**레코드 집합이** sql_variant 형식과 같은 일부 variant 형식의 필드를 기준으로 필터링 되는 경우를 가정 합니다. 조건 문자열에 사용 된 필드와 필터 값의 하위 유형이 일치 하지 않을 경우 오류 (DISP_E_TYPEMISMATCH 또는 80020005)가 발생 합니다. 예를 들어 다음을 가정 합니다.

- Rs ( **레코드 집합** 개체)는 sql_variant 형식의 열 (C)을 포함 합니다.
- 그리고이 열의 필드에 I4 형식의 1 값이 할당 되었습니다. 필드에서 조건 문자열은로 `rs.Filter = "C='A'"` 설정 됩니다.

이 구성은 런타임 중에 오류를 생성 합니다. 그러나 같은 `rs.Filter = "C=2"` 필드에 적용 해도 오류가 발생 하지는 않습니다. 그리고 필드가 현재 레코드 집합에서 필터링 됩니다.

Filter 속성에 사용할 배열을 만들 수 있는 책갈피 값에 대 한 설명은 [Bookmark 속성 (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md) 속성을 참조 하세요.

조건 문자열 형식의 필터만 지속형 **레코드 집합**의 내용에 영향을 줍니다. 조건 문자열의 예는 `OrderDate > '12/31/1999'`입니다. 책갈피 배열을 사용 하거나 **Filtergroupenum**의 값을 사용 하 여 만든 필터는 지속형 **레코드 집합**의 내용에 영향을 주지 않습니다. 이러한 규칙은 클라이언트 쪽 또는 서버 쪽 커서를 사용 하 여 만든 레코드 집합에 적용 됩니다.
  
> [!NOTE]
>  일괄 처리 업데이트 모드에서 필터 및 수정 된 **레코드 집합** 에 adFilterPendingRecords 플래그를 적용 하면 필터링이 단일 키 테이블의 키 필드를 기반으로 하 고 키 필드 값이 수정 된 경우 결과 **레코드 집합이** 비어 있습니다. 다음 문 중 하나가 true 인 경우 결과 **레코드 집합** 은 비어 있지 않습니다.  
  
-   필터링은 단일 키 테이블의 키가 아닌 필드를 기반으로 합니다.  
  
-   필터링은 다중 키 테이블의 필드를 기반으로 합니다.  
  
-   단일 키 테이블에서 키가 아닌 필드를 수정 했습니다.  
  
-   여러 키가 있는 테이블의 모든 필드를 수정 했습니다.  
  
다음 표에서는 다양 한 필터링 및 수정 조합에서 **Adfilterpendingrecords** 의 효과를 요약 하 여 보여 줍니다. 왼쪽 열에는 가능한 수정 내용이 표시 됩니다. 키가 아닌 필드, 단일 키 테이블의 키 필드 또는 다중 키 테이블의 키 필드에 대 한 수정 작업을 수행할 수 있습니다. 맨 위 행은 필터링 조건을 표시 합니다. 필터링은 키가 아닌 필드, 단일 키 테이블의 키 필드 또는 다중 키 테이블의 키 필드 중 하나를 기반으로 할 수 있습니다. 교차 하는 셀에 결과가 표시 됩니다. 더하기 **+** 기호는 **Adfilterpendingrecords** 를 적용 하 여 비어 있지 않은 **레코드 집합**을 생성 한다는 것을 의미 합니다. 빼기 **-** 기호는 빈 **레코드 집합**을 의미 합니다.  
  
||키가 아닌|단일 키|여러 키|
|-|--------------|----------------|-------------------|
|**키가 아닌**|+|+|+|
|**단일 키**|+|-|해당 없음|
|**여러 키**|+|해당 없음|+|
|||||
  
## <a name="applies-to"></a>적용 대상

[레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목

[Filter 및 recordcount 속성 예제 (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)
[필터 및 recordcount 속성 예제 (VC + +)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)
[Clear 메서드 (ado)](../../../ado/reference/ado-api/clear-method-ado.md)
[Optimize 속성-동적 (ado)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)
