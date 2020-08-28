---
description: Catalog ActiveConnection 속성 예제(VB)
title: Catalog ActiveConnection 속성 예제 (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ActiveConnection property [ADOX], Visual Basic example
ms.assetid: bb3274b1-764d-43a7-a49f-ef55680ecd26
author: rothja
ms.author: jroth
ms.openlocfilehash: 582c558222bec95914e73902b69fe9c7ce46161e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985243"
---
# <a name="catalog-activeconnection-property-example-vb"></a>Catalog ActiveConnection 속성 예제(VB)
[ActiveConnection](./activeconnection-property-adox.md) 속성을 유효한 열린 연결로 설정 하면 카탈로그가 열립니다. 열려 있는 카탈로그에서 해당 카탈로그 내에 포함 된 스키마 개체에 액세스할 수 있습니다.  
  
```  
' BeginOpenConnectionVB  
Sub Main()  
    On Error GoTo OpenConnectionError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
  
    cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source= 'Northwind.mdb';"  
    Set cat.ActiveConnection = cnn  
    Debug.Print cat.Tables(0).Type  
  
    'Clean up  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
OpenConnectionError:  
  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndOpenConnectionVB  
```  
  
 **ActiveConnection** 속성을 유효한 연결 문자열로 설정 하면 카탈로그가 "열립니다".  
  
```  
Attribute VB_Name = "Catalog"  
```  
  
## <a name="see-also"></a>참고 항목  
 [ActiveConnection 속성 (ADOX)](./activeconnection-property-adox.md)   
 [Catalog 개체 (ADOX)](./catalog-object-adox.md)   
 [Table 개체 (ADOX)](./table-object-adox.md)   
 [Tables 컬렉션 (ADOX)](./tables-collection-adox.md)   
 [Type 속성(테이블)(ADOX)](./type-property-table-adox.md)