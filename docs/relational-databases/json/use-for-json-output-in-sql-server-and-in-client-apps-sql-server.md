---
title: "SQL 서버 및 클라이언트 앱에서 FOR JSON 출력 사용(SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FOR JSON, 클라이언트 앱에서 사용"
  - "FOR JSON, SQL Server에서 사용"
ms.assetid: 302e5397-b499-4ea3-9a7f-c24ccad698eb
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 11
---
# SQL 서버 및 클라이언트 앱에서 FOR JSON 출력 사용(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  다음 예제에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 클라이언트 앱에서 **FOR JSON** 절이나 해당 출력을 사용하는 몇 가지 방식이 나와 있습니다.  
  
## SQL 서버 변수에서 FOR JSON 출력 사용  
 FOR JSON 절의 출력은 NVARCHAR(MAX) 유형이므로 다음 예에 나와 있는 것처럼 어떤 변수에나 할당할 수 있습니다.  
  
```tsql  
DECLARE @x NVARCHAR(MAX) = (SELECT TOP 10 * FROM Sales.SalesOrderHeader FOR JSON AUTO)  
```  
  
## SQL Server 사용자 정의 함수에서 FOR JSON 출력 사용  
 결과 집합의 형식을 JSON으로 지정하는 사용자 정의 함수를 만든 다음 이 JSON 출력을 반환할 수 있습니다. 다음 예에서는 판매 주문 세부 정보 행 몇 개를 가져온 다음 JSON 배열로 형식을 지정하는 사용자 정의 함수를 만듭니다.  
  
```tsql  
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
  
```tsql  
DECLARE @x NVARCHAR(MAX) = dbo.GetSalesOrderDetails(43659)  
PRINT dbo.GetSalesOrderDetails(43659)  
SELECT TOP 10 H.*, dbo.GetSalesOrderDetails(H.SalesOrderId) AS Details  
FROM Sales.SalesOrderHeader H  
```  
  
## 단일 테이블에 부모 및 자식 데이터 병합  
 다음 예에서는 각 자식 행 집합의 형식을 JSON 배열로 지정한 다음 부모 테이블의 Details 열 값으로 해당 집합을 지정합니다.  
  
```tsql  
select top 10 SalesOrderId, OrderDate,  
     (select top 3 UnitPrice, OrderQty  
        from Sales.SalesOrderDetail D  
        where H.SalesOrderId = D.SalesOrderID  
        for json auto) as Details  
into SalesOrder  
from Sales.SalesOrderHeader H  
```  
  
## JSON 열의 데이터 업데이트  
 다음 예에서는 JSON 텍스트가 포함된 열의 값을 업데이트하는 방법을 확인할 수 있습니다.  
  
```tsql  
UPDATE SalesOrder  
SET Details =  
    (SELECT TOP 1 UnitPrice, OrderQty  
      FROM Sales.SalesOrderDetail D  
      WHERE D.SalesOrderId = SalesOrder.SalesOrderId  
     FOR JSON AUTO)  
```  
  
## C# 클라이언트 앱에서 FOR JSON 출력 사용  
 다음 예에는 C# 클라이언트 앱에서 쿼리의 JSON 출력을 검색하여 StringBuilder 개체로 가져오는 방법이 나와 있습니다. 여기서 queryWithForJson 변수에는 FOR JSON 절이 들어 있는 SELECT 문의 텍스트가 포함되어 있다고 가정합니다.  
  
```csharp  
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
  
## 참고 항목  
 [FOR JSON을 사용하여 쿼리 결과를 JSON으로 서식 지정&#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  