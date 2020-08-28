---
description: Procedures Refresh 메서드 예제(VB)
title: 프로시저 Refresh 메서드 예제 (VB) | Microsoft Docs
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
- Refresh method [ADOX], Visual Basic example
ms.assetid: 499679bd-287b-487d-bdfb-3803abffec1c
author: rothja
ms.author: jroth
ms.openlocfilehash: 757c410982f43258f25729f5e88a5705c1ca814d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983494"
---
# <a name="procedures-refresh-method-example-vb"></a>Procedures Refresh 메서드 예제(VB)
다음 코드에서는 [카탈로그](./catalog-object-adox.md)의 [프로시저](./procedures-collection-adox.md) 컬렉션을 새로 고치는 방법을 보여 줍니다. **카탈로그** 의 [프로시저](./procedure-object-adox.md) 개체에 액세스할 수 있으려면이 작업을 수행 해야 합니다.  
  
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
 [Catalog 개체 (ADOX)](./catalog-object-adox.md)   
 [프로시저 컬렉션 (ADOX)](./procedures-collection-adox.md)   
 [Refresh 메서드(ADO)](../ado-api/refresh-method-ado.md)