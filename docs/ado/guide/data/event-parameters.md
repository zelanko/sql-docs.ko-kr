---
title: "이벤트 매개 변수 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Error parameter [ADO]
- Object parameter [ADO]
- Status parameter [ADO]
- events [ADO], parameters
- Reason parameter [ADO]
- event parameters [ADO]
ms.assetid: bd5c5afa-d301-4899-acda-40f98a6afa4d
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e0d73ed8eda955b5b027b662e3e5c80c50730b7f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="event-parameters"></a>이벤트 매개 변수
모든 이벤트 처리기에 이벤트 처리기를 제어 하는 상태 매개 변수입니다. 전체 이벤트에 대 한이 매개 변수는 이벤트를 생성 하는 작업의 성공 여부를 나타내는 것도 사용 됩니다. 가장 완전 이벤트 발생 하는 모든 오류 및 작업을 수행 하는 데 사용 되는 ADO 개체를 참조 하는 하나 이상의 개체 매개 변수 하는 방법에 대 한 정보를 제공 하는 오류 매개 변수를 갖게 됩니다. 예를 들어는 [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md) 에 대 한 개체 매개 변수를 포함 하는 이벤트는 **명령**, **레코드 집합**, 및 **연결** 개체 이벤트와 연결 합니다. 다음 Microsoft® Visual Basic® 예에서 pCommand, pRecordset, 및 pConnection 개체를 나타냅니다를 볼 수는 **명령**, **레코드 집합**, 및 **연결** 에서 사용 되는 개체는 **Execute** 메서드.  
  
```  
Private Sub connEvent_ExecuteComplete(ByVal RecordsAffected As Long, _  
     ByVal pError As ADODB.Error, _  
     adStatus As ADODB.EventStatusEnum, _  
     ByVal pCommand As ADODB.Command, _  
     ByVal pRecordset As ADODB.Recordset, _  
     ByVal pConnection As ADODB.Connection)  
```  
  
 제외 하 고는 **오류** 개체를 동일한 매개 변수는 이벤트에 전달 됩니다. 보류 중인 작업에 사용 되 고 작업을 완료 하는 데 허용 하는지 여부를 결정 하는 개체의 각 확인이 있습니다.  
  
 일부 이벤트 처리기는 *이유* 는 이벤트가 발생 한 이유에 대 한 추가 정보를 제공 하는 매개 변수입니다. 예를 들어는 **WillMove** 및 **두** 이벤트 탐색 방법 중 하나로 인해 발생할 수 있습니다 (**MoveNext**, **MovePrevious**등)를 호출 하거나 다시 쿼리 결과로 되 고 있습니다.  
  
## <a name="status-parameter"></a>Status 매개 변수  
 이벤트 처리기 루틴 호출 되는 *상태* 매개 변수는 다음 값 중 하나로 설정 됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|**adStatusOK**|가 않으며 완료 이벤트를 모두에 전달 합니다. 이 값을 사용 하는 성공적으로 완료 이벤트를 발생 시킨 작업을 의미 합니다.|  
