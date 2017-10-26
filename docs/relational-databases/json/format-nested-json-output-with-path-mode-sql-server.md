---
title: "PATH 모드로 중첩 JSON 출력 서식 지정(SQL Server) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 032761b0-6358-42e4-b05c-dbfd663ac881
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: 12dfc255364a410de1ad5c75f3abf38155d6d70f
ms.contentlocale: ko-kr
ms.lasthandoff: 07/31/2017

---
# <a name="format-nested-json-output-with-path-mode-sql-server"></a>PATH 모드로 중첩 JSON 출력 서식 지정(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

**FOR JSON** 절의 출력을 완전히 제어하려면 **PATH** 옵션을 지정합니다.  
  
**PATH** 모드를 통해 래퍼 개체를 만들고 복잡한 속성을 중첩할 수 있습니다. 결과는 JSON 개체의 배열로 서식 지정됩니다.  
  
대신 **AUTO** 옵션을 사용하여 **SELECT** 문의 구조에 따라 출력 형식을 자동으로 지정합니다.
 -   **AUTO** 옵션에 대한 자세한 내용은 [AUTO 모드를 사용하여 JSON 출력 형식 자동 지정](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md)을 참조하세요.
 -   두 옵션의 개요는 [FOR JSON을 사용하여 쿼리 결과를 JSON으로 서식 지정](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)을 참조하세요.
 
아래에는 **PATH** 옵션에서 **FOR JSON** 절을 사용하는 몇 가지 예가 나와 있습니다. 다음 예제에 표시된 것처럼 점으로 구분된 열 이름 또는 중첩 쿼리를 사용하여 중첩 결과를 서식 지정합니다. 기본적으로 null 값은 **FOR JSON** 출력에 포함되지 않습니다.  

## <a name="example---dot-separated-column-names"></a>예 - 점으로 구분된 열 이름  
다음 쿼리는 AdventureWorks `Person` 테이블의 처음 5개 행을 JSON 형식으로 지정합니다.  

**FOR JSON PATH** 절은 열 별칭이나 열 이름을 사용하여 JSON 출력에서 키 이름을 확인합니다. 별칭에 점이 있는 경우 PATH 옵션은 중첩된 개체를 만듭니다.  

 **쿼리**  
  
```sql  
SELECT TOP 5   
       BusinessEntityID As Id,  
       FirstName, LastName,  
       Title As 'Info.Title',  
       MiddleName As 'Info.MiddleName'  
   FROM Person.Person  
   FOR JSON PATH   
```  
  
 **결과**  
  
```json  
[{
    "Id": 1,
    "FirstName": "Ken",
    "LastName": "Sanchez",
    "Info": {
        "MiddleName": "J"
    }
}, {
    "Id": 2,
    "FirstName": "Terri",
    "LastName": "Duffy",
    "Info": {
        "MiddleName": "Lee"
    }
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
    "Info": {
        "Title": "Ms.",
        "MiddleName": "A"
    }
}]
```  
   
## <a name="example---multiple-tables"></a>예제 - 여러 테이블  
쿼리에서 둘 이상의 테이블을 참조하는 경우 **FOR JSON PATH**는 해당 별칭을 사용하여 각 열을 중첩합니다. 다음 쿼리는 쿼리에서 조인된 (OrderHeader, OrderDetails) 쌍당 하나의 JSON 개체를 만듭니다. 
  
 **쿼리**  
  
```sql  
SELECT TOP 2 SalesOrderNumber AS 'Order.Number',  
        OrderDate AS 'Order.Date',  
        UnitPrice AS 'Product.Price',  
        OrderQty AS 'Product.Quantity'  
FROM Sales.SalesOrderHeader H  
   INNER JOIN Sales.SalesOrderDetail D  
     ON H.SalesOrderID = D.SalesOrderID  
FOR JSON PATH   
```  
  
 **결과**  
  
```json  
[{
    "Order": {
        "Number": "SO43659",
        "Date": "2011-05-31T00:00:00"
    },
    "Product": {
        "Price": 2024.9940,
        "Quantity": 1
    }
}, {
    "Order": {
        "Number": "SO43659"
    },
    "Product": {
        "Price": 2024.9940
    }
}]
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>SQL Server의 기본 제공 JSON 지원에 대한 자세한 정보  
많은 특정 솔루션, 사용 사례 및 권장 사항은 Microsoft 프로그램 관리자인 Jovan Popovic이 제공하는 SQL Server 및 Azure SQL Database의 [기본 제공 JSON 지원에 대한 블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)을 참조하세요.

## <a name="see-also"></a>관련 항목:  
 [FOR 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  

