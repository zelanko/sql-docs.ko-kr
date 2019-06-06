---
title: DeleteRule 속성 예제 (VB) | Microsoft Docs
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
- DeleteRule property [ADOX], Visual Basic example
ms.assetid: 9ba00118-a80d-4a6d-a7d6-4f5492fb7ded
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d3fcadc7435c3a4527367faf41ae412dd1afa67e
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712174"
---
# <a name="deleterule-property-example-vb"></a>DeleteRule 속성 예제(VB)
이 예제에서는 합니다 [DeleteRule](../../../ado/reference/adox-api/deleterule-property-adox.md) 의 속성을 [키](../../../ado/reference/adox-api/key-object-adox.md) 개체입니다. 새 코드를 추가 [테이블](../../../ado/reference/adox-api/table-object-adox.md) 설정 하는 새 기본 키를 다음 정의 **DeleteRule** 하 **adRICascade**합니다.  
  
```  
' BeginDeleteRuleVB  
Sub Main()  
    On Error GoTo DeleteRuleXError  
  
    Dim kyPrimary As New ADOX.Key  
    Dim cat As New ADOX.Catalog  
    Dim tblNew As New ADOX.Table  
  
    ' Connect the catalog  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
                     "data source='Northwind.mdb';"  
  
    ' Name new table  
    tblNew.Name = "NewTable"  
  
    ' Append a numeric and a text field to new table.  
    tblNew.Columns.Append "NumField", adInteger, 20  
    tblNew.Columns.Append "TextField", adVarWChar, 20  
  
    ' Append the new table  
    cat.Tables.Append tblNew  
  
    ' Define the Primary key  
    kyPrimary.Name = "NumField"  
    kyPrimary.Type = adKeyPrimary  
    kyPrimary.RelatedTable = "Customers"  
    kyPrimary.Columns.Append "NumField"  
    kyPrimary.Columns("NumField").RelatedColumn = "CustomerId"  
    kyPrimary.DeleteRule = adRICascade  
  
    ' Append the primary key  
    cat.Tables("NewTable").Keys.Append kyPrimary  
    Debug.Print "The primary key is appended."  
  
    'Delete the table as this is a demonstration.  
    cat.Tables.Delete tblNew.Name  
    Debug.Print "The primary key is deleted."  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Set kyPrimary = Nothing  
    Set tblNew = Nothing  
    Exit Sub  
  
DeleteRuleXError:  
  
    Set cat = Nothing  
    Set kyPrimary = Nothing  
    Set tblNew = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
' EndDeleteRuleVB  
```  
  
## <a name="see-also"></a>관련 항목  
 [DeleteRule 속성 (ADOX)](../../../ado/reference/adox-api/deleterule-property-adox.md)   
 [Key 개체(ADOX)](../../../ado/reference/adox-api/key-object-adox.md)
