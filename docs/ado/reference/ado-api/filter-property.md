---
title: 속성 필터링 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: cede9be7c484d40c2220fc891779f7dfb6e5a8df
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47762751"
---
# <a name="filter-property"></a>Filter 속성
데이터에 대 한 필터를 나타냅니다는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값

설정 하거나 반환 된 **Variant** 다음 항목 중 하나를 포함할 수 있는 값:  
  
-   **조건 문자열:** 연결 된 하나 이상의 개별 절 이루어져 문자열로 **AND** 또는 **OR** 연산자입니다.  
  
-   **책갈피의 배열:** 고유 책갈피의 배열에서 레코드를 가리키는 값을 **레코드 집합** 개체입니다.  
  
-   A [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) 값입니다.  
  
## <a name="remarks"></a>Remarks

사용 하 여는 **필터** 레코드에 선택적으로 화면에 속성을 **레코드 집합** 개체입니다. 필터링 **레코드 집합** 현재 커서 됩니다. 현재 값을 반환 하는 다른 속성 기반 **커서** 영향을 받는 같은 [AbsolutePosition 속성 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)를 [AbsolutePage 속성 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)를 [ RecordCount 속성 (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md), 및 [PageCount 속성 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)합니다. 설정 된 **필터** 속성을 특정 새 값을 새 값을 충족 하는 첫 번째 레코드를 현재 레코드를 이동 합니다.
  
조건 문자열 형태로 절 이루어집니다 *FieldName-연산자 값* (예를 들어 `"LastName = 'Smith'"`). 복합 절이 포함 된 개별 절을 연결 하 여 만들 수 있습니다 **모양과** (예를 들어 `"LastName = 'Smith' AND FirstName = 'John'"`) 또는 **OR** (예를 들어 `"LastName = 'Smith' OR LastName = 'Jones'"`). 조건 문자열의 경우 다음 지침을 따르세요.

-   *FieldName* 에서 유효한 필드 이름 이어야 합니다 **레코드 집합**합니다. 필드 이름에 공백이 이름을 대괄호로 묶어야 합니다.  
  
-   연산자는 다음 중 하나 여야 합니다: \<, >, \<=, > =, <>, =, 또는 **와 같은**합니다.  
  
-   값이 있는 필드 값을 비교 합니다 값 (예를 들어, 'Smith', 95 24/8 / # 12.345, 또는 $50.00). 문자열 및 날짜를 사용 하 여 파운드 기호 (#)를 사용 하 여 작은따옴표를 사용 합니다. 숫자의 경우 소수점이 하, 달러 기호 및 과학적 표기법을 사용할 수 있습니다. 연산자가 **같은**, 값에서 와일드 카드를 사용할 수 있습니다. 별표 (*) 및 백분율 기호 (%) 와일드 카드만 허용 하며 문자열의 마지막 문자 여야 합니다. 값은 null 일 수 없습니다.  
  
> [!NOTE]
>  필터 값에에서 작은따옴표 (')를 포함 하려면 하나를 나타내는 두 개의 작은따옴표를 사용 합니다. 예를 들어 O'Malley를 필터링 하려면 조건 문자열 이어야 합니다 `"col1 = 'O''Malley'"`합니다. 시작 및 필터 값의 끝에 작은따옴표를 포함 하려면 파운드 기호를 사용 하 여 문자열을 묶습니다 (#). 예를 들어, '1'을 필터링 하려면 조건 문자열 이어야 합니다 `"col1 = #'1'#"`합니다.  
  
-   사이는 우선 순위가 없는 AND 등을 제공 합니다. 괄호 안에 절을 그룹화 할 수 있습니다. 그러나 OR로 연결 하는 절을 그룹화 하 고 다음 코드 조각 에서처럼 AND 사용 하 여 다른 절을 그룹에 조인할 수 없습니다.  
 `(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'`  
  
-   이 필터를 생성 하는 대신  
 `(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')`  
  
-   에 **같은** 절 패턴의 시작과 끝에 와일드 카드를 사용할 수 있습니다. 예를 들어 사용할 수 있습니다 `LastName Like '*mit*'`합니다. 문제나 **같은** 패턴의 끝에만 와일드 카드를 사용할 수 있습니다. `LastName Like 'Smit*'`) 을 입력합니다.  
  
 필터 상수 쉽게 마지막 영향을 받은 일괄 업데이트 모드를 보고, 예를 들어, 해당 레코드에 허용 하 여 개별 레코드 충돌 해결 [UpdateBatch 메서드](../../../ado/reference/ado-api/updatebatch-method.md) 메서드를 호출 합니다.  
  
설정 된 **필터** 속성 자체 기본 데이터 충돌로 인해 실패할 수 있습니다. 예를 들어, 레코드를 다른 사용자가 이미 삭제 된 경우이 오류가 발생할 수 있습니다. 이 경우 공급자는 경고를 반환 합니다 [오류 컬렉션 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md) 컬렉션 프로그램 실행을 중단 하지는 않습니다 하지만 합니다. 요청 된 모든 레코드에 충돌이 있는 경우에 런타임 시 오류가 발생 했습니다. 사용 합니다 [Status 속성 (ADO 레코드 집합)](../../../ado/reference/ado-api/status-property-ado-recordset.md) 속성을 사용 하 여 충돌 레코드를 찾습니다.  
  
설정 된 **필터** 속성을 빈 문자열로 ("") 사용 하는 것과 동일한 효과가 합니다 **adFilterNone** 상수입니다.
  
때마다 합니다 **필터** 속성이 설정 되어 현재 레코드 위치에 있는 레코드의 필터링 된 하위 집합에서 첫 번째 레코드를 이동 합니다 **레코드 집합**합니다. 마찬가지로, 합니다 **필터** 속성의 선택을 취소 레코드의 현재 위치에 있는 첫 번째 레코드를 이동 합니다 **레코드 집합**합니다.

가정를 **레코드 집합** 형식이 sql_variant 인 같은 일부 variant 형식의 필드에 따라 필터링 됩니다. 오류 (DISP_E_TYPEMISMATCH 80020005 또는) 조건 문자열에 사용 된 필드 및 필터 값의 하위 유형이 일치 하지 않을 때 발생 합니다. 예를 들어, 가정 합니다.

- A **레코드 집합** 개체 (rs) sql_variant 형식 열 (C)이 포함 됩니다.
- 이 칼럼의 필드 값이 1 I4 형식의 할당 된 하며 로 설정 된 조건 문자열 `rs.Filter = "C='A'"` 필드입니다.

이 구성은 런타임 시 오류를 생성합니다. 그러나 `rs.Filter = "C=2"` 동일한 적용 필드는 모든 오류를 생성 하지 않습니다. 및 현재 레코드 집합에서 필드 필터링 됩니다.

참조 된 [책갈피 속성 (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md) 속성에 대 한 설명은 책갈피 값 배열을 필터 속성을 사용 하 여 사용 하 여 빌드할 수 있습니다.

필터 조건 문자열의 형태로 지속형된 내용의 영향을 미치는 에서만 **레코드 집합**합니다. 조건 문자열의 예로 `OrderDate > '12/31/1999'`합니다. 책갈피 또는에서 값을 사용 하는 배열을 사용 하 여 작성 된 필터를 **FilterGroupEnum**에 지속형된 내용의 영향을 주지 않습니다 **레코드 집합**합니다. 이러한 규칙은 클라이언트 쪽 이나 서버 쪽 커서를 사용 하 여 만든 레코드 집합에 적용 됩니다.
  
> [!NOTE]
>  그 플래그는 필터링을 적용 하는 경우 수정 **레코드 집합** 일괄 처리 업데이트 모드에서는 결과 **레코드 집합** 필터링 된 필드를 기반으로 키의 경우 비어 있는 것을 키 필드 값에 단일 키 테이블을 수정 했습니다. 결과 **레코드 집합** 다음 문 중 하나가 참인 경우 비어 있지 않은 됩니다.  
  
-   필터링 된 단일 키 테이블의 키가 아닌 필드에 기반 했습니다.  
  
-   필터링은 다중 키 테이블의 모든 필드에 기반 했습니다.  
  
-   단일 키 테이블의 키가 아닌 필드에서 수정 되었습니다.  
  
-   다중 키 테이블의 필드에서 수정 되었습니다.  
  
다음 표에서 미치는 **그** 의 필터링 및 수정 하는 다양 한 조합 합니다. 왼쪽된 열은 가능한 수정 작업을 보여 줍니다. 키가 지정 되지 않은 필드를 단일 키 테이블의 키 필드 또는 여러 키가 지정 된 테이블의 키 필드 중 하나에서 수정 작업을 만들 수 있습니다. 맨 위 행은 필터링 조건을 보여 줍니다. 수 수를 기준으로 필터링 키가 지정 되지 않은 필드를 단일 키 테이블을 사용 하거나 다중 키 테이블의 키 필드의 모든 키 필드입니다. 교차 셀의 결과 보여 줍니다. A **+** 더하기 기호는 적용 의미 **그** 비어 있지 않은 결과 **레코드 집합**합니다. A **-** 빼기 기호는 빈 의미 **Recordset**합니다.  
  
||비 키|단일 키|여러 키|
|-|--------------|----------------|-------------------|
|**비 키**|+|+|+|
|**단일 키**|+|-|해당 사항 없음|
|**여러 키**|+|해당 사항 없음|+|
|||||
  
## <a name="applies-to"></a>적용 대상

[레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목

[Filter 및 RecordCount 속성 예제 (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)
[Filter 및 RecordCount 속성 예제 (VC + +)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)
[Clear 메서드 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md) 
 [Optimize 속성-동적 (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)
