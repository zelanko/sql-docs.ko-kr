---
title: SQL 쿼리 (SQLXMLOLEDB 공급자)를 포함 하는 템플릿 실행 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- templates [SQLXML]
- SQLXMLOLEDB Provider, executing template files
- templates [SQLXML], SQL queries
- XML templates [SQLXML]
- SQL queries [SQLXML]
ms.assetid: ff2bc36f-e3fb-4d8f-8e3a-2680a39eda11
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: affea1983c83dbf3cd0a8f5ab82292f88f1cae65
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080592"
---
# <a name="executing-templates-that-contain-sql-queries-sqlxmloledb-provider"></a>SQL 쿼리를 포함하는 템플릿 실행(SQLXMLOLEDB 공급자)
  이 예에서는 SQLXMLOLEDB 공급자별 속성 ClientSideXML 사용을 보여 줍니다. 이 클라이언트 쪽 ADO 예제 응용 프로그램에서는 SQL 쿼리로 구성된 XML 템플릿을 서버에서 실행합니다.  
  
 ClientSideXML 속성을 True로 설정 때문에 FOR XML 절이 없는 SELECT 문이 서버로 전송 됩니다. 서버는 쿼리를 실행하고 클라이언트로 행 집합을 반환합니다. 그러면 클라이언트에서는 행 집합에 FOR XML 변환을 적용하여 XML 문서를 생성합니다.  
  
 단일 최상위 루트 요소를 제공 하는 XML 서식 파일 (\<루트 >) XML 문서에 대 한 생성 된; 따라서 xml 루트 속성은 제공 되지 않습니다.  
  
 XML 템플릿을 실행하려면 언어 {5d531cb2-e6ed-11d2-b252-00c04f681b71}을 지정해야 합니다.  
  
> [!NOTE]  
>  코드에서 연결 문자열에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름을 지정해야 합니다. 또한 이 예에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client(SQLNCLI11)를 데이터 공급자로 사용하도록 지정하고 있으며 이를 위해서는 추가 네트워크 클라이언트 소프트웨어가 설치되어 있어야 합니다. 자세한 내용은 참조 [SQL Server Native Client에 대 한 시스템 요구 사항](../../native-client/system-requirements-for-sql-server-native-client.md)합니다.  
  
```  
Option Explicit  
  
Sub Main()  
  Dim oTestStream As New ADODB.Stream  
  Dim oTestConnection As New ADODB.Connection  
  Dim oTestCommand As New ADODB.Command  
  oTestConnection.Open "Provider=SQLXMLOLEDB.4.0;Data Provider=SQLNCLI11;Data Source=SqlServerName;Initial Catalog=AdventureWorks;Integrated Security=SSPI;"  
  
  Set oTestCommand.ActiveConnection = oTestConnection  
  oTestCommand.Properties("ClientSideXML") = True  
  oTestCommand.CommandText = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'> " & _  
        " <sql:query> " & _  
        "   SELECT TOP 10 FirstName, LastName FROM Person.Contact FOR XML AUTO " & _  
        "   </sql:query> " & _  
        " </ROOT> "  
  oTestStream.Open  
  ' You need the dialect if you are executing   
  ' XML templates (not for SQL queries).  
  oTestCommand.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  oTestCommand.Properties("Output Stream").Value = oTestStream  
  oTestCommand.Execute , , adExecuteStream  
  
  oTestStream.Position = 0  
  oTestStream.Charset = "utf-8"  
  Debug.Print oTestStream.ReadText(adReadAll)  
End Sub  
  
Sub Form_Load()  
  Main  
End Sub  
```  
  
  