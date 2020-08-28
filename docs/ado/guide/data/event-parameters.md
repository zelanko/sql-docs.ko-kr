---
description: 이벤트 매개 변수
title: 이벤트 매개 변수 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Error parameter [ADO]
- Object parameter [ADO]
- Status parameter [ADO]
- events [ADO], parameters
- Reason parameter [ADO]
- event parameters [ADO]
ms.assetid: bd5c5afa-d301-4899-acda-40f98a6afa4d
author: rothja
ms.author: jroth
ms.openlocfilehash: cc36f0ab059bb7b605b02316008a969411663a8d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991304"
---
# <a name="event-parameters"></a>이벤트 매개 변수
모든 이벤트 처리기에는 이벤트 처리기를 제어 하는 상태 매개 변수가 있습니다. 전체 이벤트의 경우이 매개 변수를 사용 하 여 이벤트를 생성 한 작업의 성공 또는 실패를 나타낼 수도 있습니다. 또한 대부분의 전체 이벤트에는 발생 한 오류에 대 한 정보를 제공 하 고 작업을 수행 하는 데 사용 되는 ADO 개체를 참조 하는 하나 이상의 개체 매개 변수를 포함 하는 오류 매개 변수가 있습니다. 예를 들어 [ExecuteComplete](../../reference/ado-api/executecomplete-event-ado.md) 이벤트는 이벤트와 연결 된 **명령**, **레코드 집합**및 **연결** 개체에 대 한 개체 매개 변수를 포함 합니다. 다음 Microsoft® Visual Basic® 예제에서는 **Execute** 메서드에서 사용 하는 **명령**, **레코드 집합**및 **연결** 개체를 나타내는 pcommand, pcommand 및 pcommand 개체를 볼 수 있습니다.  
  
```  
Private Sub connEvent_ExecuteComplete(ByVal RecordsAffected As Long, _  
     ByVal pError As ADODB.Error, _  
     adStatus As ADODB.EventStatusEnum, _  
     ByVal pCommand As ADODB.Command, _  
     ByVal pRecordset As ADODB.Recordset, _  
     ByVal pConnection As ADODB.Connection)  
```  
  
 **Error** 개체를 제외 하 고 동일한 매개 변수가 해당 이벤트에 전달 됩니다. 이를 통해 보류 중인 작업에서 사용 되는 각 개체를 검사 하 고 작업을 완료할 수 있는지 여부를 결정할 수 있습니다.  
  
 일부 이벤트 처리기에는 이벤트 발생 이유에 대 한 추가 정보를 제공 하는 *Reason* 매개 변수가 있습니다. 예를 들어 **WillMove** 및 **MoveComplete** 이벤트는 이동 하는 탐색 메서드 (**MoveNext**, **MovePrevious**등) 중 하나 또는 requery의 결과로 인해 발생할 수 있습니다.  
  
## <a name="status-parameter"></a>Status 매개 변수  
 이벤트 처리기 루틴이 호출 되 면 *Status* 매개 변수는 다음 값 중 하나로 설정 됩니다.  
  
|값|설명|  
|-----------|-----------------|  
|**adStatusOK**|둘 다에 전달 되 고 이벤트를 완료 합니다. 이 값은 이벤트를 발생 시킨 작업이 성공적으로 완료 되었음을 의미 합니다.|  
|**adStatusErrorsOccurred**|완료 이벤트만 전달 됩니다. 이 값은 이벤트를 발생 시킨 작업이 실패 했음을 의미 합니다. 그렇지 않으면에서 작업을 취소 합니다. 자세한 내용은 *Error* 매개 변수를 확인 하세요.|  
|**adStatusCantDeny**|에 전달 되는 이벤트에만 해당 됩니다. 이 값은 이벤트에서 작업을 취소할 수 없음을 의미 합니다. 이를 수행 해야 합니다.|  
  
 작업을 계속 해야 한다는 메시지가 표시 되 면 *상태* 매개 변수를 변경 되지 않은 상태로 둡니다. 그러나 들어오는 상태 매개 변수를 **adStatusCantDeny**로 설정 하지 않은 경우 *상태* 를 **adstatuscancel**로 변경 하 여 보류 중인 작업을 취소할 수 있습니다. 이렇게 하면 작업과 연결 된 Complete 이벤트의 *Status* 매개 변수는 **adStatusErrorsOccurred**로 설정 됩니다. Complete 이벤트에 전달 된 **Error** 개체에는 **adErrOperationCancelled**값이 포함 됩니다.  
  
 더 이상 이벤트를 처리 하지 않으려면 *상태* 를 **adStatusUnwantedEvent** 로 설정 하면 응용 프로그램에서 해당 이벤트에 대 한 알림을 더 이상 받지 않게 됩니다. 그러나 일부 이벤트는 여러 가지 이유로 발생할 수 있습니다. 이 경우 가능한 각 원인에 대해 **adStatusUnwantedEvent** 를 지정 해야 합니다. 예를 들어 보류 중인 **Recordchange** 이벤트의 알림 수신을 중지 하려면 *상태* 매개 변수를 **adrsnaddnew**, **adrsnaddnew**, **Adrsnaddnew**, adRsnUndoUpdate, **Adrsnaddnew**, Adrsnaddnew **delete**및 **adrsnfirstchange** 에 대해 **adStatusUnwantedEvent** 로 설정 해야 합니다. **adRsnUndoUpdate**  
  
