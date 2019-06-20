---
title: 이벤트 매개 변수 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2912328aa61437b663a290952deaaea7b5c06bca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700771"
---
# <a name="event-parameters"></a>이벤트 매개 변수
모든 이벤트 처리기에 이벤트 처리기를 제어 하는 상태 매개 변수입니다. 전체 이벤트의 경우이 매개 변수는 이벤트를 생성 하는 작업의 성공 여부를 나타내는 사용 됩니다. 가장 완전 이벤트 발생 하는 모든 오류 및 하나 이상의 개체 매개 변수는 작업을 수행 하는 데 ADO 개체를 참조 하는 방법에 대 한 정보를 제공 하는 오류 매개 변수를 수도 있습니다. 예를 들어 합니다 [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md) 이벤트에 대 한 개체 매개 변수를 포함 합니다 **명령**, **레코드 집합**, 및 **연결** 개체 이벤트와 연결 합니다. 다음 Microsoft® Visual Basic® 예에서 pCommand, pRecordset, 및 나타내는 pConnection 개체를 볼 수는 **명령**, **Recordset**, 및 **연결** 에서 사용 되는 개체를 **Execute** 메서드.  
  
```  
Private Sub connEvent_ExecuteComplete(ByVal RecordsAffected As Long, _  
     ByVal pError As ADODB.Error, _  
     adStatus As ADODB.EventStatusEnum, _  
     ByVal pCommand As ADODB.Command, _  
     ByVal pRecordset As ADODB.Recordset, _  
     ByVal pConnection As ADODB.Connection)  
```  
  
 제외 하 고는 **오류** 개체를 동일한 매개 변수는 이벤트에 전달 됩니다. 각 보류 중인 작업을 사용 하 고 작업 완료를 허용 하는지 여부를 결정 하는 개체를 살펴보면이 있습니다.  
  
 일부 이벤트 처리기를 *이유* 이벤트가 발생 한 이유에 대 한 추가 정보를 제공 하는 매개 변수입니다. 예를 들어 합니다 **WillMove** 하 고 **MoveComplete** 이벤트 탐색 방법 중 하나로 인해 발생할 수 있습니다 (**MoveNext**, **MovePrevious**등) 되 고 다시 쿼리 결과로 이상을 호출 합니다.  
  
## <a name="status-parameter"></a>상태 매개 변수  
 이벤트 처리기 루틴을 호출 되는 *상태* 매개 변수는 다음 값 중 하나로 설정 됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|**adStatusOK**|완료 이벤트에 전달 합니다. 이 값을 사용 하는 작업 완료 이벤트를 발생 시킨 의미 합니다.|  
|**adStatusErrorsOccurred**|전체 이벤트만 전달 합니다. 이 값은 이벤트를 발생 시킨 작업에 성공 하지는 이벤트 작업을 취소 있음을 의미 합니다. 확인 합니다 *오류* 매개 변수에 대 한 자세한 내용은 합니다.|  
|**adStatusCantDeny**|이벤트만 전달 합니다. 이 값은 이벤트에서 작업을 취소할 수 없습니다 것을 의미 합니다. 수행 되어야 합니다.|  
  
 작업이 계속 되어야 하는 이벤트를 확인 하는 경우 유지 된 *상태* 변경 되지 않은 매개 변수입니다. 으로 들어오는 상태 매개 변수 설정 되지 않았습니다 **adStatusCantDeny**를 변경 하 여 보류 중인 작업을 취소할 수는 있지만 *상태* 하 **adStatusCancel**합니다. 작업과 연결 된 전체 이벤트에이 작업을 수행 하는 경우 해당 *상태* 매개 변수 설정 **adStatusErrorsOccurred**합니다. 합니다 **오류** Complete 이벤트에 전달 되는 개체 값이 포함 됩니다 **adErrOperationCancelled**합니다.  
  
 에서 더 이상 이벤트를 처리 하려는 경우 설정할 수 없습니다 *상태* 하 **adStatusUnwantedEvent** 응용 프로그램에 해당 이벤트의 알림이 더 이상. 단, 일부 이벤트는 둘 이상의 이유로 발생할 수 있습니다. 이 경우 지정 해야 합니다 **adStatusUnwantedEvent** 각 원인에 대 한 합니다. 예를 들어 보류 중인 알림 수신을 중지할 **RecordChange** 설정한 이벤트는 *상태* 매개 변수를 **adStatusUnwantedEvent** 에 대 한  **adRsnAddNew**, **adRsnDelete**합니다 **adRsnUpdate**를 **adRsnUndoUpdate**를 **adRsnUndoAddNew**, **adRsnUndoDelete**, 및 **adRsnFirstChange** 발생 합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**adStatusUnwantedEvent**|이 이벤트 처리기에 더 이상 알림을 받지는 요청입니다.|  
|**adStatusCancel**|수행 된 작업의 취소를 요청 합니다.|  
  
## <a name="error-parameter"></a>오류 매개 변수  
 합니다 *오류* 매개 변수는 ADO에 대 한 참조가 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다. 경우는 *상태* 매개 변수는 설정 **adStatusErrorsOccurred**의 **오류** 작업 실패에 대 한 세부 정보를 포함 하는 개체입니다. 완료 이벤트와 연결 된는 이벤트가 설정 하 여 작업을 취소 하는 경우는 *상태* 매개 변수를 **adStatusCancel**를 오류 개체를 항상로  **adErrOperationCancelled**합니다.  
  
## <a name="object-parameter"></a>개체 매개 변수  
 각 이벤트는 작업에 관련 된 개체를 나타내는 하나 이상의 개체를 받습니다. 예를 들어 합니다 **ExecuteComplete** 이벤트를 수신를 **명령** 개체를 **레코드 집합** 개체 및 **연결** 개체.  
  
## <a name="reason-parameter"></a>따라서 매개 변수  
 합니다 *이유* 매개 변수 *adReason*, 이벤트가 발생 한 원인에 대 한 추가 정보를 제공 합니다. 사용 하 여 이벤트를 *adReason* 매개 변수 될 때마다 다른 이유로 동일한 작업에 대해서도 여러 번 호출할 수 있습니다. 예를 들어 합니다 **WillChangeRecord** 수행 하거나 삽입, 삭제 또는 수정 된 레코드의 취소 하려고 하는 작업에 대 한 이벤트 처리기가 호출 됩니다. 특정 한 이유로 발생할 때 사용할 수 있습니다만 이벤트를 처리 하려는 경우는 *adReason* 에 관심이 없는 항목을 필터링 하려면 매개 변수입니다. 예를 들어, 레코드 추가 되었기 때문에 발생 하는 경우에 레코드 변경 이벤트를 처리 하려는 경우 다음과 같이 사용할 수 있습니다.  
  
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
  
 이 경우 알림 다른 이유로 각각에 대 한 잠재적으로 발생할 수 있습니다. 그러나이 발생 한 번만 각 원인에 대 한 합니다. 각 원인에 대 한 알림을 한 번 발생 했음을 후 새 레코드 추가 대해서만 알림을 받게 됩니다.  
  
 설정 해야 하는 반면 *adStatus* 에 **adStatusUnwantedEvent** 한 번만 요청을 하지 않고 이벤트 처리기를 **adReason** 매개 변수 중지 수신 이벤트 알림입니다.  
  
## <a name="see-also"></a>관련 항목  
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)   
 [언어별 ADO 이벤트 인스턴스](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [이벤트 처리기를 함께 작동](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [이벤트 유형](../../../ado/guide/data/types-of-events.md)
