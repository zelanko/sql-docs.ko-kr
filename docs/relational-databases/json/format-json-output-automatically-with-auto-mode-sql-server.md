---
title: "AUTO 모드를 사용하여 JSON 출력 형식 자동 지정(SQL Server) | Microsoft Docs"
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
  - "FOR JSON AUTO"
ms.assetid: 178a2a4e-e0f6-49b9-9895-396956d3c7d9
caps.latest.revision: 17
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 15
---
# AUTO 모드를 사용하여 JSON 출력 형식 자동 지정(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  **SELECT** 문의 구조에 따라 JSON 출력 형식을 자동으로 지정하려면  **FOR JSON** 절을 포함하여 **AUTO** 옵션을 지정합니다.  
  
 **AUTO** 옵션을 포함하면 SELECT 목록의 열 순서와 해당 원본 테이블에 따라 JSON 출력의 형식이 자동으로 결정됩니다. 이 형식은 변경할 수 없습니다.  
  
 **FOR JSON AUTO** 옵션을 사용하는 쿼리에는 **FROM** 절이 있어야 합니다.  
  
 아래에는 **AUTO** 옵션에서 **FOR JSON** 절을 사용하는 몇 가지 예가 나와 있습니다.  
  
## 예  
 **쿼리 1**  
  
 쿼리에서 하나의 테이블만 사용하는 경우 FOR JSON AUTO 절의 결과는 FOR JSON PATH와 비슷합니다. 이 경우 FOR JSON AUTO는 중첩된 개체를 만들지 않습니다. 유일한 차이점은 점으로 구분된 별칭이 점을 포함하는 키로 생성된다는 것입니다(즉, FOR JSON AUTO는 열 별칭을 서식 지정에 사용하지 않음).  
  
```tsql  
SELECT TOP 5   
      BusinessEntityID As Id,  
      FirstName, LastName,  
      Title As 'Info.Title',  
      MiddleName As 'Info.MiddleName'  
  FROM Person.Person  
  FOR JSON AUTO  
```  
  
 **결과 1**  
  
```json  
[  
      {"Id":1,"FirstName":"Ken","LastName":"Sánchez","Info.MiddleName":"J"},  
      {"Id":2,"FirstName":"Terri","LastName":"Duffy","Info.MiddleName":"Lee"},  
      {"Id":3,"FirstName":"Roberto","LastName":"Tamburello"},  
      {"Id":4,"FirstName":"Rob","LastName":"Walters"},  
      {"Id":5,"FirstName":"Gail","LastName":"Erickson","Info.Title":"Ms.","Info.MiddleName":"A"}  
]  
```  
  
 **쿼리 2**  
  
 테이블을 조인하면 첫 번째 테이블의 열이 루트 개체의 속성으로 생성됩니다. 두 번째 테이블의 열은 중첩된 개체의 속성으로 생성됩니다. 두 번째 테이블의 테이블 이름 또는 별칭이 중첩된 배열의 이름으로 사용됩니다.  
  
```tsql  
SELECT TOP 2 SalesOrderNumber,  
       OrderDate,  
       UnitPrice,  
       OrderQty  
FROM Sales.SalesOrderHeader H  
  INNER JOIN Sales.SalesOrderDetail D  
    ON H.SalesOrderID = D.SalesOrderID  
FOR JSON AUTO  
```  
  
 **결과 2**  
  
```json  
[  
  {  
       "SalesOrderNumber":"SO43659",  
        "OrderDate":"2011-05-31T00:00:00",  
        "D":[  
            {"UnitPrice":24.99, "OrderQty":1  }  
         ]  
  },  
  {  
       "SalesOrderNumber":"SO43659" ,  
       "D":[  
          { "UnitPrice":34.40  },  
          { "UnitPrice":134.24, "OrderQty":5 }  
        ]  
  }  
]  
  
```  
  
## 예 - 중첩된 JSON 출력 생성  
 다음 예제와 같이 FOR JSON AUTO 대신 FOR JSON PATH 절과 함께 주 쿼리의 SELECT 부분에 중첩된 FOR JSON 쿼리를 작성할 수 있습니다.  
  
 **쿼리 1**  
  
```tsql  
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
  
 **결과 1**  
  
```json  
[  
  {  
       "SalesOrderNumber":"SO43659",  
        "OrderDate":"2011-05-31T00:00:00",  
        "D":[  
            { "UnitPrice":24.99,  "OrderQty":1 }  
         ]  
  },  
  {  
       "SalesOrderNumber":"SO4390" ,  
       "D":[  
            { "UnitPrice":24.99 }  
        ]  
  }  
]  
  
```  
  
## 참고 항목  
 [FOR 절&#40;Transact-SQL&#41;](../Topic/FOR%20Clause%20\(Transact-SQL\).md)  
  
  