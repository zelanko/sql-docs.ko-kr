---
title: Sort 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::get_Sort
- Recordset15::put_Sort
- Recordset15::PutSort
- Recordset15::GetSort
- Recordset15::Sort
helpviewer_keywords:
- DESC [ADO]
- ASC [ADO]
- Sort property [ADO]
ms.assetid: 3683ffa0-6f93-4906-9533-ef6942f24f39
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 946314f7be9f6c39d47a3f26b577e10834064dab
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67930940"
---
# <a name="sort-property"></a>Sort 속성
[레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 을 정렬 하는 하나 이상의 필드 이름과 각 필드가 오름차순으로 정렬 되는지 또는 내림차순으로 정렬 되는지 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 정렬할 **레코드 집합** 의 필드 이름을 나타내는 **문자열** 값을 설정 하거나 반환 합니다. 각 이름은 쉼표로 구분 되며, 선택적으로 공백 및 오름차순으로 필드를 정렬 하는 ASC, 오름차순으로 필드를 **정렬 하는**ASC 키워드 ( **ASC**)를 차례로 입력 합니다. 기본적으로 키워드가 지정 되지 않은 경우 필드는 오름차순으로 정렬 됩니다.  
  
## <a name="remarks"></a>설명  
 이 속성을 사용 하려면 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient**로 설정 해야 합니다. 인덱스가 아직 없는 경우 **Sort** 속성에 지정 된 각 필드에 대해 임시 인덱스가 생성 됩니다.  
  
 데이터는 물리적으로 다시 정렬 되지 않지만 단순히 인덱스에 지정 된 순서로 액세스 되기 때문에 정렬 작업은 효율적입니다.  
  
 **Sort** 속성의 값이 빈 문자열이 아닌 경우에는 **Sort** 속성 순서가 **레코드 집합**을 여는 데 사용 되는 SQL 문에 포함 된 **order by** 절에 지정 된 순서 보다 우선적으로 적용 됩니다.  
  
 **Sort** 속성에 액세스 하기 전에 **레코드 집합** 을 열 필요가 없습니다. **레코드 집합** 개체가 인스턴스화된 후 언제 든 지 설정할 수 있습니다.  
  
 **Sort** 속성을 빈 문자열로 설정 하면 행을 원래 순서로 다시 설정 하 고 임시 인덱스를 삭제 합니다. 기존 인덱스는 삭제 되지 않습니다.  
  
 **레코드 집합** 에 *firstName*, *middleInitial*및 *lastName*이라는 세 개의 필드가 있다고 가정 합니다. **Sort** 속성을 문자열 "`lastName DESC, firstName ASC`"로 설정 합니다 .이 문자열은 성을 기준으로 내림차순으로 정렬 한 다음 **이름을 기준으로** 오름차순으로 정렬 합니다. 중간 이니셜은 무시 됩니다.  
  
 이름이 **asc** 및 **DESC**와 충돌 하므로 필드 이름을 "ASC" 또는 "DESC"로 지정할 수 없습니다. **레코드 집합**을 반환 하는 쿼리에서 **AS** 키워드를 사용 하 여 이름이 충돌 하는 필드에 대 한 별칭을 만들 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Sort 속성 예제 (VB)](../../../ado/reference/ado-api/sort-property-example-vb.md)   
 [Sort 속성 예제 (VC + +)](../../../ado/reference/ado-api/sort-property-example-vc.md)   
 [Optimize 속성-동적 (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [SortColumn 속성 (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [SortDirection 속성(RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)
