---
title: OPENJSON을 사용하여 JSON 데이터 구문 분석 및 변환(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: json
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- OPENJSON
- JSON, importing
- importing JSON
ms.assetid: 0c139901-01e2-49ef-9d62-57e08e32c68e
caps.latest.revision: 31
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c4567aa68fe7871fcb7cfcf1be3aa6ceb94be333
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32941178"
---
# <a name="parse-and-transform-json-data-with-openjson-sql-server"></a>OPENJSON을 사용하여 JSON 데이터 구문 분석 및 변환(SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

**OPENJSON** 행 집합 함수는 JSON 텍스트를 일련의 행과 열로 변환합니다. **OPENJSON**을 사용하여 JSON 컬렉션을 행 집합으로 변환한 후 반환된 데이터에 대해 SQL 쿼리를 실행하거나 SQL Server 테이블에 삽입할 수 있습니다. 
  
**OPENJSON** 함수는 단일 JSON 개체 또는 JSON 개체 컬렉션을 받아서 하나 또는 여러 개의 행으로 변환합니다. 기본적으로 **OPENJSON** 함수는 다음 데이터를 반환합니다.
-   JSON 개체에서 이 함수는 첫 번째 수준에서 발견된 모든 키/값 쌍을 반환합니다.
-   JSON 배열에서 이 함수는 모든 요소 및 해당 인덱스를 반환합니다.  

선택적 **WITH** 절을 추가하여 출력의 구조를 명시적으로 정의하는 스키마를 제공할 수 있습니다.  
  
## <a name="option-1---openjson-with-the-default-output"></a>옵션 1 - 기본 출력을 사용하는 OPENJSON
결과에 대한 명시적 스키마를 제공하지 않고, 즉 **OPENJSON** 뒤에 **WITH** 절 없이 **OPENJSON** 함수를 사용하는 경우 함수에서 다음 세 개의 열이 있는 테이블을 반환합니다.
1.  입력 개체의 속성 **이름**(또는 입력 배열의 요소 인덱스)
2.  속성 또는 배열 요소의 **값**
3.  **형식**(예: 문자열, 숫자, 부울, 배열 또는 개체)

**OPENJSON**은 JSON 개체의 각 속성 또는 배열의 각 요소를 개별 행으로 반환합니다.  

다음은 기본 스키마와 함께 즉, 선택적 **WITH** 절 없이 **OPENJSON**을 사용하고 JSON 개체의 각 속성에 대해 행 한 개를 반환하는 간단한 예제입니다.  
 
**예제**
```sql  
DECLARE @json NVARCHAR(MAX)

SET @json='{"name":"John","surname":"Doe","age":45,"skills":["SQL","C#","MVC"]}';

SELECT *
FROM OPENJSON(@json);
```  
  
**결과**  
  
|Key|value|유형|  
|---------|-----------|----------|  
|NAME|John|1|  
|성|Doe|1|  
|나이|45|2|  
|기술|["SQL","C#","MVC"]|4|

### <a name="more-info-about-openjson-with-the-default-schema"></a>기본 스키마를 사용하는 OPENJSON에 대한 추가 정보

자세한 내용과 예제를 보려면 [기본 스키마와 함께 OPENJSON 사용&#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md)을 참조하세요.

구문 및 사용법은 [OPENJSON&#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)에서만 사용할 수 있습니다. 

    
## <a name="option-2---openjson-output-with-an-explicit-structure"></a>옵션 2 - 명시적 구조를 사용하는 OPENJSON
**OPENJSON** 함수의 **WITH** 절을 사용하여 결과의 스키마를 지정하면 함수에서 **WITH** 절에 정의한 열만 포함된 테이블이 반환됩니다. 선택적 **WITH** 절에 출력 열 집합, 해당 형식 및 각 출력 값에 대한 JSON 원본 속성의 경로를 지정합니다. **OPENJSON**은 JSON 개체 배열을 반복하고, 각 열에 대해 지정된 경로에서 값을 읽고 지정된 형식으로 변환합니다.  

다음은 **WITH** 절에 명시적으로 지정한 출력의 스키마와 함께 **OPENJSON**을 사용하는 간단한 예제입니다.  
  
**예제**
  
```sql  
DECLARE @json NVARCHAR(MAX)
SET @json =   
  N'[  
       {  
         "Order": {  
           "Number":"SO43659",  
           "Date":"2011-05-31T00:00:00"  
         },  
         "AccountNumber":"AW29825",  
         "Item": {  
           "Price":2024.9940,  
           "Quantity":1  
         }  
       },  
       {  
         "Order": {  
           "Number":"SO43661",  
           "Date":"2011-06-01T00:00:00"  
         },  
         "AccountNumber":"AW73565",  
         "Item": {  
           "Price":2024.9940,  
           "Quantity":3  
         }  
      }  
 ]'  
   
SELECT * FROM  
 OPENJSON ( @json )  
WITH (   
              Number   varchar(200) '$.Order.Number' ,  
              Date     datetime     '$.Order.Date',  
              Customer varchar(200) '$.AccountNumber',  
              Quantity int          '$.Item.Quantity'  
 ) 
```  
  
**결과**  
  
|Number|date|Customer|수량|  
|------------|----------|--------------|--------------|  
|SO43659|2011-05-31T00:00:00|AW29825|1|  
|SO43661|2011-06-01T00:00:00|AW73565|3|  
  
이 함수는 JSON 배열의 요소를 반환하고 형식을 지정합니다.  
  
-   **OPENJSON** 은 출력 테이블에 JSON 배열의 각 요소에 대한 새 행을 생성합니다. JSON 배열의 두 요소는 반환된 테이블에서 두 개의 행으로 변환됩니다.  
  
-   `colName type json_path` 구문을 사용하여 지정된 각 열에 대해 **OPENJSON**은 지정된 경로의 각 배열 요소에 있는 값을 지정된 형식으로 변환합니다. 이 예제에서는 `$.Order.Date` 경로의 각 요소에서 `Date` 열의 값을 가져와 datetime 값으로 변환합니다.  
  
### <a name="more-info-about-openjson-with-an-explicit-schema"></a>명시적 스키마를 사용하는 OPENJSON에 대한 추가 정보
자세한 내용과 예제를 보려면 [명시적 스키마와 함께 OPENJSON 사용&#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md)을 참조하세요.

구문 및 사용법은 [OPENJSON&#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)에서만 사용할 수 있습니다.

## <a name="openjson-requires-compatibility-level-130"></a>OPENJSON은 호환성 수준 130을 필요로 함
**OPENJSON** 함수는 **호환성 수준 130**에서만 사용할 수 있습니다. 데이터베이스 호환성 수준이 130보다 낮으면 SQL Server에서 **OPENJSON** 함수를 찾아 실행할 수 없습니다. 다른 기본 제공 JSON 함수는 모든 호환성 수준에서 사용할 수 있습니다.

`sys.databases` 뷰 또는 데이터베이스 속성에서 호환성 수준을 확인할 수 있습니다.

다음 명령을 사용하여 데이터베이스의 호환성 수준을 변경할 수 있습니다.   
`ALTER DATABASE <DatabaseName> SET COMPATIBILITY_LEVEL = 130`  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>SQL Server 및 Azure SQL Database에서 JSON에 대한 자세한 정보  
  
### <a name="microsoft-blog-posts"></a>Microsoft 블로그 게시물  
  
특정 솔루션, 사용 사례 및 권장 사항은 SQL Server 및 Azure SQL Database의 기본 제공 JSON 지원에 대한 [블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)을 참조하세요.  

### <a name="microsoft-videos"></a>Microsoft 비디오

SQL Server 및 Azure SQL Database에서 기본 제공 JSON 지원에 대한 시각적 소개는 다음 비디오를 참조하세요.

-   [SQL Server 2016 및 JSON 지원](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [SQL Server 2016 및 Azure SQL Database에서 JSON 사용](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL과 관계형 간에 브리지인 JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>참고 항목  
 [OPENJSON&#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
  
