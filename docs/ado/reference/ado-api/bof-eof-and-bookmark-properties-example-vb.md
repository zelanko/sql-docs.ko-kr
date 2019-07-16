---
title: BOF, EOF 및 책갈피 속성 예제 (VB) | Microsoft Docs
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
- BOF property [ADO], Visual Basic example
- Bookmark property [ADO], Visual Basic example
- EOF property [ADO], Visual Basic example
ms.assetid: b6573c6e-fee8-4267-a722-fadaec6eafe6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9ab332d7d4144d62dd3a0cee1d3585820bf77e77
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920435"
---
# <a name="bof-eof-and-bookmark-properties-example-vb"></a>BOF, EOF 및 책갈피 속성 예제(VB)
이 예제에서는 합니다 [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 및 [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 사용자의 첫 번째 또는 마지막 레코드를 지 나 이동 하려고 하는 경우 메시지를 표시 하는 속성을 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다. 사용 하 여는 [책갈피](../../../ado/reference/ado-api/bookmark-property-ado.md) 사용자가 레코드 플래그 속성을 **레코드 집합** 하 고 나중에 반환 합니다.  
  
```  
'BeginBOFVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim Cnxn As ADODB.Connection  
    Dim rstPublishers As ADODB.Recordset  
    Dim strCnxn As String  
    Dim strSQLPubs As String  
     'record variables  
    Dim strMessage As String  
    Dim intCommand As Integer  
    Dim varBookmark As Variant  
  
     ' open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
     ' Open recordset and use client cursor  
     ' to enable AbsolutePosition property  
    Set rstPublishers = New ADODB.Recordset  
    strSQLPubs = "SELECT pub_id, pub_name FROM publishers ORDER BY pub_name"  
    rstPublishers.Open strSQLPubs, strCnxn, adUseClient, adOpenStatic, adCmdText  
  
    rstPublishers.MoveFirst  
    Do Until rstPublishers.EOF  
        ' Display information about current record  
        ' and get user input  
        strMessage = "Publisher: " & rstPublishers!pub_name & _  
            vbCr & "(record " & rstPublishers.AbsolutePosition & _  
            " of " & rstPublishers.RecordCount & ")" & vbCr & vbCr & _  
            "Enter command:" & vbCr & _  
            "[1 - next / 2 - previous /" & vbCr & _  
            "3 - set bookmark / 4 - go to bookmark]"  
        intCommand = Val(InputBox(strMessage))  
  
        ' Check user input  
        Select Case intCommand  
            Case 1  
                ' Move forward trapping for EOF  
                rstPublishers.MoveNext  
                If rstPublishers.EOF Then  
                    MsgBox "Moving past the last record." & _  
                        vbCr & "Try again."  
                    rstPublishers.MoveLast  
                End If  
            Case 2  
                ' Move backward trapping for BOF  
                rstPublishers.MovePrevious  
                If rstPublishers.BOF Then  
                    MsgBox "Moving past the first record." & _  
                        vbCr & "Try again."  
                    rstPublishers.MoveFirst  
                End If  
            Case 3  
                ' Store the bookmark of the current record  
                varBookmark = rstPublishers.Bookmark  
            Case 4  
                ' Go to the record indicated by the stored bookmark  
                If IsEmpty(varBookmark) Then  
                    MsgBox "No Bookmark set!"  
                Else  
                    rstPublishers.Bookmark = varBookmark  
                End If  
            Case Else  
                Exit Do  
        End Select  
    Loop  
  
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
'EndBOFVB  
```  
  
 이 예제에서는 **책갈피** 및 [필터](../../../ado/reference/ado-api/filter-property.md) 제한 된 보기를 만들기 위한 속성을 **레코드 집합**합니다. 책갈피의 배열에서 참조 하는 레코드만 액세스할 수 있습니다.  
  
```  
Attribute VB_Name = "BOF"  
```  
  
## <a name="see-also"></a>관련 항목  
 [BOF, EOF 속성 (ADO)](../../../ado/reference/ado-api/bof-eof-properties-ado.md)   
 [책갈피 속성 (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
