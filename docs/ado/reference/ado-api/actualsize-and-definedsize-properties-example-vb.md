---
title: "ActualSize 및 DefinedSize 속성 예제 (VB) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: VB
helpviewer_keywords:
- DefinedSize property [ADO], Visual Basic example
- ActualSize property [ADO], Visual Basic example
ms.assetid: bff2c273-b535-4b32-83b3-0336a406859c
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7bcc7800bdd9554f6cd7d5d80e75df52b40249e3
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="actualsize-and-definedsize-properties-example-vb"></a>ActualSize 및 DefinedSize 속성 예제 (VB)
사용 하 여이 예제는 [ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md) 및 [DefinedSize](../../../ado/reference/ado-api/definedsize-property.md) 속성을 정의 된 크기 및 필드의 실제 크기를 표시 합니다.  
  
```  
'BeginActualSizeVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim rstStores As ADODB.Recordset  
    Dim SQLStores As String  
    Dim strCnxn As String  
     'record variables  
    Dim strMessage As String  
  
    ' Open a recordset for the Stores table  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Northwind';Integrated Security='SSPI';"  
    Set rstStores = New ADODB.Recordset  
  
    SQLStores = "Suppliers"  
    rstStores.Open SQLStores, strCnxn, adOpenForwardOnly, adLockReadOnly, adCmdTable  
    'the above two lines of code are identical as the default values for  
    'CursorType and LockType arguments match those indicated  
  
    ' Loop through the recordset displaying the contents  
    ' of the store_name field, the field's defined size,  
    ' and its actual size.  
    rstStores.MoveFirst  
  
    Do Until rstStores.EOF  
        strMessage = "Company name: " & rstStores!CompanyName & _  
        vbCrLf & "Defined size: " & _  
        rstStores!CompanyName.DefinedSize & _  
        vbCrLf & "Actual size: " & _  
        rstStores!CompanyName.ActualSize & vbCrLf  
  
        MsgBox strMessage, vbOKCancel, "ADO ActualSize Property (Visual Basic)"  
        rstStores.MoveNext  
    Loop  
  
    ' clean up  
    rstStores.Close  
    Set rstStores = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstStores Is Nothing Then  
        If rstStores.State = adStateOpen Then rstStores.Close  
    End If  
    Set rstStores = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndActualSizeVB  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ActualSize 속성 (ADO)](../../../ado/reference/ado-api/actualsize-property-ado.md)   
 [DefinedSize 속성](../../../ado/reference/ado-api/definedsize-property.md)   
 [Field 개체](../../../ado/reference/ado-api/field-object.md)
