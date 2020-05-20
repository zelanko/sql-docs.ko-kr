---
title: 'ADO 이벤트 인스턴스화: Visual Basic | Microsoft Docs'
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
author: rothja
ms.author: jroth
ms.openlocfilehash: dba3be9c80160dca2773c63b2ed7f7c706678625
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761319"
---
# <a name="ado-event-instantiation-visual-basic"></a>ADO 이벤트 인스턴스: Visual Basic
Microsoft® Visual Basic®에서 ADO 이벤트를 처리 하려면 **WithEvents** 키워드를 사용 하 여 모듈 수준 변수를 선언 해야 합니다. 변수는 클래스 모듈의 일부로만 선언할 수 있으며 모듈 수준에서 선언 되어야 합니다. 그러나 Visual Basic **폼** 개체도 클래스 이므로이는 제한적이 지 않습니다. ADO 이벤트를 처리 하는 가장 간단한 방법은 **WithEvents**를 사용 하 여 변수를 선언 하는 것입니다. 다음 예에서는 **연결** 개체에 대 한 **connectcomplete** 이벤트를 처리 합니다.  
  
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
  
 **Connection** 개체는 **WithEvents** 키워드를 사용 하 여 **폼** 수준에서 선언 되어 이벤트를 처리할 수 있습니다. Form_Load 이벤트 처리기는 실제로 *Connevent* 에 새 **연결** 개체를 할당 하 여 개체를 만든 다음 연결을 엽니다. 물론 실제 응용 프로그램은 여기에 표시 된 것 보다 Form_Load 이벤트 처리기에서 더 많은 처리를 수행 합니다.
