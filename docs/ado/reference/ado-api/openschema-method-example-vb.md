---
description: OpenSchema 메서드 예제(VB)
title: OpenSchema 메서드 예제 (VB) | Microsoft Docs
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
- OpenSchema method [ADO], Visual Basic example
ms.assetid: 455a02f0-8143-4562-8648-8fb45ffd334c
author: rothja
ms.author: jroth
ms.openlocfilehash: e3c576f5cd06b5fe075ca60a06ad1cc8877c49b4
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773752"
---
# <a name="openschema-method-example-vb"></a>OpenSchema 메서드 예제(VB)
이 예에서는 [OpenSchema](./openschema-method.md) 메서드를 사용 하 여 ***Pubs*** 데이터베이스에 있는 각 테이블의 이름 및 유형을 표시 합니다.  
  
```  
'BeginOpenSchemaVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    Dim Cnxn As ADODB.Connection  
    Dim rstSchema As ADODB.Recordset  
    Dim strCnxn As String  
  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    Set rstSchema = Cnxn.OpenSchema(adSchemaTables)  
  
    Do Until rstSchema.EOF  
        Debug.Print "Table name: " & _  
            rstSchema!TABLE_NAME & vbCr & _  
            "Table type: " & rstSchema!TABLE_TYPE & vbCr  
        rstSchema.MoveNext  
    Loop  
  
    ' clean up  
    rstSchema.Close  
    Cnxn.Close  
    Set rstSchema = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstSchema Is Nothing Then  
        If rstSchema.State = adStateOpen Then rstSchema.Close  
    End If  
    Set rstSchema = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndOpenSchemaVB  
```  
  
 이 예에서는 **OpenSchema** 메서드 ***조건*** 인수에서 TABLE_TYPE 쿼리 제약 조건을 지정 합니다. 따라서 ***Pubs*** 데이터베이스에 지정 된 뷰에 대 한 스키마 정보만 반환 됩니다. 그런 다음이 예에서는 각 테이블의 이름 및 유형을 표시 합니다.  
  
```  
Attribute VB_Name = "OpenSchema"  
```  
  
## <a name="see-also"></a>참고 항목  
 [OpenSchema 메서드](./openschema-method.md)   
 [레코드 집합 개체(ADO)](./recordset-object-ado.md)