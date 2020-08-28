---
description: 보기 및 필드 컬렉션 예제(VB)
title: Views 및 Fields 컬렉션 예제 (VB) | Microsoft Docs
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
- Views collection [ADOX], Visual Basic example
- Fields collection [ADOX]
ms.assetid: d8304849-3f80-4cf3-9425-529d2a8ebedd
author: rothja
ms.author: jroth
ms.openlocfilehash: 610ad3b837c7fc91cbfeba440b0fa2aea9fca81e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88982894"
---
# <a name="views-and-fields-collections-example-vb"></a>보기 및 필드 컬렉션 예제(VB)
다음 코드에서는 [명령](./command-property-adox.md) 속성과 [레코드 집합](../ado-api/recordset-object-ado.md) 개체를 사용 하 여 뷰에 대 한 필드 정보를 검색 하는 방법을 보여 줍니다.  
  
```  
' BeginViewFieldsVB  
Sub ViewFields()  
    On Error GoTo ViewFieldsError  
  
    Dim cnn As New ADODB.Connection  
    Dim rst As New ADODB.Recordset  
    Dim fld As ADODB.Field  
    Dim cat As New ADOX.Catalog  
  
    ' Open the Connection  
    cnn.Open _  
        "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Open the catalog  
    Set cat.ActiveConnection = cnn  
  
    ' Set the Source for the Recordset  
    Set rst.Source = cat.Views("AllCustomers").Command  
  
    ' Retrieve Field information  
    rst.Fields.Refresh  
    For Each fld In rst.Fields  
        Debug.Print fld.Name & ":" & fld.Type  
    Next  
  
    'Clean up  
    cnn.Close  
    Set cat = Nothing  
    Set rst = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
ViewFieldsError:  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
  
    Set cat = Nothing  
    Set rst = Nothing  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
' EndViewFieldsVB  
```  
  
## <a name="see-also"></a>참고 항목  
 [ActiveConnection 속성 (ADOX)](./activeconnection-property-adox.md)   
 [Catalog 개체 (ADOX)](./catalog-object-adox.md)   
 [Command 속성 (ADOX)](./command-property-adox.md)   
 [View 개체 (ADOX)](./view-object-adox.md)   
 [Views 컬렉션(ADOX)](./views-collection-adox.md)