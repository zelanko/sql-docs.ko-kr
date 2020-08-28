---
description: Provider 및 DefaultDatabase 속성 예제 (VB)
title: Provider 및 DefaultDatabase 속성 예제 (VB) | Microsoft Docs
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
- DefaultDatabase property [ADO], Visual Basic example
- provider property [ADO], Visual Basic example
ms.assetid: 677e1dbe-bcf6-4028-a62c-e99b1c88bf7b
author: rothja
ms.author: jroth
ms.openlocfilehash: fec990e1171ec40c93c9db370adb4be2553d33df
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989934"
---
# <a name="provider-and-defaultdatabase-properties-example-vb"></a>Provider 및 DefaultDatabase 속성 예제 (VB)
이 예에서는 다른 공급자를 사용 하 여 세 개의 [연결](./connection-object-ado.md) 개체를 열어 [공급자](./provider-property-ado.md) 속성을 보여 줍니다. 또한 [defaultdatabase](./defaultdatabase-property.md) 속성을 사용 하 여 Microsoft ODBC 공급자에 대 한 기본 데이터베이스를 설정 합니다.  
  
> [!NOTE]
>  Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는 경우 연결 문자열에 사용자 ID 및 암호 정보 대신 **Trusted_Connection = yes** 또는 **INTEGRATED Security = SSPI** 를 지정 해야 합니다.  
  
```  
'BeginProviderVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection strings  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    Dim Cnxn1 As ADODB.Connection  
    Dim Cnxn2 As ADODB.Connection  
    Dim Cnxn3 As ADODB.Connection  
    Dim strCnxn As String  
  
    ' Open a connection using the Microsoft ODBC provider  
    Set Cnxn1 = New ADODB.Connection  
    Cnxn1.ConnectionString = "driver={SQL Server};server='MySqlServer';" & _  
        "user id='MyUserID';password='MyPassword';"  
    Cnxn1.Open strCnxn  
    Cnxn1.DefaultDatabase = "Pubs"  
  
    ' Display the provider  
    MsgBox "Cnxn1 provider: " & Cnxn1.Provider  
  
    ' Open a connection using the Microsoft Jet provider  
    Set Cnxn2 = New ADODB.Connection  
    Cnxn2.Provider = "Microsoft.Jet.OLEDB.4.0"  
    Cnxn2.Open "Northwind.mdb", _  
        "MyUserID", "MyPassword"  
  
    ' Display the provider.  
    MsgBox "Cnxn2 provider: " & Cnxn2.Provider  
  
    ' Open a connection using the Microsoft SQL Server provider  
    Set Cnxn3 = New ADODB.Connection  
    Cnxn3.Provider = "sqloledb"  
    Cnxn3.Open "Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
  
    ' Display the provider  
    MsgBox "Cnxn3 provider: " & Cnxn3.Provider  
  
    ' clean up  
    Cnxn1.Close  
    Cnxn2.Close  
    Cnxn3.Close  
    Set Cnxn1 = Nothing  
    Set Cnxn2 = Nothing  
    Set Cnxn3 = Nothing  
    Exit Sub  
  
ErrorHandler:  
    If Not Cnxn1 Is Nothing Then  
        If Cnxn1.State = adStateOpen Then Cnxn1.Close  
    End If  
    Set Cnxn1 = Nothing  
  
    If Not Cnxn2 Is Nothing Then  
        If Cnxn2.State = adStateOpen Then Cnxn2.Close  
    End If  
    Set Cnxn2 = Nothing  
  
    If Not Cnxn3 Is Nothing Then  
        If Cnxn3.State = adStateOpen Then Cnxn3.Close  
    End If  
    Set Cnxn3 = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
'EndProviderVB  
```  
  
## <a name="see-also"></a>참고 항목  
 [Connection 개체 (ADO)](./connection-object-ado.md)   
 [DefaultDatabase 속성](./defaultdatabase-property.md)   
 [Provider 속성(ADO)](./provider-property-ado.md)