|**adStatusErrorsOccurred**|완료 이벤트에만 전달 합니다. 이 값이 이벤트를 발생 시킨 작업이 성공적 Will 이벤트에서 작업을 취소 있음을 의미 합니다. 확인 된 *오류* 자세한 내용은 매개 변수입니다.|  
|**adStatusCantDeny**|이벤트에만 전달 합니다. 이 값은 작업 Will 이벤트가 취소할 수 없습니다 것입니다. 수행 되어야 합니다.|  
  
 에서는 Will 이벤트는 작업을 계속 해야 하는 경우 둡니다는 *상태* 변경 하지 않고 매개 변수입니다. 들어오는 상태 매개 변수가 설정 되지 않은 상태로 **adStatusCantDeny**을 변경 하 여 보류 중인 작업을 취소할 수 있습니다 *상태* 를 **adStatusCancel**합니다. 이렇게 하면 해당 작업과 연결 된 전체 이벤트에 해당 *상태* 매개 변수 설정 **adStatusErrorsOccurred**합니다. **오류** 완료 이벤트에 전달 된 개체의 값이 포함 될 **adErrOperationCancelled**합니다.  
  
 설정할 수 없습니다 더 이상 이벤트를 처리 하려면 *상태* 를 **adStatusUnwantedEvent** 및 응용 프로그램에 해당 이벤트의 알림을 더 이상 받지 것입니다. 단, 여러 가지 원인에 대 한 일부 이벤트를 발생할 수 있습니다. 이 경우 지정 해야 **adStatusUnwantedEvent** 가능한 각 원인에 대 한 합니다. 예를 들어, 보류 중인 알림 수신을 중지 하려면 **RecordChange** 설정 해야 이벤트에는 *상태* 매개 변수를 **adStatusUnwantedEvent** 에 대 한  **adRsnAddNew**, **adRsnDelete**, **adRsnUpdate**, **adRsnUndoUpdate**, **adRsnUndoAddNew**, **adRsnUndoDelete**, 및 **adRsnFirstChange** 발생 합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**adStatusUnwantedEvent**|이 이벤트 처리기에 더 이상 알림을 받지를 요청 합니다.|  
|**adStatusCancel**|수행 하려는 작업의 취소를 요청 합니다.|  
  
## <a name="error-parameter"></a>오류 매개 변수  
 *오류* 매개 변수는 ADO에 대 한 참조 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다. 경우는 *상태* 로 설정 된 **adStatusErrorsOccurred**, **오류** 작업 실패에 대 한 세부 정보를 포함 하는 개체입니다. 전체 이벤트와 연결 된 Will 이벤트를 설정 하 여 작업을 취소 했습니다 하는 경우는 *상태* 매개 변수를 **adStatusCancel**, error 개체는 항상으로 설정  **adErrOperationCancelled**합니다.  
  
## <a name="object-parameter"></a>개체 매개 변수  
 각 이벤트는 작업에 포함 되는 개체를 나타내는 하나 이상의 개체를 수신 합니다. 예를 들어는 **ExecuteComplete** 이벤트 수신는 **명령** 개체는 **레코드 집합** 개체 및 **연결** 개체입니다.  
  
## <a name="reason-parameter"></a>이유 매개 변수  
 *이유* 매개 변수를 *adReason*, 이벤트가 발생 한 이유에 대 한 추가 정보를 제공 합니다. 이벤트는 *adReason* 매개 변수 될 때마다 다른 이유로 동일한 작업에 대해서도 여러 번 호출 될 수 있습니다. 예를 들어는 **WillChangeRecord** 않거나 삽입, 삭제 또는 수정 된 레코드의 취소 하려고 하는 작업에 대 한 이벤트 처리기가 호출 됩니다. 만 사용할 수 있습니다 특정 이유로 발생할 때 이벤트를 처리 하려는 경우는 *adReason* 에 관심이 없는 필터링 하려면 매개 변수입니다. 예를 들어 레코드 추가 되었기 때문에 발생 하는 경우에 레코드 변경 이벤트를 처리 하려는 경우 다음과 같이 사용할 수 있습니다.  
  
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
  
 이 경우 다른 이유로 각각에 대해 알림이 발생할 수 있습니다. 하지만는 발생 한 번만 각 이유에 합니다. 알림을 이루어진 후 한 번 각 원인에 대 한 새 레코드 추가 대 한 알림을 받게 됩니다.  
  
 설정 해야 하는 반면, *adStatus* 를 **adStatusUnwantedEvent** 한 번만 요청을 하지 않고 이벤트 처리기는 **adReason** 매개 변수 중지 수신 이벤트 알림입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)   
 [언어별 ADO 이벤트 인스턴스 생성](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [이벤트 처리기 함께 작동 하는 방법](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [이벤트 유형](../../../ado/guide/data/types-of-events.md)
