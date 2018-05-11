---
title: 기본 제공 함수를 사용하여 JSON 데이터 유효성 검사, 쿼리, 변경(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: json
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- JSON, built-in functions
- functions (JSON)
ms.assetid: 6b6c7673-d818-4fa9-8708-b4ed79cb1b41
caps.latest.revision: 21
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: dc1088d2f82ac26eda7874fbdbc613670366d723
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="validate-query-and-change-json-data-with-built-in-functions-sql-server"></a>기본 함수를 사용하여 JSON 데이터 유효성 검사, 쿼리, 변경(SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

JSON의 기본 지원에는 이 항목에서 간단히 설명하는 다음과 같은 기본 제공 함수가 포함됩니다.  
  
-   [ISJSON](#ISJSON) 은 문자열에 유효한 JSON이 포함되어 있는지 여부를 테스트합니다.  
  
-   [JSON_VALUE](#VALUE) JSON 문자열에서 스칼라 값을 추출합니다.  
  
-   [JSON_QUERY](#QUERY) 는 JSON 문자열에서 개체 또는 배열을 추출합니다.  
  
-   [JSON_MODIFY](#MODIFY) 는 JSON 문자열의 속성 값을 업데이트하고 업데이트된 JSON 문자열을 반환합니다.  
 
## <a name="json-text-for-the-examples-on-this-page"></a>이 페이지의 예제에 대한 JSON 텍스트
이 페이지의 예제에서는 복잡한 요소가 포함된 다음 JSON 텍스트를 사용합니다.

```sql 
DECLARE @jsonInfo NVARCHAR(MAX)

SET @jsonInfo=N'{  
     "info":{    
       "type":1,  
       "address":{    
         "town":"Bristol",  
         "county":"Avon",  
         "country":"England"  
       },  
       "tags":["Sport", "Water polo"]  
    },  
    "type":"Basic"  
 }' 
``` 

##  <a name="ISJSON"></a> ISJSON 함수를 사용하여 JSON 텍스트의 유효성을 검사합니다.  
 **ISJSON** 함수는 문자열에 유효한 JSON이 포함되어 있는지 여부를 테스트합니다.  
  
다음 예제는 `json_col` 열에 유효한 JSON이 포함된 행을 반환합니다.  
  
```sql  
SELECT id, json_col
FROM tab1
WHERE ISJSON(json_col) > 0 
```  

자세한 내용은 [ISJSON&#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md)을 참조하세요.  
  
##  <a name="VALUE"></a> JSON_VALUE 함수를 사용하여 JSON 텍스트에서 값을 추출합니다.  
**JSON_VALUE** 함수는 JSON 문자열에서 스칼라 값을 추출합니다.  
  
다음 예제는 중첩된 JSON 속성 `town`의 값을 지역 변수로 추출합니다.  
  
```sql  
SET @town = JSON_VALUE(@jsonInfo, '$.info.address.town')  
```  
  
자세한 내용은 [JSON_VALUE&#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)을 참조하세요.  
  
##  <a name="QUERY"></a> JSON_QUERY 함수를 사용하여 JSON 텍스트에서 개체 또는 배열 추출  
**JSON_QUERY** 함수는 JSON 문자열에서 개체 또는 배열을 추출합니다.  
 
다음 예제는 쿼리 결과에 JSON 조각을 반환하는 방법을 보여줍니다.  
  
```sql  
SELECT FirstName, LastName, JSON_QUERY(jsonInfo,'$.info.address') AS Address
FROM Person.Person
ORDER BY LastName
```  
  
자세한 내용은 [JSON_QUERY&#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)를 참조하세요.  
  
##  <a name="JSONCompare"></a> JSON_VALUE 및 JSON_QUERY 비교  
**JSON_VALUE** 와 **JSON_QUERY** 간의 주요 차이점은 **JSON_VALUE** 는 스칼라 값을 반환하고 **JSON_QUERY** 는 개체 또는 배열을 반환한다는 점입니다.  
  
다음 예제의 JSON 쿼리를 살펴보십시오.  
  
```json  
{
    "a": "[1,2]",
    "b": [1, 2],
    "c": "hi"
}  
```  
  
이 예제 JSON 텍스트에서 데이터 멤버 "a"와 "c"는 문자열 값이며 데이터 멤버 "b"는 배열입니다. **JSON_VALUE** 및 **JSON_QUERY** 는 다음 결과를 반환합니다.  
  
|경로|**JSON_VALUE** 는 다음을 반환합니다.|**JSON_QUERY** 는 다음을 반환합니다.|  
|-----------|-----------------------------|-----------------------------|  
|**$**|NULL 또는 오류|`{ "a": "[1,2]", "b": [1,2], "c":"hi"}`|  
|**$.a**|[1,2]|NULL 또는 오류|  
|**$.b**|NULL 또는 오류|[1,2]|  
|**$.b[0]**|1|NULL 또는 오류|  
|**$.c**|hi|NULL 또는 오류|  
  
## <a name="test-jsonvalue-and-jsonquery-with-the-adventureworks-sample-database"></a>AdventureWorks 예제 데이터베이스로 JSON_VALUE 및 JSON_QUERY 테스트  
AdventureWorks 예제 데이터베이스로 다음 예제를 실행하여 이 항목에서 설명하는 기본 제공 함수를 테스트합니다. AdventureWorks를 다운로드할 수 있는 위치에 대한 정보와 스크립트를 실행하여 테스트용 JSON 데이터를 추가하는 방법은 [기본 제공 JSON 지원 시험 사용](json-data-sql-server.md#test-drive-built-in-json-support-with-the-adventureworks-sample-database)을 참조하세요.
  
다음 예제에서 `SalesOrder_json` 테이블의 `Info` 열에는 JSON 텍스트가 포함되어 있습니다.  
  
### <a name="example-1---return-both-standard-columns-and-json-data"></a>예제 1 - 두 표준 열과 JSON 데이터 반환  
다음 쿼리는 표준 관계형 열과 JSON 열의 값을 모두 반환합니다.  
  
```sql  
SELECT SalesOrderNumber, OrderDate, Status, ShipDate, Status, AccountNumber, TotalDue,
 JSON_QUERY(Info,'$.ShippingInfo') ShippingInfo,
 JSON_QUERY(Info,'$.BillingInfo') BillingInfo,
 JSON_VALUE(Info,'$.SalesPerson.Name') SalesPerson,
 JSON_VALUE(Info,'$.ShippingInfo.City') City,
 JSON_VALUE(Info,'$.Customer.Name') Customer,
 JSON_QUERY(OrderItems,'$') OrderItems
FROM Sales.SalesOrder_json
WHERE ISJSON(Info) > 0
```  
  
### <a name="example-2--aggregate-and-filter-json-values"></a>예제 2 - JSON 값 집계 및 필터링  
다음 쿼리는 고객 이름(JSON에 저장)과 상태(일반 열에 저장)를 기준으로 소계를 집계합니다. 그런 다음 시(JSON에 저장) 및 OrderDate(일반 열에 저장)를 기준으로 결과를 필터링합니다.  
  
```sql  
DECLARE @territoryid INT;
DECLARE @city NVARCHAR(32);

SET @territoryid=3;

SET @city=N'Seattle';

SELECT JSON_VALUE(Info, '$.Customer.Name') AS Customer, Status, SUM(SubTotal) AS Total
FROM Sales.SalesOrder_json
WHERE TerritoryID=@territoryid
 AND JSON_VALUE(Info, '$.ShippingInfo.City') = @city
 AND OrderDate > '1/1/2015'
GROUP BY JSON_VALUE(Info, '$.Customer.Name'), Status
HAVING SUM(SubTotal)>1000
```  
  
##  <a name="MODIFY"></a> JSON_MODIFY 함수를 사용하여 JSON 텍스트의 속성 값을 업데이트합니다.  
**JSON_MODIFY** 함수는 JSON 문자열의 속성 값을 업데이트하고 업데이트된 JSON 문자열을 반환합니다.  
  
다음 예제에서는 JSON이 포함된 변수에서 JSON 속성 값을 업데이트합니다.  
  
```sql  
SET @info = JSON_MODIFY(@jsonInfo, "$.info.address[0].town", 'London')    
```  
  
 자세한 내용은 [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)을 참조하세요.  
  
## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>SQL Server 및 Azure SQL Database에서 JSON에 대한 자세한 정보  
  
### <a name="microsoft-blog-posts"></a>Microsoft 블로그 게시물  
  
특정 솔루션, 사용 사례 및 권장 사항은 SQL Server 및 Azure SQL Database의 기본 제공 JSON 지원에 대한 [블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)을 참조하세요.  

### <a name="microsoft-videos"></a>Microsoft 비디오

SQL Server 및 Azure SQL Database에서 기본 제공 JSON 지원에 대한 시각적 소개는 다음 비디오를 참조하세요.

-   [SQL Server 2016 및 JSON 지원](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [SQL Server 2016 및 Azure SQL Database에서 JSON 사용](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL과 관계형 간에 브리지인 JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>참고 항목  
 [ISJSON&#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md)   
 [JSON_VALUE&#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY&#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)   
 [JSON_MODIFY&#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)   
 [JSON 경로 식&#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)  
  
  
