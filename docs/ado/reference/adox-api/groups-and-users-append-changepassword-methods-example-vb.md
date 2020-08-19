---
description: Groups 및 Users Append, ChangePassword 메서드 예제(VB)
title: Groups 및 Users Append, ChangePassword 메서드 예제 (VB) | Microsoft Docs
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
- ChangePassword method [ADOX], Visual Basic example
- Append method [ADOX], Visual Basic example
ms.assetid: c9426757-9cdd-4a95-b506-d3d011569109
author: rothja
ms.author: jroth
ms.openlocfilehash: 7aa335dc2aabdf05ab34a0245bb0aafc14b17cf1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439985"
---
# <a name="groups-and-users-append-changepassword-methods-example-vb"></a>Groups 및 Users Append, ChangePassword 메서드 예제(VB)
이 예제에서는 시스템에 새 [그룹](../../../ado/reference/adox-api/group-object-adox.md) 및 새 [사용자](../../../ado/reference/adox-api/user-object-adox.md) 를 추가 하 여 [사용자](../../../ado/reference/adox-api/users-collection-adox.md) 의 [추가](../../../ado/reference/adox-api/append-method-adox-users.md) 방법 뿐만 아니라 [그룹](../../../ado/reference/adox-api/groups-collection-adox.md)의 [추가](../../../ado/reference/adox-api/append-method-adox-groups.md) 메서드를 보여 줍니다. 새 **그룹** 은 새 **사용자**의 **그룹** 컬렉션에 추가 됩니다. 따라서 새 **사용자** 가 **그룹**에 추가 됩니다. 또한 [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md) 메서드를 사용 하 여 **사용자** 암호를 지정 합니다.  
  
> [!NOTE]
>  Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는 경우 연결 문자열에 사용자 ID 및 암호 정보 대신 **Trusted_Connection = yes** 또는 **INTEGRATED Security = SSPI** 를 지정 해야 합니다.  
  
```  
' BeginGroupVB  
Sub Main()  
    On Error GoTo GroupXError  
  
    Dim cat As ADOX.Catalog  
    Dim usrNew As ADOX.User  
    Dim usrLoop As ADOX.User  
    Dim grpLoop As ADOX.Group  
  
    Set cat = New ADOX.Catalog  
  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';" & _  
        "jet oledb:system database=" & _  
        "'system.mdw'"  
  
    With cat  
        'Create and append new group with a string.  
        .Groups.Append "Accounting"  
  
        ' Create and append new user with an object.  
        Set usrNew = New ADOX.User  
        usrNew.Name = "Pat Smith"  
        usrNew.ChangePassword "", "Password1"  
        .Users.Append usrNew  
  
        ' Make the user Pat Smith a member of the  
        ' Accounting group by creating and adding the  
        ' appropriate Group object to the user's Groups  
        ' collection. The same is accomplished if a User  
        ' object representing Pat Smith is created and  
        ' appended to the Accounting group Users collection  
        usrNew.Groups.Append "Accounting"  
  
        ' Enumerate all User objects in the  
        ' catalog's Users collection.  
        For Each usrLoop In .Users  
            Debug.Print "  " & usrLoop.Name  
            Debug.Print "    Belongs to these groups:"  
            ' Enumerate all Group objects in each User  
            ' object's Groups collection.  
            If usrLoop.Groups.Count <> 0 Then  
                For Each grpLoop In usrLoop.Groups  
                    Debug.Print "    " & grpLoop.Name  
                Next grpLoop  
            Else  
                Debug.Print "    [None]"  
            End If  
        Next usrLoop  
  
        ' Enumerate all Group objects in the default  
        ' workspace's Groups collection.  
        For Each grpLoop In .Groups  
            Debug.Print "  " & grpLoop.Name  
            Debug.Print "    Has as its members:"  
            ' Enumerate all User objects in each Group  
            ' object's Users collection.  
            If grpLoop.Users.Count <> 0 Then  
                For Each usrLoop In grpLoop.Users  
                    Debug.Print "    " & usrLoop.Name  
                Next usrLoop  
            Else  
                Debug.Print "    [None]"  
            End If  
        Next grpLoop  
  
        ' Delete new User and Group objects because this  
        ' is only a demonstration.  
        ' These two line are commented out because the sub "OwnersX" uses  
        ' the group "Accounting".  
'        .Users.Delete "Pat Smith"  
'        .Groups.Delete "Accounting"  
  
    End With  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Set usrNew = Nothing  
    Exit Sub  
  
GroupXError:  
  
    Set cat = Nothing  
    Set usrNew = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndGroupVB  
```  
  
## <a name="see-also"></a>참고 항목  
 [Append 메서드 (ADOX Groups)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 메서드 (ADOX 사용자)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Catalog 개체 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [ChangePassword 메서드 (ADOX)](../../../ado/reference/adox-api/changepassword-method-adox.md)   
 [Group 개체 (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)   
 [Groups 컬렉션 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [User 개체 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)   
 [Users 컬렉션(ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
