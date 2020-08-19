---
description: DateCreated 및 DateModified 속성 예제(VB)
title: DateCreated 및 DateModified 속성 예제 (VB) | Microsoft Docs
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
- DateCreated property [ADOX], Visual Basic example
- DateModified property [ADOX], Visual Basic example
ms.assetid: d608ea35-6e68-402f-8184-a5041e408678
author: rothja
ms.author: jroth
ms.openlocfilehash: 51400e11416ff7a8e7a336a815e4a11d8033d316
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440185"
---
# <a name="datecreated-and-datemodified-properties-example-vb"></a>DateCreated 및 DateModified 속성 예제(VB)
이 예에서는 기존 [테이블](../../../ado/reference/adox-api/table-object-adox.md) 에 새 [열](../../../ado/reference/adox-api/column-object-adox.md) 을 추가 하 고 새 **테이블**을 만들어 [DateCreated](../../../ado/reference/adox-api/datecreated-property-adox.md) 및 [DateModified](../../../ado/reference/adox-api/datemodified-property-adox.md) 속성을 보여 줍니다. 이 예제를 실행 하려면 DateOutput 프로시저가 필요 합니다.  
  
```  
' BeginDateCreatedVB  
Sub Main()  
    On Error GoTo DateCreatedXError  
  
    Dim cat As New ADOX.Catalog  
    Dim tblEmployees As ADOX.Table  
    Dim tblNewTable As ADOX.Table  
  
    ' Connect to the catalog.  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    With cat  
        Set tblEmployees = .Tables("Employees")  
  
        ' Print current information about the Employees table.  
        DateOutput "Current properties", tblEmployees  
  
        ' Create and append column to the Employees table.  
        tblEmployees.Columns.Append "NewColumn", adInteger  
        .Tables.Refresh  
  
        ' Print new information about the Employees table.  
        DateOutput "After creating a new column", tblEmployees  
  
        ' Delete new column because this is a demonstration.  
        tblEmployees.Columns.Delete "NewColumn"  
  
        ' Create and append new Table object to the Northwind database.  
        Set tblNewTable = New ADOX.Table  
        tblNewTable.Name = "NewTable"  
        tblNewTable.Columns.Append "NewColumn", adInteger  
        .Tables.Append tblNewTable  
        .Tables.Refresh  
  
        ' Print information about the new Table object.  
        DateOutput "After creating a new table", .Tables("NewTable")  
  
        ' Delete new Table object because this is a demonstration.  
        .Tables.Delete tblNewTable.Name  
    End With  
  
    'Clean up.  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Exit Sub  
  
DateCreatedXError:  
    Set cat = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
  
Sub DateOutput(strTemp As String, tblTemp As ADOX.Table)  
    ' Print DateCreated and DateModified information about  
    ' specified Table object.  
    Debug.Print strTemp  
    Debug.Print "    Table: " & tblTemp.Name  
    Debug.Print "        DateCreated = " & tblTemp.DateCreated  
    Debug.Print "        DateModified = " & tblTemp.DateModified  
    Debug.Print  
End Sub  
' EndDateCreatedVB  
```  
  
## <a name="see-also"></a>참고 항목  
 [DateCreated 속성 (ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md)   
 [DateModified 속성 (ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md)   
 [Procedure 개체 (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)   
 [프로시저 컬렉션 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)   
 [View 개체 (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)   
 [Views 컬렉션(ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
