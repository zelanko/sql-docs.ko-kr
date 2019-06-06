---
title: PageCount 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::PageCount
helpviewer_keywords:
- PageCount property [ADO]
ms.assetid: b601b56c-0ac4-44ee-bc91-c3d2d104f00a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5187c73d4dde95a5ddd9396da95b2d4381c868c8
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66706932"
---
# <a name="pagecount-property-ado"></a>PageCount 속성(ADO)
데이터 페이지 수를 나타냅니다 합니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체를 포함 합니다.  
  
## <a name="return-value"></a>반환 값  
 반환을 **긴** 의 페이지 수를 나타내는 값을 **레코드 집합**합니다.  
  
## <a name="remarks"></a>Remarks  
 사용 합니다 **PageCount** 속성에서 데이터 페이지 수를 결정 합니다 **레코드 집합** 개체입니다. *페이지* 레코드 같은 크기의 그룹이 합니다 [PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) 속성을 설정 합니다. 보다 적은 레코드가 있기 때문에 마지막 페이지 완료 되지 않더라도 **PageSize** 에서 추가 페이지로 계산 값을 **PageCount** 값입니다. 경우는 **레코드 집합** 개체가이 속성을 지원 하지 않습니다, 값을 나타내는-1은 합니다 **PageCount** 확인할 아닙니다.  
  
 참조를 **PageSize** 하 고 [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) 에 더 많은 페이지 기능에 대 한 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [AbsolutePage, PageCount, PageSize 속성 예제 (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage, PageCount, PageSize 속성 예제 (VC + +)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePage 속성 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [PageSize 속성 (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)   
 [RecordCount 속성(ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
