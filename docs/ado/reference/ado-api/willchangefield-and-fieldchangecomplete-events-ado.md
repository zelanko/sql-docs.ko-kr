---
title: WillChangeField 및 FieldChangeComplete 이벤트 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldChangeComplete
- Recordset::WillChangeField
- Recordset::FieldChangeComplete
- WillChangeField
helpviewer_keywords:
- WillChangeField event [ADO]
- fieldchangecomplete event [ADO]
ms.assetid: 3e49fb89-c45b-4d39-823e-3cc887c59b37
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 35efd51d640943c4d5293956a0638fa85ac302f1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710077"
---
# <a name="willchangefield-and-fieldchangecomplete-events-ado"></a>WillChangeField 및 FieldChangeComplete 이벤트(ADO)
합니다 **WillChangeField** 이벤트는 보류 중인 작업을 하나 이상의 값을 변경 하기 전에 호출 됩니다 [필드](../../../ado/reference/ado-api/field-object.md) 개체를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다. 합니다 **FieldChangeComplete** 이벤트 후 하나 이상의 값 이라고 **필드** 개체 변경 되었습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
WillChangeField cFields, Fields, adStatus, pRecordset  
FieldChangeComplete cFields, Fields, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>매개 변수  
 *cFields*  
 A **긴** 의 수를 나타내는 **필드** 개체 *필드*합니다.  
  
 *Fields*  
 에 대 한 **WillChangeField**의 *필드* 매개 변수는 배열이 **변형** 포함 하는 **필드** 원래 값을 사용 하 여 개체입니다. 에 대 한 **FieldChangeComplete**의 *필드* 매개 변수는 배열이 **변형** 포함 하는 **필드** 변경된 된 값을 사용 하 여 개체 .  
  
 *pError*  
 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다. 경우에 발생 한 오류에 설명 합니다 값 *adStatus* 됩니다 **adStatusErrorsOccurred**; 설정 되지 않은 고, 그렇지 합니다.  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다.  
  
 때 **WillChangeField** 가 호출 하 고,이 매개 변수는 설정 **adStatusOK** 이벤트를 발생 시킨 작업에 성공 하는 경우. 로 설정 되어 **adStatusCantDeny** 경우이 이벤트는 보류 중인 작업의 취소를 요청할 수 없습니다.  
  
 때 **FieldChangeComplete** 가 호출 하 고,이 매개 변수 설정 **adStatusOK** 이벤트를 발생 시킨 작업 성공 하거나 **adStatusErrorsOccurred** 경우 작업에 실패 했습니다.  
  
 앞 **WillChangeField** 반환 되는 경우이 매개 변수를 설정 **adStatusCancel** 보류 중인 작업 취소 요청을 합니다.  
  
 앞 **FieldChangeComplete** 반환 되는 경우이 매개 변수를 설정 **adStatusUnwantedEvent** 후속 알림을 방지 하 합니다.  
  
 *pRecordset*  
 A **레코드 집합** 개체입니다. 합니다 **레코드 집합** 이 이벤트가 발생 한입니다.  
  
## <a name="remarks"></a>Remarks  
 A **WillChangeField** 또는 **FieldChangeComplete** 설정 하는 경우 이벤트가 발생할 수 있습니다를 [값](../../../ado/reference/ado-api/value-property-ado.md) 속성을 호출 합니다 [업데이트](../../../ado/reference/ado-api/update-method.md) 메서드 배열 매개 변수 필드 및 값을 사용 하 여입니다.  
  
## <a name="see-also"></a>관련 항목  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)
