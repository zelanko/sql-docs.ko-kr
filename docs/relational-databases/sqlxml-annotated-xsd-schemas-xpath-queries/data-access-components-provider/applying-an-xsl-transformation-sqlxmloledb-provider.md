---
title: XSL 변환 적용 (SQLXMLOLEDB)
description: SQLXMLOLEDB 공급자의 Client Xml 및 xsl 속성을 사용 하 여 ADO 응용 프로그램에서 XSL 변환을 적용 하는 방법에 대해 알아봅니다.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXMLOLEDB Provider, applying XSL transformations
- applying XSL transformations [SQLXML]
- xsl property
- Base Path property
- XSL Transformations [SQLXML]
ms.assetid: cb5e41ab-dd20-4873-af20-f417bd1bbf6d
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 13b34c51cf1d963613cab47455e718d6b46c8f5b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479254"
---
# <a name="applying-an-xsl-transformation-sqlxmloledb-provider"></a>XSL 변환 적용(SQLXMLOLEDB 공급자)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  이 예제 ADO 애플리케이션에서는 SQL 쿼리를 실행하고 결과에 XSL 변환을 적용합니다. Clientside Xml 속성을 True로 설정 하면 클라이언트 쪽에서 행 집합의 처리가 적용 됩니다. 이 예에서는 명령 언어가 {5d531cb2-e6ed-11d2-b252-00c04f681b71}로 설정되었는데 그 이유는 SQL 쿼리가 템플릿에 지정되었고, 템플릿을 실행하려면 이 명령 언어를 지정해야 하기 때문입니다. Xsl 속성은 변환을 적용 하는 데 사용할 XSL 파일을 지정 합니다. 기본 경로 속성의 값은 XSL 파일을 검색 하는 데 사용 됩니다. Xsl 속성의 값에 경로를 지정 하는 경우 경로는 기본 경로 속성에 지정 된 경로를 기준으로 합니다.  
  
 이 예에서는 다음 SQLXMLOLEDB 공급자별 속성을 사용하는 방법을 보여 줍니다.  
  
-   ClientSideXML  
  
-   xsl  
  
 이 클라이언트 쪽 ADO 예제 애플리케이션에서는 SQL 쿼리로 구성된 XML 템플릿을 서버에서 실행합니다.  
  
 ClientSideXML 속성이 True로 설정 되어 있기 때문에 FOR XML 절이 없는 SELECT 문이 서버에 전송 됩니다. 서버는 쿼리를 실행하고 클라이언트로 행 집합을 반환합니다. 그러면 클라이언트에서는 행 집합에 FOR XML 변환을 적용하여 XML 문서를 생성합니다.  
  
 Xsl 속성은 응용 프로그램에서 지정 됩니다. 따라서 XSL 변환은 클라이언트에서 생성 되는 XML 문서에 적용 되 고 결과는 두 개의 열로 이루어진 테이블입니다.  
  
 템플릿 명령을 실행 하려면 XML 템플릿 언어 {5d531cb2-e6ed-11d2-b252-00c04f681b71}-를 지정 해야 합니다.  
  
> [!NOTE]  
>  코드에서 연결 문자열에 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름을 지정해야 합니다. 또한 이 예에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 데이터 공급자로 사용하도록 지정하는데 이를 위해서는 추가 네트워크 클라이언트 소프트웨어가 설치되어 있어야 합니다. 자세한 내용은 [SQL Server Native Client에 대 한 시스템 요구 사항](../../../relational-databases/native-client/system-requirements-for-sql-server-native-client.md)을 참조 하세요.  
  
```  
Option Explicit  
Sub main()  
Dim oTestStream As New ADODB.Stream  
Dim oTestConnection As New ADODB.Connection  
Dim oTestCommand As New ADODB.Command  
oTestConnection.Open "provider=SQLXMLOLEDB.4.0;data provider=SQLNCLI11;data source=SqlServerName;initial catalog=AdventureWorks;Integrated Security=SSPI;"  
Set oTestCommand.ActiveConnection = oTestConnection  
oTestCommand.Properties("ClientSideXML") = True  
oTestCommand.CommandText = _  
        "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql' >" & _  
       " <sql:query> " & _  
        "   SELECT TOP 25 FirstName, LastName FROM Person.Contact FOR XML AUTO " & _  
        "   </sql:query> " & _  
        " </ROOT> "  
oTestStream.Open  
' You need the dialect if you are executing a template.  
oTestCommand.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
oTestCommand.Properties("Output Stream").Value = oTestStream  
oTestCommand.Properties("Base Path").Value = "c:\Schemas\SQLXML4\ExecuteTemplateWithXSL\"  
oTestCommand.Properties("xsl").Value = "myxsl.xsl"  
oTestCommand.Execute , , adExecuteStream  
  
oTestStream.Position = 0  
oTestStream.Charset = "utf-8"  
Debug.Print oTestStream.ReadText(adReadAll)  
End Sub  
Sub Form_Load()  
 main  
End Sub  
```  
  
 다음은 XSL 템플릿입니다. 이 XSL 템플릿을 적용하면 2열 테이블이 생성됩니다.  
  
```  
<?xml version='1.0' encoding='UTF-8'?>            
 <xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">   
  
    <xsl:template match = 'Person.Contact'>  
       <TR>  
         <TD><xsl:value-of select = '@FirstName' /></TD>  
         <TD><B><xsl:value-of select = '@LastName' /></B></TD>  
       </TR>  
    </xsl:template>  
    <xsl:template match = '/'>  
      <HTML>  
        <HEAD>  
           <STYLE>th { background-color: #CCCCCC }</STYLE>  
        </HEAD>  
        <BODY>  
         <TABLE border='1' style='width:300;'>  
           <TR><TH colspan='2'>Contacts</TH></TR>  
           <TR>  
              <TH >First name</TH>  
              <TH>Last name</TH>  
           </TR>  
           <xsl:apply-templates select = 'ROOT' />  
         </TABLE>  
        </BODY>  
      </HTML>  
    </xsl:template>  
</xsl:stylesheet>  
```  
  
  
