---
title: 결과 집합을 스트림으로 검색 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/20/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- streams [ADO], retrieving query results
- query results into stream [ADO]
- retrieving results into stream [ADO]
ms.assetid: 996c1321-c926-4f57-8297-85c8c20de974
author: rothja
ms.author: jroth
ms.openlocfilehash: b20363f3ffae96750046ab98bd623ea44d68a8e2
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760929"
---
# <a name="retrieving-resultsets-into-streams"></a>스트림으로 결과 집합 검색
기존 **Recordset** 개체에서 결과를 수신 하는 대신 ADO는 대신 스트림에 쿼리 결과를 검색할 수 있습니다. ADO **Stream** 개체 또는 ASP **요청** 및 **응답** 개체와 같은 COM **IStream** 인터페이스를 지 원하는 다른 개체를 사용 하 여 이러한 결과를 포함할 수 있습니다. 이 기능을 사용 하는 한 가지 방법은 XML 형식의 결과를 검색 하는 것입니다. 예를 들어 SQL Server를 사용 하는 경우 FOR XML 절을 SQL SELECT 쿼리와 함께 사용 하거나 XPath 쿼리를 사용 하는 등의 여러 가지 방법으로 XML 결과를 반환할 수 있습니다.  
  
 **레코드 집합**대신 스트림 형식으로 쿼리 결과를 받으려면 **Executeoptionenum** 의 **adExecuteStream** 상수를 **명령** 개체의 **Execute** 메서드 매개 변수로 지정 해야 합니다. 공급자가이 기능을 지 원하는 경우 실행 시 스트림에 결과가 반환 됩니다. 코드를 실행 하기 전에 추가 공급자별 속성을 지정 해야 할 수도 있습니다. 예를 들어 SQL Server에 대 한 Microsoft OLE DB 공급자를 사용 하는 경우 **명령** 개체의 **properties** 컬렉션에 있는 **출력 스트림과** 같은 속성을 지정 해야 합니다. 이 기능과 관련 된 SQL Server 특정 동적 속성에 대 한 자세한 내용은 SQL Server 온라인 설명서의 XML 관련 속성을 참조 하십시오.  
  
## <a name="for-xml-query-example"></a>FOR XML 쿼리 예제  
 다음 예제는 Northwind 데이터베이스에 VBScript로 작성 되었습니다.  
  
