---
title: "JSON에서 대괄호 제거 - WITHOUT_ARRAY_WRAPPER 옵션 | Microsoft 문서"
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: json
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- WITHOUT_ARRAY_WRAPPER
ms.assetid: aa86c2d1-458e-465f-abfa-75470137d054
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: bf0d7645df22c9a7540650e3c7f2ca2d0db8e1cc
ms.contentlocale: ko-kr
ms.lasthandoff: 07/31/2017

---
# <a name="remove-square-brackets-from-json---withoutarraywrapper-option"></a>JSON에서 대괄호 제거 - WITHOUT_ARRAY_WRAPPER 옵션
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

기본적으로 **FOR JSON** 절의 JSON 출력을 둘러싸고 있는 대괄호를 제거하려면 **WITHOUT_ARRAY_WRAPPER** 옵션을 지정합니다. 이 옵션에 단일 행 결과를 사용하여 단일 요소가 있는 배열 대신 단일 JSON 개체를 출력으로 생성합니다.

이 옵션에 여러 행 결과를 사용하면 여러 요소와 누락된 대괄호 때문에 결과 출력이 유효한 JSON이 아닙니다.  
  
## <a name="example-single-row-result"></a>예(단일 행 결과)  
다음 예제에는 **WITHOUT_ARRAY_WRAPPER** 옵션을 사용한 경우와 사용하지 않은 경우 **FOR JSON** 절의 출력이 나와 있습니다.  
  
 **쿼리**  
  
```sql  
SELECT 2015 as year, 12 as month, 15 as day  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER 
```  

 **WITHOUT_ARRAY_WRAPPER** 옵션을 사용할 때의 **결과**  
  
```json  
{
    "year": 2015,
    "month": 12,
    "day": 15
} 
```  
  
 **WITHOUT_ARRAY_WRAPPER** 옵션을 사용하지 않을 때의 **결과**(기본값)  
  
```json  
[{
    "year": 2015,
    "month": 12,
    "day": 15
}]
```  

## <a name="example-multiple-row-result"></a>예(여러 행 결과)
아래에는 **FOR JSON** 옵션을 사용한 경우와 사용하지 않은 경우 **WITHOUT_ARRAY_WRAPPER** 옵션을 지정합니다. 이 예는 여러 행 결과를 생성합니다. 여러 요소와 누락된 대괄호 때문에 출력은 유효한 JSON이 아닙니다.
  
 **Query**  
  
```sql  
SELECT TOP 3 SalesOrderNumber, OrderDate, Status  
FROM Sales.SalesOrderHeader  
ORDER BY ModifiedDate  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER 
```  
  
 **WITHOUT_ARRAY_WRAPPER** 옵션을 사용할 때의 **결과**  
  
```json  
{
    "SalesOrderNumber": "SO43662",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43661",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43660",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
} 
```  
  
 **WITHOUT_ARRAY_WRAPPER** 옵션을 사용하지 않을 때의 **결과**(기본값)  
  
```json  
[{
    "SalesOrderNumber": "SO43662",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43661",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43660",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}]
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>SQL Server의 기본 제공 JSON 지원에 대한 자세한 정보  
많은 특정 솔루션, 사용 사례 및 권장 사항은 Microsoft 프로그램 관리자인 Jovan Popovic이 제공하는 SQL Server 및 Azure SQL Database의 [기본 제공 JSON 지원에 대한 블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)을 참조하세요.
  
## <a name="see-also"></a>관련 항목:  
 [FOR 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  