|값|설명|  
|-----------|-----------------|  
|**adStatusUnwantedEvent**|이 이벤트 처리기에서 추가 알림을 수신 하지 않도록 요청 합니다.|  
|**adStatusCancel**|발생 하려는 작업의 취소를 요청 합니다.|  
  
## <a name="error-parameter"></a>오류 매개 변수  
 *Error* 매개 변수는 ADO [오류](../../reference/ado-api/error-object.md) 개체에 대 한 참조입니다. *Status* 매개 변수를 **adStatusErrorsOccurred**로 설정 하면 **Error** 개체에는 작업이 실패 한 이유에 대 한 세부 정보가 포함 됩니다. Complete 이벤트와 연결 된 이벤트에서 *상태* 매개 변수를 **adstatuscancel**로 설정 하 여 작업을 취소 한 경우에는 error 개체가 항상 **adErrOperationCancelled**로 설정 됩니다.  
  
## <a name="object-parameter"></a>개체 매개 변수  
 각 이벤트는 작업과 관련 된 개체를 나타내는 개체를 하나 이상 받습니다. 예를 들어 **ExecuteComplete** 이벤트는 **명령** 개체, **레코드 집합** 개체 및 **연결** 개체를 수신 합니다.  
  
## <a name="reason-parameter"></a>Reason 매개 변수  
 *Reason* 매개 변수 *adReason*는 이벤트가 발생 한 이유에 대 한 추가 정보를 제공 합니다. *AdReason* 매개 변수를 사용 하는 이벤트는 매번 다른 이유로 동일한 작업을 수행 하는 경우에도 여러 번 호출 될 수 있습니다. 예를 들어, 레코드 삽입, 삭제 또는 수정 작업을 수행 하거나 취소 하려는 작업에 대해 **WillChangeRecord** 이벤트 처리기가 호출 됩니다. 특정 이유에 대해 발생 하는 경우에만 이벤트를 처리 하려는 경우 *adReason* 매개 변수를 사용 하 여 관심이 없는 항목을 필터링 할 수 있습니다. 예를 들어 레코드가 추가 되기 때문에 발생 하는 경우에만 레코드 변경 이벤트를 처리 하려는 경우 다음과 같은 항목을 사용할 수 있습니다.  
  
```  
' BeginEventExampleVB01  
Private Sub rsTest_WillChangeRecord(ByVal adReason As ADODB.EventReasonEnum, ByVal cRecords As Long, adStatus As ADODB.EventStatusEnum, ByVal pRecordset As ADODB.Recordset)  
   If adReason = adRsnAddNew Then  
       ' Process event  
       '...  
   Else  
       ' Cancel event notification for all  
       ' other possible adReason values.  
       adStatus = adStatusUnwantedEvent  
   End If  
End Sub  
' EndEventExampleVB01  
```  
  
 이 경우 다른 각 이유로 알림이 발생할 수 있습니다. 그러나이는 각 원인에 대해 한 번만 발생 합니다. 각 원인에 대해 한 번씩 알림이 발생 한 후에는 새 레코드를 추가 하는 것에 대해서만 알림을 받게 됩니다.  
  
 이와 대조적으로 *Adstatus* 를 한 번만 **adStatusUnwantedEvent** 로 설정 하 여 **adReason** 매개 변수가 없는 이벤트 처리기가 이벤트 알림을 수신 하지 않도록 요청 해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ADO 이벤트 처리기 요약](./ado-event-handler-summary.md)   
 [언어별 ADO 이벤트 인스턴스화](./ado-event-instantiation-by-language.md)   
 [이벤트 처리기가 함께 작동 하는 방법](./how-event-handlers-work-together.md)   
 [이벤트 형식](./types-of-events.md)