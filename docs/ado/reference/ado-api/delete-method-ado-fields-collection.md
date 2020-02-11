---
title: Delete 메서드 (ADO Fields Collection) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Fields20::Delete
- Fields20::raw_Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 25bedc25-c51c-4cab-96ce-930b959965d9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9db49905b6548e5cb21cca976683c8b387017d32
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67919128"
---
# <a name="delete-method-ado-fields-collection"></a>Delete 메서드(ADO 필드 컬렉션)
[Fields](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션에서 개체를 삭제 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Fields.Delete Field  
```  
  
#### <a name="parameters"></a>매개 변수  
 *필드*  
 삭제할 [필드](../../../ado/reference/ado-api/field-object.md) 개체를 지정 하는 **Variant** 입니다. 이 매개 변수는 **필드 개체의** 이름 또는 **field** 개체 자체의 서 수 위치 일 수 있습니다.  
  
## <a name="remarks"></a>설명  
 열려 있는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 에서 **Fields. Delete** 메서드를 호출 하면 런타임 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Fields 컬렉션(ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Delete 메서드 (ADO Parameters Collection)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [DeleteRecord 메서드(ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
