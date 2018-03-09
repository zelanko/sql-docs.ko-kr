---
title: "속성 필터링 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::Filter
helpviewer_keywords:
- Filter property
ms.assetid: 80263a7a-5d21-45d1-84fc-34b7a9be4c22
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8e0a74efdc9eeef18eac76e582355653d6677139
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="filter-property"></a>필터 속성
데이터에 대 한 필터 나타냅니다는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **Variant** 값으로, 다음 중 하나를 포함할 수 있습니다.  
  
-   **조건 문자열** ??? 연결 된 하나 이상의 개별 절 중 구성 된 문자열 **AND** 또는 **OR** 연산자입니다.  
  
-   **책갈피 배열** ??? 값의 레코드를 가리키는 고유한 책갈피의 배열에서 **레코드 집합** 개체입니다.  
  
-   A [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) 값입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **필터** 속성을 선택적으로의 레코드 숨기는 **레코드 집합** 개체입니다. 필터링 된 **레코드 집합** 현재 커서 됩니다. 현재를 기준으로 값을 반환 하는 기타 속성도 **커서** 영향을 받는 같은 [AbsolutePosition 속성 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md), [AbsolutePage 속성 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md), [ RecordCount 속성 (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md), 및 [PageCount 속성 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)합니다. 설정 때문에 이것이 **필터** 속성을 특정 값으로 새 값을 충족 하는 첫 번째 레코드를 현재 레코드를 이동 합니다.  
  
 조건 문자열은 형태로 절 이루어져 *FieldName-연산자 값* (예를 들어 `"LastName = 'Smith'"`). 복합 절이 포함 된 개별 절을 연결 하 여 만들 수 있습니다 **AND** (예를 들어 `"LastName = 'Smith' AND FirstName = 'John'"`) 또는 **OR** (예를 들어 `"LastName = 'Smith' OR LastName = 'Jones'"`). 빈 문자열에 대 한 다음 지침을 따르세요.  
  
-   *FieldName* 에서 유효한 필드 이름 이어야 합니다는 **레코드 집합**합니다. 필드 이름에 공백이 이름을 대괄호로 묶어야 합니다.  
  
-   연산자는 다음 중 하나 여야 합니다: \<, >, \<=, > =, <>, =, 또는 **같은**합니다.  
  
-   값이 있는 필드 값을 비교 하 여 값 (예를 들어 'Smith', #8/24/&#95; 12.345, 또는 $50.00). 문자열 및 날짜와 함께 파운드 기호 (#)와 작은따옴표를 사용 합니다. 숫자를 소수점이 하, 달러 기호 및 과학적 표기법을 사용할 수 있습니다. 연산자가 **같은**, 값 와일드 카드를 사용할 수 있습니다. 별표 (*) 및 백분율 기호 (%) 와일드 카드는 허용 하 고 문자열의 마지막 문자 여야 합니다. 값은 null 일 수 없습니다.  
  
> [!NOTE]
>  필터 값에에서 작은따옴표 (')를 포함 하려면 두 개의 작은따옴표를 사용 하 여 하나를 나타냅니다. 예를 들어 O'Malley를 필터링 하려면 조건 문자열 이어야 합니다 "col1 = ' O ' Malley'"입니다. 시작과 끝 필터 값의 작은 따옴표를 포함 하려면 숫자 기호를 사용 하 여 문자열을 묶습니다 (#). 예를 들어, '1'을 필터링 하려면 조건 문자열 이어야 합니다 "col1 = '1' # #"입니다.  
  
-   사이의 선행 규칙이 AND 및 또는 합니다. 괄호 안에 절을 그룹화 할 수 있습니다. 그러나 OR로 결합 하는 절을 그룹화 하 고을 다음과 같이 AND로 다른 절에서 그룹에 조인할 수 없습니다.`(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'`  
  
-   이 필터를 생성 하는 대신,`(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')`  
  
-   에 **같은** 절 시작과 패턴의 끝 부분에 와일드 카드를 사용할 수 있습니다 (LastName 유사한 예를 들어, ' * mit\*'), 또는 패턴의 끝에만 (LastName 유사한 예를 들어 ' Smit\*').  
  
 필터 상수 보다 쉽게 마지막 하는 동안 해당 레코드를 보고, 예를 들어 허용 하 여 일괄 처리 업데이트 모드에 있는 동안 개별 레코드 충돌 영향을 해결 하려면 [UpdateBatch 메서드](../../../ado/reference/ado-api/updatebatch-method.md) 메서드를 호출 합니다.  
  
 기본 데이터와의 충돌로 인해 실패할 수 있습니다 자체 Filter 속성 설정 (예를 들어 레코드 이미 삭제 되었습니다 다른 사용자에 의해). 이 경우 공급자는 경고를 반환 된 [오류 컬렉션 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md) 컬렉션 참조 하지 않는 프로그램 실행이 중단 합니다. 런타임 오류는 요청 된 모든 레코드에 충돌이 있는 경우에 발생 합니다. 사용 하 여는 [Status 속성 (ADO 레코드 집합)](../../../ado/reference/ado-api/status-property-ado-recordset.md) 속성 충돌 레코드를 찾을 수 있습니다.  
  
 설정의 **필터** 속성을 빈 문자열 ("")를 사용 하 여 것과 동일한 결과가 **adFilterNone** 상수입니다.  
  
 때마다는 **필터** 속성이 설정 되어 현재 레코드 위치 레코드로 이동 하는 첫 번째에 있는 레코드의 필터링 된 하위 집합에는 **레코드 집합**합니다. 마찬가지로,는 **필터** 속성의 선택을 취소의 첫 번째 레코드를 이동 현재 레코드 위치는 **레코드 집합**합니다.  
  
 경우는 **레코드 집합** 오류가 variant 형식 (예: sql_variant)의 필드에 따라 필터링 됩니다 (DISP_E_TYPEMISMATCH 또는 80020005) 조건 문자열에서 사용 되는 필드 및 필터 값의 하위 유형이 일치 하지 않는 경우 발생 합니다. 예를 들어 경우는 **레코드 집합** 개체 (rs) sql_variant 형식 열 (C)를 포함 하 고이 열의 필드 값이 1 rs의 조건 문자열을 설정 하는 I4 형식의 지정 된 합니다. 필터 = "C = 'A'" 필드에 오류가 생성 됩니다.는 런타임 시. 그러나 rs 합니다. 필터 = "C = 2"에 적용 된 필드는 필드는 현재 레코드 집합에서 필터링 하지만 오류를 생성 하지 않습니다.  
  
 참조는 [책갈피 속성 (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md) 속성에 대 한 설명은 책갈피 값을 필터 속성을 사용 하면 배열을 빌드할 수 있습니다.  
  
 조건 문자열의 형태로 필터링 (예: OrderDate > ' 12/31/1999 ')의 지속형 내용이 영향을 **레코드 집합**합니다. 배열의 책갈피를 사용 하 여 만든 필터 또는 FilterGroupEnum에서 값을 사용 하는 지속형된 내용의 영향을 주지 것입니다 **레코드 집합**합니다. 이러한 규칙은 클라이언트 쪽 이나 서버 쪽 커서를 사용 하 여 만든 레코드 집합에 적용 됩니다.  
  
> [!NOTE]
>  필터링 된을 그 플래그를 적용 하면 수정할 **레코드 집합** 일괄 업데이트 모드의 결과 **레코드 집합** 의 키 필드 기반 필터링 하는 경우 비어는 키 필드 값에 단일 키 테이블을 수정 했습니다. 결과 **레코드 집합** -비어 있지 않은 경우 다음 중 하나에 됩니다.  
  
-   단일 키 테이블의 키가 아닌 필드를 기준으로 필터링  
  
-   다중 키 테이블의 모든 필드를 기준으로 필터링  
  
-   단일 키 테이블의 키가 아닌 필드에서 수정 되었습니다.  
  
-   다중 키 테이블의 모든 필드에서 수정 되었습니다.  
  
 다음 표에서 요약의 효과 **그** 필터링 및 수정 작업의 다양 한 조합에서 합니다. 왼쪽된 열에는 가능한 수정; 표시 단일 키 테이블의 키 필드 또는 다중 키 테이블의 키 필드 중 하나에 있는 아닌 필드에서 수정할 수 있습니다. 맨 위 행은 필터링 조건을;를 보여 줍니다. 필터링 기반 아닌 필드의 모든 다중 키 테이블의 키 필드 또는 단일 키 테이블의 키 필드입니다. 교차 셀의 결과 보여 줍니다: +의 해당 적용 **그** 비어 있지 않은 결과 **레코드 집합**;-빈 의미 **레코드 집합**합니다.  
  
||비 키|단일 키|여러 키|  
|-|--------------|----------------|-------------------|  
|**비 키**|+|+|+|  
|**단일 키**|+|-|해당 사항 없음|  
|**여러 키**|+|해당 사항 없음|+|  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [필터 및 RecordCount 속성 예제 (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
 [필터 및 RecordCount 속성 예제 (VC + +)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
 [Clear 메서드 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Optimize 속성-동적(ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)
