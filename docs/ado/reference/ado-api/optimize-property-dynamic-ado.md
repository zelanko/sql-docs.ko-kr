---
title: "동적 속성 (ADO)를 최적화 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Optimize property [ADO]
ms.assetid: a491c4ce-2b04-4c84-be83-3846bde8d16b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4aeae41d865e585c4c8b93c86bd6f8e9753eaea1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="optimize-property-dynamic-ado"></a>동적 속성 (ADO)를 최적화 합니다.
인덱스를 만들지 여부를 지정 된 [필드](../../../ado/reference/ado-api/field-object.md)합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **부울** 인덱스를 만들 수 있는지 여부를 나타내는 값입니다.  
  
## <a name="remarks"></a>주의  
 인덱스에는 찾거나 값이 정렬 하는 작업의 성능을 향상 시킬 수는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다. 인덱스는 ADO; 내부 명시적으로 액세스 하거나 응용 프로그램에서 사용할 수 없습니다.  
  
 필드에 인덱스를 만들려면 설정는 **최적화** 속성을 **True**합니다. 인덱스를 삭제 하려면이 속성을 설정 **False**합니다.  
  
 **최적화** 동적 속성에 추가 된 [필드](../../../ado/reference/ado-api/field-object.md) 개체 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션 때는 [앞](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성이**adUseClient**합니다.  
  
## <a name="usage"></a>사용법  
  
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
 [Field 개체](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>관련 항목:  
 [속성 예제 (VB)를 최적화 합니다.](../../../ado/reference/ado-api/optimize-property-example-vb.md)   
 [최적화 속성 예제 (VC + +)](../../../ado/reference/ado-api/optimize-property-example-vc.md)   
 [필터 속성](../../../ado/reference/ado-api/filter-property.md)   
 [Find 메서드 (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Sort 속성](../../../ado/reference/ado-api/sort-property.md)

