---
title: "테이블 예제 (VB) 간에 새 외래 키 관계 만들기 | Microsoft Docs"
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
- Key Type property [ADOX], Visual Basic example
- RelatedTable property [ADOX], Visual Basic example
- Keys Append method [ADOX], Visual Basic example
- UpdateRule property [ADOX], Visual Basic example
- RelatedColumn property [ADOX], Visual Basic example
ms.assetid: 13b5b1c3-6af6-439e-bb65-976578ba6bc2
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: baf04a542b1f488e8570713df938f3a03aa753f1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="keys-append-method-key-type-relatedcolumn-relatedtable-and-updaterule-properties-example-vb"></a>키 추가 방법, 키 형식, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)
다음 코드에 라는 두 개의 기존 테이블 간에 새 외래 키 관계를 만드는 방법을 보여 줍니다 **고객** 및 **Orders**합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [Append 메서드 (ADOX 열)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 메서드 (ADOX 키)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [카탈로그 개체 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Column 개체 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)   
 [Columns 컬렉션 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [키 개체 (ADOX)](../../../ado/reference/adox-api/key-object-adox.md)   
 [키 컬렉션 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)   
 [Name 속성 (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)   
 [RelatedColumn 속성 (ADOX)](../../../ado/reference/adox-api/relatedcolumn-property-adox.md)   
 [RelatedTable 속성 (ADOX)](../../../ado/reference/adox-api/relatedtable-property-adox.md)   
 [Table 개체 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)   
 [테이블 컬렉션 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [Type 속성 (Key) (ADOX)](../../../ado/reference/adox-api/type-property-key-adox.md)   
 [UpdateRule 속성(ADOX)](../../../ado/reference/adox-api/updaterule-property-adox.md)

