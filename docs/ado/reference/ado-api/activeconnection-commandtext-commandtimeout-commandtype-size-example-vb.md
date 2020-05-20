---
title: 저장 프로시저 속성 예제 (VB) | Microsoft Docs
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
- Size property [ADO], Visual Basic example
- CommandTimeout property [ADO], Visual Basic example
- CommandText property [ADO], Visual Basic example
- ActiveConnection property [ADO], Visual Basic example
- Direction property [ADO], Visual Basic example
ms.assetid: dade4531-0bcc-4a52-8f86-b110ba2a3f9d
author: rothja
ms.author: jroth
ms.openlocfilehash: a90ae6ceca85a314de5112f02b2389e26bfa5bdc
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760749"
---
# <a name="activeconnection-commandtext-commandtimeout-commandtype-size-and-direction-properties-example-vb"></a>ActiveConnection, CommandText, CommandTimeout, CommandType, Size 및 Direction 속성 예제 (VB)
이 예에서는 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md), [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md), [CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md), [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md), [Size](../../../ado/reference/ado-api/size-property-ado-parameter.md)및 [Direction](../../../ado/reference/ado-api/direction-property.md) 속성을 사용 하 여 저장 프로시저를 실행 합니다.  
  
```  
'BeginActiveConnectionVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset, command and connection variables  
    Dim Cnxn As ADODB.Connection  
    Dim cmdByRoyalty As ADODB.Command  
    Dim prmByRoyalty As ADODB.Parameter  
    Dim rstByRoyalty As ADODB.Recordset  
    Dim rstAuthors As ADODB.Recordset  
    Dim strCnxn As String  
    Dim strSQLAuthors As String  
    Dim strSQLByRoyalty As String  
     'record variables  
    Dim intRoyalty As Integer  
    Dim strAuthorID As String  
  
    ' Define a command object for a stored procedure  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    Set cmdByRoyalty = New ADODB.Command  
    Set cmdByRoyalty.ActiveConnection = Cnxn  
    ' Set the criteria  
    strSQLByRoyalty = "byroyalty"  
    cmdByRoyalty.CommandText = strSQLByRoyalty  
    cmdByRoyalty.CommandType = adCmdStoredProc  
    cmdByRoyalty.CommandTimeout = 15  
  
    ' Define the stored procedure's input parameter  
    intRoyalty = Trim(InputBox("Enter royalty:"))  
    Set prmByRoyalty = New ADODB.Parameter  
    prmByRoyalty.Type = adInteger  
    prmByRoyalty.Size = 3  
    prmByRoyalty.Direction = adParamInput  
    prmByRoyalty.Value = intRoyalty  
  
    cmdByRoyalty.Parameters.Append prmByRoyalty  
  
    ' Create a recordset by executing the command.  
    Set rstByRoyalty = cmdByRoyalty.Execute()  
  
    ' Open the Authors Table to get author names for display  
    Set rstAuthors = New ADODB.Recordset  
    strSQLAuthors = "Authors"  
  
    'rstAuthors.Open strSQLAuthors, strCnxn, , , adCmdTable  
    rstAuthors.Open strSQLAuthors, strCnxn, adOpenForwardOnly, adLockReadOnly, adCmdTable  
    'the above two lines of code are identical as the default values for  
    'CursorType and LockType arguments match those shown  
  
    ' Print the recordset and add author names from Table  
    Debug.Print "Authors with " & intRoyalty & _  
       " percent royalty"  
  
    Do Until rstByRoyalty.EOF  
        strAuthorID = rstByRoyalty!au_id  
        Debug.Print , rstByRoyalty!au_id & ", ";  
        rstAuthors.Filter = "au_id = '" & strAuthorID & "'"  
        Debug.Print rstAuthors!au_fname & " " & _  
            rstAuthors!au_lname  
        rstByRoyalty.MoveNext  
    Loop  
  
    ' clean up  
    rstAuthors.Close  
    rstByRoyalty.Close  
    Cnxn.Close  
    Set rstAuthors = Nothing  
    Set rstByRoyalty = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstAuthors Is Nothing Then  
        If rstAuthors.State = adStateOpen Then rstAuthors.Close  
    End If  
    Set rstAuthors = Nothing  
  
    If Not rstByRoyalty Is Nothing Then  
        If rstByRoyalty.State = adStateOpen Then rstByRoyalty.Close  
    End If  
    Set rstByRoyalty = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndActiveConnectionVB  
```  
  
## <a name="see-also"></a>참고 항목  
 [ActiveCommand 속성 (ADO)](../../../ado/reference/ado-api/activecommand-property-ado.md)   
 [Command 개체 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [CommandText 속성 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandTimeout 속성 (ADO)](../../../ado/reference/ado-api/commandtimeout-property-ado.md)   
 [CommandType 속성 (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md)   
 [Connection 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Direction 속성](../../../ado/reference/ado-api/direction-property.md)   
 [Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)   
 [Record 개체 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Size 속성(ADO 매개 변수)](../../../ado/reference/ado-api/size-property-ado-parameter.md)
