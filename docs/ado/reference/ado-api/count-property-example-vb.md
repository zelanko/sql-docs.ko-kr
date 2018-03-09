---
title: "Count 속성 예제 (VB) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Count property [ADO], Visual Basic example
ms.assetid: 35033910-623b-449a-a57d-baff3ed5ab8f
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4ab29cd1d57ebdb721085c7f743d96b2c0052ea6
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="count-property-example-vb"></a>Count 속성 예제 (VB)
이 예제에서는 [Count](../../../ado/reference/ado-api/count-property-ado.md) 의 두 컬렉션을 사용 하 여 속성의 ***직원*** 데이터베이스입니다. 속성 각 컬렉션의 개체 수를 가져오고 이러한 컬렉션을 열거 하는 루프에 대 한 상한값을 설정 합니다. 사용 하지 않고 해당이 컬렉션을 열거 하는 다른 방법은 **Count** 속성을 사용 하려는 것 `For Each...Next` 문.  
  
```  
'BeginCountVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    ' recordset and connection variables  
    Dim rstEmployees As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strSQLEmployees As String  
    Dim strCnxn As String  
  
    Dim intLoop As Integer  
  
    ' Open a connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Northwind';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open recordset with data from Employee table  
    Set rstEmployees = New ADODB.Recordset  
    strSQLEmployees = "Employee"  
    'rstEmployees.Open strSQLEmployee, Cnxn, , , adCmdTable  
    rstEmployees.Open strSQLEmployees, Cnxn, adOpenForwardOnly, adLockReadOnly, adCmdTable  
    'the above two lines opening the recordset are identical as  
    'the default values for CursorType and LockType arguments match those specified  
  
    ' Print information about Fields collection  
    Debug.Print rstEmployees.Fields.Count & " Fields in Employee"  
  
    For intLoop = 0 To rstEmployees.Fields.Count - 1  
        Debug.Print "   " & rstEmployees.Fields(intLoop).Name  
    Next intLoop  
  
    ' Print information about Properties collection  
    Debug.Print rstEmployees.Properties.Count & " Properties in Employee"  
  
    For intLoop = 0 To rstEmployees.Properties.Count - 1  
        Debug.Print "   " & rstEmployees.Properties(intLoop).Name  
    Next intLoop  
  
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
'EndCountVB  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Count 속성(ADO)](../../../ado/reference/ado-api/count-property-ado.md)
