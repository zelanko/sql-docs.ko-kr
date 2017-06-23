---
title: "JSON에서 대괄호 제거 - WITHOUT_ARRAY_WRAPPER 옵션 | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
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
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 36e612b6c3759d968687d8ba35286c399de02a74
ms.contentlocale: ko-kr
ms.lasthandoff: 06/23/2017

---
# <a name="remove-square-brackets-from-json---withoutarraywrapper-option"></a>JSON에서 대괄호 제거 - WITHOUT_ARRAY_WRAPPER 옵션
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

기본적으로 **FOR JSON** 절의 JSON 출력을 둘러싸고 있는 대괄호를 제거하려면 **WITHOUT_ARRAY_WRAPPER** 옵션을 지정합니다. 단일 요소가 있는 배열 대신 출력으로 단일 JSON 개체를 생성 하는 단일 행 결과 함께이 옵션을 사용 합니다.

다중 행 결과 함께이 옵션을 사용 하는 경우 결과 출력 유효한 JSON으로 인해 않습니다 여러 요소와 누락 된 대괄호입니다.  
  
## <a name="example-single-row-result"></a>예 (단일 행 결과)  
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
  
 **결과** (기본값) 없이 **WITHOUT_ARRAY_WRAPPER** 옵션  
  
```json  
[{
    "year": 2015,
    "month": 12,
    "day": 15
}]
```  

## <a name="example-multiple-row-result"></a>예 (여러 행 결과)
아래에는 **FOR JSON** 옵션을 사용한 경우와 사용하지 않은 경우 **WITHOUT_ARRAY_WRAPPER** 옵션을 지정합니다. 이 예에서는 다중 행 결과 생성 합니다. 여러 요소와 대괄호 누락으로 인해 출력은 유효한 JSON 하지 않습니다.
  
 **쿼리**  
  
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
  
 **결과** (기본값) 없이 **WITHOUT_ARRAY_WRAPPER** 옵션  
  
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

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>기본 제공 SQL Server에서 JSON 지원에 대 한 자세한 정보  
특정 솔루션에 많이 사용 사례 및 권장 사항, 참조는 [기본 제공 JSON 지원에 대 한 블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) SQL Server와 Microsoft 프로그램 관리자 인 Jovan popovic의 Azure SQL 데이터베이스에 있습니다.
  
## <a name="see-also"></a>관련 항목:  
 [FOR 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  

