---
title: "PATH 모드로 중첩 JSON 출력 서식 지정(SQL Server) | Microsoft Docs"
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
ms.assetid: 032761b0-6358-42e4-b05c-dbfd663ac881
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 16
---
# PATH 모드로 중첩 JSON 출력 서식 지정(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  JSON 출력의 형식을 완전하게 제어하려면 **FOR JSON** 절로 **PATH** 옵션을 지정합니다.  
  
 **PATH** 모드를 통해 래퍼 개체를 만들고 복잡한 속성을 중첩할 수 있습니다. 결과는 JSON 개체의 배열로 서식 지정됩니다.  
  
 아래에는 **PATH** 옵션에서 **FOR JSON** 절을 사용하는 몇 가지 예가 나와 있습니다. 다음 예제에 표시된 것처럼 점으로 구분된 열 이름 또는 중첩 쿼리를 사용하여 중첩 결과를 서식 지정합니다. 기본적으로 null 값은 출력에 포함되지 않습니다.  
  
## 예 - 점으로 구분된 열 이름  
 다음 쿼리는 AdventureWorks Person 테이블의 처음 5개의 행을 JSON 형식으로 지정합니다.  
  
 **Query**  
  
```tsql  
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
[  
    {"Id":1,"FirstName":"Ken","LastName":"Sánchez","Info":{"MiddleName":"J"}},  
    {"Id":2,"FirstName":"Terri","LastName":"Duffy","Info":{"MiddleName":"Lee"}},  
    {"Id":3,"FirstName":"Roberto","LastName":"Tamburello"},  
    {"Id":4,"FirstName":"Rob","LastName":"Walters"},  
    {"Id":5,"FirstName":"Gail","LastName":"Erickson","Info":{"Title":"Ms.","MiddleName":"A"}}  
]  
```  
  
 FOR JSON PATH 절은 열 별칭이나 열 이름을 사용하여 JSON 출력에서 키 이름을 식별합니다. 일부 별칭에 점이 포함되어 있을 경우 FOR JSON PATH 절에서 중첩된 개체를 만듭니다. NULL 값이 포함된 셀은 출력에 생성되지 않습니다.  
  
## 예제 - 여러 테이블  
 쿼리에서 둘 이상의 테이블을 참조하는 경우 결과가 단순 목록으로 표시된 다음 FOR JSON PATH에서 해당 별칭을 사용하여 각 열을 중첩합니다. 다음 쿼리는 쿼리에서 조인된 (OrderHeader, OrderDetails) 쌍당 하나의 JSON 개체를 만듭니다.  
  
 **Query**  
  
```tsql  
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
[  
  {  
    "Order":{  
        "Number":"SO43659",  
        "Date":"2011-05-31T00:00:00"  
      },  
    "Product":{  
         "Price":2024.9940,  
         "Quantity":1  
     }  
  },  
  {  
    "Order":{ "Number":"SO43659“ },  
    "Product":{"Price":2024.9940}  
  }  
]  
```  
  
## 참고 항목  
 [FOR 절&#40;Transact-SQL&#41;](../Topic/FOR%20Clause%20\(Transact-SQL\).md)  
  
  