---
title: SQL 쿼리 실행(SQLXMLOLEDB 공급자)
description: 클라이언트 쪽 SQL 쿼리를 실행할 때 SQLXMLOLEDB 공급자의 Clientside Xml 및 xml 루트 속성을 사용 하는 방법에 대해 알아봅니다.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- queries [SQLXML], SQLXMLOLEDB Provider
- xml root property [SQLXML]
- SQLXMLOLEDB Provider, executing SQL queries
- SQL queries [SQLXML]
ms.assetid: 50334cf5-9c87-4c00-9beb-e08577c4fa82
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a54a5cc0612a1740be9c6884bcc65c25b16b3fa3
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467164"
---
# <a name="executing-sql-queries-sqlxmloledb-provider"></a>SQL 쿼리 실행(SQLXMLOLEDB 공급자)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  이 예에서는 다음 SQLXMLOLEDB 공급자별 속성을 사용하는 방법을 보여 줍니다.  
  
-   ClientSideXML  
  
-   xml root  
  
 이 클라이언트 쪽 ADO 예제 애플리케이션에서는 예제 SQL 쿼리가 클라이언트에서 실행됩니다. ClientSideXML 속성이 True로 설정 되어 있기 때문에 FOR XML 절이 없는 SELECT 문이 서버에 전송 됩니다. 서버는 쿼리를 실행하고 클라이언트로 행 집합을 반환합니다. 그러면 클라이언트에서는 행 집합에 FOR XML 변환을 적용하여 XML 문서를 생성합니다.  
  
 Xml root 속성은 생성 되는 XML 문서에 대해 단일 최상위 루트 요소를 제공 합니다.  
  
> [!NOTE]  
>  코드에서 연결 문자열에 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름을 지정해야 합니다. 또한 이 예에서는 데이터 공급자에 대해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client(SQLNCLI11)를 사용하도록 지정하는데, 이렇게 하려면 추가 네트워크 클라이언트를 설치해야 합니다. 자세한 내용은 [SQL Server Native Client에 대 한 시스템 요구 사항](../../../relational-databases/native-client/system-requirements-for-sql-server-native-client.md)을 참조 하세요.  
  
```  
Option Explicit  
Sub main()  
Dim oTestStream As New ADODB.Stream  
Dim oTestConnection As New ADODB.Connection  
Dim oTestCommand As New ADODB.Command  
  
oTestConnection.Open "provider=SQLXMLOLEDB.4.0;data provider=SQLNCLI11;data source=SqlServerName;initial catalog=AdventureWorks;Integrated Security=SSPI ;"  
oTestCommand.ActiveConnection = oTestConnection  
oTestCommand.Properties("ClientSideXML") = True  
oTestCommand.CommandText = "SELECT TOP 10 FirstName, LastName FROM Person.Contact FOR XML AUTO"  
oTestStream.Open  
oTestCommand.Properties("Output Stream").Value = oTestStream  
oTestCommand.Properties("xml root") = "root"  
oTestCommand.Execute , , adExecuteStream  
  
oTestStream.Position = 0  
oTestStream.Charset = "utf-8"  
Debug.Print oTestStream.ReadText(adReadAll)  
End Sub  
Sub Form_Load()  
 main  
End Sub  
```  
  
  
