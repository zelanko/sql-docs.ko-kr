---
title: "SQL Server 및 클라이언트 앱에서 FOR JSON 출력 사용(SQL Server) | Microsoft 문서"
ms.custom: SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR JSON, using in client apps
- FOR JSON, using in SQL Server
ms.assetid: 302e5397-b499-4ea3-9a7f-c24ccad698eb
caps.latest.revision: "12"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b38fbe15cf94f9356196939cb4afbab5a5ca4295
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="use-for-json-output-in-sql-server-and-in-client-apps-sql-server"></a>SQL 서버 및 클라이언트 앱에서 FOR JSON 출력 사용(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

다음 예제에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 클라이언트 앱에서 **FOR JSON** 절 및 해당 JSON 출력을 사용하는 몇 가지 방법이 나와 있습니다.  
  
## <a name="use-for-json-output-in-sql-server-variables"></a>SQL 서버 변수에서 FOR JSON 출력 사용  
FOR JSON 절의 출력은 NVARCHAR(MAX) 형식이므로 다음 예에 나와 있는 것처럼 어떤 변수에나 할당할 수 있습니다.  
  
```sql  
DECLARE @x NVARCHAR(MAX) = (SELECT TOP 10 * FROM Sales.SalesOrderHeader FOR JSON AUTO)  
```  
  
## <a name="use-for-json-output-in-sql-server-user-defined-functions"></a>SQL Server 사용자 정의 함수에서 FOR JSON 출력 사용  
 결과 집합의 형식을 JSON으로 지정하는 사용자 정의 함수를 만든 다음 이 JSON 출력을 반환할 수 있습니다. 다음 예에서는 판매 주문 세부 정보 행 몇 개를 가져온 다음 JSON 배열로 형식을 지정하는 사용자 정의 함수를 만듭니다.  
  
```sql  
CREATE FUNCTION GetSalesOrderDetails(@salesOrderId int)  
 RETURNS NVARCHAR(MAX)  
AS  
BEGIN  
   RETURN (SELECT UnitPrice, OrderQty  
           FROM Sales.SalesOrderDetail  
           WHERE SalesOrderID = @salesOrderId  
           FOR JSON AUTO)  
END
```  
  
 이 함수는 다음 예에 나와 있는 것처럼 일괄 처리나 쿼리로 사용할 수 있습니다.  
  
```sql  
DECLARE @x NVARCHAR(MAX) = dbo.GetSalesOrderDetails(43659)

PRINT dbo.GetSalesOrderDetails(43659)

SELECT TOP 10
  H.*, dbo.GetSalesOrderDetails(H.SalesOrderId) AS Details
FROM Sales.SalesOrderHeader H
```  
  
## <a name="merge-parent-and-child-data-into-a-single-table"></a>단일 테이블에 부모 및 자식 데이터 병합  
다음 예제에서 각 자식 행 집합을 JSON 배열로 형식 지정합니다. JSON 배열은 부모 테이블의 Details 열 값이 됩니다.  
  
```sql  
SELECT TOP 10 SalesOrderId, OrderDate,  
      (SELECT TOP 3 UnitPrice, OrderQty  
         FROM Sales.SalesOrderDetail D  
         WHERE H.SalesOrderId = D.SalesOrderID  
         FOR JSON AUTO) AS Details  
INTO SalesOrder  
FROM Sales.SalesOrderHeader H  
```  
  
## <a name="update-the-data-in-json-columns"></a>JSON 열의 데이터 업데이트  
 다음 예에서는 JSON 텍스트가 포함된 열의 값을 업데이트하는 방법을 확인할 수 있습니다.  
  
```sql  
UPDATE SalesOrder  
SET Details =  
     (SELECT TOP 1 UnitPrice, OrderQty  
       FROM Sales.SalesOrderDetail D  
       WHERE D.SalesOrderId = SalesOrder.SalesOrderId  
      FOR JSON AUTO 
```  
  
## <a name="use-for-json-output-in-a-c-client-app"></a>C# 클라이언트 앱에서 FOR JSON 출력 사용  
 다음 예에는 C# 클라이언트 앱에서 쿼리의 JSON 출력을 검색하여 StringBuilder 개체로 가져오는 방법이 나와 있습니다. 여기서 `queryWithForJson` 변수에는 FOR JSON 절이 들어 있는 SELECT 문의 텍스트가 포함되어 있다고 가정합니다.  
  
```csharp  
var queryWithForJson = "SELECT ... FOR JSON";
var conn = new SqlConnection("<connection string>");
var cmd = new SqlCommand(queryWithForJson, conn);
conn.Open();
var jsonResult = new StringBuilder();
var reader = cmd.ExecuteReader();
if (!reader.HasRows)
{
    jsonResult.Append("[]");
}
else
{
    while (reader.Read())
    {
        jsonResult.Append(reader.GetValue(0).ToString());
    }
}
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>SQL Server의 기본 제공 JSON 지원에 대한 자세한 정보  
많은 특정 솔루션, 사용 사례 및 권장 사항은 Microsoft 프로그램 관리자인 Jovan Popovic이 제공하는 SQL Server 및 Azure SQL Database의 [기본 제공 JSON 지원에 대한 블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)을 참조하세요.
 
## <a name="see-also"></a>관련 항목:  
 [FOR JSON을 사용하여 쿼리 결과를 JSON으로 서식 지정&#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  