```html
<!-- BeginRecordAndStreamVBS -->  
<%@ LANGUAGE = VBScript %>  
<%  Option Explicit      %>  
  
<HTML>  
<HEAD>  
<META NAME="GENERATOR" Content="Microsoft Developer Studio"/>  
<META HTTP-EQUIV="Content-Type" content="text/html"; charset="iso-8859-1">  
<TITLE>FOR XML Query Example</TITLE>  
  
<STYLE>  
   BODY  
   {  
      FONT-FAMILY: Tahoma;  
      FONT-SIZE: 8pt;  
      OVERFLOW: auto  
   }  
  
   H3  
   {  
      FONT-FAMILY: Tahoma;  
      FONT-SIZE: 8pt;  
      OVERFLOW: auto  
   }  
</STYLE>  
  
<!-- #include file="adovbs.inc" -->  
<%  
   Response.Write "<H3>Server-side processing</H3>"  
  
   Response.Write "Page Generated @ " & Now() & "<BR/>"  
  
   Dim adoConn  
   Set adoConn = Server.CreateObject("ADODB.Connection")  
  
   Dim sConn  
   sConn = "Provider=SQLOLEDB;Data Source=" & _  
      Request.ServerVariables("SERVER_NAME") & ";" & _  
      Initial Catalog=Northwind;Integrated Security=SSPI;"  
  
   Response.write "Connect String = " & sConn & "<BR/>"  
  
   adoConn.ConnectionString = sConn  
   adoConn.CursorLocation = adUseClient  
  
   adoConn.Open  
  
   Response.write "ADO Version = " & adoConn.Version & "<BR/>"  
   Response.write "adoConn.State = " & adoConn.State & "<BR/>"  
  
   Dim adoCmd  
   Set adoCmd = Server.CreateObject("ADODB.Command")  
   Set adoCmd.ActiveConnection = adoConn  
  
   Dim sQuery  
   sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'><sql:query>SELECT * FROM PRODUCTS WHERE ProductName='Gumbr Gummibrchen' FOR XML AUTO</sql:query></ROOT>"  
  
   Response.write "Query String = " & sQuery & "<BR/>"  
  
   Dim adoStreamQuery  
   Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
   adoStreamQuery.Open  
   adoStreamQuery.WriteText sQuery, adWriteChar  
   adoStreamQuery.Position = 0  
  
   adoCmd.CommandStream = adoStreamQuery  
   adoCmd.Dialect = "{5D531CB2-E6Ed-11D2-B252-00C04F681B71}"  
  
   Response.write "Pushing XML to client for processing "  & "<BR/>"  
  
   adoCmd.Properties("Output Stream") = Response  
   Response.write "<XML ID='MyDataIsle'>"  
   adoCmd.Execute , , 1024  
   Response.write "</XML>"  
  
%>  
  
<SCRIPT language="VBScript" For="window" Event="onload">  
   Dim xmlDoc  
   Set xmlDoc = MyDataIsle.XMLDocument  
   xmlDoc.resolveExternals=false  
   xmlDoc.async=false  
  
   If xmlDoc.parseError.Reason <> "" then  
      Msgbox "parseError.Reason = " & xmlDoc.parseError.Reason  
   End If  
  
   Dim root, child  
   Set root = xmlDoc.documentElement  
   For each child in root.childNodes  
      dim OutputXML  
      OutputXML = document.all("log").innerHTML  
      document.all("log").innerHTML = OutputXML & "<LI>" & child.getAttribute("ProductName") & "</LI>"  
   Next  
</SCRIPT>  
  
</HEAD>  
  
<BODY>  
  
   <H3>Client-side processing of XML Document MyDataIsle</H3>  
   <UL id=log>  
   </UL>  
  
</BODY>  
</HTML>  
<!-- EndRecordAndStreamVBS -->  
  
```  
  
 FOR XML 절은 XML 문서 형식으로 데이터를 반환 하도록 SQL Server에 지시 합니다.  
  
### <a name="for-xml-syntax"></a>FOR XML 구문  
  
```syntax
FOR XML [RAW|AUTO|EXPLICIT]  
```  
  
 FOR XML RAW는 열 값이 특성으로 포함 된 일반 행 요소를 생성 합니다. FOR XML AUTO는 추론을 사용 하 여 테이블 이름에 따라 요소 이름이 있는 계층적 트리를 생성 합니다. FOR XML EXPLICIT는 메타 데이터에 의해 완전히 설명 된 관계로 범용 테이블을 생성 합니다.  
  
 예제 SQL SELECT FOR XML 문은 다음과 같습니다.  
  
```sql
SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO  
```  
  
 명령은 앞에서 설명한 대로 문자열에 지정 하거나, **CommandText**에 할당 하거나, **commandstream**에 할당 된 XML 템플릿 쿼리 형식으로 지정할 수 있습니다. XML 템플릿 쿼리에 대 한 자세한 내용은 ADO의 [명령 스트림](../../../ado/guide/data/command-streams.md) 또는 SQL Server 온라인 설명서에서 명령 입력에 대 한 스트림 사용을 참조 하세요.  
  
 FOR XML 쿼리는 XML 템플릿 쿼리로 다음과 같이 표시 됩니다.  
  
```xml
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO </sql:query>  
```  
  
 이 예에서는 **출력 스트림** 속성에 대해 ASP **Response** 개체를 지정 합니다.  
  
```vb
adoCmd.Properties("Output Stream") = Response  
```  
  
 그런 다음 **Execute**의 **adExecuteStream** 매개 변수를 지정 합니다. 이 예에서는 xml 태그의 스트림을 래핑하여 XML 데이터 아일랜드를 만듭니다.  
  
```vb
Response.write "<XML ID=MyDataIsle>"  
adoCmd.Execute , , adExecuteStream  
Response.write "</XML>"  
```  
  
### <a name="remarks"></a>설명  
 이 시점에서 XML은 클라이언트 브라우저로 스트리밍 되었으며 표시 될 준비가 되었습니다. 이 작업은 클라이언트 쪽 VBScript를 사용 하 여 XML 문서를 DOM 인스턴스에 바인딩하고 각 자식 노드를 반복 하 여 HTML로 제품 목록을 작성 하는 방법으로 수행 됩니다.
