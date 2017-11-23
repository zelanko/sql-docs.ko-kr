---
title: "결과 집합 스트림으로 검색 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- streams [ADO], retrieving query results
- query results into stream [ADO]
- retrieving results into stream [ADO]
ms.assetid: 996c1321-c926-4f57-8297-85c8c20de974
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ed2d2412cf8314875f9469689677c22ae4e60e7e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="retrieving-resultsets-into-streams"></a>스트림으로 결과 집합을 검색합니다.
기존에 결과 수신 하는 대신 **레코드 집합** 개체, ADO는 스트림으로 대신 쿼리 결과 검색할 수 있습니다. ADO **스트림** 개체 (또는 다른 개체를 지 원하는 COM **IStream** ASP 같은 인터페이스 **요청** 및 **응답** 개체 )는 이러한 결과 포함 하는 데 사용할 수 있습니다. XML 형식으로 결과 검색 하는이 기능을 사용 합니다. SQL server에서는 예를 들어 XML 결과 수 반환할 SQL SELECT 쿼리에서 FOR XML 절을 사용 하 여 XPath 쿼리를 사용 하 여 등 여러 가지 방법으로입니다.  
  
 쿼리 결과를 받으려면 대신 스트림 형식에는 **레코드 집합**를 지정 해야 합니다는 **adExecuteStream** 에서 상수 **ExecuteOptionEnum** 의 매개 변수로 **Execute** 의 메서드는 **명령** 개체입니다. 공급자에이 기능을 지 원하는 경우 결과 실행 시 스트림에서 반환 됩니다. 코드를 실행 하기 전에 추가 공급자별 속성을 지정 해야 할 수 있습니다. Microsoft OLE DB Provider for SQL Server와 같은 사용 예를 들어 **출력 스트림에** 에 **속성** 의 컬렉션은 **명령** 개체 여야 합니다 지정 합니다. 이 기능과 관련 된 SQL Server 관련 동적 속성에 대 한 자세한 내용은 SQL Server 온라인 설명서의 XML-Related 속성을 참조 하십시오.  
  
## <a name="for-xml-query-example"></a>XML 쿼리 예를 보려면  
 다음 예에서는 VBScript에서 Northwind 데이터베이스에 기록 됩니다.  
  
```  
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
  
 FOR XML 절을 사용 하면 SQL Server 데이터 형식으로 XML 문서를 반환 합니다.  
  
### <a name="for-xml-syntax"></a>XML 구문에 대 한  
  
```  
FOR XML [RAW|AUTO|EXPLICIT]  
```  
  
 원시 XML에서 특성으로 열 값이 있는 요소를 제네릭 행을 생성 합니다. FOR XML AUTO 휴리스틱을 사용 하 여 테이블 이름을 기반으로 하는 요소 이름을 사용 하 여 계층적 트리를 생성 합니다. FOR XML EXPLICIT 범용 테이블 메타 데이터에서 완벽 하 게 설명 하는 관계를 생성 합니다.  
  
 SQL SELECT FOR XML 문을 예는 다음과 같습니다.  
  
```  
SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO  
```  
  
 이 명령은 같이 이전에 할당 된 문자열에 지정할 수 있습니다 **CommandText**, 또는 XML 서식 파일에 할당 된 쿼리 형식 **CommandStream**합니다. XML 서식 파일 쿼리에 대 한 자세한 내용은 참조 하십시오. [스트림을 명령](../../../ado/guide/data/command-streams.md) ADO 또는 SQL Server 온라인 설명서에 명령 입력에 대 한 스트림을 사용 합니다.  
  
 XML 서식 파일 쿼리로 FOR XML 쿼리는 다음과 같이 나타납니다.  
  
```  
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO </sql:query>  
```  
  
 이 예에서는 ASP 지정 **응답** 개체에 대 한는 **출력 스트림에** 속성:  
  
```  
adoCmd.Properties("Output Stream") = Response  
```  
  
 그런 다음 지정 **adExecuteStream** 의 매개 변수 **Execute**합니다. 이 예에서는 XML 데이터 아일랜드를 만들려면 XML 태그에서 스트림을 래핑합니다.  
  
```  
Response.write "<XML ID=MyDataIsle>"  
adoCmd.Execute , , adExecuteStream  
Response.write "</XML>"  
```  
  
### <a name="remarks"></a>주의  
 이 시점에서 클라이언트 브라우저에 XML 스트리밍된 및 표시 될 준비가 된 것입니다. 이 XML 문서를 HTML에서 제품의 목록을 작성 하는 DOM 및 각 자식 노드 전체 반복의 인스턴스로 바인딩할 클라이언트 측 VBScript를 사용 하 여 수행 됩니다.
