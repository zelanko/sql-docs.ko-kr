---
title: Command 및 CommandText 속성 예제 (VB) | Microsoft Docs
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
- CommandText property [ADOX], Visual Basic example
- Command property [ADOX], Visual Basic example
ms.assetid: 413263a8-05c0-4404-929d-69f82b987ba3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 742f00402a553d8f918e0de0c3aad0f6c6e4af64
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63180187"
---
# <a name="command-and-commandtext-properties-example-vb"></a>Command 및 CommandText 속성 예제(VB)
다음 코드를 사용 하는 방법에 설명 합니다 [명령](../../../ado/reference/adox-api/command-property-adox.md) 프로시저의 텍스트를 업데이트 하는 속성입니다.  
  
```  
' BeginProcedureTextVB  
Sub Main()  
    On Error GoTo ProcedureTextError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim cmd As New ADODB.Command  
  
    ' Open the connection.  
    cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Open the catalog.  
    Set cat.ActiveConnection = cnn  
  
    ' Get the command.  
    Set cmd = cat.Procedures("CustomerById").Command  
  
    ' Update the CommandText.  
    cmd.CommandText = "Select CustomerId, CompanyName, ContactName " & _  
        "From Customers " & _  
        "Where CustomerId = [CustId]"  
  
    ' Update the procedure.  
    Set cat.Procedures("CustomerById").Command = cmd  
  
    'Clean up.  
    cnn.Close  
    Set cat = Nothing  
    Set cmd = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
ProcedureTextError:  
    Set cat = Nothing  
    Set cmd = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndProcedureTextVB  
```  
  
## <a name="see-also"></a>관련 항목  
 [ActiveConnection 속성 (ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)   
 [Catalog 개체 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Command 속성 (ADOX)](../../../ado/reference/adox-api/command-property-adox.md)   
 [Procedure 개체 (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)   
 [Procedures 컬렉션(ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)
