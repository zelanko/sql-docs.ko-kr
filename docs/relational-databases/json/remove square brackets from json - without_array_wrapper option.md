---
title: "WITHOUT_ARRAY_WRAPPER 옵션(SQL Server)으로 JSON 출력에서 대괄호 제거 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WITHOUT_ARRAY_WRAPPER"
ms.assetid: aa86c2d1-458e-465f-abfa-75470137d054
caps.latest.revision: 11
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# WITHOUT_ARRAY_WRAPPER 옵션(SQL Server)으로 JSON 출력에서 대괄호 제거
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  기본적으로 **FOR JSON** 절의 JSON 출력을 둘러싸고 있는 대괄호를 제거하려면 **WITHOUT_ARRAY_WRAPPER** 옵션을 지정합니다. 이 옵션을 사용하여 단일 JSON 개체를 출력으로 생성합니다.  
  
 이 옵션을 지정하지 않으면 JSON 출력은 대괄호로 묶입니다.  
  
## 예  
 다음 예제에는 **WITHOUT_ARRAY_WRAPPER** 옵션을 사용한 경우와 사용하지 않은 경우 **FOR JSON** 절의 출력이 나와 있습니다.  
  
 **Query**  
  
```tsql  
SELECT 2015 as year, 12 as month, 15 as day  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER  
```  
  
 **WITHOUT_ARRAY_WRAPPER** 옵션을 사용할 때의 **결과**  
  
```json  
{ "year":2015, "month":12, "day":15 }  
```  
  
 **WITHOUT_ARRAY_WRAPPER** 옵션을 사용하지 않을 때의 **결과**  
  
```json  
[ { "year":2015, "month":12, "day":15 } ]  
```  
  
 아래에는 **WITHOUT_ARRAY_WRAPPER** 옵션을 사용한 **FOR JSON** 절의 다른 예가 나와 있습니다.  
  
 **Query**  
  
```tsql  
SELECT TOP 1 SalesOrderNumber, OrderDate, Status  
FROM Sales.SalesOrderHeader  
ORDER BY ModifiedDate  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER  
```  
  
 **WITHOUT_ARRAY_WRAPPER** 옵션을 사용할 때의 **결과**  
  
```json  
{  
    "SalesOrderNumber":"SO43660",  
    "OrderDate":"2011-05-31T00:00:00",  
    "Status":5  
}  
```  
  
 **WITHOUT_ARRAY_WRAPPER** 옵션을 사용하지 않을 때의 **결과**  
  
```json  
[  
    {  
        "SalesOrderNumber":"SO43660",  
        "OrderDate":"2011-05-31T00:00:00",  
        "Status":5  
    }  
]  
```  
  
## 참고 항목  
 [FOR 절&#40;Transact-SQL&#41;](../Topic/FOR%20Clause%20\(Transact-SQL\).md)  
  
  