---
title: WillChangeField 및 FieldChangeComplete 이벤트 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 108aea1a4f8106c3a84b411591d4866235726efc
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35282855"
---
# <a name="willchangefield-and-fieldchangecomplete-events-ado"></a>WillChangeField 및 FieldChangeComplete 이벤트 (ADO)
**WillChangeField** 이벤트는 보류 중인 작업이 하나 이상의 값을 변경 하기 전에 호출 됩니다 [필드](../../../ado/reference/ado-api/field-object.md) 개체에 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다. **FieldChangeComplete** 하나 이상의 값 보다 이후 라고 이벤트 **필드** 개체 변경 되었습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
WillChangeField cFields, Fields, adStatus, pRecordset  
FieldChangeComplete cFields, Fields, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>매개 변수  
 *cFields*  
 A **긴** 의 수를 나타내는 **필드** 개체 *필드*합니다.  
  
 *Fields*  
 에 대 한 **WillChangeField**, *필드* 매개 변수는 배열입니다 **변형** 포함 된 **필드** 원래 값이 있는 개체입니다. 에 대 한 **FieldChangeComplete**, *필드* 매개 변수는 배열입니다 **변형** 포함 된 **필드** 에서 변경 된 값을 사용 하 여 개체 .  
  
 *pError*  
 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다. 경우에 발생 한 오류를 설명 하는 것의 값 *adStatus* 은 **adStatusErrorsOccurred**; 설정 되지 않은 그렇지 않은 경우.  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다.  
  
 때 **WillChangeField** 은 호출,이 매개 변수 설정 **adStatusOK** 이벤트를 발생 시킨 작업에 성공 하면 합니다. 로 설정 된 **adStatusCantDeny** 경우이 이벤트는 보류 중인 작업의 취소를 요청할 수 없습니다.  
  
 때 **FieldChangeComplete** 은 호출,이 매개 변수 설정 **adStatusOK** 이벤트를 발생 시킨 작업에 성공 하면 또는 **adStatusErrorsOccurred** 경우 작업에 실패 했습니다.  
  
 하기 전에 **WillChangeField** 반환 되 면이 매개 변수를 설정 **adStatusCancel** 보류 중인 작업의 취소 요청을 합니다.  
  
 하기 전에 **FieldChangeComplete** 반환 되 면이 매개 변수를 설정 **adStatusUnwantedEvent** 알림 메시지가 방지 하기 위해 합니다.  
  
 *pRecordset*  
 A **레코드 집합** 개체입니다. **레코드 집합** 이 이벤트가 발생 하는 것에 대 한 합니다.  
  
## <a name="remarks"></a>Remarks  
 A **WillChangeField** 또는 **FieldChangeComplete** 설정 하는 경우 이벤트가 발생할 수 있습니다는 [값](../../../ado/reference/ado-api/value-property-ado.md) 속성과 호출은 [업데이트](../../../ado/reference/ado-api/update-method.md) 메서드 필드 및 값 배열 매개 변수와 함께  
  
## <a name="see-also"></a>관련 항목  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)
