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
manager: craigg
ms.openlocfilehash: 313ebe2cee8fdae430401eb5443604a84b057a83
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63241144"
---
# <a name="save-and-open-methods-example-vb"></a>Save 및 Open 메서드 예제(VB)
이러한 세 가지 예를 보여 줍니다 하는 방법을 [저장](../../../ado/reference/ado-api/save-method.md) 하 고 [오픈](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드를 함께 사용할 수 있습니다.  
  
 출장 예정인을 데이터베이스에서 테이블 가져가려는 가정 합니다. 진행 하기 전에으로 데이터에 액세스 하는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 이동 가능한 형식으로 저장 합니다. 대상에 도착 하는 경우 액세스를 **Recordset** 는 로컬 연결이 끊긴 **레코드 집합**. 변경 하는 **레코드 집합**, 한 다음 다시 저장 합니다. 마지막으로, 홈을 반환 하는 경우 데이터베이스에 다시 연결을 이동 중에 변경한 내용으로 업데이트.  
  
 첫째, 액세스 및 저장 합니다 ***작성자*** 테이블입니다.  
  
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
  
 이 시점에서 대상에 도착 했습니다. 액세스는 ***작성자*** 로컬 테이블로 연결 끊김 **레코드 집합**합니다. 있어야 합니다 **MSPersist** 저장된 된 파일에 액세스 하는 데 사용 하는 컴퓨터의 공급자 a:\Pubs.xml 합니다.  
  
```  
Attribute VB_Name = "Save"  
```  
  
 마지막으로 돌아가면 홈입니다. 이제 데이터베이스에서 변경 내용을 업데이트 합니다.  
  
```  
Attribute VB_Name = "Save"  
```  
  
## <a name="see-also"></a>관련 항목  
 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [레코드 집합 지 속성에 대 한 자세한 정보](../../../ado/guide/data/more-about-recordset-persistence.md)   
 [Save 메서드](../../../ado/reference/ado-api/save-method.md)
