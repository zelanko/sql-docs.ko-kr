---
title: 입력 속성 예제 (필드) (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Type property [field] [ADO], Visual Basic example
ms.assetid: accb72f5-a3bd-4a7e-92b6-6da0783b4b75
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 700ceebeb78f1cda3d609255bd5406fd711900f1
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35282642"
---
# <a name="type-property-example-field-vb"></a>형식 속성 예제 (필드) (VB)
이 예제에서는 [형식](../../../ado/reference/ado-api/type-property-ado.md) 속성의 값에 해당 하는 상수 이름을 표시 하 여는 [형식](../../../ado/reference/ado-api/type-property-ado.md) 모든 속성은 [필드](../../../ado/reference/ado-api/field-object.md) 개체에 ***직원*** 테이블입니다. FieldType 함수는이 절차를 실행 하려면 필요 합니다.  
  
```  
'BeginTypeFieldVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
    Dim Cnxn As ADODB.Connection  
    Dim rstEmployees As ADODB.Recordset  
    Dim fld As ADODB.Field  
    Dim strCnxn As String  
    Dim strSQLEmployee As String  
    Dim FieldType As String  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open recordset with data from Employees table  
    Set rstEmployees = New ADODB.Recordset  
    strSQLEmployee = "employee"  
    rstEmployees.Open strSQLEmployee, Cnxn, , , adCmdTable  
    'rstEmployees.Open strSQLEmployee, Cnxn, adOpenStatic, adLockReadOnly, adCmdTable  
     ' the above two lines of code are identical  
  
    Debug.Print "Fields in Employees Table:" & vbCr  
  
    ' Enumerate Fields collection of Employees table  
    For Each fld In rstEmployees.Fields  
        ' translate field-type code to text  
        Select Case fld.Type  
            Case adChar  
               FieldType = "adChar"  
            Case adVarChar  
               FieldType = "adVarChar"  
            Case adSmallInt  
               FieldType = "adSmallInt"  
            Case adUnsignedTinyInt  
               FieldType = "adUnsignedTinyInt"  
            Case adDBTimeStamp  
               FieldType = "adDBTimeStamp"  
        End Select  
        ' show results  
        Debug.Print "  Name: " & fld.Name & vbCr & _  
          "  Type: " & FieldType & vbCr  
    Next fld  
  
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
  
    Set fld = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndTypeFieldVB  
  
Attribute VB_Name = "TypeField"  
```  
  
## <a name="see-also"></a>관련 항목  
 [Field 개체](../../../ado/reference/ado-api/field-object.md)   
 [Type 속성(ADO)](../../../ado/reference/ado-api/type-property-ado.md)
