---
title: PATH 모드로 중첩 JSON 출력 서식 지정(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.reviewer: douglasl
ms.technology: ''
ms.topic: conceptual
ms.assetid: 032761b0-6358-42e4-b05c-dbfd663ac881
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4ca812a4b48d1f25b8e190987a66cc97fe891492
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47670781"
---
# <a name="format-nested-json-output-with-path-mode-sql-server"></a>PATH 모드로 중첩 JSON 출력 서식 지정(SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

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

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>SQL Server 및 Azure SQL Database에서 JSON에 대한 자세한 정보  
  
### <a name="microsoft-blog-posts"></a>Microsoft 블로그 게시물  
  
특정 솔루션, 사용 사례 및 권장 사항은 SQL Server 및 Azure SQL Database의 기본 제공 JSON 지원에 대한 [블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)을 참조하세요.  

### <a name="microsoft-videos"></a>Microsoft 비디오

SQL Server 및 Azure SQL Database에서 기본 제공 JSON 지원에 대한 시각적 소개는 다음 비디오를 참조하세요.

-   [SQL Server 2016 및 JSON 지원](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [SQL Server 2016 및 Azure SQL Database에서 JSON 사용](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL과 관계형 간에 브리지인 JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)

## <a name="see-also"></a>참고 항목  
 [FOR 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
