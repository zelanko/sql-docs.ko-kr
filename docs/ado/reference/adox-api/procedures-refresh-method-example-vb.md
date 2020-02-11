---
title: 프로시저 Refresh 메서드 예제 (VB) | Microsoft Docs
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
- Refresh method [ADOX], Visual Basic example
ms.assetid: 499679bd-287b-487d-bdfb-3803abffec1c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9b5201be26bfd9df41c9cb1d8908f59499520878
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67965372"
---
# <a name="procedures-refresh-method-example-vb"></a>Procedures Refresh 메서드 예제(VB)
다음 코드에서는 [카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md)의 [프로시저](../../../ado/reference/adox-api/procedures-collection-adox.md) 컬렉션을 새로 고치는 방법을 보여 줍니다. **카탈로그** 의 [프로시저](../../../ado/reference/adox-api/procedure-object-adox.md) 개체에 액세스할 수 있으려면이 작업을 수행 해야 합니다.  
  
```  
' BeginProceduresRefreshVB  
Sub Main()  
    On Error GoTo ProcedureRefreshError  
  
    Dim cat As New ADOX.Catalog  
  
    ' Open the Catalog  
    cat.ActiveConnection = _  
        "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Refresh the Procedures collection  
    cat.Procedures.Refresh  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Exit Sub  
  
ProcedureRefreshError:  
    Set cat = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndProceduresRefreshVB  
```  
  
## <a name="see-also"></a>참고 항목  
 [Catalog 개체 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [프로시저 컬렉션 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)   
 [Refresh 메서드(ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)
