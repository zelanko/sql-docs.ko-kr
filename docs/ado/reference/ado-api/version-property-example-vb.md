---
title: Version 속성 예제 (VB) | Microsoft Docs
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
- Version property [ADO], Visual Basic example
ms.assetid: 708efd50-2905-4168-b7e4-91b2e9b23539
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 023ee009831cb3576691f0af5dfb85752d51fcc1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67938743"
---
# <a name="version-property-example-vb"></a>Version 속성 예제(VB)
이 예에서는 [Connection](../../../ado/reference/ado-api/connection-object-ado.md) 개체의 [Version](../../../ado/reference/ado-api/version-property-ado.md) 속성을 사용 하 여 현재 ADO 버전을 표시 합니다. 또한 다음과 같은 몇 가지 동적 속성을 사용 하 여 표시 합니다.  
  
-   현재 DBMS 이름 및 버전입니다.  
  
-   OLE DB 버전입니다.  
  
-   공급자 이름 및 버전입니다.  
  
-   ODBC 버전입니다.  
  
-   ODBC 드라이버 이름 및 버전입니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [Connection 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Version 속성(ADO)](../../../ado/reference/ado-api/version-property-ado.md)
