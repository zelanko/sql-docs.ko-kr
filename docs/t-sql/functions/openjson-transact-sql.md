---
title: OPENJSON (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENJSON
- OPENJSON_TSQL
helpviewer_keywords:
- OPENJSON rowset function
- JSON, importing
- JSON, converting from
ms.assetid: 233d0877-046b-4dcc-b5da-adeb22f78531
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 29b296b2ae7e04871e81a9c236cb990bdd19562b
ms.openlocfilehash: 27eeb54d6493bb200e56caada1238d6fafb5b339
ms.contentlocale: ko-kr
ms.lasthandoff: 10/11/2017

---
# <a name="openjson-transact-sql"></a>OPENJSON (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

**OPENJSON** JSON 텍스트를 구문 분석 하 고 JSON 입력의 행과 열으로 개체 및 속성을 반환 하는 테이블 반환 함수입니다. 즉, **OPENJSON** JSON 문서를 통해 행 집합 뷰를 제공 합니다. 행 집합 및 열을 채우는 데 사용 되는 JSON 속성 경로에 열을 명시적으로 지정할 수 있습니다. 이후 **OPENJSON** 사용할 수는 행 집합 반환을 **OPENJSON** 에 `FROM` 절은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 처럼 다른 테이블, 뷰 또는 테이블 반환 함수를 사용할 수 있습니다.  
  
사용 하 여 **OPENJSON** JSON 데이터를 가져오는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], JSON 데이터를 응용 프로그램에 대 한 관계형 형식으로 변환 하거나 서비스에 직접 사용할 수 없는 JSON 또는 합니다.  
  
> [!NOTE]  
>  **OPENJSON** 함수는 더 높은 호환성 수준 130 에서만 사용할 수 있습니다. 데이터베이스 호환성 수준이 130보다 낮으면 SQL Server에서 **OPENJSON** 함수를 찾아 실행할 수 없습니다. 다른 JSON 함수는 모든 호환성 수준에서 사용할 수 있습니다.
> 
> `sys.databases` 뷰 또는 데이터베이스 속성에서 호환성 수준을 확인할 수 있습니다. 다음 명령 사용 하 여 데이터베이스의 호환성 수준을 변경할 수 있습니다.  
> 
> `ALTER DATABASE DatabaseName SET COMPATIBILITY_LEVEL = 130`
>   
> 호환성 수준 120 새 Azure SQL 데이터베이스에도 기본 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘")[TRANSACT-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
OPENJSON( jsonExpression [ , path ] )  [ <with_clause> ]

<with_clause> ::= WITH ( { colName type [ column_path ] [ AS JSON ] } [ ,...n ] )
```  

**OPENJSON** 구문 분석 하는 테이블 반환 함수는 *jsonExpression* 첫 번째 인수로 제공 되 고 식의 JSON 개체에서 데이터를 포함 하는 하나 이상의 행을 반환 합니다. *jsonExpression* 중첩 된 하위 개체를 포함할 수 있습니다. 내에서 하위 개체의 구문을 분석 하려는 경우 *jsonExpression*를 지정할 수 있습니다는 **경로** JSON 하위 개체에 대 한 매개 변수입니다.

### <a name="openjson"></a>openjson

![OPENJSON TVF에 대 한 구문](../../relational-databases/json/media/openjson-syntax.png "OPENJSON 구문")  

기본적으로는 **OPENJSON** 키 이름이 고 값을 포함 하는 세 개의 열을 반환 하는 테이블 반환 함수 이며 각 {키: 값을 (를) 쌍의 형식에 *jsonExpression*합니다. 대신 지정 하면 결과의 스키마 집합을 **OPENJSON** 제공 하 여 반환 *with_clause*합니다.
  
### <a name="withclause"></a>with_clause
  
![WITH 절에서 OPENJSON TVF에 대 한 구문](../../relational-databases/json/media/openjson-shema-syntax.png "OPENJSON 사용 구문")

*with_clause* 에 대 한 해당 형식 가진 열 목록이 포함 되어 **OPENJSON** 돌아갑니다. 기본적으로 **OPENJSON** 의 키와 일치 *jsonExpression* 에서 열 이름의 *with_clause* (이 경우 일치 하는 항목 키 있음을 의미 대/소문자 구분). 열 이름에는 키 이름이 일치 하지 않으면를 제공할 수 있습니다는 선택적 *column_path*, 변수인는 [JSON 경로 식](../../relational-databases/json/json-path-expressions-sql-server.md) 내에서 키를 참조 하는 *jsonExpression*합니다. 

## <a name="arguments"></a>인수  
### <a name="jsonexpression"></a>*jsonExpression*  
JSON 텍스트를 포함 하는 유니코드 문자 식입니다.  
  
OPENJSON은 JSON 식에 있는 개체의 속성 또는 배열의 요소를 반복 하 고 각 요소 또는 속성에 대 한 행을 반환 합니다. 다음 예에서는 변수로 제공 된 개체의 각 속성 반환 *jsonExpression*:  
  
```sql  
DECLARE @json NVARCHAR(4000) = N'{  
   "StringValue":"John",  
   "IntValue":45,  
   "TrueValue":true,  
   "FalseValue":false,  
   "NullValue":null,  
   "ArrayValue":["a","r","r","a","y"],  
   "ObjectValue":{"obj":"ect"}  
}'

