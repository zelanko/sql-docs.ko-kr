---
description: 명령 개체 매개 변수
title: Command 개체 매개 변수 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Command object [ADO], parameters
ms.assetid: 10e7ef4a-78bf-4e91-931e-cbc6c065dd4c
author: rothja
ms.author: jroth
ms.openlocfilehash: 81fd1df9c0c7a49cc1b6b9e5bc804b905bd6294f
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806337"
---
# <a name="command-object-parameters"></a>명령 개체 매개 변수
이전 항목에서는 [간단한 명령 만들기 및 실행](./creating-and-executing-a-simple-command.md)에 대해 설명 했습니다. [명령](../../reference/ado-api/command-object-ado.md) 개체에 대 한 더 흥미로운 사용은 SQL 명령이 매개 변수화 된 다음 예제에 나와 있습니다. 이렇게 수정 하면 매번 매개 변수에 다른 값을 전달 하 여 명령을 다시 사용할 수 있습니다. **Command** 개체의 [준비 된 속성](../../reference/ado-api/prepared-property-ado.md) 속성이 **true**로 설정 되어 있기 때문에 ADO에서는 처음으로 실행 하기 전에 해당 공급자가 [CommandText](../../reference/ado-api/commandtext-property-ado.md) 에 지정 된 명령을 컴파일해야 합니다. 또한 컴파일된 명령을 메모리에 유지 합니다. 이렇게 하면 명령 실행이 처음 실행 될 때 약간 느리게 실행 되 고,이를 준비 하는 데 필요한 오버 헤드로 인해 성능이 저하 되지만 그 이후에 명령이 호출 될 때마다 성능이 향상 됩니다. 따라서 명령은 두 번 이상 사용 되는 경우에만 준비 해야 합니다.  
  
```  
'BeginManualParamCmd  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim objCmd As New ADODB.Command  
    Dim objParm1 As New ADODB.Parameter  
    Dim objRs As New ADODB.Recordset  
  
    ' Set the CommandText as a parameterized SQL query.  
    objCmd.CommandText = "SELECT OrderID, OrderDate, " & _  
                         "RequiredDate, ShippedDate " & _  
                         "FROM Orders " & _  
                         "WHERE CustomerID = ? " & _  
                         "ORDER BY OrderID"  
    objCmd.CommandType = adCmdText  
  
    ' Prepare command because we will be executing it more than once.  
    objCmd.Prepared = True  
  
    ' Create new parameter for CustomerID. Initial value is ALFKI.  
    Set objParm1 = objCmd.CreateParameter("CustId", adChar, _  
                    adParamInput, 5, "ALFKI")  
    objCmd.Parameters.Append objParm1  
  
    ' Connect to the data source.  
    Set objConn = GetNewConnection  
    objCmd.ActiveConnection = objConn  
  
    ' Execute once and display.  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    ' .Set new param value, re-execute command, and display.  
    objCmd("CustId") = "CACTU"  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    'clean up  
    objRs.Close  
    objConn.Close  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
    Set objParm1 = Nothing  
    Exit Sub  
  
ErrHandler:  
    'clean up  
    If objRs.State = adStateOpen Then  
        objRs.Close  
    End If  
  
    If objConn.State = adStateOpen Then  
        objConn.Close  
    End If  
  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
    Set objParm1 = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
'EndManualParamCmd  
  
'BeginNewConnection  
Private Function GetNewConnection() As ADODB.Connection  
    Dim oCn As New ADODB.Connection  
    Dim sCnStr As String  
  
    sCnStr = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _  
             "Integrated Security='SSPI';Initial Catalog='Northwind';"  
    oCn.Open sCnStr  
  
    If oCn.State = adStateOpen Then  
        Set GetNewConnection = oCn  
    End If  
  
End Function  
'EndNewConnection  
```  
  
 모든 공급자가 준비 된 명령을 지 원하는 것은 아닙니다. 공급자가 명령 준비를 지원 하지 않는 경우이 속성이 **True**로 설정 되 면 즉시 오류를 반환할 수 있습니다. 오류가 반환 되지 않으면 명령 준비 요청을 무시 하 고 **준비** 된 속성을 **false**로 설정 합니다.