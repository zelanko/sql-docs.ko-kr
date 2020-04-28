---
title: Views Refresh 메서드 예제 (VB) | Microsoft Docs
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
- Refresh method [ADOX]
ms.assetid: cdad2d66-6ade-40dc-9e74-e40cfa9bc127
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e0d50c8cab60ddf1839c5683023af0b90ebe527c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67964730"
---
# <a name="views-refresh-method-example-vb"></a>Views Refresh 메서드 예제(VB)
다음 코드에서는 [카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md)의 [뷰](../../../ado/reference/adox-api/views-collection-adox.md) 컬렉션을 새로 고치는 방법을 보여 줍니다. 이렇게 하려면 **카탈로그** 의 [보기](../../../ado/reference/adox-api/view-object-adox.md) 개체에 액세스할 수 있어야 합니다.  
  
```  
' BeginViewsRefreshVB  
Sub Main()  
    On Error GoTo ProcedureViewsRefreshError  
  
    Dim cat As New ADOX.Catalog  
  
    ' Open the catalog.  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Refresh the Procedures collection.  
    cat.Views.Refresh  
  
    'Clean up  
    Set cat = Nothing  
    Exit Sub  
  
ProcedureViewsRefreshError:  
  
    If Not cat Is Nothing Then  
        Set cat = Nothing  
    End If  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndViewsRefreshVB  
```  
  
## <a name="see-also"></a>참고 항목  
 [Refresh 메서드 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [Views 컬렉션(ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
