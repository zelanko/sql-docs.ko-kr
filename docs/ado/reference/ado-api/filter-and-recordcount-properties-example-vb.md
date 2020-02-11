---
title: Filter 및 RecordCount 속성 예제 (VB) | Microsoft Docs
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
- RecordCount property [ADO], Visual Basic example
- Filter property [ADO], Visual Basic example
ms.assetid: e8bc63c7-8967-438a-9a49-512478a87a15
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6f94440d9ddd0d0b5091f2a106f603397147ebda
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67918646"
---
# <a name="filter-and-recordcount-properties-example-vb"></a>Filter 및 RecordCount 속성 예제(VB)
이 예에서는 ***Pubs*** 데이터베이스의 Publishers 테이블에서 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 을 엽니다. 그런 다음 [Filter](../../../ado/reference/ado-api/filter-property.md) 속성을 사용 하 여 특정 국가/지역의 해당 게시자로 표시 되는 레코드 수를 제한 합니다. **RecordCount** 속성은 필터링 되거나 필터링 되지 않은 레코드 집합 간의 차이를 표시 하는 데 사용 됩니다.  
  
```  
'BeginFilterVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    ' recordset variables  
    Dim rstPublishers As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim SQLPublishers As String  
  
     ' criteria variables  
    Dim intPublisherCount As Integer  
    Dim strCountry As String  
    Dim strMessage As String  
  
     ' open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' open recordset with data from Publishers table  
    Set rstPublishers = New ADODB.Recordset  
    SQLPublishers = "publishers"  
    rstPublishers.Open SQLPublishers, strCnxn, adOpenStatic, , adCmdTable  
  
    intPublisherCount = rstPublishers.RecordCount  
  
    ' get user input  
    strCountry = Trim(InputBox("Enter a country to filter on (e.g. USA):"))  
  
    If strCountry <> "" Then  
        ' open a filtered Recordset object  
        rstPublishers.Filter = "Country ='" & strCountry & "'"  
  
        If rstPublishers.RecordCount = 0 Then  
            MsgBox "No publishers from that country."  
        Else  
           ' print number of records for the original recordset  
           ' and the filtered recordset  
            strMessage = "Orders in original recordset: " & _  
                vbCr & intPublisherCount & vbCr & _  
                "Orders in filtered recordset (Country = '" & _  
                strCountry & "'): " & vbCr & _  
                rstPublishers.RecordCount  
            MsgBox strMessage  
        End If  
    End If  
  
    ' clean up  
    rstPublishers.Close  
    Cnxn.Close  
    Set rstPublishers = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstPublishers Is Nothing Then  
        If rstPublishers.State = adStateOpen Then rstPublishers.Close  
    End If  
    Set rstPublishers = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
'EndFilterVB  
```  
  
> [!NOTE]
>  선택할 데이터를 알고 있는 경우 일반적으로 SQL 문을 사용 하 여 **레코드 집합** 을 여는 것이 더 효율적입니다. 이 예에서는 하나의 **레코드 집합** 을 만들고 특정 국가에서 레코드를 가져올 수 있는 방법을 보여 줍니다.  
  
```  
Attribute VB_Name = "Filter"  
```  
  
## <a name="see-also"></a>참고 항목  
 [필터 속성](../../../ado/reference/ado-api/filter-property.md)   
 [RecordCount 속성 (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
