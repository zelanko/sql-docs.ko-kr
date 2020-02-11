---
title: GetRows 메서드 예제 (VB) | Microsoft Docs
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
- Getrows method [ADO], Visual Basic example
ms.assetid: 9f7c78bb-7bb8-4c4f-8e5a-4d3bfc8a208f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fedde638e343281c5d3810cc80c9ba8db820e839
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67918458"
---
# <a name="getrows-method-example-vb"></a>GetRows 메서드 예제(VB)
이 예에서는 [GetRows](../../../ado/reference/ado-api/getrows-method-ado.md) 메서드를 사용 하 여 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 에서 지정 된 수의 행을 검색 하 고 결과 데이터로 배열을 채웁니다. **Getrows** 메서드는 [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 에 도달 했거나 **getrows** 에서 다른 사용자가 삭제 한 레코드를 검색 하려고 시도 하는 경우 두 경우에 원하는 수의 행 보다 더 작은 값을 반환 합니다. 함수는 두 번째 사례가 발생 하는 경우에만 **False** 를 반환 합니다. GetRowsOK 함수는이 프로시저를 실행 하는 데 필요 합니다.  
  
```  
'BeginGetRowsVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
     ' connection and recordset variables  
    Dim rstEmployees As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strSQLEmployees As String  
    Dim strCnxn As String  
    ' array variable  
    Dim arrEmployees As Variant  
    ' detail variables  
    Dim strMessage As String  
    Dim intRows As Integer  
    Dim intRecord As Integer  
  
    ' open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' open recordset client-side to enable RecordCount  
    Set rstEmployees = New ADODB.Recordset  
    strSQLEmployees = "SELECT fName, lName, hire_date FROM Employee ORDER BY lName"  
    rstEmployees.Open strSQLEmployees, Cnxn, adOpenStatic, adLockReadOnly, adCmdText  
  
    ' get user input for number of rows  
    Do  
        strMessage = "Enter number of rows to retrieve:"  
        intRows = Val(InputBox(strMessage))  
  
          ' if bad user input exit the loop  
        If intRows <= 0 Then  
            MsgBox "Please enter a positive number", vbOKOnly, "Not less than zero!"  
        ' if number of requested records is over the total  
        ElseIf intRows > rstEmployees.RecordCount Then  
            MsgBox "Not enough records in Recordset to retrieve " & intRows & " rows.", _  
            vbOKOnly, "Over the available total"  
        Else  
            Exit Do  
        End If  
    Loop  
  
      ' else put the data in an array and print  
    arrEmployees = rstEmployees.GetRows(intRows)  
  
    Dim x As Integer, y As Integer  
  
    For x = 0 To intRows - 1  
        For y = 0 To 2  
            Debug.Print arrEmployees(y, x) & " ";  
        Next y  
        Debug.Print vbCrLf  
    Next x  
  
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
'EndGetRowsVB  
```  
  
## <a name="see-also"></a>참고 항목  
 [GetRows 메서드 (ADO)](../../../ado/reference/ado-api/getrows-method-ado.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
