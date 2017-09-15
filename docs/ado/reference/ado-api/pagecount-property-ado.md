---
title: "PageCount 속성 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::PageCount
helpviewer_keywords:
- PageCount property [ADO]
ms.assetid: b601b56c-0ac4-44ee-bc91-c3d2d104f00a
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 44759f9316e46be72120febd022f9a47554eb6bd
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="pagecount-property-ado"></a>PageCount 속성 (ADO)
데이터 페이지 수를 나타냅니다는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체에 포함 되어 있습니다.  
  
## <a name="return-value"></a>반환 값  
 반환 된 **긴** 의 페이지 수를 나타내는 값의 **레코드 집합**합니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **PageCount** 속성에 있는 데이터 페이지 수를 확인 하 고 **레코드 집합** 개체입니다. *페이지* 같은 크기의 레코드의 그룹은 [PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) 속성을 설정 합니다. 보다 적은 수의 레코드가 있기 때문에 마지막 페이지가 완료 되는 경우에는 **PageSize** 에서 추가 페이지로 계산 값은 **PageCount** 값입니다. 경우는 **레코드 집합** 개체가이 속성을 지원 하지 않습니다, 값이 표시 되는 됩니다는 **PageCount** 결정할 수 있는있지 않습니다.  
  
 참조는 **PageSize** 및 [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) 에 더 많은 페이지 기능에 대 한 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [AbsolutePage, PageCount, 및 PageSize 속성 예제 (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage, PageCount, 및 PageSize 속성 예제 (VC + +)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePage 속성 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [PageSize 속성 (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)   
 [RecordCount 속성(ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)

