---
description: Optimize 속성-동적(ADO)
title: Optimize 속성-동적 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Optimize property [ADO]
ms.assetid: a491c4ce-2b04-4c84-be83-3846bde8d16b
author: rothja
ms.author: jroth
ms.openlocfilehash: 91da30a49a0eff7d8b32274e8486002f78f2a05f
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773642"
---
# <a name="optimize-property-dynamic-ado"></a>Optimize 속성-동적(ADO)
[필드](./field-object.md)에 인덱스를 만들지 여부를 지정 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 인덱스를 만들어야 하는지 여부를 나타내는 **부울** 값을 설정 하거나 반환 합니다.  
  
## <a name="remarks"></a>설명  
 인덱스는 [레코드 집합](./recordset-object-ado.md)에서 값을 찾거나 정렬 하는 작업의 성능을 향상 시킬 수 있습니다. 인덱스는 ADO 내부에 있습니다. 응용 프로그램에서 명시적으로 액세스 하거나 사용할 수 없습니다.  
  
 필드에 인덱스를 만들려면 **Optimize** 속성을 **True**로 설정 합니다. 인덱스를 삭제 하려면이 속성을 **False**로 설정 합니다.  
  
 **Optimize** 는 [CursorLocation](./cursorlocation-property-ado.md) 속성이 **AdUseClient**로 설정 된 경우 [Field](./field-object.md) object [Properties](./properties-collection-ado.md) 컬렉션에 추가 되는 동적 속성입니다.  
  
## <a name="usage"></a>사용  
  
```  
Dim rs As New Recordset  
Dim fld As Field  
rs.CursorLocation = adUseClient      'Enable index creation  
rs.Fields.Append "Field1", adChar, 35, adFldIsNullable  
rs.Open  
Set fld = rs.Fields(0)  
fld.Properties("Optimize") = True    'Create an index  
fld.Properties("Optimize") = False   'Delete an index  
```  
  
## <a name="applies-to"></a>적용 대상  
 [Field 개체](./field-object.md)  
  
## <a name="see-also"></a>참고 항목  
 [Optimize 속성 예제 (VB)](./optimize-property-example-vb.md)   
 [Optimize 속성 예제 (VC + +)](./optimize-property-example-vc.md)   
 [필터 속성](./filter-property.md)   
 [Find 메서드 (ADO)](./find-method-ado.md)   
 [Sort 속성](./sort-property.md)