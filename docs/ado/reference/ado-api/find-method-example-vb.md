---
description: Find 메서드 예제(VB)
title: Find 메서드 예제 (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Find method [ADO], Visual Basic example
ms.assetid: bbf27dcc-9815-4e2f-8ea8-b8c9fe6dedd6
author: rothja
ms.author: jroth
ms.openlocfilehash: 88d21354042ccccae5e165823fa738fa071db3e5
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88972884"
---
# <a name="find-method-example-vb"></a>Find 메서드 예제(VB)
이 예에서는 [레코드 집합](./recordset-object-ado.md) 개체의 [Find](./find-method-ado.md) 메서드를 사용 하 여 ***Pubs*** 데이터베이스의 비즈니스 타이틀 수를 찾고 계산 합니다. 이 예에서는 기본 공급자가 유사한 기능을 지원 하지 않는다고 가정 합니다.  
  
```  
'BeginFindVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
     ' connection and recordset variables  
    Dim Cnxn As New ADODB.Connection  
    Dim rstTitles As New ADODB.Recordset  
    Dim strCnxn As String  
    Dim strSQLTitles As String  
  
     ' record variables  
    Dim mark As Variant  
    Dim count As Integer  
  
     ' open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' open recordset with default parameters which are  
    ' sufficient to search forward through a Recordset  
    Set rstTitles = New ADODB.Recordset  
    strSQLTitles = "SELECT title_id FROM titles"  
    rstTitles.Open strSQLTitles, Cnxn, adOpenStatic, adLockReadOnly, adCmdText  
  
    count = 0  
    rstTitles.Find "title_id LIKE 'BU%'"  
  
    Do While Not rstTitles.EOF  
        'continue if last find succeeded  
        Debug.Print "Title ID: "; rstTitles!title_id  
        'count the last title found  
        count = count + 1  
        ' note current position  
        mark = rstTitles.Bookmark  
        rstTitles.Find "title_id LIKE 'BU%'", 1, adSearchForward, mark  
        ' above code skips current record to avoid finding the same row repeatedly;  
        ' last arg (bookmark) is redundant because Find searches from current position  
    Loop  
  
    Debug.Print "The number of business titles is " & count  
  
    ' clean up  
    rstTitles.Close  
    Cnxn.Close  
    Set rstTitles = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstTitles Is Nothing Then  
        If rstTitles.State = adStateOpen Then rstTitles.Close  
    End If  
    Set rstTitles = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndFindVB  
```  
  
## <a name="see-also"></a>참고 항목  
 [Find 메서드 (ADO)](./find-method-ado.md)   
 [레코드 집합 개체(ADO)](./recordset-object-ado.md)