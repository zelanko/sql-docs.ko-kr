---
title: "Status 속성 (ADO 필드) | Microsoft Docs"
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
f1_keywords:
- Field::Status
- Field::get_Status
- Field::GetStatus
helpviewer_keywords:
- Status property [ADO Field]
ms.assetid: 8cd1f7f4-0a3a-4f07-b8ba-6582e70140ad
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 65acf492f0364b26fa6a12240fbbd49c7d1dfed3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="status-property-ado-field"></a>Status 속성 (ADO 필드)
상태를 표시 한 [필드](../../../ado/reference/ado-api/field-object.md) 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 반환 된 [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md) 값입니다. 기본값은 **adFieldOK**합니다.  
  
## <a name="remarks"></a>주의  
  
## <a name="record-field-status"></a>레코드 필드 상태  
 값으로 변경 한 **필드** 의 필드 컬렉션의 개체는 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체는 개체의 될 때까지 캐시 됩니다 [업데이트](../../../ado/reference/ado-api/update-method.md) 메서드를 호출 합니다. 해당 시점에 오류가 발생 하는 필드의 값을 변경, OLE DB 오류가 발생 **DB_E_ERRORSOCCURRED** (2147749409). Status 속성 중 아무 메서드나는 **필드** 개체에 **필드** 오류의 원인이 된 컬렉션에서 값이 포함 됩니다는 [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md) 의 원인을 설명 하는 문제가 있습니다.  
  
 성능, 추가 및 삭제를 향상 시키기 위해는 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션의는 **레코드** 개체 될 때까지 캐시 됩니다는 **업데이트** 메서드를 호출 하 고 변경 내용을 다음 낙관적 일괄 업데이트에서 이루어집니다. 경우는 **업데이트** 메서드는, 서버가 업데이트 되지 않습니다. OLE DB 공급자 (DB_E_ERRORSOCCURRED) 오류가 반환 되 고 업데이트가 실패할 경우와 **상태** 속성은 작업 및 오류 상태 코드의 결합된 된 값을 나타냅니다. 예를 들어 **adFieldPendingInsert OR adFieldPermissionDenied**합니다. **상태** 각 속성이 **필드** 는 이유를 확인 하는 데 사용할 수는 **필드** 되지 추가, 수정 되었거나 삭제 합니다.  
  
 여러 유형의 수정 또는 삭제 되지 않도록 문제를 추가할 때 발생 한 **필드** 통해 보고 됩니다는 **상태** 속성입니다. 예를 들어, 사용자를 삭제 하는 경우는 **필드**에서 삭제 되도록 표시 되는 **필드** 컬렉션입니다. 경우 후속 **업데이트** 사용자가을 삭제 하려고 하기 때문에 오류를 반환 합니다.는 **필드** 를 갖지 않습니다 권한는 **필드** 갖습니다는  **상태** 의 **adFieldPermissionDenied OR adFieldPendingDelete**합니다. 호출의 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 메서드 복원 원래 값과 설정에서 **상태** 를 **adFieldOK**합니다.  
  
 마찬가지로,는 **업데이트** 반환 될 수 있으며 오류가 발생 하기 때문에 새 **필드** 가 추가 되 고 잘못 된 값을 지정 합니다. 있는 경우에 새 **필드** 에 포함 됩니다는 **필드** 컬렉션의 상태 및 **adFieldPendingInsert** 용도나 **adFieldCantCreate** (공급자에 따라). 새 항목에 대 한 적절 한 값을 제공할 수 있습니다 **필드** 호출 **업데이트** 다시 합니다.  
  
## <a name="recordset-field-status"></a>레코드 집합 필드의 상태  
 값으로 변경는 **필드** 의 필드 컬렉션의에서 개체는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체의 될 때까지 캐시 [업데이트](../../../ado/reference/ado-api/update-method.md) 메서드를 호출 합니다. 해당 시점에 오류가 발생 하는 필드의 값을 변경, OLE DB 오류가 발생 **DB_E_ERRORSOCCURRED** (2147749409). Status 속성 중 아무 메서드나는 **필드** 개체에 **필드** 오류의 원인이 된 컬렉션에서 값이 포함 됩니다는 [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md) 의 원인을 설명 하는 문제가 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Field 개체](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>관련 항목:  
 [상태 속성 예제 (필드) (VB)](../../../ado/reference/ado-api/status-property-example-field-vb.md)   
 [Status 속성 예제(VC++)](../../../ado/reference/ado-api/status-property-example-vc.md)   

