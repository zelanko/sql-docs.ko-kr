---
title: NumericScale 및 Precision 속성 예제 (VB) | Microsoft Docs
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
- Precision property [ADOX], Visual Basic example
- NumericScale property [ADOX], Visual Basic example
ms.assetid: ea2ec614-34c8-41b7-8ebd-063798bd56b4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 844fb21747e8785a580f178828a522c4038fcb73
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66708500"
---
# <a name="adox-code-example-numericscale-and-precision-properties-example-vb"></a>ADOX 코드 예제: NumericScale 및 Precision 속성 예제(VB)
이 예제에서는 합니다 [NumericScale](../../../ado/reference/adox-api/numericscale-property-adox.md) 및 [정밀도](../../../ado/reference/adox-api/precision-property-adox.md) 의 속성을 [열](../../../ado/reference/adox-api/column-object-adox.md) 개체. 이 코드에 대 한 해당 값을 표시 합니다 **Order Details** 목차를 *Northwind* 데이터베이스.  
  
```  
' BeginNumericScalePrecVB  
Sub Main()  
    On Error GoTo NumericScalePrecXError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim tblOD As ADOX.Table  
    Dim colLoop As ADOX.Column  
  
    ' Connect the catalog.  
    cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "data source='Northwind.mdb';"  
    Set cat.ActiveConnection = cnn  
  
    ' Retrieve the Order Details table  
    Set tblOD = cat.Tables("Order Details")  
  
    ' Display numeric scale and precision of  
    ' small integer fields.  
    For Each colLoop In tblOD.Columns  
        If colLoop.Type = adSmallInt Then  
            MsgBox "Column: " & colLoop.Name & vbCr & _  
                "Numeric scale: " & _  
                colLoop.NumericScale & vbCr & _  
                "Precision: " & colLoop.Precision  
        End If  
    Next colLoop  
  
    'Clean up  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
NumericScalePrecXError:  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndNumericScalePrecVB  
```  
  
## <a name="see-also"></a>관련 항목  
 [Column 개체 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)   
 [NumericScale 속성 (ADOX)](../../../ado/reference/adox-api/numericscale-property-adox.md)   
 [Precision 속성(ADOX)](../../../ado/reference/adox-api/precision-property-adox.md)
