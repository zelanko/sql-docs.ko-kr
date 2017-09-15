---
title: "프로시저 메서드 예제 (VB) 새로 고침 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Refresh method [ADOX], Visual Basic example
ms.assetid: 499679bd-287b-487d-bdfb-3803abffec1c
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d0a9122b1adaa6d5a070bb568605b20a04199d95
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="procedures-refresh-method-example-vb"></a>프로시저는 메서드 예제를 (VB)를 새로 고칩니다.
다음 코드에서는 새로 고치는 방법을 보여 줍니다.는 [프로시저](../../../ado/reference/adox-api/procedures-collection-adox.md) 의 컬렉션을 [카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md)합니다. 하기 전에 반드시 지정 해야 [프로시저](../../../ado/reference/adox-api/procedure-object-adox.md) 에서 개체는 **카탈로그** 액세스할 수 있습니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 개체 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [프로시저 컬렉션 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)   
 [Refresh 메서드(ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)