SELECT *
FROM OPENJSON(@json)
```  
  
**결과**  
  
|Key|value|형식|  
|---------|-----------|----------|  
|StringValue|John|1.|  
|IntValue|45|2|  
|trueValue|true|3|  
|falseValue|false|3|  
|nullValue|NULL|0|  
|ArrayValue|["a", "r", "r", "","y"]|4|  
|ObjectValue|{"obj": "ect"을 (를)|5|  

### <a name="path"></a>*경로*  
개체 또는 배열 내에서 참조 하는 선택적 JSON 경로 식 *jsonExpression*합니다. **OPENJSON** 지정된 된 위치에 JSON 텍스트를 검색 하 고 참조 된 조각에만 구문 분석 합니다. 자세한 내용은 참조 하십시오. [JSON 경로 식 &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).

[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 및 [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]의 값으로 변수를 제공할 수 있습니다 *경로*합니다.
  
다음 예에서는 중첩된 된 개체를 지정 하 여 반환 된 *경로*:  

```sql  
DECLARE @json NVARCHAR(4000) = N'{  
      "path": {  
            "to":{  
                 "sub-object":["en-GB", "en-UK","de-AT","es-AR","sr-Cyrl"]  
                 }  
              }  
 }';

SELECT [key], value
FROM OPENJSON(@json,'$.path.to."sub-object"')
```  
  
 **결과**  
  
|Key|값|  
|---------|-----------|  
|0|en-GB|  
|1|en-UK|  
|2|de-AT|  
|3|es-AR|  
|4|sr-Cyrl|  
 
때 **OPENJSON** 구문 분석 하는 JSON 배열, 함수 반환는 요소의 인덱스도 JSON 텍스트의 키로 합니다.

JSON 식의 속성을 사용 하 여 경로 단계와 일치 하는 데 사용 하는 비교는 대/소문자 구분 및 데이터 정렬을 인식 하지 않는 (즉, BIN2 비교). 

### <a name="withclause"></a>*with_clause*
에 대 한 출력 스키마를 명시적으로 정의 된 **OPENJSON** 함수를 반환 합니다. 선택적 *with_clause* 다음과 같은 요소가 포함 될 수 있습니다.

*colName* 출력 열의 이름입니다.  
  
기본적으로 **OPENJSON** 열의 이름을 사용 하 여 JSON 텍스트의 속성과 일치 합니다. 예를 들어, 열을 지정 하면 *이름* 스키마에서 OPENJSON JSON 텍스트에 "name" 속성으로이 열을 채우는 하려고 합니다. 사용 하 여 기본 매핑을 재정의할 수는 *column_path* 인수입니다.  
  
*type*  
출력 열에 대 한 데이터 형식이입니다.  

> [!NOTE]
> 사용 하는 경우는 **AS JSON** 옵션을 열 *형식* 해야 `NVARCHAR(MAX)`합니다.
  
*column_path*  
지정된 된 열에 반환 하려면이 속성을 지정 하는 JSON 경로가입니다. 자세한 정보에 대 한 설명을 참조는 *경로* 이전에이 항목의 매개 변수입니다.  
  
사용 하 여 *column_path* 출력 열의 이름에는 속성의 이름과 일치 하지 않습니다 때 기본 매핑 규칙을 재정의할 수 있습니다.  
  
JSON 식의 속성을 사용 하 여 경로 단계와 일치 하는 데 사용 하는 비교는 대/소문자 구분 및 데이터 정렬을 인식 하지 않는 (즉, BIN2 비교).  
  
경로 대 한 자세한 내용은 참조 하십시오. [JSON 경로 식 &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
*JSON으로*  
사용 하 여는 **AS JSON** 옵션 열 정의에 참조 된 속성 배열 또는 JSON 개체 내부에 포함 되도록 지정할 수 있습니다. 지정 하는 경우는 **AS JSON** 옵션을 열의 형식을 nvarchar (max) 이어야 합니다.

-   지정 하지 않으면 **AS JSON** 는 열에 대 한 함수는 스칼라 값을 반환 (예: int, string, true, false) 지정된 된 JSON 속성에서 지정된 된 경로에 있습니다. 경로 개체 또는 배열이 면 나타내고 지정된 된 경로에 속성을 찾을 수 없습니다, 경우 함수 lax 모드에서 null을 반환 하거나 strict 모드에서 오류를 반환 합니다. 이 동작은의 동작과 비슷하지만 **JSON_VALUE** 함수입니다.  
  
-   지정 하는 경우 **AS JSON** 는 열에 대 한 함수는 JSON 조각을 반환 지정된 된 JSON 속성에서 지정된 된 경로에 있습니다. 경로 스칼라 값을 나타내고 지정된 된 경로에 속성을 찾을 수 없습니다, 경우 함수 lax 모드에서 null을 반환 하거나 strict 모드에서 오류를 반환 합니다. 이 동작은의 동작과 비슷하지만 **JSON_QUERY** 함수입니다.  
  
> [!NOTE]  
> 제공 해야 하는 JSON 속성에서 중첩 된 JSON 조각을 반환 하려는 경우는 **AS JSON** 플래그입니다. 이 옵션이 없으면 속성을 찾을 수 없는 경우 OPENJSON 대신 참조 된 JSON 개체 또는 배열에 NULL 값을 반환 합니다. 또는 strict 모드에서 런타임 오류를 반환 합니다.  
  
예를 들어 다음 쿼리에서 반환 하 고 배열 요소의 형식을 지정:  
  
```sql  
DECLARE @json NVARCHAR(MAX) = N'[  
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
   
