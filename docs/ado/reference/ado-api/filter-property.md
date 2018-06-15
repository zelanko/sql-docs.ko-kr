---
title: 속성 필터링 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Filter
helpviewer_keywords:
- Filter property
ms.assetid: 80263a7a-5d21-45d1-84fc-34b7a9be4c22
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 72efa7b9a70bdfdf141c32d5487cc2a5b9776d16
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35278762"
---
# <a name="filter-property"></a>필터 속성
데이터에 대 한 필터 나타냅니다는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값

설정 하거나 반환는 **Variant** 값으로, 다음 항목 중 하나를 포함할 수 있습니다.  
  
-   **조건 문자열:** 하나 이상의 개별 절과 연결 된 구성 문자열 **AND** 또는 **OR** 연산자입니다.  
  
-   **책갈피 배열:** 값의 레코드를 가리키는 고유한 책갈피의 배열에서 **레코드 집합** 개체입니다.  
  
-   A [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) 값입니다.  
  
## <a name="remarks"></a>Remarks

사용 하 여는 **필터** 속성을 선택적으로의 레코드 숨기는 **레코드 집합** 개체입니다. 필터링 된 **레코드 집합** 현재 커서 됩니다. 현재를 기준으로 값을 반환 하는 기타 속성도 **커서** 영향을 받는 같은 [AbsolutePosition 속성 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md), [AbsolutePage 속성 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md), [ RecordCount 속성 (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md), 및 [PageCount 속성 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)합니다. 설정의 **필터** 속성 특정 새 값을 새 값을 충족 하는 첫 번째 레코드를 현재 레코드를 이동 합니다.
  
조건 문자열은 형태로 절 이루어져 *FieldName-연산자 값* (예를 들어 `"LastName = 'Smith'"`). 복합 절이 포함 된 개별 절을 연결 하 여 만들 수 있습니다 **AND** (예를 들어 `"LastName = 'Smith' AND FirstName = 'John'"`) 또는 **OR** (예를 들어 `"LastName = 'Smith' OR LastName = 'Jones'"`). 빈 문자열에 대 한 다음 지침을 따르세요.

-   *FieldName* 에서 유효한 필드 이름 이어야 합니다는 **레코드 집합**합니다. 필드 이름에 공백이 이름을 대괄호로 묶어야 합니다.  
  
-   연산자는 다음 중 하나 여야 합니다: \<, >, \<=, > =, <>, =, 또는 **같은**합니다.  
  
-   값이 있는 필드 값을 비교 하 여 값 (예를 들어 'Smith', #8/24/95 # 12.345, 또는 $50.00). 문자열 및 날짜와 함께 파운드 기호 (#)와 작은따옴표를 사용 합니다. 숫자를 소수점이 하, 달러 기호 및 과학적 표기법을 사용할 수 있습니다. 연산자가 **같은**, 값 와일드 카드를 사용할 수 있습니다. 별표 (*) 및 백분율 기호 (%) 와일드 카드는 허용 하 고 문자열의 마지막 문자 여야 합니다. 값은 null 일 수 없습니다.  
  
> [!NOTE]
>  필터 값에에서 작은따옴표 (')를 포함 하려면 두 개의 작은따옴표를 사용 하 여 하나를 나타냅니다. 예를 들어 O'Malley를 필터링 하려면 조건 문자열 이어야 합니다 `"col1 = 'O''Malley'"`합니다. 시작과 끝 필터 값의 작은 따옴표를 포함 하려면 숫자 기호를 사용 하 여 문자열을 묶습니다 (#). 예를 들어, '1'을 필터링 하려면 조건 문자열 이어야 합니다 `"col1 = #'1'#"`합니다.  
  
-   사이의 선행 규칙이 AND 및 또는 합니다. 괄호 안에 절을 그룹화 할 수 있습니다. 그러나 OR로 결합 하는 절을 그룹화 하 고을 다음 코드 조각에서와 같이 AND로 다른 절에서 그룹에 조인할 수 없습니다.  
 `(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'`  
  
-   이 필터를 생성 하는 대신,  
 `(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')`  
  
-   에 **같은** 절 시작과 패턴의 끝 부분에 와일드 카드를 사용할 수 있습니다. 사용할 수는 예를 들어 `LastName Like '*mit*'`합니다. 또는 **같은** 와일드 카드 패턴의 끝에만 사용할 수 있습니다. `LastName Like 'Smit*'`)을 입력합니다.  
  
 필터 상수 보다 쉽게 마지막 하는 동안 해당 레코드를 보고, 예를 들어 허용 하 여 일괄 처리 업데이트 모드에 있는 동안 개별 레코드 충돌 영향을 해결 하려면 [UpdateBatch 메서드](../../../ado/reference/ado-api/updatebatch-method.md) 메서드를 호출 합니다.  
  
설정의 **필터** 속성 자체 기본 데이터와의 충돌로 인해 실패할 수 있습니다. 예를 들어 레코드를 다른 사용자가 이미 삭제 되었을 때이 오류가 발생할 수 있습니다. 이 경우 공급자는 경고를 반환는 [오류 컬렉션 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md) 컬렉션 되지만 프로그램 실행을 중단 하지는 않습니다. 런타임 시 오류는 요청 된 모든 레코드에 충돌이 있는 경우에 발생 합니다. 사용 하 여는 [Status 속성 (ADO 레코드 집합)](../../../ado/reference/ado-api/status-property-ado-recordset.md) 속성 충돌 레코드를 찾을 수 있습니다.  
  
설정의 **필터** 속성을 빈 문자열 ("")를 사용 하 여 것과 동일한 결과가 **adFilterNone** 상수입니다.
  
때마다는 **필터** 속성이 설정 되어 현재 레코드 위치 레코드로 이동 하는 첫 번째에 있는 레코드의 필터링 된 하위 집합에는 **레코드 집합**합니다. 마찬가지로,는 **필터** 속성의 선택을 취소의 첫 번째 레코드를 이동 현재 레코드 위치는 **레코드 집합**합니다.

되었다고 가정는 **레코드 집합** 형식이 sql_variant 인 같은 일부 variant 형식의 필드에 따라 필터링 됩니다. 오류 (DISP_E_TYPEMISMATCH 80020005 또는) 조건 문자열에서 사용 되는 필드 및 필터 값의 하위 유형이 일치 하지 않을 때 발생 합니다. 예를 들어 있다고 가정 합니다.

- A **레코드 집합** 개체 (rs) sql_variant 형식 열 (C)이 포함 되어 있습니다.
- 및이 열의 필드 값이 1 I4 형식의 할당 합니다. 로 설정 된 조건 문자열 `rs.Filter = "C='A'"` 필드입니다.

이 구성은 런타임 시 오류를 생성합니다. 그러나 `rs.Filter = "C=2"` 동일한 적용 된 필드는 모든 오류를 생성 하지 않습니다. 한 필드는 필터링 하 여 현재 레코드 집합 제외 합니다.

참조는 [책갈피 속성 (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md) 속성에 대 한 설명은 책갈피 값을 필터 속성을 사용 하면 배열을 빌드할 수 있습니다.

필터 조건 문자열의 형태로 지속형된 내용의 영향을 미치는 에서만 **레코드 집합**합니다. 조건 문자열의 예로 `OrderDate > '12/31/1999'`합니다. 책갈피 또는에서 값을 사용 하는 배열을 사용 하 여 작성 된 필터는 **FilterGroupEnum**, 지속형된는 내용의 영향을 미치지 않는 **레코드 집합**합니다. 이러한 규칙은 클라이언트 쪽 이나 서버 쪽 커서를 사용 하 여 만든 레코드 집합에 적용 됩니다.
  
> [!NOTE]
>  필터링 된을 그 플래그를 적용 하면 수정할 **레코드 집합** 일괄 업데이트 모드의 결과 **레코드 집합** 의 키 필드 기반 필터링 하는 경우 비어는 키 필드 값에 단일 키 테이블을 수정 했습니다. 결과 **레코드 집합** 비어 있지 다음 문 중 하나에 됩니다.  
  
-   단일 키 테이블의 키가 아닌 필드를 기준으로 필터링  
  
-   다중 키 테이블의 모든 필드를 기준으로 필터링  
  
-   단일 키 테이블의 키가 아닌 필드에서 수정 되었습니다.  
  
-   다중 키 테이블의 모든 필드에서 수정 되었습니다.  
  
다음 표에서 요약의 효과 **그** 필터링 및 수정 작업의 다양 한 조합에서 합니다. 왼쪽된 열은 가능한 수정 작업을 보여 줍니다. 단일 키 테이블의 키 필드 또는 다중 키 테이블의 키 필드 중 하나에 있는 아닌 필드에서 수정할 수 있습니다. 맨 위 행은 필터링 조건을 보여 줍니다. 필터링 기반 아닌 필드의 모든 다중 키 테이블의 키 필드 또는 단일 키 테이블의 키 필드입니다. 교차 셀의 결과 보여 줍니다. A **+** 더하기 기호를 적용 의미 **그** 비어 있지 않은 결과 **레코드 집합**합니다. A **-** 빼기 기호는 빈 의미 **레코드 집합**합니다.  
  
||비 키|단일 키|여러 키|
|-|--------------|----------------|-------------------|
|**비 키**|+|+|+|
|**단일 키**|+|-|해당 사항 없음|
|**여러 키**|+|해당 사항 없음|+|
|||||
  
## <a name="applies-to"></a>적용 대상

[레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목

[필터 및 RecordCount 속성 예제 (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)
[필터 및 RecordCount 속성 예제 (VC + +)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)
[Clear 메서드 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md) 
 [(ADO) 속성-동적 최적화](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)
