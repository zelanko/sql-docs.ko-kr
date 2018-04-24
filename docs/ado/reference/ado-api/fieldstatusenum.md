---
title: FieldStatusEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldStatusEnum
helpviewer_keywords:
- FieldStatusEnum enumeration [ADO]
ms.assetid: e06da1e2-303f-41b2-a3b0-61e233da152c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4f0ff45d215ea7e4165bf12c0cd69a5ebc69860a
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="fieldstatusenum"></a>FieldStatusEnum
지정 된 [상태](../../../ado/reference/ado-api/status-property-ado-field.md) 의 [Field 개체](../../../ado/reference/ado-api/field-object.md)합니다.  
  
 **adFieldPending\***  값 나타냅니다 작업을 설정할 수 상태 발생 한 다른 상태 값과 결합 될 수 있습니다.  
  
|상수|Value|Description|  
|--------------|-----------|-----------------|  
|**adFieldAlreadyExists**|26|지정된 된 필드 이미 있음을 나타냅니다.|  
|**adFieldBadStatus**|12|잘못 된 상태 값 보냈음을 ADO에서 OLE DB 공급자를 나타냅니다. OLE DB 1.0 또는 1.1 공급자 또는의 잘못 된 조합이 원인일 [값](../../../ado/reference/ado-api/value-property-ado.md) 및 [상태](../../../ado/reference/ado-api/status-property-ado-field.md)합니다.|  
|**adFieldCannotComplete**|20|지정 하는 URL의 서버 [소스](../../../ado/reference/ado-api/source-property-ado-record.md) 작업을 완료할 수 없습니다.|  
|**adFieldCannotDeleteSource**|23|새 위치로 이동 된 트리 또는 하위 트리 이동 작업 중 소스를 삭제할 수 없습니다 되지만 나타냅니다.|  
|**adFieldCantConvertValue**|2|필드 검색 하거나 데이터의 손실 없이 저장할 수 없습니다 나타냅니다.|  
|**adFieldCantCreate**|7|공급자 (예: 허용 된 필드 수) 제한을 초과 하기 때문에 필드 추가 하지 못했습니다 나타냅니다.|  
|**adFieldDataOverflow**|6|공급자에서 반환 되는 데이터 필드의 데이터 형식을 오버플로 있는지를 나타냅니다.|  
|**adFieldDefault**|13|데이터를 설정할 때 필드에 대 한 기본값 사용 되었음을 나타냅니다.|  
|**adFieldDoesNotExist**|16|지정 된 필드 없다는 것을 나타냅니다.|  
|**adFieldIgnore**|15|설정 데이터 소스에 값이 될 때이 필드를 건너뛰었음을 나타냅니다. 공급자 설정 값이 없습니다.|  
|**adFieldIntegrityViolation**|10|필드는 계산 된 또는 파생 된 엔터티 이기 때문에 수정 될 수 없음을 나타냅니다.|  
|**adFieldInvalidURL**|17|데이터 소스 URL에 잘못 된 문자가 포함 되어 있음을 나타냅니다.|  
|**adFieldIsNull**|3|공급자가 VT_NULL 유형의 VARIANT 값을 반환 하는 필드가 비어 있지 않으면 나타냅니다.|  
|**adFieldOK**|0|기본. 필드를 추가 되거나 삭제 되었음을 나타냅니다.|  
|**adFieldOutOfSpace**|22|공급자가 충분 한 저장 공간 완료 이동 또는 복사 작업을 가져올 수 있는지를 나타냅니다.|  
|**adFieldPendingChange**|0x40000|하나를 의미할 수 필드는 삭제 되었으며 다시 추가 아마도 다른 데이터 형식으로 또는 이전 상태에 있는 필드의 값의 **adFieldOK** 변경 되었습니다. 필드의 최종 형식을 수정 하는 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 후 컬렉션의 [업데이트](../../../ado/reference/ado-api/update-method.md) 메서드를 호출 합니다.|  
|**adFieldPendingDelete**|0x20000|나타냅니다는 **삭제** 작업으로 인해 상태가 설정 됩니다. 필드에서 삭제 되도록 표시 되었습니다는 **필드** 후 컬렉션의 **업데이트** 메서드를 호출 합니다.|  
|**adFieldPendingInsert**|0x10000|나타냅니다는 **Append** 작업으로 인해 상태가 설정 됩니다. **필드** 에 추가할 수를 표시 하는 **필드** 후 컬렉션의 **업데이트** 메서드를 호출 합니다.|  
|**adFieldPendingUnknown**|0x80000|공급자를 설정할 수 있는 작업으로 인해 필드 상태를 확인할 수 없음을 나타냅니다.|  
|**adFieldPendingUnknownDelete**|0x100000|필드의 상태를 설정할 수 및에서 필드를 삭제할 수는 어떤 작업으로 인해 공급자 확인할 수 없음을 나타냅니다는 **필드** 후 컬렉션의 **업데이트** 메서드를 호출 합니다.|  
|**adFieldPermissionDenied**|9|읽기 전용으로 정의 되어 있으므로 필드 수정 될 수 없음을 나타냅니다.|  
|**adFieldReadOnly**|24|데이터 원본의 필드는 읽기 전용으로 정의 되어 있는지를 나타냅니다.|  
|**adFieldResourceExists**|19|공급자가 대상 URL에 개체가 이미 개체를 덮어쓸 수 없기 때문에 작업을 수행할 수 없음을 나타냅니다.|  
|**adFieldResourceLocked**|18|공급자 데이터 원본 하나 이상의 다른 응용 프로그램 또는 프로세스에 의해 잠겨 있기 때문에 작업을 수행할 수 없음을 나타냅니다.|  
|**adFieldResourceOutOfScope**|25|현재 레코드의 범위를 벗어나는 원본 또는 대상 URL 임을 나타냅니다.|  
|**adFieldSchemaViolation**|11|값 필드에 대 한 데이터 원본 스키마 제약 조건을 위반 했음을 나타냅니다.|  
|**adFieldSignMismatch**|5|공급자에서 반환 된 데이터 값은 부호가 되지만 ADO 필드 값의 데이터 유형은 부호가 없기 나타냅니다.|  
|**adFieldTruncated**|4|가변 길이 데이터가 잘렸음을 데이터 원본에서에서 읽을 때를 나타냅니다.|  
|**adFieldUnavailable**|8|공급자 데이터 원본에서 읽는 값 확인 하지 못했습니다 나타냅니다. 예를 들어 행 방금 만든, 열에 대 한 기본값을 사용할 수 없습니다. 및 새 값을 아직 지정 하지 했습니다.|  
|**adFieldVolumeNotFound**|21|공급자는 URL에서 표시 하는 저장소 볼륨을 찾을 수 임을 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 이러한 상수는 ADO/wfc 필요가 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Status 속성(ADO 필드)](../../../ado/reference/ado-api/status-property-ado-field.md)
