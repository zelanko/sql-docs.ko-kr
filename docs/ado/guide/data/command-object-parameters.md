---
title: 개체 매개 변수를 명령 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f4fb4128333f1fdc5865186a202188fc64b6109f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47701741"
---
# <a name="command-object-parameters"></a>명령 개체 매개 변수
이전에 설명 된 항목 [만들고 간단한 명령 실행](../../../ado/guide/data/creating-and-executing-a-simple-command.md)합니다. 더 흥미로운 하는 데는 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체는 SQL 명령의 매개 변수가 다음 예제에 표시 됩니다. 이 수정 될 때마다 매개 변수에 대해 다른 값에서 전달 하는 명령은 다시 사용할 수 있습니다. 때문에 합니다 [준비 속성](../../../ado/reference/ado-api/prepared-property-ado.md) 속성을 **명령** 개체로 설정 됩니다 **true**, ADO 공급자에 지정 된 명령을 걸립니다 [ CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 처음으로 실행 하기 전에 합니다. 또한 메모리에서 컴파일된 명령 또한 유지 합니다. 이 속도 느려집니다 명령의 실행 약간는 첫 번째 있지만 명령 이후에 호출 될 때마다 향상 된 성능이에서 결과 준비 하는 데 필요한 오버 헤드로 인해 실행 됩니다. 따라서 여러 번 사용 될 경우에 명령 준비 해야 합니다.  
  
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
  
 준비 된 명령을 지원 하지 않는 공급자입니다. 이 속성이 즉시 오류가 공급자 명령 준비를 지원 하지 않는 경우 반환할 수 있습니다 **True**합니다. 오류를 반환 하지는 않습니다, 명령 및 집합을 준비 하려면 요청을 무시 합니다 **Prepared** 속성을 **false**합니다.
