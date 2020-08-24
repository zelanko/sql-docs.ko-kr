---
description: Clustered 속성 예제(VB)
title: Clustered 속성 예제 (VB) | Microsoft Docs
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
- Clustered property [ADOX], Visual Basic example
ms.assetid: 1cd30769-c8af-43e7-be27-12ed0434daa1
author: rothja
ms.author: jroth
ms.openlocfilehash: 1992c8c5796052e46719c34ecbc43d6b94553b6e
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771142"
---
# <a name="clustered-property-example-vb"></a>Clustered 속성 예제(VB)
이 예에서는 [인덱스](./index-object-adox.md)의 [클러스터형](./clustered-property-adox.md) 속성을 보여 줍니다. Microsoft Jet 데이터베이스는 클러스터형 인덱스를 지원 하지 않으므로이 예에서는 **Northwind** 데이터베이스에 있는 모든 인덱스의 **클러스터형** 속성에 대해 **False** 를 반환 합니다.  
  
```  
' BeginClusteredVB  
Sub Main()  
    On Error GoTo ClusteredXError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim tblLoop As ADOX.Table  
    Dim idxLoop As ADOX.Index  
    Dim strCnn As String  
  
    strCnn = "Provider='SQLOLEDB';Data Source='MySqlServer';Initial Catalog='pubs';" & _  
        "Integrated Security='SSPI';"  
    ' Connect to the catalog.  
    cnn.Open strCnn  
    cat.ActiveConnection = cnn  
  
    ' Enumerate the tables.  
    For Each tblLoop In cat.Tables  
        'Enumerate the indexes.  
        For Each idxLoop In tblLoop.Indexes  
            Debug.Print tblLoop.Name & " " & _  
                idxLoop.Name & " " & idxLoop.Clustered  
        Next idxLoop  
    Next tblLoop  
  
    'Clean up.  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
ClusteredXError:  
  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndClusteredVB  
```  
  
## <a name="see-also"></a>참고 항목  
 [Catalog 개체 (ADOX)](./catalog-object-adox.md)   
 [Clustered 속성 (ADOX)](./clustered-property-adox.md)   
 [Index 개체 (ADOX)](./index-object-adox.md)   
 [테이블 개체(ADOX)](./table-object-adox.md)