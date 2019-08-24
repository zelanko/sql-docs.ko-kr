---
title: 애플리케이션에서 XML 데이터 사용 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- parameters [XML in SQL Server]
- XML [SQL Server], ADO
- columns [XML in SQL Server], ADO.NET
- ADO [XML in SQL Server]
- columns [XML in SQL Server], SQL Server Native Client
- xml data type [SQL Server], ADO
- SQLNCLI, XML
- xml data type [SQL Server], SQL Server Native Client
- SQL Server Native Client, XML
- ADO.NET [XML in SQL Server]
- XML [SQL Server], ADO.NET
- columns [XML in SQL Server], ADO
- xml data type [SQL Server], ADO.NET
- XML [SQL Server], SQL Server Native Client
ms.assetid: 5dabf7e0-c6df-451d-a070-4661f84607fd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4d9d64edf29d1e494d25474845295c505caedee8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63232424"
---
# <a name="use-xml-data-in-applications"></a>애플리케이션에서 XML 데이터 사용
  이 항목에서는 애플리케이션에서 `xml` 데이터 형식을 사용하기 위해 제공되는 옵션에 대해 설명합니다. 이 항목에는 다음에 대한 정보가 포함됩니다.  
  
-   ADO 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 사용하여 `xml` 유형의 열에서 XML 처리  
  
-   ADO.NET을 사용하여 `xml` 유형의 열에서 XML 처리  
  
-   ADO.NET을 사용하여 매개 변수에서 `xml` 유형 처리  
  
## <a name="handling-xml-from-an-xml-type-column-by-using-ado-and-sql-server-native-client"></a>ADO 및 SQL Server Native Client를 사용하여 xml 유형의 열에서 XML 처리  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 제공된 유형 및 기능에 액세스하여 MDAC 구성 요소를 사용하려면 ADO 연결 문자열에 DataTypeCompatibility 초기화 속성을 설정해야 합니다.  
  
 예를 들어 다음 Visual Basic Scripting Edition(VBScript) 예제는 `Demographics` 예제 데이터베이스의 `Sales.Store` 테이블에서 `AdventureWorks2012`라는 `xml` 데이터 형식 열을 쿼리한 결과를 보여 줍니다. 특히 이 쿼리는 이 열의 항목 값에서 `CustomerID` 가 `3`인 행을 검색합니다.  
  
```  
Const DS = "MyServer"  
Const DB = "AdventureWorks2012"  
  
Set objConn = CreateObject("ADODB.Connection")  
Set objRs = CreateObject("ADODB.Recordset")  
  
CommandText = "SELECT Demographics" & _  
              " FROM Sales.Store" & _  
              " INNER JOIN Sales.Customer" & _  
              " ON Sales.Store.BusinessEntityID = sales.customer.StoreID" & _  
              " WHERE Sales.Customer.CustomerID = 3" & _  
              " OR Sales.Customer.CustomerID = 4"  
  
ConnectionString = "Provider=SQLNCLI11" & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;" & _  
                   "DataTypeCompatibility=80"  
  
'Connect to the data source.  
objConn.Open ConnectionString  
  
'Execute command through the connection and display  
Set objRs = objConn.Execute(CommandText)  
  
Dim rowcount  
rowcount = 0  
Do While Not objRs.EOF  
   rowcount = rowcount + 1  
   MsgBox "Row " & rowcount & _  
           vbCrLf & vbCrLf & objRs(0)  
   objRs.MoveNext  
Loop  
  
'Clean up.  
objRs.Close  
objConn.Close  
Set objRs = Nothing  
Set objConn = Nothing  
```  
  
 이 예에서는 데이터 형식 호환성 속성을 설정하는 방법을 보여 줍니다. 기본적으로 이 속성은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 사용할 경우 0으로 설정됩니다. 이 값을 80으로 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 공급자가 `xml` 및 사용자 정의 형식 열을 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 데이터 형식으로 나타냅니다. 이러한 유형은 각각 DBTYPE_WSTR 및 DBTYPE_BYTES입니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 클라이언트 컴퓨터에도 설치되어 있어야 하며 연결 문자열에는 "`Provider=SQLNCLI11;...`"에서 데이터 공급자로 사용할 수 있도록 이 클라이언트가 지정되어 있어야 합니다.  
  
#### <a name="to-test-this-example"></a>이 예를 테스트하려면  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client가 설치되어 있고 MDAC 2.6.0 이상 버전을 클라이언트 컴퓨터에서 사용할 수 있는지 확인하십시오.  
  
     자세한 내용은 [SQL Server Native Client 프로그래밍](../native-client/sql-server-native-client-programming.md)을 참조하세요.  
  
2.  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 예제 데이터베이스가 설치되어 있는지 확인합니다.  
  
     이 예에는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스가 필요합니다.  
  
3.  이 항목의 앞에 표시된 코드를 복사하여 텍스트 또는 코드 편집기에 붙여 넣습니다. 파일을 HandlingXmlDataType.vbs로 저장합니다.  
  
4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에 필요한 대로 스크립트를 수정하고 변경 내용을 저장합니다.  
  
     예를 들어 `MyServer` 가 지정된 경우 이를 `(local)` 이나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 설치된 서버의 실제 이름으로 바꿔야 합니다.  
  
5.  HandlingXmlDataType.vbs를 실행하고 스크립트를 실행합니다.  
  
 결과는 다음 예제 결과와 비슷해야 합니다.  
  
```  
Row 1  
  
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
  
Row 2  
  
<StoreSurvey xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
  <AnnualSales>300000</AnnualSales>  
  <AnnualRevenue>30000</AnnualRevenue>  
  <BankName>United Security</BankName>  
  <BusinessType>BM</BusinessType>  
  <YearOpened>1976</YearOpened>  
  <Specialty>Road</Specialty>  
  <SquareFeet>6000</SquareFeet>  
  <Brands>2</Brands>  
  <Internet>DSL</Internet>  
  <NumberEmployees>5</NumberEmployees>  
</StoreSurvey>  
```  
  
## <a name="handling-xml-from-an-xml-type-column-by-using-adonet"></a>ADO.NET을 사용하여 xml 유형의 열에서 XML 처리  
 XML을 처리 하는 `xml` ADO.NET을 사용 하 여 데이터 형식 열 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 의 표준 동작을 사용할 수는 `SqlCommand` 클래스입니다. 예를 들어 `xml` 데이터 형식 열과 해당 값은 `SqlDataReader`를 사용하여 SQL 열을 검색하는 것과 같은 방식으로 검색할 수 있습니다. 하지만 `xml` 데이터 형식 열의 콘텐츠를 XML로 사용하려는 경우 이 콘텐츠를 먼저 `XmlReader` 유형에 할당해야 합니다.  
  
 자세한 내용과 코드 예는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] SDK 설명서의 "XML Column Values in a Data Reader"를 참조하십시오.  
  
## <a name="handling-an-xml-type-column-in-parameters-by-using-adonet"></a>ADO.NET을 사용하여 매개 변수의 xml 유형 열 처리  
 ADO.NET 및 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]의 매개 변수로 전달된 xml 데이터 형식을 처리하려면 `SqlXml` 데이터 형식의 인스턴스로 값을 제공할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 `xml` 데이터 형식 열은 `string` 또는 `integer`와 같이 다른 열 및 데이터 형식과 동일한 방식으로 매개 변수 값을 수락할 수 있기 때문에 특수한 조치가 필요하지 않습니다.  
  
 자세한 내용과 코드 예는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] SDK 설명서의 "XML Values as Command Parameters"를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [XML 데이터&#40;SQL Server&#41;](xml-data-sql-server.md)  
  
  
