---
description: ActiveCommand 속성 예제(VB)
title: ActiveCommand 속성 예제 (VB) | Microsoft Docs
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
- ActiveCommand property [ADO], Visual Basic example
ms.assetid: 23b06499-62df-4f46-88eb-6da392f9b456
author: rothja
ms.author: jroth
ms.openlocfilehash: 4c2cd1df656d07b274fe000c427dd3eae07da76b
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759913"
---
# <a name="activecommand-property-example-vb"></a>ActiveCommand 속성 예제(VB)
이 예제에서는 [ActiveCommand](./activecommand-property-ado.md) 속성을 보여 줍니다.  
  
 서브루틴에는 **ActiveCommand** 속성을 사용 하 여 **레코드 집합**을 만든 명령 텍스트 및 매개 변수를 표시 하는 [레코드 집합](./recordset-object-ado.md) 개체가 제공 됩니다.  
  
```  
'BeginActiveCommandVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
        'recordset and connection variables  
    Dim cmd As ADODB.Command  
    Dim rst As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
        'record variables  
    Dim strPrompt As String  
    Dim strName As String  
  
    Set Cnxn = New ADODB.Connection  
    Set cmd = New ADODB.Command  
  
    strPrompt = "Enter an author's name (e.g., Ringer): "  
    strName = Trim(InputBox(strPrompt, "ActiveCommandX Example"))  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
  
        'create SQL command string  
    cmd.CommandText = "SELECT * FROM Authors WHERE au_lname = ?"  
    cmd.Parameters.Append cmd.CreateParameter("LastName", adChar, adParamInput, 20, strName)  
  
    Cnxn.Open strCnxn  
    cmd.ActiveConnection = Cnxn  
  
        'create the recordset by executing command string  
    Set rst = cmd.Execute(, , adCmdText)  
        'see the results  
    Call ActiveCommandXprint(rst)  
  
    ' clean up  
    Cnxn.Close  
    Set rst = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rst Is Nothing Then  
        If rst.State = adStateOpen Then rst.Close  
    End If  
    Set rst = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndActiveCommandVB  
```  
  
 **ActiveCommandXprint** 루틴에는 **레코드 집합** 개체만 제공 되지만 **레코드 집합**을 만든 명령 텍스트 및 매개 변수를 인쇄 해야 합니다. 이 작업은 **레코드 집합** 개체의 **ActiveCommand** 속성이 연결 된 [명령](./command-object-ado.md) 개체를 생성 하기 때문에 수행할 수 있습니다.  
  
 **Command** 개체의 [CommandText](./commandtext-property-ado.md) 속성은 **레코드 집합**을 만든 매개 변수가 있는 명령을 생성 합니다. **Command** 개체의 [Parameters](./parameters-collection-ado.md) 컬렉션은 명령의 매개 변수 자리 표시자 ("**?**")로 대체 된 값을 생성 합니다.  
  
 마지막으로 오류 메시지 또는 작성자의 이름과 ID가 출력 됩니다.  
  
```  
'BeginActiveCommandPrintVB  
Public Sub ActiveCommandXprint(rstp As ADODB.Recordset)  
  
    Dim strName As String  
  
    strName = rstp.ActiveCommand.Parameters.Item("LastName").Value  
  
    Debug.Print "Command text = '"; rstp.ActiveCommand.CommandText; "'"  
    Debug.Print "Parameter = '"; strName; "'"  
  
    If rstp.BOF = True Then  
       Debug.Print "Name = '"; strName; "', not found."  
    Else  
       Debug.Print "Name = '"; rstp!au_fname; " "; rstp!au_lname; _  
             "', author ID = '"; rstp!au_id; "'"  
    End If  
  
    rstp.Close  
    Set rstp = Nothing  
End Sub  
'EndActiveCommandPrintVB  
```  
  
## <a name="see-also"></a>관련 항목  
 [ActiveCommand 속성 (ADO)](./activecommand-property-ado.md)   
 [Command 개체 (ADO)](./command-object-ado.md)   
 [레코드 집합 개체(ADO)](./recordset-object-ado.md)