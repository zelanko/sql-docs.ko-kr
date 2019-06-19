---
title: StayInSync 속성 예제 (VB) | Microsoft Docs
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
- StayInSync property [ADO], Visual Basic example
ms.assetid: b682bcc3-04b3-42b0-86f4-c17e0cd29baf
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b8c271409657aa48ea1187c719254f2eef6b89b8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711035"
---
# <a name="stayinsync-property-example-vb"></a>StayInSync 속성 예제(VB)
이 예제에서는 하는 방법을 [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md) 속성을 계층적 구조에서 액세스할 행을 용이 하 게 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.  
  
 외부 루프는 각 저자의 성 및 이름, 상태 및 식별을 표시합니다. 추가 된 **레코드 집합** 에서 각 행이 검색에 대 한 합니다 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션에 자동으로 할당 하 고 **rstTitleAuthor** 여는 **StayInSync**  속성 때마다 부모 **레코드 집합** 새 행으로 이동 합니다. 내부 루프에는 추가 된 레코드 집합의 각 행에서 4 개의 필드가 표시 됩니다.  
  
```  
'BeginStayInSyncVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    Dim Cnxn As ADODB.Connection  
    Dim rst As ADODB.Recordset  
    Dim rstTitleAuthor As New ADODB.Recordset  
    Dim strCnxn As String  
  
    ' Open the connection with Data Shape attributes  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider=MSDataShape;Data Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Create a recordset  
    Set rst = New ADODB.Recordset  
    rst.StayInSync = True  
    rst.Open "SHAPE {select * from Authors} " & _  
                   "APPEND ( { select * from titleauthor} AS chapTitleAuthor " & _  
                   "RELATE au_id TO au_id) ", Cnxn, , , adCmdText  
  
    Set rstTitleAuthor = rst("chapTitleAuthor").Value  
    Do Until rst.EOF  
        Debug.Print rst!au_fname & " " & rst!au_lname & " " & _  
                   rst!State & " " & rst!au_id  
  
        Do Until rstTitleAuthor.EOF  
            Debug.Print rstTitleAuthor(0) & " " & rstTitleAuthor(1) & " " & _  
                   rstTitleAuthor(2) & " " & rstTitleAuthor(3)  
            rstTitleAuthor.MoveNext  
        Loop  
  
        rst.MoveNext  
    Loop  
  
    ' Clean up  
    rst.Close  
    Cnxn.Close  
    Set rst = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' Clean up  
    If Not rst Is Nothing Then  
        If rst.State = adStateOpen Then rst.Close  
    End If  
    Set rst = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndStayInSyncVB  
```  
  
## <a name="see-also"></a>관련 항목  
 [필드 컬렉션 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [StayInSync 속성](../../../ado/reference/ado-api/stayinsync-property.md)
