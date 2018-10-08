---
title: ASP.NET에서 중첩 FOR XML 쿼리 사용 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, nested FOR XML queries
- queries [XML in SQL Server], ASP.NET and
- nested FOR XML queries in ASP.NET
- ASP.NET [SQL Server]
ms.assetid: 691ac7dd-afc5-4760-932c-2b1dcd9394ed
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5302085b959f212e4397a6dc5866c8112c28a681
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47665961"
---
# <a name="use-nested-for-xml-queries-in-aspnet"></a>ASP.NET에서 중첩 FOR XML 쿼리 사용
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  이 예에서ASP.NET 응용 프로그램은 SQL Server에서 저장 프로시저를 실행하여 브라우저에  XML을 반환합니다. 저장 프로시저는 중첩 쿼리를 사용하여 XML을 생성합니다. 유사한 SELECT 문은 [중첩 AUTO 모드 쿼리를 사용하여 형제 생성](../../relational-databases/xml/generate-siblings-with-a-nested-auto-mode-query.md)항목에 설명되어 있습니다. 다음 예에서는 중첩 FOR XML 쿼리를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 요소 중심 XML을 생성하는 한 가지 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
  
```  
CREATE PROC GetSalesOrderInfo AS  
SELECT   
      (SELECT top 2 SalesOrderID, SalesPersonID, CustomerID,  
         (select top 3 SalesOrderID, ProductID, OrderQty, UnitPrice  
           from Sales.SalesOrderDetail  
            WHERE  SalesOrderDetail.SalesOrderID = SalesOrderHeader.SalesOrderID  
            FOR XML AUTO, TYPE)  
      FROM  Sales.SalesOrderHeader  
        WHERE SalesOrderHeader.SalesOrderID = SalesOrder.SalesOrderID  
      for xml auto, type),  
        (SELECT *   
         FROM  (SELECT SalesPersonID, EmployeeID  
              FROM Sales.SalesPerson, HumanResources.Employee  
              WHERE SalesPerson.SalesPersonID = Employee.EmployeeID) As SalesPerson  
         WHERE  SalesPerson.SalesPersonID = SalesOrder.SalesPersonID  
       FOR XML AUTO, TYPE, ELEMENTS)  
FROM (SELECT SalesOrderHeader.SalesOrderID, SalesOrderHeader.SalesPersonID  
      FROM Sales.SalesOrderHeader, Sales.SalesPerson  
      WHERE SalesOrderHeader.SalesPersonID = SalesPerson.SalesPersonID  
     ) as SalesOrder  
ORDER BY SalesOrder.SalesOrderID  
FOR XML AUTO, TYPE  
GO  
```  
  
 이 코드는 .aspx 응용 프로그램입니다. 이 코드는 저장 프로시저를 실행하고 브라우저에 XML을 반환합니다.  
  
```  
<%@LANGUAGE=C# Debug=true %>  
<%@import Namespace="System.Xml"%>  
<%@import namespace="System.Data.SqlClient" %><%  
Response.Expires = -1;  
Response.ContentType = "text/xml";  
%>  
  
<%  
using(System.Data.SqlClient.SqlConnection c = new System.Data.SqlClient.SqlConnection("Data Source=server;Database=AdventureWorks;Integrated Security=SSPI;"))  
using(System.Data.SqlClient.SqlCommand cmd = c.CreateCommand())  
{  
   cmd.CommandText = "GetSalesOrderInfo";  
   cmd.CommandType = CommandType.StoredProcedure;  
   cmd.Connection.Open();  
   System.Xml.XmlReader r = cmd.ExecuteXmlReader();  
   System.Xml.XmlTextWriter w = new System.Xml.XmlTextWriter(Response.Output);  
   w.WriteStartElement("Root");  
   r.MoveToContent();  
   while(! r.EOF)  
   {  
      w.WriteNode(r, true);  
   }  
   w.WriteEndElement();  
   w.Flush();  
}  
%>  
```  
  
##### <a name="to-test-the-application"></a>응용 프로그램을 테스트하려면  
  
1.  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 저장 프로시저를 만듭니다.  
  
2.  .aspx 응용 프로그램을 c:\inetpub\wwwroot 디렉터리에 GetSalesOrderInfo.aspx로 저장합니다.  
  
3.  응용 프로그램(`http://server/GetSalesOrderInfo.aspx`)을 실행합니다.  
  
## <a name="see-also"></a>참고 항목  
 [중첩 FOR XML 쿼리 사용](../../relational-databases/xml/use-nested-for-xml-queries.md)  
  
  
