---
title: 애플리케이션 코드에서 FOR XML 결과 사용 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, application code usage
- XML [SQL Server], FOR XML clause
- ASP.NET [SQL Server]
- .NET Framework [SQL Server], FOR XML data
- ADO [SQL Server]
- XML data islands [SQL Server]
- data islands [SQL Server]
ms.assetid: 41ae67bd-ece9-49ea-8062-c8d658ab4154
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9927e5a4477961fbd7122ae96b05e42c74bf2196
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2020
ms.locfileid: "80665054"
---
# <a name="use-for-xml-results-in-application-code"></a>애플리케이션 코드에서 FOR XML 결과 사용
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  SQL 쿼리에서 FOR XML 절을 사용하면 쿼리 결과 검색은 물론 XML 데이터로 캐스팅할 수도 있습니다. 이 기능을 사용하면 XML 애플리케이션 코드에서 FOR XML 쿼리 결과를 사용할 수 있을 때 다음을 수행할 수 있습니다.  
  
-   SQL 테이블에서 [XML 데이터&#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md) 값 인스턴스를 쿼리합니다.  
  
-   [TYPE Directive in FOR XML Queries](../../relational-databases/xml/type-directive-in-for-xml-queries.md) 을 적용하여 XML 유형의 텍스트 또는 이미지 형식의 데이터를 포함하는 쿼리 결과를 반환합니다.  
  
 이 항목에서는 이러한 접근 방식을 보여 주는 예를 제공합니다.  
  
## <a name="retrieving-for-xml-data-with-ado-and-xml-data-islands"></a>ADO 및 XML 데이터 아일랜드로 FOR XML 데이터 검색  
 ADO **Stream** 개체나 ASP(Active Server Pages) **Request** 및 **Response** 개체와 같이 COM **IStream** 인터페이스를 지원하는 다른 개체를 사용하여 FOR XML 쿼리를 사용할 때 결과를 포함시킬 수 있습니다.  
  
 예를 들어 다음 ASP 코드에서는 AdventureWorks 예제 데이터베이스의 Sales.Store 테이블에서 **xml** 데이터 형식의 열인 Demographics를 쿼리한 결과를 보여 줍니다. 특히 이 쿼리는 이 열의 항목 값에서 CustomerID가 3인 행을 검색합니다.  
  
```  
<!-- BeginRecordAndStreamVBS -->  
<%@ LANGUAGE = VBScript %>  
<!-- %  Option Explicit      % -->  
<!-- 'Request.ServerVariables("SERVER_NAME") & ";" & _ -->  
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
   sConn = "Provider=SQLOLEDB;Data Source=(local);" & _  
            "Initial Catalog=AdventureWorks;Integrated Security=SSPI;"  
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
   sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'><sql:query>SELECT Demographics from Sales.Store WHERE CustomerID = 3 FOR XML AUTO</sql:query></ROOT>"  
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
   Dim root  
   Set root = xmlDoc.documentElement.childNodes.Item(0).childNodes.Item(0).childNodes.Item(0)  
   For each child in root.childNodes  
      dim OutputXML  
      OutputXML = document.all("log").innerHTML  
      document.all("log").innerHTML = OutputXML & "<LI><B>" & child.nodeName &  ":</B>  " & child.Text  & "</LI>"  
   Next  
   MsgBox xmlDoc.xml  
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
  
 이 ASP 페이지 예에는 ADO를 사용하여 FOR XML 쿼리를 실행하고 XML 데이터 아일랜드인 MyDataIsle로 XML 결과를 반환하는 서버 쪽 VBScript가 포함됩니다. 이 XML 데이터 아일랜드는 추가 클라이언트 쪽 처리를 위해 브라우저에 반환됩니다. 그런 다음 추가 클라이언트 쪽 VBScript 코드를 사용하여 XML 데이터 아일랜드의 콘텐츠를 처리합니다. 이 프로세스는 콘텐츠를 결과 DHTML의 일부로 표시하고 XML 데이터 아일랜드의 처리된 콘텐츠를 표시하는 메시지 상자를 열기 전에 수행됩니다.  
  
#### <a name="to-test-this-example"></a>이 예를 테스트하려면  
  
1.  IIS가 설치되어 있으며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대한 AdventureWorks 예제 데이터베이스가 설치되었는지 확인합니다.  
  
     이 예에서는 ASP 지원이 설정된 인터넷 정보 서비스(IIS) 버전 5.0 이상이 설치되어 있어야 합니다. 또한 AdventureWorks 예제 데이터베이스가 설치되어 있어야 합니다.  
  
2.  이전에 제공된 코드 예를 복사하여 사용하는 XML 또는 텍스트 편집기에 붙여 넣습니다. IIS에 사용되는 루트 디렉터리에 파일을 RetrieveResults.asp로 저장합니다. 일반적으로 루트 디렉터리의 위치는 C:\Inetpub\wwwroot입니다.  
  
3.  다음 URL을 사용하여 브라우저 창에서 ASP 페이지를 엽니다. 먼저 'MyServer'를 "localhost" 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 IIS가 설치된 서버의 실제 이름으로 바꿉니다.  
  
    ```  
    https://MyServer/RetrieveResults.asp  
    ```  
  
 생성된 HTML 페이지 결과는 다음 예제 출력과 유사하게 표시됩니다.  
  
##### <a name="server-side-processing"></a>서버 쪽 처리  
 Page Generated \@ 3/11/2006 3:36:02 PM  
  
 Connect String = Provider=SQLOLEDB;Data Source=MyServer;Initial Catalog=AdventureWorks;Integrated Security=SSPI;  
  
 ADO Version = 2.8  
  
 adoConn.State = 1  
  
 Query String = SELECT Demographics from Sales.Store WHERE CustomerID = 3 FOR XML AUTO  
  
 Pushing XML to client for processing  
  
##### <a name="client-side-processing-of-xml-document-mydataisle"></a>XML 문서 MyDataIsle의 클라이언트 쪽 처리  
  
-   **AnnualSales:** 1500000  
  
-   **AnnualRevenue:** 150000  
  
-   **BankName:** Primary International  
  
-   **BusinessType:** OS  
  
-   **YearOpened:** 1974  
  
-   **Specialty:** Road  
  
-   **SquareFeet:** 38000  
  
-   **Brands:** 3  
  
-   **Internet:** DSL  
  
-   **NumberEmployees:** 40  
  
 그런 다음 VBScript 메시지 상자에 FOR XML 쿼리 결과에 의해 반환된 다음과 같은 원래의 필터링되지 않은 XML 데이터 아일랜드 콘텐츠가 표시됩니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Sales.Store>  
    <Demographics>  
      <StoreSurvey xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
        <AnnualSales>1500000</AnnualSales>  
        <AnnualRevenue>150000</AnnualRevenue>  
        <BankName>Primary International</BankName>  
        <BusinessType>OS</BusinessType>  
        <YearOpened>1974</YearOpened>  
        <Specialty>Road</Specialty>  
        <SquareFeet>38000</SquareFeet>  
        <Brands>3</Brands>  
        <Internet>DSL</Internet>  
        <NumberEmployees>40</NumberEmployees>  
      </StoreSurvey>  
    </Demographics>  
  </Sales.Store>  
</ROOT>  
```  
  
## <a name="retrieving-for-xml-data-with-aspnet-and-the-net-framework"></a>ASP.NET 및 .NET Framework에서 FOR XML 데이터 검색  
 이전 예에서와 같이 다음 ASP.NET 코드에서는 AdventureWorks 예제 데이터베이스의 Sales.Store 테이블에서 **xml** 데이터 형식의 열인 Demographics를 쿼리한 결과를 보여 줍니다. 이전 예에서와 같이 이 쿼리는 이 열의 항목 값에서 CustomerID가 3인 행을 검색합니다.  
  
 이 예에서는 다음 Microsoft .NET Framework 관리 API를 사용하여 FOR XML 쿼리 결과를 반환 및 렌더링합니다.  
  
1.  **SqlConnection** 을 사용하여 지정된 연결 문자열 변수인 strConn의 내용에 따라 SQL Server에 대한 연결을 엽니다.  
  
2.  그런 다음**SqlDataAdapter** 를 데이터 어댑터로 사용하고 SQL 연결 및 지정된 SQL 쿼리 문자열을 사용하여 FOR XML 쿼리를 실행합니다.  
  
3.  쿼리가 실행된 후 **SqlDataAdapter.Fill** 메서드를 호출하고 데이터 세트 인 **DataSet,** MyDataSet의 해당 항목을 전달하여 데이터 세트 에 FOR XML 쿼리 출력을 채웁니다.  
  
4.  그런 다음, **DataSet.GetXml** 메서드를 호출하여 서버에서 생성된 HTML 페이지에 표시될 수 있는 문자열로 쿼리 결과를 반환합니다.  
  
    ```  
    <%@ Page Language="VB" %>  
    <HTML>  
    <HEAD>  
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
    </HEAD>  
    <BODY>  
    <%  
    Dim s as String  
    s = "<H3>Server-side processing</H3>" & _  
        "Page Generated @ " & Now() & "<BR/>"  
  
    Dim SQL As String   
    SQL = "SELECT Demographics from Sales.Store WHERE CustomerID = 3 FOR XML AUTO"  
  
    Dim strConn As String   
    strConn = "Server=(local);Database=AdventureWorks;Integrated Security=SSPI;"  
  
    Dim MySqlConn As New System.Data.SqlClient.SqlConnection(strConn)  
    Dim MySqlAdapter As New System.Data.SqlClient.SqlDataAdapter(SQL,MySqlConn)  
    Dim MyDataSet As New System.Data.DataSet  
  
    MySqlConn.Open()  
    s = s & "<P>SqlConnection opened.</P>"   
  
    MySqlAdapter.Fill(MyDataSet)  
    s = s & "<P>" & MyDataSet.GetXml  & "</P>"  
  
    MySqlConn.Close()  
    s = s & "<P>SqlConnection closed.</P>"   
  
    Message.InnerHtml=s  
    %>  
    <SPAN id="Message" runat=server />  
    </BODY>  
    </HTML>  
    ```  
  
#### <a name="to-test-this-example"></a>이 예를 테스트하려면  
  
1.  IIS가 설치되어 있으며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대한 AdventureWorks 예제 데이터베이스가 설치되었는지 확인합니다.  
  
     이 예에서는 ASP.NET 지원이 설정된 인터넷 정보 서비스(IIS) 버전 5.0 이상이 설치되어 있어야 합니다. 또한 AdventureWorks 예제 데이터베이스가 설치되어 있어야 합니다.  
  
2.  이전에 제공된 코드를 복사하여 사용하는 XML 또는 텍스트 편집기에 붙여 넣습니다. IIS에 사용되는 루트 디렉터리에 파일을 RetrieveResults.aspx로 저장합니다. 일반적으로 루트 디렉터리의 위치는 C:\Inetpub\wwwroot입니다.  
  
3.  다음 URL을 사용하여 브라우저 창에서 ASP.NET 페이지를 엽니다. 먼저 'MyServer'를 "localhost" 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 IIS가 설치된 서버의 실제 이름으로 바꿉니다.  
  
    ```  
    https://MyServer/RetrieveResults.aspx  
    ```  
  
 생성된 HTML 페이지 결과는 다음 예제 출력과 유사하게 표시됩니다.  
  
##### <a name="server-side-processing"></a>서버 쪽 처리  
  
```  
Page Generated @ 3/11/2006 3:36:02 PM  
  
SqlConnection opened.  
  
<Sales.Store><Demographics><StoreSurvey xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey"><AnnualSales>1500000</AnnualSales><AnnualRevenue>150000</AnnualRevenue><BankName>Primary International</BankName><BusinessType>OS</BusinessType><YearOpened>1974</YearOpened><Specialty>Road</Specialty><SquareFeet>38000</SquareFeet><Brands>3</Brands><Internet>DSL</Internet><NumberEmployees>40</NumberEmployees></StoreSurvey></Demographics></Sales.Store>  
  
SqlConnection closed.  
```  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**xml** 데이터 형식 지원을 통해 **TYPE 지시어** 를 지정하여 FOR XML 쿼리의 결과가 문자열이나 이미지 형식의 데이터 대신 [xml](../../relational-databases/xml/type-directive-in-for-xml-queries.md)데이터 형식으로 반환되도록 요청할 수 있습니다. FOR XML 쿼리에서 TYPE 지시어가 사용된 경우 이 지시어는 [애플리케이션에서 XML 데이터 사용](../../relational-databases/xml/use-xml-data-in-applications.md)에 표시된 것과 비슷하게 FOR XML 결과에 대한 프로그래밍 방식의 액세스를 제공합니다.  
  
## <a name="see-also"></a>참고 항목  
 [FOR XML&#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
