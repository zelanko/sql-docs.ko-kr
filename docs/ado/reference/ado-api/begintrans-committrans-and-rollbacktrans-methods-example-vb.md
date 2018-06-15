---
title: BeginTrans, CommitTrans 및 RollbackTrans 메서드 예제 (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- RollbackTrans method [ADO], Visual Basic example
- CommitTrans method [ADO], Visual Basic example
- BeginTrans method [ADO], Visual Basic example
ms.assetid: aa7de324-cd71-4bd0-8043-24229f4a785e
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 72defd0f6467f432be5ee5f41e5b3d57b97ade9b
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35276042"
---
# <a name="begintrans-committrans-and-rollbacktrans-methods-example-vb"></a>BeginTrans, CommitTrans 및 RollbackTrans 메서드 예제 (VB)
에 있는 모든 심리학 책의 책 종류를 변경 하는이 예제는 ***타이틀*** 데이터베이스의 테이블입니다. 후의 [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 메서드 시작에 대 한 모든 변경 내용을 격리 하는 트랜잭션을 ***타이틀*** 테이블은 [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 메서드는 변경 내용을 저장 합니다. 사용할 수는 [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 메서드를 사용 하 여 저장 하는 변경 내용을 취소 하는 [업데이트](../../../ado/reference/ado-api/update-method.md) 메서드.  
  
```  
'BeginBeginTransVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim rstTitles As ADODB.Recordset  
    Dim strSQLTitles As String  
    'record variables  
    Dim strTitle As String  
    Dim strMessage As String  
  
    ' Open connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Set Cnxn = New ADODB.Connection  
    Cnxn.Open strCnxn  
  
    ' Open recordset dynamic to allow for changes  
    Set rstTitles = New ADODB.Recordset  
    strSQLTitles = "Titles"  
    rstTitles.Open strSQLTitles, Cnxn, adOpenDynamic, adLockPessimistic, adCmdTable  
  
    Cnxn.BeginTrans  
  
    ' Loop through recordset and prompt user  
    ' to change the type for a specified title  
  
    rstTitles.MoveFirst  
  
    Do Until rstTitles.EOF  
        If Trim(rstTitles!Type) = "psychology" Then  
            strTitle = rstTitles!Title  
            strMessage = "Title: " & strTitle & vbCr & _  
            "Change type to self help?"  
  
            ' If yes, change type for the specified title  
            If MsgBox(strMessage, vbYesNo) = vbYes Then  
                rstTitles!Type = "self_help"  
                rstTitles.Update  
            End If  
        End If  
    rstTitles.MoveNext  
    Loop  
  
    ' Prompt user to commit all changes made  
    If MsgBox("Save all changes?", vbYesNo) = vbYes Then  
        Cnxn.CommitTrans  
    Else  
        Cnxn.RollbackTrans  
    End If  
  
    ' Print recordset  
    rstTitles.Requery  
    rstTitles.MoveFirst  
    Do While Not rstTitles.EOF  
        Debug.Print rstTitles!Title & " - " & rstTitles!Type  
        rstTitles.MoveNext  
    Loop  
  
    ' Restore original data as this is a demo  
    rstTitles.MoveFirst  
  
    Do Until rstTitles.EOF  
        If Trim(rstTitles!Type) = "self_help" Then  
            rstTitles!Type = "psychology"  
            rstTitles.Update  
        End If  
        rstTitles.MoveNext  
    Loop  
  
    ' clean up  
    rstTitles.Close  
    Cnxn.Close  
    Set rstTitles = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstTitles Is Nothing Then  
        If rstTitles.State = adStateOpen Then rstTitles.Close  
    End If  
    Set rstTitles = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
  
'EndBeginTransVB  
```  
  
## <a name="see-also"></a>관련 항목  
 [BeginTrans, CommitTrans 및 RollbackTrans 메서드 (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)   
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
