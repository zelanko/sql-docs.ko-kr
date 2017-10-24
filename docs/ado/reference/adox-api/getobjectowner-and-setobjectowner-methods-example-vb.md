---
title: "GetObjectOwner 및 SetObjectOwner 메서드 예제 (VB) | Microsoft Docs"
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
- SetObjectOwner method [ADOX], Visual Basic example
- GetObjectOwner method [ADOX], Visual Basic example
ms.assetid: e44ec3d4-42ae-447d-aaed-bdea53cb0cca
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 65254f67ef864418a4c75e9e3f2b035c610e594e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getobjectowner-and-setobjectowner-methods-example-vb"></a>GetObjectOwner 및 SetObjectOwner 메서드 예제 (VB)
이 예제에서는 [GetObjectOwner](../../../ado/reference/adox-api/getobjectowner-method-adox.md) 및 [SetObjectOwner](../../../ado/reference/adox-api/setobjectowner-method.md) 메서드. 이 코드 그룹의 있다고 가정 Accounting (참조는 [그룹 및 사용자 추가, ChangePassword 메서드 예제 (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md) 시스템에이 그룹을 추가 하는 방법을 보려면). Categories 테이블의 소유자는 계정으로 설정 됩니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 개체 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [GetObjectOwner 메서드 (ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)   
 [SetObjectOwner 메서드](../../../ado/reference/adox-api/setobjectowner-method.md)

