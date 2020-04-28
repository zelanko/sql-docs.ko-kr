---
title: Connection Close 메서드, Table Type 속성 예제 (VB) | Microsoft Docs
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
- Close method [ADOX], Visual Basic example
- Type property [ADOX], Visual Basic example
ms.assetid: f88e7a3b-19ed-46e2-b2ce-3b611d9b8166
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4559a8d46852f37f2e828ce8f4abbd0e40845744
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67966706"
---
# <a name="connection-close-method-table-type-property-example-vb"></a>Connection Close 메서드, Table Type 속성 예제(VB)
[ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) 속성을 **Nothing** 으로 설정 하면 카탈로그에 대 한 연결을 닫습니다. 연결 된 컬렉션은 비어 있습니다. 카탈로그의 스키마 개체에서 만든 개체는 분리 됩니다. 캐시 된 개체의 모든 속성을 계속 사용할 수 있지만 공급자를 호출 해야 하는 속성을 읽으려고 하면 오류가 발생 합니다.  
  
```  
' BeginCloseConnectionVB  
Sub Main()  
    On Error GoTo CloseConnectionByNothingError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim tbl As ADOX.Table  
  
    cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source= 'Northwind.mdb';"  
    Set cat.ActiveConnection = cnn  
    Set tbl = cat.Tables(0)  
    Debug.Print tbl.Type    ' Cache tbl.Type info  
    Set cat.ActiveConnection = Nothing  
    Debug.Print tbl.Type    ' tbl is orphaned  
    ' Previous line will succeed if this info was cached.  
    Debug.Print tbl.Columns(0).DefinedSize  
    ' Previous line will fail if this info has not been cached.  
  
    'Clean up.  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
CloseConnectionByNothingError:  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndCloseConnectionVB  
```  
  
 카탈로그를 여는 데 사용 된 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체를 닫는 것은 **ActiveConnection** 속성을 **Nothing**으로 설정 하는 것과 동일한 효과가 있습니다.  
  
```  
Attribute VB_Name = "Connection"  
```  
  
## <a name="see-also"></a>참고 항목  
 [ActiveConnection 속성 (ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)   
 [Catalog 개체 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Column 개체 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)   
 [Columns 컬렉션 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Table 개체 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)   
 [Tables 컬렉션 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [Type 속성(테이블)(ADOX)](../../../ado/reference/adox-api/type-property-table-adox.md)
