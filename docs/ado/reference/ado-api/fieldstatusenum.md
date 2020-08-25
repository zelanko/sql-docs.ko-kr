---
description: FieldStatusEnum
title: FieldStatusEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldStatusEnum
helpviewer_keywords:
- FieldStatusEnum enumeration [ADO]
ms.assetid: e06da1e2-303f-41b2-a3b0-61e233da152c
author: rothja
ms.author: jroth
ms.openlocfilehash: 21f3ebabab3096217348e2309070d81e90128b8e
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775332"
---
# <a name="fieldstatusenum"></a>FieldStatusEnum
[필드 개체](./field-object.md)의 [상태](./status-property-ado-field.md) 를 지정 합니다.  
  
 **Adfieldpending \* ** 값은 상태를 설정 하는 작업을 나타내며 다른 상태 값과 결합 될 수 있습니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adFieldAlreadyExists**|26|지정 된 필드가 이미 있음을 나타냅니다.|  
|**adFieldBadStatus**|12|잘못 된 상태 값이 ADO에서 OLE DB 공급자로 전송 되었음을 나타냅니다. OLE DB 1.0 또는 1.1 공급자 또는 잘못 된 [값](./value-property-ado.md) 과 [상태](./status-property-ado-field.md)조합이 포함 될 수 있습니다.|  
|**adFieldCannotComplete**|20|[원본](./source-property-ado-record.md) 으로 지정 된 URL의 서버에서 작업을 완료할 수 없음을 나타냅니다.|  
|**adFieldCannotDeleteSource**|23|이동 작업을 수행 하는 동안 트리 또는 하위 트리를 새 위치로 이동 했지만 원본을 삭제할 수 없음을 나타냅니다.|  
|**adFieldCantConvertValue**|2|필드를 데이터 손실 없이 검색 하거나 저장할 수 없음을 나타냅니다.|  
|**adFieldCantCreate**|7|공급자가 제한을 초과 하 여 필드를 추가할 수 없음을 나타냅니다 (예: 허용 되는 필드 수).|  
|**adFieldDataOverflow**|6|공급자에서 반환 된 데이터가 필드의 데이터 형식을 오버플로 했음을 나타냅니다.|  
|**adFieldDefault**|13|필드의 기본값이 데이터를 설정할 때 사용 되었음을 나타냅니다.|  
|**adFieldDoesNotExist**|16|지정 된 필드가 존재 하지 않음을 나타냅니다.|  
|**adFieldIgnore**|15|원본에서 데이터 값을 설정할 때이 필드를 생략 했음을 나타냅니다. 공급자에 값이 설정 되어 있지 않습니다.|  
|**adFieldIntegrityViolation**|10|필드가 계산 된 엔터티 또는 파생 된 엔터티 이므로 수정할 수 없음을 나타냅니다.|  
|**adFieldInvalidURL**|17|데이터 원본 URL에 잘못 된 문자가 포함 되어 있음을 나타냅니다.|  
|**adFieldIsNull**|3|공급자가 VT_NULL 형식의 VARIANT 값을 반환 했으며 필드가 비어 있지 않음을 나타냅니다.|  
|**adFieldOK**|0|기본값 필드가 성공적으로 추가 또는 삭제 되었음을 나타냅니다.|  
|**adFieldOutOfSpace**|22|공급자가 이동 또는 복사 작업을 완료 하기에 충분 한 저장소 공간을 확보할 수 없음을 나타냅니다.|  
|**adFieldPendingChange**|0x40000|는 필드가 삭제 된 후 다른 데이터 형식으로 다시 추가 되었거나 이전에 **adFieldOK** 상태가 된 필드의 값이 변경 되었음을 나타냅니다. 필드의 마지막 형태는 [Update](./update-method.md) 메서드를 호출한 후에 [Fields](./fields-collection-ado.md) 컬렉션을 수정 합니다.|  
|**adFieldPendingDelete**|0x20000|**삭제** 작업으로 인해 상태가 설정 되었음을 나타냅니다. **업데이트** 메서드를 호출한 후 필드가 **Fields** 컬렉션에서 삭제 되도록 표시 되었습니다.|  
|**adFieldPendingInsert**|0x10000|**추가** 작업으로 인해 상태가 설정 되었음을 나타냅니다. **업데이트** 메서드를 호출한 **후 필드가** **Fields** 컬렉션에 추가 된 것으로 표시 되었습니다.|  
|**adFieldPendingUnknown**|0x80000|공급자가 필드 상태를 설정 하는 작업을 확인할 수 없음을 나타냅니다.|  
|**adFieldPendingUnknownDelete**|0x100000|는 공급자가 필드 상태를 설정 하는 작업을 확인할 수 없으며 **Update** 메서드를 호출한 후에 **Fields** 컬렉션에서 필드가 삭제 됨을 나타냅니다.|  
|**Adfield이상 거부 됨**|9|필드가 읽기 전용으로 정의 되어 있으므로 수정할 수 없음을 나타냅니다.|  
|**adFieldReadOnly**|24|데이터 원본의 필드가 읽기 전용으로 정의 됨을 나타냅니다.|  
|**adFieldResourceExists**|19|대상 URL에 개체가 이미 있지만 개체를 덮어쓸 수 없기 때문에 공급자가 작업을 수행할 수 없음을 나타냅니다.|  
|**adFieldResourceLocked**|18|하나 이상의 다른 응용 프로그램이 나 프로세스에 의해 데이터 원본이 잠겨 있으므로 공급자가 작업을 수행할 수 없음을 나타냅니다.|  
|**adFieldResourceOutOfScope**|25|원본 또는 대상 URL이 현재 레코드 범위 밖에 있음을 나타냅니다.|  
|**adFieldSchemaViolation**|11|값이 필드에 대 한 데이터 원본 스키마 제약 조건을 위반 했음을 나타냅니다.|  
|**adFieldSignMismatch**|5|공급자가 반환한 데이터 값이 서명 되었지만 ADO 필드 값의 데이터 형식이 서명 되지 않았음을 나타냅니다.|  
|**adFieldTruncated**|4|데이터 소스에서 읽을 때 가변 길이 데이터가 잘린 상태임을 나타냅니다.|  
|**adFieldUnavailable 수 없음**|8|데이터 원본에서 읽을 때 공급자가 값을 확인할 수 없음을 나타냅니다. 예를 들어 방금 만든 행은 열에 대 한 기본값을 사용할 수 없으며 새 값이 아직 지정 되지 않았습니다.|  
|**adFieldVolumeNotFound**|21|공급자가 URL로 표시 된 저장소 볼륨을 찾을 수 없음을 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 이러한 상수에는 ADO/WFC 해당 항목이 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Status 속성(ADO 필드)](./status-property-ado-field.md)