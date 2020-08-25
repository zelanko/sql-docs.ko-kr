---
description: Keys Append 메서드, Key Type, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제(VB)
title: 테이블 간의 새 외래 키 관계 만들기 예 (VB) | Microsoft Docs
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
- Key Type property [ADOX], Visual Basic example
- RelatedTable property [ADOX], Visual Basic example
- Keys Append method [ADOX], Visual Basic example
- UpdateRule property [ADOX], Visual Basic example
- RelatedColumn property [ADOX], Visual Basic example
ms.assetid: 13b5b1c3-6af6-439e-bb65-976578ba6bc2
author: rothja
ms.author: jroth
ms.openlocfilehash: a96894fc9842de991647e7d25b728c5f7a663566
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770092"
---
# <a name="keys-append-method-key-type-relatedcolumn-relatedtable-and-updaterule-properties-example-vb"></a>Keys Append 메서드, Key Type, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제(VB)
다음 코드에서는 **Customers** 와 **Orders**라는 두 개의 기존 테이블 간에 새 외래 키 관계를 만드는 방법을 보여 줍니다.  
  
```  
' BeginCreateKeyVB  
Sub Main()  
    On Error GoTo CreateKeyError  
  
    Dim kyForeign As New ADOX.Key  
    Dim cat As New ADOX.Catalog  
  
    ' Connect to the catalog.  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Define the foreign key.  
    kyForeign.Name = "CustOrder"  
    kyForeign.Type = adKeyForeign  
    kyForeign.RelatedTable = "Customers"  
    kyForeign.Columns.Append "CustomerId"  
    kyForeign.Columns("CustomerId").RelatedColumn = "CustomerId"  
    kyForeign.UpdateRule = adRICascade  
  
    ' Append the foreign key to the keys collection.  
    cat.Tables("Orders").Keys.Append kyForeign  
  
    'Delete the key t demonstrate the Delete method.  
    cat.Tables("Orders").Keys.Delete kyForeign.Name  
  
    'Clean up.  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Set kyForeign = Nothing  
    Exit Sub  
  
CreateKeyError:  
    Set cat = Nothing  
    Set kyForeign = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
' EndCreateKeyVB  
```  
  
## <a name="see-also"></a>참고 항목  
 [Append 메서드 (ADOX Columns)](./append-method-adox-columns.md)   
 [Append 메서드 (ADOX 키)](./append-method-adox-keys.md)   
 [Catalog 개체 (ADOX)](./catalog-object-adox.md)   
 [Column 개체 (ADOX)](./column-object-adox.md)   
 [Columns 컬렉션 (ADOX)](./columns-collection-adox.md)   
 [Key 개체 (ADOX)](./key-object-adox.md)   
 [Keys 컬렉션 (ADOX)](./keys-collection-adox.md)   
 [Name 속성 (ADOX)](./name-property-adox.md)   
 [RelatedColumn 속성 (ADOX)](./relatedcolumn-property-adox.md)   
 [RelatedTable 속성 (ADOX)](./relatedtable-property-adox.md)   
 [Table 개체 (ADOX)](./table-object-adox.md)   
 [Tables 컬렉션 (ADOX)](./tables-collection-adox.md)   
 [Type 속성 (Key) (ADOX)](./type-property-key-adox.md)   
 [UpdateRule 속성(ADOX)](./updaterule-property-adox.md)