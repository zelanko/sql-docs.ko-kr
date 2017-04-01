---
title: "OPENJSON을 사용하여 JSON 데이터를 행과 열로 변환(SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/31/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "OPENJSON"
  - "JSON, 가져오기"
  - "JSON 가져오기"
ms.assetid: 0c139901-01e2-49ef-9d62-57e08e32c68e
caps.latest.revision: 31
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# OPENJSON을 사용하여 JSON 데이터를 행과 열로 변환(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  **OPENJSON** 행 집합 함수를 사용하면 JSON 텍스트를 일련의 행과 열로 변환할 수 있습니다. **OPENJSON**을 사용하여 JSON 컬렉션에 대해 SQL 쿼리를 실행하거나 JSON 텍스트를 SQL Server 테이블로 가져올 수 있습니다.  
  
> [!NOTE] **OPENJSON** 함수는 **호환성 수준 130**에서만 사용할 수 있습니다. 데이터베이스 호환성 수준이 130보다 낮으면 SQL Server에서 **OPENJSON** 함수를 찾아 실행할 수 없습니다. 다른 JSON 함수는 모든 호환성 수준에서 사용할 수 있습니다. sys.databases 뷰 또는 데이터베이스 속성에서 호환성 수준을 확인할 수 있습니다.
> 
>   다음 명령을 사용하여 데이터베이스의 호환성 수준을 변경할 수 있습니다.   
>   ALTER DATABASE DatabaseName SET COMPATIBILITY_LEVEL = 130  
  
 **OPENJSON** 함수는 단일 JSON 개체 또는 JSON 개체 컬렉션을 받아서 하나 또는 여러 개의 행으로 변환합니다. 기본적으로 **OPENJSON** 함수는 JSON 배열의 모든 요소나 첫 번째 수준의 JSON 개체에 있는 모든 키:값 쌍을 해당 인덱스와 함께 반환합니다.  
  
 WITH 절을 사용하여 **OPENJSON** 함수에서 반환될 행의 스키마를 지정할 수 있습니다. 이 명시적 스키마는 출력의 구조를 정의합니다.  
  
## 결과 스키마 없이 OPENJSON 사용

다음은 기본 스키마와 함께 **OPENJSON**  을(를) 사용하고 JSON 개체의 각 속성에 대해 행 한 개를 반환하는 빠른 예제입니다.  
 
반환된 결과의 지정된 스키마 없이(즉, OPENJSON 뒤에 WITH 절 없이) **OPENJSON** 함수를 사용할 경우 함수에서 입력 개체의 속성 이름(또는 입력 배열의 요소 인덱스), 속성 또는 배열 요소의 값, 형식(예: 문자열, 숫자, 부울, 배열 또는 개체) 등 세 개의 열이 있는 테이블이 반환됩니다. JSON 개체(또는 배열 요소)의 속성은 별도 행에 반환됩니다.  

-   자세한 내용과 예제를 보려면 [기본 스키마와 함께 OPENJSON 사용&#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md)을 참조하세요.
-   구문 및 사용법은 [OPENJSON&#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)을 참조하세요. 

```tsql  
SET @json = '{"name":"John","surname":"Doe","age":45,"skills":["SQL","C#","MVC"]}';  
  
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
    
## 명시적 스키마와 함께 OPENJSON 사용

다음은 명시적으로 지정된 스키마와 함께 **OPENJSON**을 사용하는 빠른 예제입니다.  
  
**OPENJSON** 함수의 WITH 절에 반환된 결과의 스키마를 지정하면 함수에서 WITH 절에 정의한 열이 있는 테이블이 반환됩니다. WITH 절에 설정된 출력 열, 해당 형식, 그리고 각 출력 값에 대한 JSON 원본 속성의 경로를 지정할 수 있습니다. **OPENJSON**은 JSON 개체 배열을 반복하고, 각 열에 대해 지정된 경로에서 값을 읽고 지정된 형식으로 변환합니다.  

-   자세한 내용과 예제를 보려면 [명시적 스키마와 함께 OPENJSON 사용&#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md)을 참조하세요.
-   구문 및 사용법은 [OPENJSON&#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)을 참조하세요.
  
```tsql  
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
  
-   **OPENJSON**은 출력 테이블에 JSON 배열의 각 요소에 대한 새 행을 생성합니다. JSON 배열의 두 요소는 반환된 테이블에서 두 개의 행으로 변환됩니다.  
  
-   `colName type json_path` 구문을 사용하여 지정된 각 열에 대해 **OPENJSON**은 지정된 경로의 배열 요소에 있는 값을 지정된 형식으로 변환하고 출력 테이블의 셀을 채웁니다. 이 예제에서는 `$.Order.Date` 경로의 각 개체에서 Date 열의 값을 가져와 datetime 값으로 변환합니다.  
  
JSON 컬렉션을 행 집합으로 변환한 후 반환된 데이터에 대해 SQL 쿼리를 실행하거나 테이블에 삽입할 수 있습니다.  
  
## OPENJSON 및 SQL Server의 기본 제공 JSON 지원에 대해 자세히 알아보기  
 [Microsoft 프로그램 관리자인 Jovan Popovic의 블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)  
  
## 참고 항목  
 [OPENJSON&#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
  