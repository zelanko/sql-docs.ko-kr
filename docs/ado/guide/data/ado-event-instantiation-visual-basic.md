---
title: 'ADO 이벤트 인스턴스: Visual Basic | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
ms.assetid: dce0a2a3-326f-4aaf-a822-6c5549833afa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ead713a37d4ecf8bdfecd0d6c485684d1ad0777f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926076"
---
# <a name="ado-event-instantiation-visual-basic"></a>ADO 이벤트 인스턴스: Visual Basic
모듈 수준 변수를 사용 하 여 선언 해야 Microsoft® Visual Basic®에서 ADO 이벤트를 처리 하기 위해 합니다 **WithEvents** 키워드입니다. 이 변수는 클래스 모듈의 일부로 선언되어야 하고, 모듈 수준에서 선언되어야 합니다. 그러나이 아니므로 제한적 것으로 Visual Basic **폼** 개체는 클래스 이기도 합니다. ADO 이벤트를 처리 하는 가장 간단한 방법은 사용 하는 변수를 선언 하는 것 **WithEvents**합니다. 다음 예제에서는 처리 합니다 **ConnectComplete** 에 대 한 이벤트를 **연결** 개체:  
  
```  
' BeginEventExampleVB02  
Dim WithEvents connEvent As Connection  
Attribute connEvent.VB_VarHelpID = -1  
  
Private Sub Form_Load()  
Dim strConn As String  
  
   ' Create a new object with event  
   ' handling enabled.  
   strConn = "Provider=sqloledb;" & _  
      "Data Source=MyServer;" & _  
      "Initial Catalog=Northwind;" & _  
      "Integrated Security=SSPI;"  
   Set connEvent = New ADODB.Connection  
   connEvent.Open strConn  
End Sub  
  
Private Sub connEvent_ConnectComplete(ByVal pError As ADODB.Error, _  
    adStatus As ADODB.EventStatusEnum, _  
    ByVal pConnection As ADODB.Connection)  
Dim strMsg As String  
  
   If adStatus = adStatusErrorsOccurred Then  
      Select Case pError.Number  
         Case adErrOperationCancelled  
            ' The operation was cancelled in the  
            ' Will event. Notify the user and exit.  
            strMsg = "I'm sorry you can't connect right now." & vbCrLf  
            strMsg = strMsg & "Click OK to exit."  
            Unload Me  
         Case Else  
            strMsg = "Error " & Format(pError.Number) & vbCrLf  
            strMsg = strMsg & pError.Description  
            strMsg = strMsg & "Click OK to exit."  
            Unload Me  
      End Select  
   End If  
   frmWait.btnOK.Enabled = True  
End Sub  
' EndEventExampleVB02  
```  
  
 **연결** 개체에 선언 되어를 **폼** 사용 하 여 수준를 **WithEvents** 키워드를 이벤트 처리를 사용 하도록 설정 합니다. Form_Load 이벤트 처리기를 실제로 새로 할당 하 여 개체를 만듭니다 **연결** 개체를 *connEvent* 다음 연결을 엽니다. 물론 실제 응용 프로그램은 여기 나와 있는 것 보다 Form_Load 이벤트 처리기에서 더 많은 처리를 수행 합니다.
