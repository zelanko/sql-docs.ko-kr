---
title: "기본 스키마와 함께 OPENJSON 사용(SQL Server) | Microsoft Docs"
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
- OPENJSON, with default schema
ms.assetid: 8e28a8f8-71a8-4c25-96b8-0bbedc6f41c4
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: ff76c19a4834cb583779b4ab33d1167780f44b0c
ms.contentlocale: ko-kr
ms.lasthandoff: 07/31/2017

---
# <a name="use-openjson-with-the-default-schema-sql-server"></a>기본 스키마와 함께 OPENJSON 사용(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  기본 스키마와 함께 **OPENJSON** 을 사용하는 경우 개체의 각 속성 또는 배열의 각 요소에 대해 행 한 개가 있는 테이블이 반환됩니다.  
  
 아래에는 기본 스키마와 함께 **OPENJSON** 을 사용하는 몇 가지 예가 나와 있습니다. 자세한 내용 및 더 많은 예제를 보려면 [OPENJSON&#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)을 참조하세요.  
  
## <a name="example---return-each-property-of-an-object"></a>예 - 개체의 각 속성 반환  
 **Query**  
  
```sql  
SELECT *
FROM OPENJSON('{"name":"John","surname":"Doe","age":45}') 
```  
  
 **결과**  
  
|Key|값|  
|---------|-----------|  
|name|John|  
|surname|Doe|  
|age|45|  
  
## <a name="example---return-each-element-of-an-array"></a>예 - 배열의 각 요소 반환  
 **Query**  
  
```sql  
SELECT [key],value
FROM OPENJSON('["en-GB", "en-UK","de-AT","es-AR","sr-Cyrl"]') 
```  
  
 **결과**  
  
|Key|값|  
|---------|-----------|  
|0|en-GB|  
|1|en-UK|  
|2|de-AT|  
|3|es-AR|  
|4|sr-Cyrl|  
  
## <a name="example---convert-json-to-a-temporary-table"></a>예 - JSON을 임시 테이블로 변환  
 다음 쿼리는 **info** 개체의 모든 속성을 반환합니다.  
  
```sql  
DECLARE @json NVARCHAR(MAX)

SET @json=N'{  
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

SELECT *
FROM OPENJSON(@json,N'lax $.info')
```  
  
 **결과**  
  
|Key|값|형식|  
|---------|-----------|----------|  
|형식|1|0|  
|address|{ "town":"Bristol", "county":"Avon", "country":"England" }|5|  
|tags|[ "Sport", "Water polo" ]|4|  
  
## <a name="example---combine-relational-data-and-json-data"></a>예 - 관계형 데이터와 JSON 데이터 결합  
 다음 예에서는 SalesOrderHeader 테이블에 JSON 형식의 SalesOrderReasons 배열을 포함하는 SalesReason 텍스트 열이 있습니다. SalesOrderReasons 개체는 "Manufacturer", "Quality" 등의 속성을 포함합니다. 이 예에서는 판매 이유가 별도의 자식 테이블에 저장된 것처럼 JSON 판매 이유 배열을 확장하여 모든 판매 주문 행을 관련 판매 이유에 연결하는 보고서를 만듭니다.  
  
```sql  
SELECT SalesOrderID,OrderDate,value AS Reason
FROM Sales.SalesOrderHeader
CROSS APPLY OPENJSON(SalesReasons)
```  
  
 이 예에서 OPENJSON은 이유가 값 열로 표시되는 판매 이유 테이블을 반환합니다. CROSS APPLY 연산자는 각 판매 주문 행을 OPENJSON 테이블 반환 함수가 반환하는 행에 연결합니다.  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>SQL Server의 기본 제공 JSON 지원에 대한 자세한 정보  
많은 특정 솔루션, 사용 사례 및 권장 사항은 Microsoft 프로그램 관리자인 Jovan Popovic이 제공하는 SQL Server 및 Azure SQL Database의 [기본 제공 JSON 지원에 대한 블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)을 참조하세요.
  
## <a name="see-also"></a>관련 항목:  
 [OPENJSON&#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
  

