---
title: Status 속성 (ADO 필드) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field::Status
- Field::get_Status
- Field::GetStatus
helpviewer_keywords:
- Status property [ADO Field]
ms.assetid: 8cd1f7f4-0a3a-4f07-b8ba-6582e70140ad
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a647051e7953d6f2977074feda94cf7e9f3d9d82
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711020"
---
# <a name="status-property-ado-field"></a>Status 속성(ADO 필드)
상태를 나타내는 [필드](../../../ado/reference/ado-api/field-object.md) 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 반환 된 [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md) 값입니다. 기본값은 **adFieldOK**합니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="record-field-status"></a>레코드 필드 상태  
 값으로 변경를 **필드** 의 필드 컬렉션의 개체를 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체는 개체의 될 때까지 캐시 됩니다 [업데이트](../../../ado/reference/ado-api/update-method.md) 메서드가 호출 됩니다. 이 시점에서 오류가 발생 하는 필드의 값으로 변경, OLE DB 오류 발생 **DB_E_ERRORSOCCURRED** (2147749409). 상태 속성을 **필드** 개체를 **필드** 오류를 발생 시키는 컬렉션에서 값이 포함 됩니다는 [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md) 원인을 설명 하는 문제가 발생 합니다.  
  
 성능, 추가 및 삭제를 향상 시키기 위해는 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션을 **레코드** 개체까지 캐시 됩니다는 **업데이트** 메서드를 호출 하 고 변경 내용을 다음 낙관적 일괄 업데이트에서 이루어집니다. 경우는 **업데이트** 메서드는, 서버 업데이트 되지 않습니다. OLE DB 공급자 오류 (DB_E_ERRORSOCCURRED)를 반환 하는 다음 업데이트가 실패할 경우와 **상태** 속성 작업 및 오류 상태 코드의 결합된 된 값을 나타냅니다. 예를 들어 **adFieldPendingInsert OR adFieldPermissionDenied**합니다. **상태** 각각에 대 한 속성 **필드** 이유를 확인 하려면 사용할 수는 **필드** 가 없는 추가, 수정 또는 삭제 합니다.  
  
 다양 한 유형의 수정 또는 삭제 되지 않도록 문제를 추가할 때 발생을 **필드** 를 통해 보고 되는 **상태** 속성. 예를 들어, 사용자를 삭제 하는 경우는 **필드**에서 삭제 하도록 표시 되어 있으므로 합니다 **필드** 컬렉션입니다. 경우 후속 **업데이트** 사용자를 삭제 하려고 하기 때문에 오류를 반환 합니다.는 **필드** 는 없는 권한이 **필드** 갖습니다는  **상태** 의 **adFieldPermissionDenied OR adFieldPendingDelete**합니다. 호출을 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 메서드 복원에 대 한 원래 값 집합과 합니다 **상태** 에 **adFieldOK**합니다.  
  
 마찬가지로, 합니다 **업데이트** 하므로 메서드는 오류를 반환할 수 있습니다 새 **필드** 가 추가 되 고 부적절 한 값을 지정 합니다. 하는 경우 새 **필드** 에 **필드** 컬렉션의 상태와 **adFieldPendingInsert** 용도나 **adFieldCantCreate** (공급자에 따라). 새 항목에 대 한 적절 한 값을 제공할 수 있습니다 **필드** 호출 **업데이트** 다시 합니다.  
  
## <a name="recordset-field-status"></a>레코드 집합 필드 상태  
 값으로 변경를 **필드** 의 필드 컬렉션의 개체를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체의 될 때까지 캐시 됩니다 [업데이트](../../../ado/reference/ado-api/update-method.md) 메서드가 호출 됩니다. 이 시점에서 오류가 발생 하는 필드의 값으로 변경, OLE DB 오류 발생 **DB_E_ERRORSOCCURRED** (2147749409). 상태 속성을 **필드** 개체를 **필드** 오류를 발생 시키는 컬렉션에서 값이 포함 됩니다는 [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md) 원인을 설명 하는 문제가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Field 개체](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>관련 항목  
 [Status 속성 예제 (필드) (VB)](../../../ado/reference/ado-api/status-property-example-field-vb.md)   
 [Status 속성 예제(VC++)](../../../ado/reference/ado-api/status-property-example-vc.md)   
