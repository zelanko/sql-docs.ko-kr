---
description: 기본 함수를 사용하여 JSON 데이터 유효성 검사, 쿼리, 변경(SQL Server)
title: 기본 함수를 사용하여 JSON 데이터 유효성 검사, 쿼리, 변경
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- JSON, built-in functions
- functions (JSON)
ms.assetid: 6b6c7673-d818-4fa9-8708-b4ed79cb1b41
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 76644f677a03f34312e6731f5a973167313ad22a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424095"
---
# <a name="validate-query-and-change-json-data-with-built-in-functions-sql-server"></a>기본 함수를 사용하여 JSON 데이터 유효성 검사, 쿼리, 변경(SQL Server)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

JSON의 기본 제공 지원에는 이 항목에서 간단히 설명하는 다음과 같은 기본 제공 함수가 포함됩니다.  
  
-   [ISJSON](#ISJSON) 은 문자열에 유효한 JSON이 포함되어 있는지 여부를 테스트합니다.  
  
-   [JSON_VALUE](#VALUE) JSON 문자열에서 스칼라 값을 추출합니다.  
  
-   [JSON_QUERY](#QUERY) 는 JSON 문자열에서 개체 또는 배열을 추출합니다.  
  
-   [JSON_MODIFY](#MODIFY) 는 JSON 문자열의 속성 값을 업데이트하고 업데이트된 JSON 문자열을 반환합니다.  
 
## <a name="json-text-for-the-examples-on-this-page"></a>이 페이지의 예제에 대한 JSON 텍스트

이 페이지의 예제는 다음 예제에 표시된 콘텐츠와 비슷한 JSON 텍스트를 사용합니다.

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller",
         "givenName": "Lisa",
         "gender": "female",
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

중첩된 복합 요소를 포함하는 이 JSON 문서는 다음 샘플 테이블에 저장됩니다.

```sql
CREATE TABLE Families (
   id int identity constraint PK_JSON_ID primary key,
   doc nvarchar(max)
)
``` 

##  <a name="validate-json-text-by-using-the-isjson-function"></a><a name="ISJSON"></a> ISJSON 함수를 사용하여 JSON 텍스트의 유효성을 검사합니다.  
 **ISJSON** 함수는 문자열에 유효한 JSON이 포함되어 있는지 여부를 테스트합니다.  
  
다음 예제는 JSON 열에 유효한 JSON 텍스트가 포함된 행을 반환합니다. 명시적 JSON 제약 조건이 없으면 NVARCHAR 열에 텍스트를 입력할 수 있습니다.  
  
```sql  
SELECT *
FROM Families
WHERE ISJSON(doc) > 0 
```  

자세한 내용은 [ISJSON&#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md)을 참조하세요.  
  
##  <a name="extract-a-value-from-json-text-by-using-the-json_value-function"></a><a name="VALUE"></a> JSON_VALUE 함수를 사용하여 JSON 텍스트에서 값을 추출합니다.  
**JSON_VALUE** 함수는 JSON 문자열에서 스칼라 값을 추출합니다. 다음 쿼리는 `id`JSON 필드가 `city` 및 `state` JSON 필드를 기준으로 정렬된 값 `AndersenFamily`과 일치하는 문서를 반환합니다.

```sql  
SELECT JSON_VALUE(f.doc, '$.id')  AS Name, 
       JSON_VALUE(f.doc, '$.address.city') AS City,
       JSON_VALUE(f.doc, '$.address.county') AS County
FROM Families f 
WHERE JSON_VALUE(f.doc, '$.id') = N'AndersenFamily'
ORDER BY JSON_VALUE(f.doc, '$.address.city') DESC, JSON_VALUE(f.doc, '$.address.state') ASC
```  

이 쿼리의 결과는 다음 표에 나와 있습니다.

| Name | City | 국가 |
| --- | --- | --- |
| AndersenFamily | NY | Manhattan |

자세한 내용은 [JSON_VALUE&#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)을 참조하세요.  
  
##  <a name="extract-an-object-or-an-array-from-json-text-by-using-the-json_query-function"></a><a name="QUERY"></a> JSON_QUERY 함수를 사용하여 JSON 텍스트에서 개체 또는 배열 추출  

**JSON_QUERY** 함수는 JSON 문자열에서 개체 또는 배열을 추출합니다. 다음 예제는 쿼리 결과에 JSON 조각을 반환하는 방법을 보여줍니다.  
  
```sql
SELECT JSON_QUERY(f.doc, '$.address') AS Address,
       JSON_QUERY(f.doc, '$.parents') AS Parents,
       JSON_QUERY(f.doc, '$.parents[0]') AS Parent0
FROM Families f 
WHERE JSON_VALUE(f.doc, '$.id') = N'AndersenFamily'
```  
이 쿼리의 결과는 다음 표에 나와 있습니다.

| 주소 | 부모 항목 | Parent0 |
| --- | --- | --- |
| { "state": "NY", "county": "Manhattan", "city": "NY" } | [{ "familyName": "Wakefield", "givenName": "Robin" }, {"familyName": "Miller", "givenName": "Ben" } ]| { "familyName": "Wakefield", "givenName": "Robin" } |

자세한 내용은 [JSON_QUERY&#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)를 참조하세요.  

## <a name="parse-nested-json-collections"></a>중첩된 JSON 컬렉션 구문 분석

`OPENJSON` 함수를 사용하면 JSON 하위 배열을 행 집합으로 변환한 다음, 부모 요소와 조인할 수 있습니다. 예를 들어, 모든 제품군 문서를 반환하고 내부 JSON 배열로 저장된 `children` 개체와 "조인"할 수 있습니다.

```sql
SELECT JSON_VALUE(f.doc, '$.id')  AS Name, 
       JSON_VALUE(f.doc, '$.address.city') AS City,
       c.givenName, c.grade
FROM Families f
        CROSS APPLY OPENJSON(f.doc, '$.children')
            WITH(grade int, givenName nvarchar(100))  c
```

이 쿼리의 결과는 다음 표에 나와 있습니다.

| Name | City | givenName | grade |
| --- | --- | --- | --- |
| AndersenFamily | NY | Jesse | 1 |
| AndersenFamily | NY | Lisa | 8 |

하나의 부모 행이 생성된 두 개의 자식 행과 조인되기 때문에 자식 하위 배열의 두 요소를 구문 분석하면 두 행이 결과로 반환됩니다. `OPENJSON` 함수는 `doc` 열에서 `children` 조각을 구문 분석하고 각 요소에서 `grade` 및 `givenName`을 행 세트로 반환합니다. 이 행 집합은 부모 문서와 조인할 수 있습니다.
 
## <a name="query-nested-hierarchical-json-sub-arrays"></a>중첩된 계층적 JSON 하위 배열 쿼리

중첩된 JSON 구조를 쿼리하기 위해 여러 `CROSS APPLY OPENJSON` 호출을 적용할 수 있습니다. 이 예제에 사용된 JSON 문서에는 `children`이라는 중첩 배열이 있습니다. 여기에서 각 자식에는 `pets`의 중첩된 배열이 있습니다. 다음 쿼리는 각 문서의 자식을 구문 분석하고, 각 배열 개체를 행으로 반환한 다음, `pets` 배열을 구문 분석합니다.

```sql
SELECT  familyName,
    c.givenName AS childGivenName,
    c.firstName AS childFirstName,
    p.givenName AS petName 
FROM Families f 
    CROSS APPLY OPENJSON(f.doc) 
        WITH (familyName nvarchar(100), children nvarchar(max) AS JSON)
        CROSS APPLY OPENJSON(children) 
        WITH (givenName nvarchar(100), firstName nvarchar(100), pets nvarchar(max) AS JSON) as c
            OUTER APPLY OPENJSON (pets)
            WITH (givenName nvarchar(100))  as p
```

첫 번째 `OPENJSON` 호출은 AS JSON 절을 사용하여 `children` 배열의 조각을 반환합니다. 이 배열 조각은 `pets` 배열뿐만 아니라 각 자식의 `givenName`, `firstName`을 반환하는 두 번째 `OPENJSON` 함수에 제공됩니다. `pets` 배열은 애완 동물의 `givenName`을 반환하는 세 번째 `OPENJSON` 함수에 제공됩니다.
이 쿼리의 결과는 다음 표에 나와 있습니다.

| familyName | childGivenName | childFirstName | petName |
| --- | --- | --- | --- |
| AndersenFamily | Jesse | Merriam | Goofy |
| AndersenFamily | Jesse | Merriam | 그림자 |
| AndersenFamily | Lisa | Miller| `NULL` |

루트 문서는 첫 번째 `OPENJSON(children)` 호출로 반환된 두 `children` 행과 조인되어 두 개의 행(또는 튜플)을 만듭니다. 그런 다음, 각 행이 `OUTER APPLY` 연산자를 사용하여 `OPENJSON(pets)`에서 생성된 새 행과 조인됩니다. Jesse에는 두 마리의 애완 동물이 있으므로 `(AndersenFamily, Jesse, Merriam)`이 Goofy 및 Shadow에 대해 생성된 두 개의 행과 조인됩니다. Lisa에게는 애완 동물이 없으므로 이 튜플에 대해 `OPENJSON(pets)`에서 반환되는 행이 없습니다. 그러나 `OUTER APPLY`를 사용하고 있기 때문에 열에 `NULL`이 반환됩니다. `OUTER APPLY` 대신, `CROSS APPLY`를 사용하는 경우 이 튜플에 조인할 수 있는 애완 동물 행이 없기 때문에 Lisa는 결과에 반환되지 않습니다.

##  <a name="compare-json_value-and-json_query"></a><a name="JSONCompare"></a> JSON_VALUE 및 JSON_QUERY 비교  
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
  
## <a name="test-json_value-and-json_query-with-the-adventureworks-sample-database"></a>AdventureWorks 예제 데이터베이스로 JSON_VALUE 및 JSON_QUERY 테스트  
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
  
##  <a name="update-property-values-in-json-text-by-using-the-json_modify-function"></a><a name="MODIFY"></a> JSON_MODIFY 함수를 사용하여 JSON 텍스트의 속성 값을 업데이트합니다.  
**JSON_MODIFY** 함수는 JSON 문자열의 속성 값을 업데이트하고 업데이트된 JSON 문자열을 반환합니다.  
  
다음 예제에서는 JSON이 포함된 변수에서 JSON 속성 값을 업데이트합니다.  
  
```sql  
SET @info = JSON_MODIFY(@jsonInfo, "$.info.address[0].town", 'London')    
```  
  
 자세한 내용은 [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)을 참조하세요.  
  
## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>SQL Server 및 Azure SQL Database에서 JSON에 대한 자세한 정보  
  
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
  
  
