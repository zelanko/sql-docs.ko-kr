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
ms.openlocfilehash: d90eff53ef998a009aecd4d82fc3b502a487c01d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67930831"
---
# <a name="status-property-ado-field"></a>Status 속성(ADO 필드)
[필드](../../../ado/reference/ado-api/field-object.md) 개체의 상태를 나타냅니다.  
  
## <a name="return-value"></a>Return Value  
 [Fieldstatusenum](../../../ado/reference/ado-api/fieldstatusenum.md) 값을 반환 합니다. 기본값은 **adFieldOK**입니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="record-field-status"></a>레코드 필드 상태  
 [Record](../../../ado/reference/ado-api/record-object-ado.md) 개체의 Fields 컬렉션에 있는 **Field** 개체의 값에 대 한 변경 내용은 개체의 [Update](../../../ado/reference/ado-api/update-method.md) 메서드를 호출할 때까지 캐시 됩니다. 이 시점에서 필드 값을 변경 하 여 오류가 발생 하면 OLE DB **DB_E_ERRORSOCCURRED** (2147749409) 오류가 발생 합니다. **필드** 컬렉션에서 오류를 발생 시킨 **Field** 개체의 Status 속성에는 문제의 원인을 설명 하는 [fieldstatusenum](../../../ado/reference/ado-api/fieldstatusenum.md) 의 값이 포함 됩니다.  
  
 성능 향상을 위해 **Record** 개체의 [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션에 대 한 추가 및 삭제는 **Update** 메서드가 호출 될 때까지 캐시 된 다음 일괄 낙관적 업데이트에서 변경 됩니다. **Update** 메서드를 호출 하지 않으면 서버가 업데이트 되지 않습니다. 업데이트가 실패 하면 OLE DB 공급자 오류 (DB_E_ERRORSOCCURRED)가 반환 되 고 **Status** 속성은 작업 및 오류 상태 코드의 결합 된 값을 나타냅니다. 예를 들어 **Adfieldpendinginsert 또는 Adfield는 거부**됩니다. 각 **필드** 의 **Status** 속성은 **필드가** 추가, 수정 또는 삭제 되지 않은 이유를 확인 하는 데 사용할 수 있습니다.  
  
 **필드** 를 추가, 수정 또는 삭제할 때 발생 하는 많은 유형의 문제는 **Status** 속성을 통해 보고 됩니다. 예를 들어 사용자가 **필드**를 삭제 **하는 경우 필드 컬렉션에서** 삭제 되도록 표시 됩니다. 사용자가 권한이 없는 **필드** 를 삭제 하려고 했기 때문에 후속 **업데이트** 에서 오류를 반환 하는 경우이 **필드** 의 **상태** 는 **adfield사용 거부 또는 adfieldpendingdelete**입니다. [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 메서드를 호출 하면 원래 값이 복원 되 **** 고 상태가 **adFieldOK**로 설정 됩니다.  
  
 마찬가지로 새 **필드가** 추가 되 고 잘못 된 값이 지정 되었으므로 **업데이트** 메서드에서 오류를 반환할 수 있습니다. 이 경우 새 **필드** 는 **Fields** 컬렉션에 있고 공급자에 따라 **Adfieldpendinginsert** 및 **adFieldCantCreate** 의 상태가 됩니다. 새 **필드** 에 적절 한 값을 제공 하 고 **Update** 를 다시 호출할 수 있습니다.  
  
## <a name="recordset-field-status"></a>레코드 집합 필드 상태  
 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 의 Fields 컬렉션에 있는 **Field** 개체의 값에 대 한 변경 내용은 개체의 [Update](../../../ado/reference/ado-api/update-method.md) 메서드를 호출할 때까지 캐시 됩니다. 이 시점에서 필드 값을 변경 하 여 오류가 발생 하면 OLE DB **DB_E_ERRORSOCCURRED** (2147749409) 오류가 발생 합니다. **필드** 컬렉션에서 오류를 발생 시킨 **Field** 개체의 Status 속성에는 문제의 원인을 설명 하는 [fieldstatusenum](../../../ado/reference/ado-api/fieldstatusenum.md) 의 값이 포함 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Field 개체](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>참고 항목  
 [Status 속성 예제 (필드) (VB)](../../../ado/reference/ado-api/status-property-example-field-vb.md)   
 [Status 속성 예제(VC++)](../../../ado/reference/ado-api/status-property-example-vc.md)   
