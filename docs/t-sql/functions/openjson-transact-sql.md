---
title: OPENJSON(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: genemi
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OPENJSON
- OPENJSON_TSQL
helpviewer_keywords:
- OPENJSON rowset function
- JSON, importing
- JSON, converting from
ms.assetid: 233d0877-046b-4dcc-b5da-adeb22f78531
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
ms.openlocfilehash: a9088b3502a010ce6b46f29516eefee5aa8934d1
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56012045"
---
# <a name="openjson-transact-sql"></a>OPENJSON(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

**OPENJSON**은 JSON 텍스트를 구문 분석하고 JSON 입력의 개체 및 속성을 행 및 열로 반환하는 테이블 반환 함수입니다. 즉, **OPENJSON**은 JSON 문서를 통해 행 집합 뷰를 제공합니다. 행 집합의 열과 열을 채우는 데 사용되는 JSON 속성 경로를 명시적으로 지정할 수 있습니다. **OPENJSON**은 행 집합을 반환하기 때문에 다른 테이블, 뷰 또는 테이블 반환 함수를 사용할 수 있는 것처럼, **OPENJSON**을 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 `FROM` 절에서 사용할 수 있습니다.  
  
**OPENJSON**을 사용하여 JSON 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 가져오거나 JSON을 직접 사용할 수 없는 앱이나 서비스에 대한 관계형 형식으로 JSON 데이터를 변환합니다.  
  
> [!NOTE]  
>  **OPENJSON** 함수는 호환성 수준 130 이상에서만 사용할 수 있습니다. 데이터베이스 호환성 수준이 130보다 낮으면 SQL Server에서 **OPENJSON** 함수를 찾아 실행할 수 없습니다. 다른 JSON 함수는 모든 호환성 수준에서 사용할 수 있습니다.
> 
> `sys.databases` 뷰 또는 데이터베이스 속성에서 호환성 수준을 확인할 수 있습니다. 다음 명령을 사용하여 데이터베이스의 호환성 수준을 변경할 수 있습니다.  
> 
> `ALTER DATABASE DatabaseName SET COMPATIBILITY_LEVEL = 130`
>   
> 새 Azure SQL Database에서도 호환성 수준 120이 기본값일 수 있습니다.  
  
 ![토픽 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "토픽 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
OPENJSON( jsonExpression [ , path ] )  [ <with_clause> ]

<with_clause> ::= WITH ( { colName type [ column_path ] [ AS JSON ] } [ ,...n ] )
```  

**OPENJSON** 테이블 반환 함수는 첫 번째 인수로 제공된 *jsonExpression*를 구문 분석하고 식의 JSON 개체에서 데이터를 포함하는 하나 이상의 행을 반환합니다. *jsonExpression*은 중첩된 하위 개체를 포함할 수 있습니다. *jsonExpression* 내에서 하위 개체를 구문 분석하려는 경우 JSON 하위 개체에 대한 **path** 매개 변수를 지정할 수 있습니다.

### <a name="openjson"></a>openjson

![OPENJSON TVF에 대한 구문](../../relational-databases/json/media/openjson-syntax.png "OPENJSON 구문")  

기본적으로 **OPENJSON** 테이블 반환 함수는 키 이름, 값 및 *jsonExpression*에 있는 각 {키:값} 쌍의 형식을 포함하는 세 개의 열을 반환합니다. 대신, *with_clause*을 제공하여 **OPENJSON**이 반환하는 결과 집합의 스키마를 명시적으로 지정할 수 있습니다. 
  
### <a name="withclause"></a>with_clause
  
![OPENJSON TVF의 WITH 절에 대한 구문](../../relational-databases/json/media/openjson-shema-syntax.png "OPENJSON WITH 구문")

*with_clause*는 반환할 **OPENJSON**에 대한 열과 형식의 목록을 포함합니다. 기본적으로 **OPENJSON**은 *jsonExpression*의 키와 *with_clause*의 열 이름을 일치시킵니다(이 경우 matches 키는 대/소문자를 구분함을 의미). 열 이름이 키 이름과 일치하지 않으면 *jsonExpression* 내의 키를 참조하는 [JSON 경로 식](../../relational-databases/json/json-path-expressions-sql-server.md)인 선택적 *column_path*를 제공할 수 있습니다. 

## <a name="arguments"></a>인수  
### <a name="jsonexpression"></a>*jsonExpression*  
JSON 텍스트를 포함하는 유니코드 문자 식입니다.  
  
OPENJSON은 JSON 식에 있는 배열의 요소 또는 개체의 속성을 반복하고 각 요소 또는 속성마다 하나의 행을 반환합니다. 다음 예제에서는 *jsonExpression*으로 제공된 개체의 각 속성을 반환합니다.  
  
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
  
|Key|value|유형|  
|---------|-----------|----------|  
|StringValue|John|1|  
|IntValue|45|2|  
|TrueValue|true|3|  
|FalseValue|false|3|  
|NullValue|NULL|0|  
|ArrayValue|["a", "r", "r",”a”,"y"]|4|  
|ObjectValue|{"obj":"ect"}|5|  

### <a name="path"></a>*path*  
*jsonExpression* 내의 개체 또는 배열을 참조하는 선택적 JSON 경로 식입니다. **OPENJSON**은 지정된 위치에서 JSON 텍스트를 검색하고 참조된 조각만 구문 분석합니다. 자세한 내용은 [JSON 경로 식&#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)을 참조하세요.

[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 및 [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]에서 *path* 값으로 변수를 제공할 수 있습니다.
  
다음 예제에서는 *path*를 지정하여 중첩된 개체를 반환합니다.  

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
 
**OPENJSON**이 JSON 배열을 구문 분석할 때, 이 함수는 JSON 텍스트에 있는 요소의 인덱스를 키로 반환합니다.

경로 단계와 JSON 식의 속성을 일치시키는 데 사용되는 비교는 대/소문자를 구분하고 데이터 정렬을 인식하지 못합니다(즉, BIN2 비교). 

### <a name="withclause"></a>*with_clause*
반환할 **OPENJSON** 함수의 출력 스키마를 명시적으로 정의합니다. 선택적 *with_clause*는 다음 요소를 포함할 수 있습니다.

*colName*은 출력 열의 이름입니다.  
  
기본적으로 **OPENJSON**은 열의 이름을 사용하여 JSON 텍스트의 속성을 일치시킵니다. 예를 들어, 스키마에 열 *name*을 지정하면 OPENJSON은 이 열을 JSON 텍스트의 "name" 속성으로 채웁니다. *column_path* 인수를 사용하여 이 기본 매핑을 재정의할 수 있습니다.  
  
*type*  
출력 열의 데이터 형식입니다.  

> [!NOTE]
> **AS JSON** 옵션도 사용하는 경우 열 *type*은 `NVARCHAR(MAX)`여야 합니다.
  
*column_path*  
지정된 열에서 반환할 속성을 지정하는 JSON 경로입니다. 자세한 내용은 이 토픽 이전의 *path* 매개 변수에 대한 설명을 참조하세요.  
  
출력 열의 이름이 속성의 이름과 일치하지 않으면, *column_path*를 사용하여 기본 매핑 규칙을 재정의하세요.  
  
경로 단계와 JSON 식의 속성을 일치시키는 데 사용되는 비교는 대/소문자를 구분하고 데이터 정렬을 인식하지 못합니다(즉, BIN2 비교).  
  
경로에 대한 자세한 내용은 [JSON 경로 식&#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)을 참조하세요.  
  
*AS JSON*  
열 정의에 **AS JSON** 옵션을 사용하여 참조된 속성이 JSON 개체 또는 배열 내부에 포함되도록 지정합니다. **AS JSON** 옵션을 지정하면 열의 형식이 NVARCHAR(MAX)여야 합니다.

-   열에 **AS JSON**을 지정하지 않으면 지정된 경로의 지정된 JSON 속성에서 스칼라 값(예: int, string, true, false)이 반환됩니다. 경로가 개체 또는 배열을 나타내고, 지정된 경로에서 속성을 찾을 수 없으면, 이 함수는 lax 모드에서 null을 반환하거나 strict 모드에서 오류를 반환합니다. 이 동작은 **JSON_VALUE** 함수의 동작과 비슷합니다.  
  
-   열에 **AS JSON**을 지정하면 지정된 경로의 지정된 JSON 속성에서 JSON 조각이 반환됩니다. 경로가 스칼라 값을 나타내고 지정된 경로에서 속성을 찾을 수 없으면, 이 함수는 lax 모드에서 null을 반환하거나 strict 모드에서 오류를 반환합니다. 이 동작은 **JSON_QUERY** 함수의 동작과 비슷합니다.  
  
> [!NOTE]  
> JSON 속성에서 중첩된 JSON 조각을 반환하려면 **AS JSON** 플래그를 제공해야 합니다. 이 옵션이 없으면 속성을 찾을 수 없으며, OPENJSON은 참조된 JSON 개체 또는 배열 대신 NULL 값을 반환하거나 strict 모드에서 런타임 오류를 반환합니다.  
  
예를 들어 다음 쿼리는 배열 요소를 반환하고 형식을 지정합니다.  
  
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
  
|Number|date|Customer|수량|주문|  
|------------|----------|--------------|--------------|-----------|  
|SO43659|2011-05-31T00:00:00|AW29825|1|{"Number":"SO43659","Date":"2011-05-31T00:00:00"}|  
|SO43661|2011-06-01T00:00:00|AW73565|3|{"Number":"SO43661","Date":"2011-06-01T00:00:00"}|  
  

## <a name="return-value"></a>반환 값  
OPENJSON 함수가 반환하는 열은 WITH 옵션에 따라 달라집니다.  
  
1. 기본 스키마를 사용하여 OPENJSON을 호출하면(즉, WITH 절에 명시적 스키마를 지정하지 않으면) 이 함수는 다음 열이 있는 테이블을 반환합니다.  
    1.  **Key**. 지정된 속성의 이름 또는 지정된 배열의 요소 인덱스를 포함하는 nvarchar(4000) 값입니다. 키 열에는 BIN2 데이터 정렬이 있습니다.  
    2.  **값**. 속성 값을 포함하는 nvarchar(max) 값입니다. 값 열은 *jsonExpression*에서 해당 데이터 정렬을 상속받습니다.
    3.  **Type**. 값의 형식을 포함하는 int 값입니다. OPENJSON을 기본 스키마와 함께 사용하는 경우에만 **Type** 열이 반환됩니다. Type 열은 다음 값 중 하나를 가집니다.  
  
        |Type 열의 값|JSON 데이터 형식|  
        |------------------------------|--------------------|  
        |0|null|  
        |1|string|  
        |2|ssNoversion|  
        |3|true/false|  
        |4|array|  
        |5|개체(object)|  
  
     첫 번째 수준 속성만 반환됩니다. JSON 텍스트의 형식이 올바르지 않으면 문이 실패합니다.  

2. OPENJSON을 호출하고 WITH 절에 명시적 스키마를 지정하면, 함수는 WITH 절에 정의한 스키마가 있는 테이블을 반환합니다.  

## <a name="remarks"></a>Remarks  

**OPENJSON**의 두 번째 인수 또는 *with_clause*에 사용된 *json_path*는 **lax** 또는 **strict** 키워드로 시작될 수 있습니다.

-   **lax** 모드에서 지정된 경로의 개체 또는 값을 찾을 수 없는 경우 **OPENJSON**에서 오류를 반환하지 않습니다. 경로를 찾을 수 없는 경우 **OPENJSON**은 빈 결과 집합 또는 NULL 값을 반환합니다.
-   **strict** 모드에서 경로를 찾을 수 없는 경우 **OPENJSON**은 오류를 반환합니다.

이 페이지의 예제 중 일부는 경로 모드인 lax 또는 strict를 명시적으로 지정합니다. 경로 모드는 선택적입니다. 경로 모드를 명시적으로 지정하지 않으면 lax 모드가 기본값입니다. 경로 모드 및 경로 식에 대한 자세한 내용은 [JSON 경로 식&#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)을 참조하세요.    

*with_clause*의 열 이름은 JSON 텍스트의 키와 일치합니다. 열 이름 `[Address.Country]`를 지정하면 키 `Address.Country`와 일치합니다. 개체 `Address` 내에서 중첩된 키 `Country`를 참조하려면 열 경로에 경로 `$.Address.Country`를 지정해야 합니다.

*json_path*에는 영숫자가 포함된 키가 포함될 수 있습니다. 키에 특수 문자가 있으면 *json_path*에서 키 이름을 큰따옴표로 이스케이프합니다. 예를 들어 `$."my key $1".regularKey."key with . dot"`은 다음 JSON 텍스트에서 값 1과 일치합니다.

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
  
### <a name="example-1---convert-a-json-array-to-a-temporary-table"></a>예 1 - JSON 배열을 임시 테이블로 변환  
다음 예에서는 JSON 숫자 배열로 식별자 목록을 제공합니다. 이 쿼리는 JSON 배열을 식별자 테이블로 변환하고 지정된 id를 사용하여 모든 제품을 필터링합니다.  
  
```sql  
DECLARE @pSearchOptions NVARCHAR(4000) = N'[1,2,3,4]'

SELECT *
FROM products
INNER JOIN OPENJSON(@pSearchOptions) AS productTypes
 ON product.productTypeID = productTypes.value
```  
  
이 쿼리는 다음 예와 동일합니다. 그러나 아래 예에서는 숫자를 매개 변수로 전달하는 대신 쿼리에 포함해야 합니다.  
  
```sql  
SELECT *
FROM products
WHERE product.productTypeID IN (1,2,3,4)
```  
  
### <a name="example-2---merge-properties-from-two-json-objects"></a>예 2 - 두 JSON 개체의 속성 병합  
다음 예에서는 두 JSON 개체의 모든 속성의 합집합을 선택합니다. 두 개체에는 중복된 *name* 속성이 있습니다. 이 예에서는 키 값을 사용하여 중복 행을 결과에서 제외합니다.  
  
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
  
### <a name="example-3---join-rows-with-json-data-stored-in-table-cells-using-cross-apply"></a>예 3 - CROSS APPLY를 사용하여 테이블 셀에 저장된 JSON 데이터와 행 조인  
다음 예에서 `SalesOrderHeader` 테이블에는 JSON 형식의 `SalesOrderReasons` 배열을 포함하는 `SalesReason` 텍스트 열이 있습니다. `SalesOrderReasons` 개체에는 *Quality* 및 *Manufacturer*와 같은 속성이 포함됩니다. 이 예에서는 모든 판매 주문 행을 관련된 판매 이유에 조인하는 보고서를 만듭니다. OPENJSON 연산자는 이유가 별도의 자식 테이블에 저장된 것처럼 JSON 판매 이유 배열을 확장합니다. 그런 다음, CROSS APPLY 연산자가 각 판매 주문 행을 OPENJSON 테이블 반환 함수가 반환한 행에 조인합니다.  
  
```sql  
SELECT SalesOrderID,OrderDate,value AS Reason
FROM Sales.SalesOrderHeader
CROSS APPLY OPENJSON(SalesReasons)
```  
  
> [!TIP] 
> 개별 필드에 저장된 JSON 배열을 확장하고 부모 행과 조인해야 하는 경우, 일반적으로 [!INCLUDE[tsql](../../includes/tsql-md.md)] CROSS APPLY 연산자를 사용합니다. CROSS APPLY에 대한 자세한 내용은 [FROM&#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)을 참조하세요.  
  
반환할 행의 명시적으로 정의된 스키마와 `OPENJSON`을 사용하여 동일한 쿼리를 다시 작성할 수 있습니다.  
  
```sql  
SELECT SalesOrderID, OrderDate, value AS Reason  
FROM Sales.SalesOrderHeader  
     CROSS APPLY OPENJSON (SalesReasons) WITH (value nvarchar(100) '$')
```  
  
이 예에서 `$` 경로는 배열에 있는 각 요소를 참조합니다. 반환된 값을 명시적으로 캐스팅하려는 경우 이러한 형식의 쿼리를 사용할 수 있습니다.  
  
### <a name="example-4---combine-relational-rows-and-json-elements-with-cross-apply"></a>예 4 - CROSS APPLY를 사용하여 관계형 행과 JSON 요소 결합  
다음 쿼리는 관계형 행과 JSON 요소를 다음 테이블에 나와 있는 결과에 결합합니다.  
  
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
|Whole Food Markets|17991 Redmond Way|WA  98052|47.666124|-122.10155|  
|Sears|148th Ave NE|WA  98052|47.63024|-122.141246,17|  
  
### <a name="example-5---import-json-data-into-sql-server"></a>예 5 - SQL Server로 JSON 데이터 가져오기  
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
        dateOfBirth datetime2, spouse nvarchar(50))
```  
  
## <a name="see-also"></a>참고 항목  
 [JSON 경로 식&#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [OPENJSON을 사용하여 JSON 데이터를 행과 열로 변환&#40;SQL Server&#41;](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)   
 [기본 스키마와 함께 OPENJSON 사용&#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md)   
 [명시적 스키마와 함께 OPENJSON 사용&#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md)  
  
  
