---
description: WillChangeField 및 FieldChangeComplete 이벤트(ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: be000a8ff9154c79c2b98c9bc57f79f3537743c9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441535"
---
# <a name="willchangefield-and-fieldchangecomplete-events-ado"></a>WillChangeField 및 FieldChangeComplete 이벤트(ADO)
**WillChangeField** 이벤트는 보류 중인 작업이 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)에 있는 하나 이상의 [필드](../../../ado/reference/ado-api/field-object.md) 개체 값을 변경 하기 전에 호출 됩니다. **FieldChangeComplete** 이벤트는 하나 이상의 **Field** 개체의 값이 변경 된 후에 호출 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
WillChangeField cFields, Fields, adStatus, pRecordset  
FieldChangeComplete cFields, Fields, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>매개 변수  
 *cFields*  
 *필드*의 **필드** 개체 수를 나타내는 **Long** 입니다.  
  
 *필드*  
 **WillChangeField**의 경우 *Fields* 매개 변수는 원래 값이 포함 된 **필드** 개체를 포함 하는 **variant** 배열입니다. **FieldChangeComplete**의 경우 *Fields* 매개 변수는 변경 된 값이 있는 **필드** 개체를 포함 하는 **변형** 배열입니다.  
  
 *pError*  
 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다. *Adstatus* 값이 **adStatusErrorsOccurred**인 경우 발생 하는 오류를 설명 합니다. 그렇지 않으면 설정 되지 않습니다.  
  
 *adStatus*  
 [Eventstatusenum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다.  
  
 **WillChangeField** 가 호출 되 면이 매개 변수는 이벤트를 발생 시킨 작업이 성공한 경우 **adstatusok** 로 설정 됩니다. 이 이벤트는 보류 중인 작업의 취소를 요청할 수 없는 경우 **adStatusCantDeny** 로 설정 됩니다.  
  
 **FieldChangeComplete** 가 호출 되 면이 매개 변수는 이벤트를 발생 시킨 작업이 성공한 경우 **adstatusok** 로 설정 되 고, 작업이 실패 한 경우에는 **adStatusErrorsOccurred** 로 설정 됩니다.  
  
 **WillChangeField** 가 반환 되기 전에이 매개 변수를 **adstatuscancel** 로 설정 하 여 보류 중인 작업의 취소를 요청 합니다.  
  
 **FieldChangeComplete** 가 반환 되기 전에이 매개 변수를 **adStatusUnwantedEvent** 로 설정 하 여 후속 알림이 발생 하지 않도록 합니다.  
  
 *pRecordset*  
 **레코드 집합** 개체입니다. 이 이벤트가 발생 한 **레코드 집합** 입니다.  
  
## <a name="remarks"></a>설명  
 **WillChangeField** 또는 **FieldChangeComplete** 이벤트는 [Value](../../../ado/reference/ado-api/value-property-ado.md) 속성을 설정 하 고 필드 및 값 배열 매개 변수를 사용 하 여 [Update](../../../ado/reference/ado-api/update-method.md) 메서드를 호출할 때 발생할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ADO Events 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)
