---
title: 명령을 라는 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2604fdc39789be2e0c86cc7d2cbc6491d55ba1ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701955"
---
# <a name="named-commands"></a>명명된 명령
[만들기 및 실행 하는 간단한 명령을](../../../ado/guide/data/creating-and-executing-a-simple-command.md) 명령을 실행 하는 방법을 보여 줍니다. 다른 방법이 있습니다: 명명 된 명령을 하 고 그런 다음이 명령에서 직접 명명 된 호출 수를 **연결** 개체 (에 할당 된를 **ActiveConnection** 속성은 **명령** 개체). 명령 이름에 이름을 할당 의미는 **이름** 의 속성을 **명령** 개체. 예:  
  
```  
objCmd.Name = "GetCustomers"  
objCmd.ActiveConnection = objConn  
objConn.GetCustomers objRs  
```  
  
 명명 된 명령에서 "사용자 지정 메서드" 것 처럼 작동 합니다 **연결** 개체입니다. 명령의 결과이 "사용자 지정 메서드"를 out 매개 변수로 반환 됩니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
