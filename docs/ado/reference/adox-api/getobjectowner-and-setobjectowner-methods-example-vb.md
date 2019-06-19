---
title: GetObjectOwner 및 SetObjectOwner 메서드 예제 (VB) | Microsoft Docs
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
- SetObjectOwner method [ADOX], Visual Basic example
- GetObjectOwner method [ADOX], Visual Basic example
ms.assetid: e44ec3d4-42ae-447d-aaed-bdea53cb0cca
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: dd0091d76ae956d7391e1a29f63f0fcabe8720f7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718870"
---
# <a name="getobjectowner-and-setobjectowner-methods-example-vb"></a>GetObjectOwner 및 SetObjectOwner 메서드 예제(VB)
이 예제에서는 합니다 [GetObjectOwner](../../../ado/reference/adox-api/getobjectowner-method-adox.md) 하 고 [SetObjectOwner](../../../ado/reference/adox-api/setobjectowner-method.md) 메서드. 이 코드 그룹의 가정 계정 (참조를 [그룹과 사용자 Append, ChangePassword 메서드 예제 (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md) 시스템에이 그룹에 추가 하는 방법을 보려면). Categories 테이블의 소유자는 계정으로 설정 됩니다.  
  
```  
' BeginOwnersVB  
Sub OwnersX()  
  
    Dim tblLoop As New ADOX.Table  
    Dim cat As New ADOX.Catalog  
    Dim strOwner As String  
  
    ' Open the Catalog.  
    cat.ActiveConnection = "Provider=Microsoft.Jet.OLEDB.4.0;" & _  
        "Data Source=c:\Program Files\" & _  
        "Microsoft Office\Office\Samples\Northwind.mdb;" & _  
        "jet oledb:system database=" & _  
        "c:\Program Files\Microsoft Office\Office\system.mdw"  
  
    ' Print the original owner of Categories  
    strOwner = cat.GetObjectOwner("Categories", adPermObjTable)  
    Debug.Print "Owner of Categories: " & strOwner  
  
    ' Set the owner of Categories to Accounting  
    cat.SetObjectOwner "Categories", adPermObjTable, "Accounting"  
  
    ' List the owners of all tables and columns in the catalog.  
    For Each tblLoop In cat.Tables  
        Debug.Print "Table: " & tblLoop.Name  
        Debug.Print "   Owner: " & _  
            cat.GetObjectOwner(tblLoop.Name, adPermObjTable)  
    Next tblLoop  
  
    ' Restore the original owner of Categories  
    cat.SetObjectOwner "Categories", adPermObjTable, strOwner  
  
End Sub  
' EndOwnersVB  
```  
  
## <a name="see-also"></a>관련 항목  
 [Catalog 개체 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [GetObjectOwner 메서드 (ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)   
 [SetObjectOwner 메서드](../../../ado/reference/adox-api/setobjectowner-method.md)
