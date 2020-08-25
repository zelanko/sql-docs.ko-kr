---
description: RecordCount 속성(ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b307a4116731016858ce4cc74f37bdcfbd258f3a
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88772482"
---
# <a name="recordcount-property-ado"></a>RecordCount 속성(ADO)

레코드 [집합](./recordset-object-ado.md) 개체의 레코드 수를 나타냅니다.
  
## <a name="return-value"></a>반환 값

레코드 **집합**의 레코드 수를 나타내는 **Long** 값을 반환 합니다.
  
## <a name="remarks"></a>설명

**RecordCount** 속성을 사용 하 여 레코드 **집합** 개체에 있는 레코드 수를 확인 합니다. ADO에서 레코드 수를 확인할 수 없거나 공급자나 커서 유형이 **RecordCount**를 지원 하지 않는 경우 속성은-1을 반환 합니다. 닫힌 **레코드 집합** 에서 **RecordCount** 속성을 읽으면 오류가 발생 합니다.

#### <a name="bookmarks-or-approximate-positioning"></a>책갈피 또는 대략적인 위치

레코드 *집합 개체가 책갈피* 또는 대략적인 위치를 지 원하는 경우이 속성은 레코드 집합의 정확한 레코드 수를 반환 합니다. 이 속성은 레코드 집합의 전체 채우기 여부와 관계 없이 정확한 수를 반환 합니다.

이와 대조적으로 레코드 집합 개체가 책갈피 또는 대략적인 위치를 지원 *하지* 않는 경우이 속성에 액세스 하면 리소스에서 상당한 드레이닝이 발생할 수 있습니다. 모든 레코드를 검색 하 여 정확한 RecordCount 값을 반환 하기 위해 계산 해야 하므로 드레이닝이 발생 합니다.

- 책갈피와 관련 된 **Adbookmark** 입니다.
- **Adapproxposition** 은 대략적인 위치와 관련이 있습니다.

> [!NOTE]
> ADO 버전 2.8 및 이전 버전에서 SQLOLEDB 공급자는 서버 쪽 커서를 사용 하는 경우 **(adApproxPosition)** 와 **지원 (adbookmark)** 모두에 대해 **True** 를 반환 한다는 사실에도 불구 하 고 모든 레코드를 인출 합니다.
  
레코드 **집합** 개체의 커서 유형은 레코드 수를 확인할 수 있는지 여부에 영향을 줍니다. **RecordCount** 속성은 앞 으로만 이동 가능한 커서에 대해-1을 반환 합니다. 정적 또는 키 집합 커서의 실제 개수입니다. 데이터 원본에 따라-1 또는 동적 커서의 실제 개수입니다.
  
## <a name="applies-to"></a>적용 대상

[레코드 집합 개체(ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목

[Filter 및 RecordCount 속성 예제 (VB)](./filter-and-recordcount-properties-example-vb.md)   
[Filter 및 RecordCount 속성 예제 (VC + +)](./filter-and-recordcount-properties-example-vc.md)   
[AbsolutePosition 속성 (ADO)](./absoluteposition-property-ado.md)   
[PageCount 속성(ADO)](./pagecount-property-ado.md)