SELECT *
FROM OPENJSON ( @json )  
WITH (   
              Number   varchar(200)   '$.Order.Number',  
              Date     datetime       '$.Order.Date',  
              Customer varchar(200)   '$.AccountNumber',  
              Quantity int            '$.Item.Quantity',  
              [Order]  nvarchar(MAX)  AS JSON  
 )
```  
  
**결과**  
  
|Number|날짜|Customer|수량|주문|  
|------------|----------|--------------|--------------|-----------|  
|SO43659|2011-05-31T00:00:00|AW29825|1.|{"Number": "SO43659", "날짜": "2011-05-31T00:00:00"을 (를)|  
|SO43661|2011-06-01T00:00:00|AW73565|3|{"Number": "SO43661", "날짜": "2011-06-01T00:00:00"을 (를)|  
  

## <a name="return-value"></a>반환 값  
OPENJSON 함수에서 반환 하는 열은 WITH 옵션에 따라 달라 집니다.  
  
1. -기본 스키마와 함께 OPENJSON을 호출 하는 경우 즉,-WITH 절에 명시적 스키마를 지정 하지 않으면 반환 됩니다는 다음과 같은 열이 있는 테이블:  
    1.  **키**합니다. 지정 된 배열의 요소 인덱스 또는 지정된 된 속성의 이름을 포함 하는 nvarchar (4000) 값입니다. 키 열에는 BIN2 데이터 정렬을 있습니다.  
    2.  **값**. 속성의 값을 포함 하는 nvarchar (max) 값입니다. 값 열에서 해당 데이터 정렬을 상속 *jsonExpression*합니다.
    3.  **형식**합니다. 값의 형식을 포함 하는 int 값입니다. **형식** 기본 스키마와 함께 OPENJSON을 사용 하는 경우에 열이 반환 됩니다. 유형 열에는 다음 값 중 하나가 있습니다.  
  
        |유형 열의 값|JSON 데이터 형식|  
        |------------------------------|--------------------|  
        |0|null|  
        |1.|string|  
        |2|int|  
        |3|true/false|  
        |4|array|  
        |5|개체(object)|  
  
     만 첫 번째 수준의 속성이 반환 됩니다. JSON 텍스트의 형식이 잘못 되었습니다 문은 실패 합니다.  

2. OPENJSON을 호출 하는 경우 WITH 절에 명시적 스키마를 지정 하면 함수는 WITH 절에 정의 된 스키마와 테이블을 반환 합니다.  

## <a name="remarks"></a>주의  

*json_path* 의 두 번째 인수에 사용 된 **OPENJSON** 또는 *with_clause* 로 시작할 수는 **lax** 또는 **엄격한** 키워드입니다.

-   **lax** 모드 **OPENJSON** 개체 또는 지정된 된 경로에서 값을 찾을 수 없는 경우 오류가 발생 하지 않습니다. 경로 찾을 수 없는 경우 **OPENJSON** 빈 결과 집합 또는 NULL 값을 반환 합니다.
-   **엄격한**, 모드 **OPENJSON** 경로 찾을 수 없는 경우 오류를 반환 합니다.

이 페이지의 예제 중 일부 lax 또는 strict path 모드를 명시적으로 지정합니다. Path 모드는 선택 사항입니다. Path 모드를 명시적으로 지정 하지 않으면, lax 모드는 기본값입니다. Path 모드와 경로 식에 대 한 자세한 내용은 참조 하십시오. [JSON 경로 식 &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).    

열 이름은 *with_clause* JSON 텍스트의 키와 일치 합니다. 열 이름을 지정 하면 `[Address.Country]`, 키와 일치 하는 `Address.Country`합니다. 중첩 된 키를 참조 하려는 경우 `Country` 개체 내에서 `Address`, 경로 지정 해야 `$.Address.Country` 열 경로입니다.

*json_path* 영숫자 문자로 키가 포함 될 수 있습니다. 키 이름을 이스케이프 *json_path* 는 키에 특수 문자를 포함 하는 경우 큰따옴표를 포함 합니다. 예를 들어 `$."my key $1".regularKey."key with . dot"` 일치 값이 다음 JSON 텍스트에서 1:

```json
{
  "my key $1": {
    "regularKey":{
      "key with . dot": 1
    }
  }
}
```  

## <a name="examples"></a>예  
  
### <a name="example-1---convert-a-json-array-to-a-temporary-table"></a>예제 1-임시 테이블을 JSON 배열 변환  
다음 예에서는 숫자의 JSON 배열로 식별자 목록을 제공합니다. 쿼리는 식별자의 테이블에 JSON 배열을 변환 하 고 지정한 id 가진 모든 제품을 필터링 합니다.  
  
```sql  
DECLARE @pSearchOptions NVARCHAR(4000) = N'[1,2,3,4]'

