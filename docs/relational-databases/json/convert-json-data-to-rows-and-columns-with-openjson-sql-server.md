---
title: "OPENJSON을 사용하여 JSON 데이터를 행과 열로 변환(SQL Server) | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 01/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OPENJSON
- JSON, importing
- importing JSON
ms.assetid: 0c139901-01e2-49ef-9d62-57e08e32c68e
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ea85d2dff3afe1b5e5b56117255576f8d0ae2180
ms.lasthandoff: 04/11/2017

---
# <a name="convert-json-data-to-rows-and-columns-with-openjson-sql-server"></a>OPENJSON을 사용하여 JSON 데이터를 행과 열로 변환(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

**OPENJSON** 행 집합 함수는 JSON 텍스트를 일련의 행과 열로 변환합니다. **OPENJSON**을 사용하여 JSON 컬렉션에 대해 SQL 쿼리를 실행하거나 JSON 텍스트를 SQL Server 테이블로 가져올 수 있습니다.  
  
 **OPENJSON** 함수는 단일 JSON 개체 또는 JSON 개체 컬렉션을 받아서 하나 또는 여러 개의 행으로 변환합니다. 기본적으로 **OPENJSON** 함수는 다음을 반환합니다.
-   JSON 개체의 첫 번째 수준에서 발견된 모든 키:값 쌍입니다.
-   JSON 배열의 모든 요소 및 해당 인덱스입니다.  
  
필요에 따라 **WITH** 절을 추가하여 **OPENJSON** 함수에서 반환하는 행의 스키마를 지정합니다. 이 명시적 스키마는 출력의 구조를 정의합니다.  
  
## <a name="use-openjson-without-an-explicit-schema-for-the-output"></a>출력에 대한 명시적 스키마 없이 OPENJSON 사용
결과에 대한 명시적 스키마를 제공하지 않고, 즉 OPENJSON 뒤에 **WITH** 절 없이 **OPENJSON** 함수를 사용하는 경우 함수에서 다음 세 개의 열이 있는 테이블을 반환합니다.
1.  입력 개체의 속성 이름(또는 입력 배열의 요소 인덱스)
2.  속성 또는 배열 요소의 값
3.  형식(예: 문자열, 숫자, 부울, 배열 또는 개체)

JSON 개체의 각 속성 또는 배열의 각 요소가 개별 행으로 반환됩니다.  

다음은 기본 스키마와 함께 **OPENJSON**을 사용하고 JSON 개체의 각 속성에 대해 행 한 개를 반환하는 빠른 예제입니다.  
 
**예제**
```tsql  
DECLARE @json NVARCHAR(MAX)

SET @json='{"name":"John","surname":"Doe","age":45,"skills":["SQL","C#","MVC"]}';

SELECT *
FROM OPENJSON(@json);
```  
  
**결과**  
  
|Key|value|유형|  
|---------|-----------|----------|  
|name|John|1|  
|성|Doe|1|  
|나이|45|2|  
|기술|["SQL","C#","MVC"]|4|

### <a name="more-info"></a>추가 정보

자세한 내용과 예제를 보려면 [기본 스키마와 함께 OPENJSON 사용&#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md)을 참조하세요.

구문 및 사용법은 [OPENJSON&#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)에서만 사용할 수 있습니다. 

    
## <a name="use-openjson-with-an-explicit-schema-for-the-output"></a>출력에 대한 명시적 스키마로 OPENJSON 사용
**OPENJSON** 함수의 **WITH** 절을 사용하여 결과의 스키마를 지정하면 함수에서 **WITH** 절에 정의한 열만 포함된 테이블이 반환됩니다. **WITH** 절에 설정된 출력 열, 해당 형식, 그리고 각 출력 값에 대한 JSON 원본 속성의 경로를 지정합니다. **OPENJSON**은 JSON 개체 배열을 반복하고, 각 열에 대해 지정된 경로에서 값을 읽고 지정된 형식으로 변환합니다.  

다음은 명시적으로 지정된 결과의 스키마와 함께 **OPENJSON**을 사용하는 빠른 예제입니다.  
  
**예제**
  
```tsql  
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
  
|Number|날짜|Customer|수량|  
|------------|----------|--------------|--------------|  
|SO43659|2011-05-31T00:00:00|AW29825|1|  
|SO43661|2011-06-01T00:00:00|AW73565|3|  
  
 이 함수는 JSON 배열의 요소를 반환하고 형식을 지정합니다.  
  
-   **OPENJSON** 은 출력 테이블에 JSON 배열의 각 요소에 대한 새 행을 생성합니다. JSON 배열의 두 요소는 반환된 테이블에서 두 개의 행으로 변환됩니다.  
  
-   `colName type json_path` 구문을 사용하여 지정된 각 열에 대해 **OPENJSON** 함수는 지정된 경로의 각 배열 요소에 있는 값을 지정된 형식으로 변환하고 출력 테이블의 셀을 채웁니다. 이 예제에서는 `$.Order.Date` 경로의 각 개체에서 `Date` 열의 값을 가져와 datetime 값으로 변환합니다.  
  
**OPENJSON**을 사용하여 JSON 컬렉션을 행 집합으로 변환한 후 반환된 데이터에 대해 SQL 쿼리를 실행하거나 테이블에 삽입할 수 있습니다.  

### <a name="more-info"></a>추가 정보
자세한 내용과 예제를 보려면 [명시적 스키마와 함께 OPENJSON 사용&#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md)을 참조하세요.

구문 및 사용법은 [OPENJSON&#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)에서만 사용할 수 있습니다.

## <a name="openjson-requires-compatibility-level-130"></a>OPENJSON은 호환성 수준 130을 필요로 함
**OPENJSON** 함수는 **호환성 수준 130**에서만 사용할 수 있습니다. 데이터베이스 호환성 수준이 130보다 낮으면 SQL Server에서 **OPENJSON** 함수를 찾아 실행할 수 없습니다. 다른 기본 제공 JSON 함수는 모든 호환성 수준에서 사용할 수 있습니다. sys.databases 뷰 또는 데이터베이스 속성에서 호환성 수준을 확인할 수 있습니다.

다음 명령을 사용하여 데이터베이스의 호환성 수준을 변경할 수 있습니다.   
`ALTER DATABASE <DatabaseName> SET COMPATIBILITY_LEVEL = 130`  

## <a name="learn-more-about-openjson-and-built-in-json-support-in-sql-server"></a>OPENJSON 및 SQL Server의 기본 제공 JSON 지원에 대해 자세히 알아보기  
 [Microsoft 프로그램 관리자인 Jovan Popovic의 블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)  
  
## <a name="see-also"></a>참고 항목  
 [OPENJSON&#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
  

