---
title: Save 및 Open 메서드 예제 (VB) | Microsoft Docs
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
- Save method [ADO], Visual Basic example
- Open method [ADO]
ms.assetid: ddccdf58-9c57-4c9b-8b7f-0cf193f955fb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6d42488f8f167cc7c98f663478c742963d24253c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931190"
---
# <a name="save-and-open-methods-example-vb"></a>Save 및 Open 메서드 예제(VB)
다음 세 가지 예제에서는 [Save](../../../ado/reference/ado-api/save-method.md) 및 [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드를 함께 사용할 수 있는 방법을 보여 줍니다.  
  
 비즈니스 여행에 대해 진행 중 이며 데이터베이스의 테이블을 함께 사용 하려는 경우를 가정 합니다. 이동 하기 전에 데이터를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 으로 액세스 하 여 전송 가능한 형태로 저장 합니다. 대상에 도착 하면 연결 되지 않은 로컬 **레코드**집합으로 **레코드 집합** 에 액세스 합니다. **레코드 집합**을 변경한 후 다시 저장 합니다. 마지막으로 home을 반환 하는 경우 데이터베이스에 다시 연결 하 여 이동 시 변경한 내용으로 업데이트 합니다.  
  
 먼저 ***Authors*** 테이블을 액세스 하 고 저장 합니다.  
  
```  
'BeginSaveVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim rstAuthors As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strSQLAuthors As String  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    Set rstAuthors = New ADODB.Recordset  
    strSQLAuthors = "SELECT au_id, au_lname, au_fname, city, phone FROM Authors"  
    rstAuthors.Open strSQLAuthors, Cnxn, adOpenDynamic, adLockOptimistic, adCmdText  
  
    'For sake of illustration, save the Recordset to a diskette in XML format  
    rstAuthors.Save "c:\Pubs.xml", adPersistXML  
  
    ' clean up  
    rstAuthors.Close  
    Cnxn.Close  
    Set rstAuthors = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    'clean up  
    If Not rstAuthors Is Nothing Then  
        If rstAuthors.State = adStateOpen Then rstAuthors.Close  
    End If  
    Set rstAuthors = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndSaveVB  
```  
  
 이 시점에서 대상에 도달 했습니다. 연결 되지 않은 로컬 **레코드 집합**으로 ***Authors*** 테이블에 액세스 합니다. 저장 된 파일에 액세스 하는 데 사용 하는 컴퓨터에 **Mspersist** 공급자 (a:\Pubs.xml.)가 있어야 합니다.  
  
```  
Attribute VB_Name = "Save"  
```  
  
 마지막으로 home을 반환 합니다. 이제 변경 내용으로 데이터베이스를 업데이트 합니다.  
  
```  
Attribute VB_Name = "Save"  
```  
  
## <a name="see-also"></a>참고 항목  
 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [레코드 집합 지 속성에 대 한 자세한 정보](../../../ado/guide/data/more-about-recordset-persistence.md)   
 [Save 메서드](../../../ado/reference/ado-api/save-method.md)
