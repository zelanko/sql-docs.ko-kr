---
title: RecordCount 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::RecordCount
- Recordset15::GetRecordCount
- Recordset15::get_RecordCount
helpviewer_keywords:
- RecordCount property [ADO]
ms.assetid: 834f0121-394a-44d4-ad7d-999b43a6fe63
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7304062298a95406a223ba58026379a3bebf392f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931474"
---
# <a name="recordcount-property-ado"></a>RecordCount 속성(ADO)

레코드 수가 표시를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.
  
## <a name="return-value"></a>반환 값

반환을 **긴** 의 레코드 수를 나타내는 값을 **레코드 집합**합니다.
  
## <a name="remarks"></a>설명

사용 합니다 **RecordCount** 속성을 레코드 수에 **레코드 집합** 개체입니다. 속성 공급자 또는 커서 유형을 지원 하지 않는 경우 또는 ADO 레코드의 수를 확인할 수 없는 경우-1을 반환 **RecordCount**합니다. 읽기를 **RecordCount** 속성에 닫힌 **레코드 집합** 오류가 발생 합니다.

#### <a name="bookmarks-or-approximate-positioning"></a>책갈피 또는 대략적인 위치

경우 레코드 집합 개체 *않습니다* 두 책갈피를 지원 하거나 예상 된 위치 지정이 속성을 반환 레코드의 정확한 수를 레코드 집합의 합니다. 이 속성에 있는지 여부를 레코드 집합 완전히 채워지면에 관계 없이 정확한 수를 반환 합니다.

반대로, 레코드 집합 개체의 역할이 *되지* 책갈피 또는 대략적인 위치를 지 원하는,이 속성에 액세스 하면 리소스가 많이 소모 될 수 있습니다. 드레이닝 모든 레코드가 검색 해야 하 고 정확 하 게 RecordCount 값을 반환할 계산 때문에 발생 합니다.

- **adBookmark** 책갈피와 관련이 있습니다.
- **adApproxPosition** 대략적인 위치와 관련이 있습니다.

> [!NOTE]
> ADO 버전 2.8 및 이전 버전에서는 SQLOLEDB 공급자 인출 모든 레코드를 반환 하는 경우에도 서버 쪽 커서를 사용 하면 **True** 둘 다에 대해 **지원 (adApproxPosition)** 고**지원 (adBookmark)** 합니다.
  
커서 유형의 합니다 **레코드 집합** 개체 레코드의 수를 확인할 수 있는지 여부에 영향을 줍니다. 합니다 **RecordCount** 속성은-1을 정방향 전용 커서, 정적 실제 또는 키 집합 커서 및-1 또는 데이터 원본에 따라 동적 커서에 대 한 실제 수를 반환 합니다.
  
## <a name="applies-to"></a>적용 대상

[레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목

[Filter 및 RecordCount 속성 예제 (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
[Filter 및 RecordCount 속성 예제 (VC + +)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
[AbsolutePosition 속성 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
[PageCount 속성(ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
