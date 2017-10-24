---
title: "버전 속성 예제 (VB) | Microsoft Docs"
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
- Version property [ADO], Visual Basic example
ms.assetid: 708efd50-2905-4168-b7e4-91b2e9b23539
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d9eff4d790e78fc96cd9922b29cbcd6248f81e44
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="version-property-example-vb"></a>버전 속성 예제 (VB)
사용 하 여이 예제는 [버전](../../../ado/reference/ado-api/version-property-ado.md) 속성은 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 현재 ADO 버전을 표시 하는 개체입니다. 또한 여러 동적 속성을 사용 하 여 보여 줍니다.  
  
-   현재 DBMS 이름과 버전입니다.  
  
-   OLE DB 버전입니다.  
  
-   공급자 이름 및 버전입니다.  
  
-   ODBC 버전입니다.  
  
-   ODBC 드라이버 이름과 버전입니다.  
  
```  
'BeginVersionVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strVersionInfo As String  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    strVersionInfo = "ADO Version: " & Cnxn.Version & vbCr  
    strVersionInfo = strVersionInfo & "DBMS Name: " & Cnxn.Properties("DBMS Name") & vbCr  
    strVersionInfo = strVersionInfo & "DBMS Version: " & Cnxn.Properties("DBMS Version") & vbCr  
    strVersionInfo = strVersionInfo & "OLE DB Version: " & Cnxn.Properties("OLE DB Version") & vbCr  
    strVersionInfo = strVersionInfo & "Provider Name: " & Cnxn.Properties("Provider Name") & vbCr  
    strVersionInfo = strVersionInfo & "Provider Version: " & Cnxn.Properties("Provider Version") & vbCr  
  
    MsgBox strVersionInfo  
  
    ' clean up  
    Cnxn.Close  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndVersionVB  
```  
  
## <a name="see-also"></a>관련 항목:  
 [연결 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Version 속성(ADO)](../../../ado/reference/ado-api/version-property-ado.md)

