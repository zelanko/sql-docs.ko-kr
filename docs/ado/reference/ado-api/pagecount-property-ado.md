---
description: PageCount 속성(ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: aa050f7e99115ca13bf8871378ffa21b1f326d94
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773542"
---
# <a name="pagecount-property-ado"></a>PageCount 속성(ADO)
[레코드 집합](./recordset-object-ado.md) 개체가 포함 하는 데이터 페이지 수를 나타냅니다.  
  
## <a name="return-value"></a>반환 값  
 **레코드 집합**의 페이지 수를 나타내는 **Long** 값을 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **PageCount** 속성을 사용 하 여 **레코드 집합** 개체에 있는 데이터 페이지 수를 확인 합니다. *페이지* 는 크기가 [PageSize](./pagesize-property-ado.md) 속성 설정과 같은 레코드의 그룹입니다. **PageSize** 값 보다 레코드 수가 적기 때문에 마지막 페이지가 불완전 한 경우에도 **PageCount** 값에서 추가 페이지로 계산 됩니다. **레코드 집합** 개체가이 속성을 지원 하지 않는 경우이 값은 **PageCount** 을 확인할 수 없음을 나타내는-1입니다.  
  
 페이지 기능에 대 한 자세한 내용은 **PageSize** 및 [AbsolutePage](./absolutepage-property-ado.md) 속성을 참조 하세요.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [AbsolutePage, PageCount 및 PageSize 속성 예제 (VB)](./absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage, PageCount 및 PageSize 속성 예제 (VC + +)](./absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePage 속성 (ADO)](./absolutepage-property-ado.md)   
 [PageSize 속성 (ADO)](./pagesize-property-ado.md)   
 [RecordCount 속성(ADO)](./recordcount-property-ado.md)