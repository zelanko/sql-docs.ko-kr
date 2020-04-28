---
title: AbsolutePosition 및 CursorLocation 속성 예제 (VB) | Microsoft Docs
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
- AbsolutePosition property [ADO], Visual Basic example
- CursorLocation property [ADO], Visual Basic example
ms.assetid: c4755799-c60a-4b5e-a01f-b85dd0e0a7f9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 29307c3764a81f60ad02108ba498daab85bc0b3f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67921711"
---
# <a name="absoluteposition-and-cursorlocation-properties-example-vb"></a>AbsolutePosition 및 CursorLocation 속성 예제 (VB)
이 예에서는 [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) 속성을 통해 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)의 모든 레코드를 열거 하는 루프의 진행률을 추적할 수 있는 방법을 보여 줍니다. [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 사용 하 여 커서를 클라이언트 커서로 설정 하 여 **AbsolutePosition** 속성을 사용 하도록 설정 합니다.  
  
```  
'BeginAbsolutePositionVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim rstEmployees As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strSQL As String  
        'record variables  
    Dim strMessage As String  
  
    'Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open Employee recordset with  
    ' Client-side cursor to enable AbsolutePosition property  
    Set rstEmployees = New ADODB.Recordset  
    strSQL = "employee"  
    rstEmployees.Open strSQL, strCnxn, adUseClient, adLockReadOnly, adCmdTable  
  
    ' Enumerate Recordset  
    Do While Not rstEmployees.EOF  
        ' Display current record information  
        strMessage = "Employee: " & rstEmployees!lname & vbCr & _  
            "(record " & rstEmployees.AbsolutePosition & _  
            " of " & rstEmployees.RecordCount & ")"  
        If MsgBox(strMessage, vbOKCancel) = vbCancel Then Exit Do  
        rstEmployees.MoveNext  
    Loop  
  
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
'EndAbsolutePositionVB  
```  
  
## <a name="see-also"></a>참고 항목  
 [AbsolutePosition 속성 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
 [CursorLocation 속성 (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
