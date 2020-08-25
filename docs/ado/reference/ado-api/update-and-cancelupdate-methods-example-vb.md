---
description: Update 및 CancelUpdate 메서드 예제(VB)
title: Update 및 CancelUpdate 메서드 예제 (VB) | Microsoft Docs
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
- CancelUpdate method [ADO]
- Update method [ADO], Visual Basic example
ms.assetid: 55bedd08-7440-4da4-b854-4ac9ef2fdedb
author: rothja
ms.author: jroth
ms.openlocfilehash: 71ce20eb1c1fc76643d4650080afdbb956cfe882
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777032"
---
# <a name="update-and-cancelupdate-methods-example-vb"></a>Update 및 CancelUpdate 메서드 예제(VB)
이 예제에서는 [CancelUpdate](./cancelupdate-method-ado.md) 메서드와 함께 [Update](./update-method.md) 메서드를 보여 줍니다.  
  
```  
'BeginUpdateVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
    ' recordset and connection variables  
    Dim rstEmployees As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strSQLEmployees As String  
     ' buffer variables  
    Dim strOldFirst As String  
    Dim strOldLast As String  
    Dim strMessage As String  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open recordset to enable changes  
    Set rstEmployees = New ADODB.Recordset  
    strSQLEmployees = "SELECT fname, lname FROM Employee ORDER BY lname"  
    rstEmployees.Open strSQLEmployees, Cnxn, adOpenKeyset, adLockOptimistic, adCmdText  
  
    ' Store original data  
    strOldFirst = rstEmployees!fname  
    strOldLast = rstEmployees!lname  
    ' Change data in edit buffer  
    rstEmployees!fname = "Linda"  
    rstEmployees!lname = "Kobara"  
  
    ' Show contents of buffer and get user input  
    strMessage = "Edit in progress:" & vbCr & _  
        "  Original data = " & strOldFirst & " " & _  
        strOldLast & vbCr & "  Data in buffer = " & _  
        rstEmployees!fname & " " & rstEmployees!lname & vbCr & vbCr & _  
        "Use Update to replace the original data with " & _  
        "the buffered data in the Recordset?"  
  
    If MsgBox(strMessage, vbYesNo) = vbYes Then  
        rstEmployees.Update  
    Else  
        rstEmployees.CancelUpdate  
    End If  
  
    ' show the resulting data  
    MsgBox "Data in recordset = " & rstEmployees!fname & " " & _  
       rstEmployees!lname  
  
    ' restore original data because this is a demonstration  
    If Not (strOldFirst = rstEmployees!fname And _  
           strOldLast = rstEmployees!lname) Then  
        rstEmployees!fname = strOldFirst  
        rstEmployees!lname = strOldLast  
        rstEmployees.Update  
    End If  
  
    ' clean up  
    rstEmployees.Close  
    Cnxn.Close  
    Set rstEmployees = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstEmployees Is Nothing Then  
        If rstEmployees.State = adStateOpen Then rstEmployees.Close  
    End If  
    Set rstEmployees = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndUpdateVB  
```  
  
 이 예제에서는 [AddNew](./addnew-method-ado.md) 메서드와 함께 **업데이트** 메서드를 보여 줍니다.  
  
```  
Attribute VB_Name = "Update"  
```  
  
## <a name="see-also"></a>참고 항목  
 [CancelUpdate 메서드 (ADO)](./cancelupdate-method-ado.md)   
 [레코드 집합 개체 (ADO)](./recordset-object-ado.md)   
 [Update 메서드](./update-method.md)