---
title: "연결 닫기 메서드를 테이블 형식 속성 예제 (VB) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Close method [ADOX], Visual Basic example
- Type property [ADOX], Visual Basic example
ms.assetid: f88e7a3b-19ed-46e2-b2ce-3b611d9b8166
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 95ea01c8cfb495ce104e60cbb3e24110fac98116
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="connection-close-method-table-type-property-example-vb"></a>테이블 형식 속성 예제 (VB) 연결 Close 메서드
설정의 [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) 속성을 **Nothing** 카탈로그에 대 한 연결을 종료 해야 합니다. 연결된 컬렉션은 비어 있게 됩니다. 카탈로그의 스키마 개체에서 생성 된 모든 개체가 분리 됩니다. 캐시 된 경우 해당 개체에 속성을 사용할 수 있지만 공급자를 호출 하는 속성을 읽는 시도 실패 합니다.  
  
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
  
 닫기는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체의 카탈로그를 열기 위해 사용 된 설정으로 동일한 영향을 미치지는 **ActiveConnection** 속성을 **Nothing**합니다.  
  
```  
Attribute VB_Name = "Connection"  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ActiveConnection 속성 (ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)   
 [카탈로그 개체 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Column 개체 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)   
 [Columns 컬렉션 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Table 개체 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)   
 [테이블 컬렉션 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [Type 속성(테이블)(ADOX)](../../../ado/reference/adox-api/type-property-table-adox.md)

