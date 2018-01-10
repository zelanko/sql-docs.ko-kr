---
title: "AUTO 모드를 사용하여 JSON 출력 형식 자동 지정(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.component: json
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: FOR JSON AUTO
ms.assetid: 178a2a4e-e0f6-49b9-9895-396956d3c7d9
caps.latest.revision: "17"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: aef9d09f6f8a9606a742be05a2076bf65aeb9a40
ms.sourcegitcommit: 4aeedbb88c60a4b035a49754eff48128714ad290
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/05/2018
---
# <a name="format-json-output-automatically-with-auto-mode-sql-server"></a>AUTO 모드를 사용하여 JSON 출력 형식 자동 지정(SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

**SELECT** 문의 구조에 따라 **FOR JSON** 절 출력 형식을 자동으로 지정하려면 **AUTO** 옵션을 지정합니다.  
  
**AUTO** 옵션을 지정하면 SELECT 목록의 열 순서와 해당 원본 테이블에 따라 JSON 출력의 형식이 자동으로 결정됩니다. 이 형식은 변경할 수 없습니다.
 
대신 **PATH** 옵션을 사용하여 출력에 대한 제어를 관리합니다.
-   **PATH** 옵션에 대한 자세한 내용은 [PATH 모드로 중첩 JSON 출력 서식 지정](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md)을 참조하세요.
-   두 옵션의 개요는 [FOR JSON을 사용하여 쿼리 결과를 JSON으로 서식 지정](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)을 참조하세요.

**FOR JSON AUTO** 옵션을 사용하는 쿼리에는 **FROM** 절이 있어야 합니다.  
  
아래에는 **AUTO** 옵션에서 **FOR JSON** 절을 사용하는 몇 가지 예가 나와 있습니다.  
  
## <a name="examples"></a>예

### <a name="example-1"></a>예 1
 **쿼리**  
  
쿼리에서 하나의 테이블만 참조하는 경우 FOR JSON AUTO 절의 결과는 FOR JSON PATH의 결과와 비슷합니다. 이 경우 FOR JSON AUTO는 중첩된 개체를 만들지 않습니다. 유일한 차이점은 FOR JSON AUTO는 점으로 구분된 별칭(예를 들어 다음 예제에서 `Info.MiddleName`)을 중첩된 개체가 아닌 점이 있는 키로 출력한다는 것입니다.  
  
```sql  
SELECT TOP 5   
       BusinessEntityID As Id,  
       FirstName, LastName,  
       Title As 'Info.Title',  
       MiddleName As 'Info.MiddleName'  
   FROM Person.Person  
   FOR JSON AUTO  
```  
  
 **결과**  
  
```json  
[{
    "Id": 1,
    "FirstName": "Ken",
    "LastName": "Sánchez",
    "Info.MiddleName": "J"
}, {
    "Id": 2,
    "FirstName": "Terri",
    "LastName": "Duffy",
    "Info.MiddleName": "Lee"
}, {
    "Id": 3,
    "FirstName": "Roberto",
    "LastName": "Tamburello"
}, {
    "Id": 4,
    "FirstName": "Rob",
    "LastName": "Walters"
}, {
    "Id": 5,
    "FirstName": "Gail",
    "LastName": "Erickson",
    "Info.Title": "Ms.",
    "Info.MiddleName": "A"
}]
```  

### <a name="example-2"></a>예제 2

**쿼리**  
  
테이블을 조인하면 첫 번째 테이블의 열이 루트 개체의 속성으로 생성됩니다. 두 번째 테이블의 열은 중첩된 개체의 속성으로 생성됩니다. 테이블 이름 또는 두 번째 테이블의 별칭(예를 들어 다음 예제에서 `D`)은 중첩된 배열의 이름으로 사용됩니다.  
  
```sql  
SELECT TOP 2 SalesOrderNumber,  
        OrderDate,  
        UnitPrice,  
        OrderQty  
FROM Sales.SalesOrderHeader H  
   INNER JOIN Sales.SalesOrderDetail D  
     ON H.SalesOrderID = D.SalesOrderID  
FOR JSON AUTO   
```  
  
**결과**  
  
```json  
[{
    "SalesOrderNumber": "SO43659",
    "OrderDate": "2011-05-31T00:00:00",
    "D": [{
        "UnitPrice": 24.99,
        "OrderQty": 1
    }]
}, {
    "SalesOrderNumber": "SO43659",
    "D": [{
        "UnitPrice": 34.40
    }, {
        "UnitPrice": 134.24,
        "OrderQty": 5
    }]
}]
```  

### <a name="example-3"></a>예제 3
 
**쿼리**  
FOR JSON AUTO를 사용하는 대신 다음 예제에서처럼 SELECT 문에 FOR JSON PATH 하위 쿼리를 중첩할 수 있습니다. 이 예제는 앞의 예제와 동일한 결과를 출력합니다.  
  
```sql  
SELECT TOP 2  
    SalesOrderNumber,  
    OrderDate,  
    (SELECT UnitPrice, OrderQty  
      FROM Sales.SalesOrderDetail AS D  
      WHERE H.SalesOrderID = D.SalesOrderID  
     FOR JSON PATH) AS D  
FROM Sales.SalesOrderHeader AS H  
FOR JSON PATH  
```  
  
**결과**  
  
```json  
[{
    "SalesOrderNumber": "SO43659",
    "OrderDate": "2011-05-31T00:00:00",
    "D": [{
        "UnitPrice": 24.99,
        "OrderQty": 1
    }]
}, {
    "SalesOrderNumber": "SO4390",
    "D": [{
        "UnitPrice": 24.99
    }]
}]
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>SQL Server의 기본 제공 JSON 지원에 대한 자세한 정보  
많은 특정 솔루션, 사용 사례 및 권장 사항은 Microsoft 프로그램 관리자인 Jovan Popovic이 제공하는 SQL Server 및 Azure SQL Database의 [기본 제공 JSON 지원에 대한 블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)을 참조하세요.

## <a name="see-also"></a>참고 항목  
 [FOR 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
