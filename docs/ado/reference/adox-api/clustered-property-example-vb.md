---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f2eb5e19e166a468a9ee30758da79d503f1b9932
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966958"
---
# <a name="clustered-property-example-vb"></a>Clustered 속성 예제(VB)
이 예제에서는 합니다 [클러스터형](../../../ado/reference/adox-api/clustered-property-adox.md) 의 속성을 [인덱스](../../../ado/reference/adox-api/index-object-adox.md)합니다. Microsoft Jet 데이터베이스에이 예제에서는 반환은 클러스터형된 인덱스를 지원 하지 않습니다 **False** 에 대 한 합니다 **클러스터형** 의 모든 인덱스의 속성을 **Northwind** 데이터베이스입니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [Catalog 개체 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Clustered 속성 (ADOX)](../../../ado/reference/adox-api/clustered-property-adox.md)   
 [Index 개체 (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)   
 [Table 개체(ADOX)](../../../ado/reference/adox-api/table-object-adox.md)
