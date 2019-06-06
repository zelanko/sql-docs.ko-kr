---
title: 정렬 속성 | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 092eb49216874a59e4bcba09431fcc01dc3679a4
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711152"
---
# <a name="sort-property"></a>Sort 속성
하나 이상의 필드 이름을 나타냅니다 합니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 정렬 되어 각 필드를 오름차순 또는 내림차순으로 정렬 되는지 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환을 **문자열** 이름 필드를 나타내는 값을 **레코드 집합** 정렬할 합니다. 각 이름에 쉼표를 분리 되 고 필요에 따라 뒤에 빈 값 및 키워드 **ASC**를 오름차순으로 필드를 정렬 하는 또는 **DESC**, 필드를 내림차순으로 정렬 하는 합니다. 기본적으로 키워드를 지정 하지, 필드 오름차순 정렬 됩니다.  
  
## <a name="remarks"></a>Remarks  
 이 속성을 입력 해야 합니다 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 설정할 **adUseClient**합니다. 에 지정 된 각 필드에 대 한 임시 인덱스가 생성 됩니다는 **정렬** 속성 인덱스 아직 없는 경우.  
  
 정렬 작업을 효율적으로 데이터 실제로 다시 정렬 하지 않지만 인덱스로 지정 된 순서 대로 액세스 하기만 하면 됩니다.  
  
 때의 값을 **정렬** 속성이 빈 문자열인 경우 이외의 **정렬** 순서 속성에서 지정 된 순서 보다 우선는 **ORDER BY** 절 여는 데 사용 된 SQL 문에 포함 된 **레코드 집합**합니다.  
  
 **레코드 집합** 에 액세스 하기 전에 열 수 없는 합니다 **정렬** 속성 후 언제 든 지 설정할 수 있습니다는 **레코드 집합** 개체를 인스턴스화할 합니다.  
  
 설정 된 **정렬** 속성을 빈 문자열은 원래 순서 대로 행 다시 설정 하 고 임시 인덱스를 삭제 합니다. 기존 인덱스를 삭제 되지 않습니다.  
  
 가정를 **Recordset** 라는 세 개의 필드가 있습니다 *firstName*, *middleInitial*, 및 *lastName*. 설정 합니다 **정렬** 속성 문자열을 "`lastName DESC, firstName ASC`", 순서는 **레코드 집합** 내림차순으로 성을 기준으로 다음 오름차순 성을 합니다. 중간 이니셜이 무시 됩니다.  
  
 필드가 없으면 이름을 지정할 수 있습니다 "ASC" 또는 "DESC" 키워드를 사용 하 여 명명할 **ASC** 하 고 **DESC**합니다. 사용 하 여 이름이 충돌 하는 필드에 대 한 별칭을 만들 수 있습니다 합니다 **AS** 쿼리에서 반환 하는 키워드는 **레코드 집합**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Sort 속성 예제 (VB)](../../../ado/reference/ado-api/sort-property-example-vb.md)   
 [Sort 속성 예제 (VC + +)](../../../ado/reference/ado-api/sort-property-example-vc.md)   
 [Optimize 속성-동적 (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [SortColumn 속성 (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [SortDirection 속성(RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)
