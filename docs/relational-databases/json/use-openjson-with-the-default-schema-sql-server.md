---
description: 기본 스키마와 함께 OPENJSON 사용
title: 기본 스키마와 함께 OPENJSON 사용
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- OPENJSON, with default schema
ms.assetid: 8e28a8f8-71a8-4c25-96b8-0bbedc6f41c4
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d88098e4317ebc5f4feb6b21b61cd9a98afee038
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424135"
---
# <a name="use-openjson-with-the-default-schema"></a>기본 스키마와 함께 OPENJSON 사용 
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  기본 스키마와 함께 **OPENJSON**을 사용하여 개체의 각 속성 또는 배열의 각 요소에 대해 행 한 개가 있는 테이블을 반환합니다.  
  
 아래에는 기본 스키마와 함께 **OPENJSON** 을 사용하는 몇 가지 예가 나와 있습니다. 자세한 내용 및 더 많은 예제를 보려면 [OPENJSON&#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)을 참조하세요.  
  
## <a name="example---return-each-property-of-an-object"></a>예 - 개체의 각 속성 반환  
 **쿼리**  
  
```sql  
SELECT *
FROM OPENJSON('{"name":"John","surname":"Doe","age":45}') 
```  
  
 **결과**  
  
|키|값|  
|---------|-----------|  
|name|John|  
|surname|Doe|  
|age|45|  
  
## <a name="example---return-each-element-of-an-array"></a>예 - 배열의 각 요소 반환  
 **쿼리**  
  
```sql  
SELECT [key],value
FROM OPENJSON('["en-GB", "en-UK","de-AT","es-AR","sr-Cyrl"]') 
```  
  
 **결과**  
  
|키|값|  
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
  
|키|값|Type|  
|---------|-----------|----------|  
|type|1|0|  
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

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>SQL Server 및 Azure SQL Database에서 JSON에 대한 자세한 정보  
  
### <a name="microsoft-videos"></a>Microsoft 비디오

SQL Server 및 Azure SQL Database에서 기본 제공 JSON 지원에 대한 시각적 소개는 다음 비디오를 참조하세요.

-   [SQL Server 2016 및 JSON 지원](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [SQL Server 2016 및 Azure SQL Database에서 JSON 사용](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL과 관계형 간에 브리지인 JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>참고 항목  
 [OPENJSON&#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