SELECT *
FROM products
INNER JOIN OPENJSON(@pSearchOptions) AS productTypes
 ON product.productTypeID = productTypes.value
```  
  
이 쿼리는 다음 예제와 동일 합니다. 그러나 아래 예에서 해야 쿼리 매개 변수로 전달 하는 대신에 숫자를 포함 합니다.  
  
```sql  
SELECT *
FROM products
WHERE product.productTypeID IN (1,2,3,4)
```  
  
### <a name="example-2---merge-properties-from-two-json-objects"></a>예제 2-두 JSON 개체에서 병합 속성  
다음 예제에서는 두 JSON 개체의 모든 속성의 합집합을 선택 합니다. 두 개체에는 중복 된 *이름* 속성입니다. 이 예제에서는 결과에서 중복 행을 제외 하는 키 값을 사용 합니다.  
  
```sql  
DECLARE @json1 NVARCHAR(MAX),@json2 NVARCHAR(MAX)

SET @json1=N'{"name": "John", "surname":"Doe"}'

SET @json2=N'{"name": "John", "age":45}'

SELECT *
FROM OPENJSON(@json1)
UNION ALL
SELECT *
FROM OPENJSON(@json2)
WHERE [key] NOT IN (SELECT [key] FROM OPENJSON(@json1))
```  
  
### <a name="example-3---join-rows-with-json-data-stored-in-table-cells-using-cross-apply"></a>예제 3-CROSS APPLY를 사용 하 여 표 셀에 저장 된 JSON 데이터와 조인 행  
다음 예제에서는 `SalesOrderHeader` 테이블에는 `SalesReason` 의 배열이 포함 된 텍스트 열 `SalesOrderReasons` JSON 형식에서입니다. `SalesOrderReasons` 개체와 같은 속성을 포함 *품질* 및 *제조업체*합니다. 이 예제에서는 모든 판매 주문 행을 관련된 판매 이유에 연결 하는 보고서를 만듭니다. OPENJSON 연산자는 이유는 별도 자식 테이블에 저장 된 경우 처럼 JSON 판매 이유 배열을 확장 합니다. 그런 다음 CROSS APPLY 연산자는 OPENJSON 테이블 반환 함수에서 반환 된 행을 각 판매 주문 행을 조인 합니다.  
  
```sql  
SELECT SalesOrderID,OrderDate,value AS Reason
FROM Sales.SalesOrderHeader
CROSS APPLY OPENJSON(SalesReasons)
```  
  
> [!TIP] 
> 일반적으로 사용, JSON 배열 개별 필드에 저장 하 고 해당 부모 행이 있는 테이블을 조인 확장 해야 할 경우는 [!INCLUDE[tsql](../../includes/tsql-md.md)] CROSS APPLY 연산자입니다. CROSS APPLY 하는 방법에 대 한 자세한 내용은 참조 하십시오. [from&#40; Transact SQL &#41; ](../../t-sql/queries/from-transact-sql.md).  
  
동일한 쿼리를 사용 하 여 다시 작성할 수 있습니다 `OPENJSON` 반환할 행의 명시적으로 정의 된 스키마와 함께:  
  
```sql  
SELECT SalesOrderID, OrderDate, value AS Reason  
FROM Sales.SalesOrderHeader  
     CROSS APPLY OPENJSON (SalesReasons) WITH (value nvarchar(100) '$')
