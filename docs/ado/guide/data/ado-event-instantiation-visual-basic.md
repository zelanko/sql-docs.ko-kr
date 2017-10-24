---
title: "ADO 이벤트 인스턴스화: Visual Basic | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: dce0a2a3-326f-4aaf-a822-6c5549833afa
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 56510bc99d0a6a7c20d18b93b22a60decdfcc2e2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="ado-event-instantiation-visual-basic"></a>ADO 이벤트 인스턴스화: Visual Basic
모듈 수준 변수를 사용 하 여 선언 해야 Microsoft® Visual Basic®에서 ADO 이벤트를 처리 하기 위해는 **WithEvents** 키워드입니다. 변수는 클래스 모듈의 일부로 선언 될 수 있으며 모듈 수준에서 선언 해야 합니다. 그러나이 보이기 어려워, 제한적 이므로 아닙니다 Visual Basic **양식** 개체는 클래스 이기도 합니다. 사용 하는 변수를 선언 하는 ADO 이벤트를 처리 하는 가장 간단한 방법은 **WithEvents**합니다. 다음 예제에서는 핸들의 **ConnectComplete** 에 대 한 이벤트는 **연결** 개체:  
  
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
  
 **연결** 개체에 선언는 **양식** 를 사용 하 여 수준는 **WithEvents** 키워드를 이벤트 처리를 사용 하도록 설정 합니다. Form_Load 이벤트 처리기는 새 할당 하 여 개체를 실제로 만드는 **연결** 개체를 *connEvent* 다음 연결을 엽니다. 물론, 실제 응용 프로그램에서 Form_Load 이벤트 처리기는 여기 표시 된 것 보다 더 많은 처리 작업 방식.

