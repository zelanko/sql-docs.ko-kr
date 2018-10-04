---
title: Procedures Refresh 메서드 예제 (VB) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 6f46bc9aceeec0e03329572814653a94ea64aa50
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47632311"
---
# <a name="procedures-refresh-method-example-vb"></a>Procedures Refresh 메서드 예제(VB)
다음 코드를 새로 고치는 방법을 보여 줍니다 합니다 [프로시저](../../../ado/reference/adox-api/procedures-collection-adox.md) 의 컬렉션을 [카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md)합니다. 하기 전에 반드시 [프로시저](../../../ado/reference/adox-api/procedure-object-adox.md) 에서 개체를 **카탈로그** 액세스할 수 있습니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [Catalog 개체 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Procedures 컬렉션 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)   
 [Refresh 메서드(ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)
