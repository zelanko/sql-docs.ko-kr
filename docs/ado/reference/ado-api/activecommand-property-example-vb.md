---
title: "ActiveCommand 속성 예제 (VB) | Microsoft Docs"
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
helpviewer_keywords:
- ActiveCommand property [ADO], Visual Basic example
ms.assetid: 23b06499-62df-4f46-88eb-6da392f9b456
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bd034cdbd1b8188cb76344c1fb74f1b1e3fc9ba5
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="activecommand-property-example-vb"></a>ActiveCommand 속성 예제 (VB)
이 예제에서는 [ActiveCommand](../../../ado/reference/ado-api/activecommand-property-ado.md) 속성입니다.  
  
 서브루틴 제공할지는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 **ActiveCommand** 속성을 사용 하는 명령 텍스트 및 매개 변수를 만든 표시는 **레코드 집합**합니다.  
  
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
  
 **ActiveCommandXprint** 루틴만 제공 됩니다는 **레코드 집합** 명령 텍스트 및 매개 변수를 만든 인쇄 해야 아직 개체는 **레코드 집합**합니다. 때문에이 수행할 수 있습니다는 **레코드 집합** 개체의 **ActiveCommand** 속성 관련 된 생성 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체입니다.  
  
 **명령** 개체의 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 속성을 만든 매개 변수가 있는 명령이 생성 된 **레코드 집합**합니다. **명령** 개체의 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 명령의 매개 변수 자리 표시자에 대 한 대체 된 값을 생성 하는 컬렉션 ("**?**").  
  
 마지막으로 오류 메시지 또는 만든이의 이름 및 ID 인쇄 됩니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [ActiveCommand 속성 (ADO)](../../../ado/reference/ado-api/activecommand-property-ado.md)   
 [Command 개체 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
