---
description: Procedures Append 메서드 예제(VB)
title: 프로시저 Append 메서드 예제 (VB) | Microsoft Docs
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
- Append method [ADOX], Visual Basic example
ms.assetid: ce83b966-474b-4f57-8eb9-370996dfc5c0
author: rothja
ms.author: jroth
ms.openlocfilehash: b8b9b58c50a1e3c77a6239c73222ea7a1656b882
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769642"
---
# <a name="procedures-append-method-example-vb"></a>Procedures Append 메서드 예제(VB)
다음 코드에서는 [Command](../ado-api/command-object-ado.md) 개체와 [procedure collection](./procedures-collection-adox.md) [Append](./append-method-adox-procedures.md) 메서드를 사용 하 여 기본 데이터 소스에 새 프로시저를 만드는 방법을 보여 줍니다.  
  
```  
' BeginCreateProcedureVB  
Sub Main()  
    On Error GoTo CreateProcedureError  
  
    Dim cnn As New ADODB.Connection  
    Dim cmd As New ADODB.Command  
    Dim prm As ADODB.Parameter  
    Dim cat As New ADOX.Catalog  
  
    ' Open the Connection  
    cnn.Open _  
        "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Create the parameterized command (Microsoft Jet specific)  
    Set cmd.ActiveConnection = cnn  
    cmd.CommandText = "PARAMETERS [CustId] Text;" & _  
    "Select * From Customers Where CustomerId = [CustId]"  
  
    ' Open the Catalog  
    Set cat.ActiveConnection = cnn  
  
    ' Create the new Procedure  
    cat.Procedures.Append "CustomerById", cmd  
  
    'Clean  
    cnn.Close  
    Set cat = Nothing  
    Set cmd = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
CreateProcedureError:  
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
' EndCreateProcedureVB  
```  
  
## <a name="see-also"></a>참고 항목  
 [ActiveConnection 속성 (ADOX)](./activeconnection-property-adox.md)   
 [Append 메서드 (ADOX 프로시저)](./append-method-adox-procedures.md)   
 [Catalog 개체 (ADOX)](./catalog-object-adox.md)   
 [Procedure 개체 (ADOX)](./procedure-object-adox.md)   
 [Procedures 컬렉션(ADOX)](./procedures-collection-adox.md)