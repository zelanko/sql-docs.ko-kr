---
title: "정렬 속성 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fc2498f80dfc5a057eff9350ed1949ee02ee5f4f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sort-property"></a>정렬 속성
에 있는 하나 이상의 필드 이름 나타냅니다는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 정렬 된 각 필드를 오름차순 또는 내림차순 정렬 되는지 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **문자열** 에서 이름을 필드를 나타내는 값의 **레코드 집합** 을 정렬할 합니다. 각 이름에 쉼표를 구분 하 고 필요에 따라 다음 빈와 키워드를 **ASC**, 필드를 오름차순으로 정렬 하 또는 **DESC**, 필드를 내림차순으로 정렬입니다. 기본적으로 없는 키워드가 지정 된 필드를 오름차순 정렬 됩니다.  
  
## <a name="remarks"></a>주의  
 이 속성에 필요는 [앞](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성에 설정할을 **adUseClient**합니다. 임시 인덱스에 지정 된 각 필드에 대해 생성 됩니다는 **정렬** 인덱스가 아직 없는 경우 속성을 사용 합니다.  
  
 데이터는 실제로 다시 정렬 되지 않습니다 되지만 인덱스로 지정 된 순서로 단순히 액세스 하는 정렬 작업이 효율적입니다.  
  
 때의 값은 **정렬** 속성은 빈 문자열이 면 이외의 **정렬** 속성 순서에 지정 된 순서 보다 우선는 **ORDER BY** 절 여는 데 사용 된 SQL 문에 포함 된 **레코드 집합**합니다.  
  
 **레코드 집합** 있어서는 안에 액세스 하기 전에 열 수는 **정렬** 속성 후 언제 든 지 설정할 수 있습니다는 **레코드 집합** 개체가 인스턴스화될 합니다.  
  
 설정의 **정렬** 속성을 빈 문자열로 원래 순서 행이 재설정 되 고 임시 인덱스를 삭제 합니다. 기존 인덱스를 삭제 되지 않습니다.  
  
 가정는 **레코드 집합** 라는 세 개의 필드가 포함 *firstName*, *middleInitial*, 및 *lastName*합니다. 설정의 **정렬** 속성 문자열을 "`lastName DESC, firstName ASC`", 정렬 됩니다는 **레코드 집합** 내림차순으로 성을 기준으로 다음 오름차순 이름 기준입니다. 중간 이니셜이 무시 됩니다.  
  
 이러한 이름은 키워드와 충돌 하기 때문에 "ASC" 또는 "DESC" 필드가 없습니다 라는 수 **ASC** 및 **DESC**합니다. 사용 하 여 이름이 충돌 하는 필드에 대 한 별칭을 만들 수 있습니다는 **AS** 키워드를 반환 하는 쿼리에서 **레코드 집합**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [정렬 속성 예제 (VB)](../../../ado/reference/ado-api/sort-property-example-vb.md)   
 [정렬 속성 예제 (VC + +)](../../../ado/reference/ado-api/sort-property-example-vc.md)   
 [동적 속성 (ADO)를 최적화 합니다.](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [SortColumn 속성 (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [SortDirection 속성(RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)
