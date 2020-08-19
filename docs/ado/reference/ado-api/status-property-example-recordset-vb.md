---
description: Status 속성 예제(레코드 집합)(VB)
title: Status 속성 예제 (레코드 집합) (VB) | Microsoft Docs
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
- Status property [ADO Recordset], Visual Basic example
ms.assetid: e37b4d46-380d-4615-b4bb-e1a7b0851771
author: rothja
ms.author: jroth
ms.openlocfilehash: 83ee7fc06923a4e0010fab835ea05e00768cbb94
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441925"
---
# <a name="status-property-example-recordset-vb"></a>Status 속성 예제(레코드 집합)(VB)
이 예에서는 [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) 속성을 사용 하 여 일괄 처리 업데이트를 발생 하기 전에 일괄 처리 작업에서 수정 된 레코드를 표시 합니다.  
  
```  
'BeginStatusRecordsetVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
    ' connection and recordset variables  
    Dim rstTitles As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strSQLTitles As String  
  
     ' open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
     ' open recordset for batch update  
    Set rstTitles = New ADODB.Recordset  
    strSQLTitles = "Titles"  
    rstTitles.Open strSQLTitles, Cnxn, adOpenKeyset, adLockBatchOptimistic, adCmdTable  
  
    ' change the type of psychology titles  
    Do Until rstTitles.EOF  
        If Trim(rstTitles!Type) = "psychology" Then rstTitles!Type = "self_help"  
        rstTitles.MoveNext  
    Loop  
  
    ' display Title ID and status  
    rstTitles.MoveFirst  
    Do Until rstTitles.EOF  
        If rstTitles.Status = adRecModified Then  
            Debug.Print rstTitles!title_id & " - Modified"  
        Else  
            Debug.Print rstTitles!title_id  
        End If  
    rstTitles.MoveNext  
    Loop  
  
    ' clean up  
    rstTitles.Close  
    Cnxn.Close  
    Set rstTitles = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstTitles Is Nothing Then  
        If rstTitles.State = adStateOpen Then  
            ' Cancel the update because this is a demonstration  
            rstTitles.CancelBatch  
            rstTitles.Close  
        End If  
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
'EndStatusRecordsetVB  
```  
  
## <a name="see-also"></a>참고 항목  
 [Status 속성(ADO 레코드 집합)](../../../ado/reference/ado-api/status-property-ado-recordset.md)
