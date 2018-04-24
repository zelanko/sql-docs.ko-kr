---
title: 항목 속성 예제 (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Item property [ADO], Visual Basic example
ms.assetid: b4476603-691b-4081-8797-a3d0b331dce5
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cf4f6c78b5dd6c93dfcb0ae43a5fa1b271c64c2d
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="item-property-example-vb"></a>항목 속성 예제 (VB)
이 예제에서는 방법을 [항목](../../../ado/reference/ado-api/item-property-ado.md) 속성이 컬렉션의 멤버에 액세스 합니다. 열고는 ***작성자*** 목차는 ***Pubs*** 매개 변수가 있는 명령 사용 하 여 데이터베이스입니다.  
  
 액세스 하는 데이터베이스에 대해 실행 된 명령에서 매개 변수는 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체의 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 인덱스 및 이름을 사용 하 여 컬렉션입니다. 반환 된 필드 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 다음 해당 개체에서 액세스 하는 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 인덱스 및 이름을 사용 하 여 컬렉션입니다.  
  
```  
'BeginItemVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    Dim Cnxn As ADODB.Connection  
    Dim rstAuthors As ADODB.Recordset  
    Dim cmd As ADODB.Command  
    Dim prm As ADODB.Parameter  
    Dim fld As ADODB.Field  
    Dim strCnxn As String  
  
    Dim ix As Integer  
    Dim limit As Long  
    Dim Column(0 To 8) As Variant  
  
    Set Cnxn = New ADODB.Connection  
    Set rstAuthors = New ADODB.Recordset  
    Set cmd = New ADODB.Command  
  
    'Set the array with the Authors table field (column) names  
    Column(0) = "au_id"  
    Column(1) = "au_lname"  
    Column(2) = "au_fname"  
    Column(3) = "phone"  
    Column(4) = "address"  
    Column(5) = "city"  
    Column(6) = "state"  
    Column(7) = "zip"  
    Column(8) = "contract"  
  
    cmd.CommandText = "SELECT * FROM Authors WHERE state = ?"  
    Set prm = cmd.CreateParameter("ItemXparm", adChar, adParamInput, 2, "CA")  
    cmd.Parameters.Append prm  
     ' set connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
    cmd.ActiveConnection = Cnxn  
     ' open recordset  
    rstAuthors.Open cmd, , adOpenStatic, adLockReadOnly  
    'Connection and CommandType are omitted because  
    'a Command object is provided  
  
    Debug.Print "The Parameters collection accessed by index..."  
    Set prm = cmd.Parameters.Item(0)  
    Debug.Print "Parameter name = '"; prm.Name; "', value = '"; prm.Value; "'"  
    Debug.Print  
  
    Debug.Print "The Parameters collection accessed by name..."  
    Set prm = cmd.Parameters.Item("ItemXparm")  
    Debug.Print "Parameter name = '"; prm.Name; "', value = '"; prm.Value; "'"  
    Debug.Print  
  
    Debug.Print "The Fields collection accessed by index..."  
  
    rstAuthors.MoveFirst  
    limit = rstAuthors.Fields.Count - 1  
    For ix = 0 To limit  
       Set fld = rstAuthors.Fields.Item(ix)  
       Debug.Print "Field "; ix; ": Name = '"; fld.Name; _  
                   "', Value = '"; fld.Value; "'"  
    Next ix  
  
    Debug.Print  
  
    Debug.Print "The Fields collection accessed by name..."  
  
    rstAuthors.MoveFirst  
    For ix = 0 To 8  
       Set fld = rstAuthors.Fields.Item(Column(ix))  
       Debug.Print "Field name = '"; fld.Name; "', Value = '"; fld.Value; "'"  
    Next ix  
  
    ' clean up  
    rstAuthors.Close  
    Cnxn.Close  
    Set rstAuthors = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstAuthors Is Nothing Then  
        If rstAuthors.State = adStateOpen Then rstAuthors.Close  
    End If  
    Set rstAuthors = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    Set cmd = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
'EndItemVB  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Command 개체 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Fields 컬렉션 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Item 속성 (ADO)](../../../ado/reference/ado-api/item-property-ado.md)   
 [Parameters 컬렉션 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