```  
  
이 예제는 `$` 경로 배열에 있는 각 요소를 참조 합니다. 반환된 된 값을 명시적으로 캐스트 하려는 경우 이러한 유형의 쿼리를 사용할 수 있습니다.  
  
### <a name="example-4---combine-relational-rows-and-json-elements-with-cross-apply"></a>CROSS APPLY와 관계형 행과 JSON 요소를 결합 하는 예 4-  
다음 쿼리는 다음 표에 나와 있는 결과으로 관계형 행과 JSON 요소를 결합 합니다.  
  
```sql  
SELECT store.title, location.street, location.lat, location.long  
FROM store  
CROSS APPLY OPENJSON(store.jsonCol, 'lax $.location')   
     WITH (street varchar(500) ,  postcode  varchar(500) '$.postcode' ,  
     lon int '$.geo.longitude', lat int '$.geo.latitude')  
     AS location
```  
  
**결과**  
  
|title|street|postcode|lon|lat|  
|-----------|------------|--------------|---------|---------|  
|전체 음식 시장|17991 Redmond 방법|WA 98052|47.666124|-122.10155|  
|Sears|148th Ave NE|WA 98052|47.63024|-122.141246,17|  
  
### <a name="example-5---import-json-data-into-sql-server"></a>예 5-가져오기를 SQL Server로 JSON 데이터  
다음 예에는 전체 JSON 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 로드합니다.  
  
```sql  
DECLARE @json NVARCHAR(max)  = N'{  
  "id" : 2,  
  "firstName": "John",  
  "lastName": "Smith",  
  "isAlive": true,  
  "age": 25,  
  "dateOfBirth": "2015-03-25T12:00:00",  
  "spouse": null  
  }';  
   
  INSERT INTO Person  
  SELECT *   
  FROM OPENJSON(@json)  
  WITH (id int,  
        firstName nvarchar(50), lastName nvarchar(50),   
        isAlive bit, age int,  
        dateOfBirth datetime2, spouse nvarchar(50)
```  
  
## <a name="see-also"></a>관련 항목:  
 [JSON 경로 식 &#40; SQL Server &#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [JSON 데이터를 openjson&#40; 인 행과 열으로 변환 SQL Server &#41;](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)   
 [기본 스키마 &#40;와 함께 OPENJSON 사용 SQL Server &#41;](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md)   
 [명시적 스키마 &#40;와 함께 OPENJSON 사용 SQL Server &#41;](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md)  
  
  

