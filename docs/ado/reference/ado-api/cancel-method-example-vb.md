---
description: Cancel 메서드 예제(VB)
title: Cancel 메서드 예제 (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Cancel method [ADO], Visual Basic example
ms.assetid: 5c0530ad-68d0-4cba-b1af-9386d566c7c5
author: rothja
ms.author: jroth
ms.openlocfilehash: 3ca981db6a75beb2c4c4c04c03386f8e8b82920f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975634"
---
# <a name="cancel-method-example-vb"></a>Cancel 메서드 예제(VB)
이 예에서는 [cancel](./cancel-method-ado.md) 메서드를 사용 하 여 연결을 사용 하는 경우 [연결](./connection-object-ado.md) 개체에서 실행 중인 명령을 취소 합니다.  
  
```  
'BeginCancelVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strCmdChange As String  
    Dim strCmdRestore As String  
     'record variables  
    Dim blnChanged As Boolean  
  
    ' Open a connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Define command strings  
    strCmdChange = "UPDATE titles SET type = 'self_help' WHERE type = 'psychology'"  
    strCmdRestore = "UPDATE titles SET type = 'psychology' " & _  
                     "WHERE type = 'self_help'"  
  
    ' Begin a transaction, then execute a command asynchronously  
    Cnxn.BeginTrans  
    Cnxn.Execute strCmdChange, , adAsyncExecute  
    ' do something else for a little while -  
    ' use i = 1 to 32000 to allow completion  
    Dim i As Integer  
    For i = 1 To 1000  
        i = i + i  
        Debug.Print i  
    Next i  
  
    ' If the command has NOT completed, cancel the execute and  
    ' roll back the transaction; otherwise, commit the transaction  
    If CBool(Cnxn.State And adStateExecuting) Then  
        Cnxn.Cancel  
        Cnxn.RollbackTrans  
        blnChanged = False  
        MsgBox "Update canceled."  
    Else  
        Cnxn.CommitTrans  
        blnChanged = True  
        MsgBox "Update complete."  
    End If  
  
    ' If the change was made, restore the data  
    ' because this is only a demo  
    If blnChanged Then  
        Cnxn.Execute strCmdRestore  
        MsgBox "Data restored."  
    End If  
  
    ' clean up  
    Cnxn.Close  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndCancelVB  
```  
  
## <a name="see-also"></a>참고 항목  
 [Cancel 메서드 (ADO)](./cancel-method-ado.md)   
 [연결 개체(ADO)](./connection-object-ado.md)