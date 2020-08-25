---
description: 명명된 명령
title: 명명 된 명령 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- named commands [ADO]
- commands [ADO]
ms.assetid: 5a0ec8f9-5ba3-4f9f-b80d-2073aa049586
author: rothja
ms.author: jroth
ms.openlocfilehash: 0c5b5f21c1af3a3438b9e00cd00f4ed2baf338e2
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88805800"
---
# <a name="named-commands"></a>명명된 명령
[간단한 명령을 만들고 실행](./creating-and-executing-a-simple-command.md) 하면 명령을 실행 하는 한 가지 방법이 표시 됩니다. 또 다른 방법으로, 명명 된 명령으로 만든 다음 **연결** 개체 ( **명령** 개체의 **ActiveConnection** 속성에 할당 됨)에서 직접이 명명 된 명령을 호출할 수 있습니다. 명령 이름 지정은 **명령** 개체의 **name** 속성에 이름을 할당 하는 것을 의미 합니다. 예를 들면 다음과 같습니다.  
  
```  
objCmd.Name = "GetCustomers"  
objCmd.ActiveConnection = objConn  
objConn.GetCustomers objRs  
```  
  
 명명 된 명령은 **연결** 개체에 대 한 "사용자 지정 메서드" 처럼 작동 합니다. 명령의 결과는이 "사용자 지정 메서드"의 출력 매개 변수로 반환 됩니다.  
  
 다음 예제에서는이 기능을 보여 줍니다.  
  
```  
'BeginNamedCmd  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim objCmd As New ADODB.Command  
    Dim objRs As New ADODB.Recordset  
  
    ' Connect to the data source.  
    Set objConn = GetNewConnection  
  
    objCmd.CommandText = "SELECT CustomerID, CompanyName FROM Customers"  
    objCmd.CommandType = adCmdText  
  
    'Name the command.  
    objCmd.Name = "GetCustomers"  
  
    objCmd.ActiveConnection = objConn  
  
    ' Execute using Command.Name from the Connection.  
    objConn.GetCustomers objRs  
  
    ' Display.  
    Do While Not objRs.EOF  
        Debug.Print objRs(0) & vbTab & objRs(1)  
        objRs.MoveNext  
    Loop  
  
    'clean up  
    objRs.Close  
    objConn.Close  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
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
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
'EndNamedCmd  
```  
  
## <a name="see-also"></a>참고 항목  
 [연결 개체(ADO)](../../reference/ado-api/connection-object-ado.md)