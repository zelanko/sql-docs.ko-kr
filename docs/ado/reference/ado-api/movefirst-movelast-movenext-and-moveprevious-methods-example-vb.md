---
title: 레코드 집합 예제의 레코드 이동 포인터 (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- MovePrevious method [ADO], Visual Basic example
- MoveLast method [ADO], Visual Basic example
- MoveFirst method [ADO], Visual Basic example
- MoveNext method [ADO], Visual Basic example
ms.assetid: 31d3b083-c677-423e-8d26-a212eaeea281
author: rothja
ms.author: jroth
ms.openlocfilehash: a4f0d0394e660bc691b4e13a2971d9d3181bbcee
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758629"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-example-vb"></a>MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 예제 (VB)
이 예에서는 [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)및 [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) 메서드를 사용 하 여 제공 된 명령에 따라 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 의 레코드 포인터를 이동 합니다. 이 프로시저를 실행 하려면 MoveAny 프로시저가 필요 합니다.  
  
```  
'BeginMoveFirstVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    ' connection and recordset variables  
    Dim rstAuthors As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strSQLAuthors  
     ' record variables  
    Dim strMessage As String  
    Dim intCommand As Integer  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open recordset from Authors table  
    Set rstAuthors = New ADODB.Recordset  
    rstAuthors.CursorLocation = adUseClient  
    ' Use client cursor to enable AbsolutePosition property  
    strSQLAuthors = "Authors"  
    rstAuthors.Open strSQLAuthors, Cnxn, adOpenStatic, adLockReadOnly, adCmdTable  
  
    ' Show current record information and get user's method choice  
    Do  
        strMessage = "Name: " & rstAuthors!au_fname & " " & _  
            rstAuthors!au_lname & vbCr & "Record " & _  
            rstAuthors.AbsolutePosition & " of " & _  
            rstAuthors.RecordCount & vbCr & vbCr & _  
            "[1 - MoveFirst, 2 - MoveLast, " & vbCr & _  
            "3 - MoveNext, 4 - MovePrevious]"  
        intCommand = Val(Left(InputBox(strMessage), 1))  
  
         ' for exiting the loop  
        If intCommand < 1 Or intCommand > 4 Then  
            MsgBox "You either entered a non-number or canceled the input box. Exit the application."  
            Exit Do  
        End If  
  
        ' Use specified method while trapping for BOF and EOF  
        Select Case intCommand  
            Case 1  
                rstAuthors.MoveFirst  
            Case 2  
                rstAuthors.MoveLast  
            Case 3  
                rstAuthors.MoveNext  
                If rstAuthors.EOF Then  
                    MsgBox "Already at end of recordset!"  
                    rstAuthors.MoveLast  
                End If  
            Case 4  
                rstAuthors.MovePrevious  
                If rstAuthors.BOF Then  
                    MsgBox "Already at beginning of recordset!"  
                    rstAuthors.MoveFirst  
                End If  
        End Select  
    Loop  
  
    ' clean up  
    rstAuthors.Close  
    Cnxn.Close  
    Set rstAuthors = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstAuthors Is Nothing Then  
        If rstAuthors.State = adStateOpen Then rstAuthors.Close  
    End If  
    Set rstAuthors = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
  
'EndMoveFirstVB  
```  
  
## <a name="see-also"></a>참고 항목  
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
