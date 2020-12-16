---
description: SQL Server의 JSON 데이터
title: JSON 데이터 작업
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: quickstart
helpviewer_keywords:
- JSON
- JSON, built-in support
ms.assetid: c9a4e145-33c3-42b2-a510-79813e67806a
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||= azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3ca366f274f4880fdb629eab4b77fa180bacb60b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463514"
---
# <a name="json-data-in-sql-server"></a>SQL Server의 JSON 데이터

[!INCLUDE[appliesto-ss2016-asdb-asdw-xxx-md.md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

JSON은 최신 웹 및 모바일 애플리케이션에서 데이터를 교환하는 데 사용되는 일반적인 텍스트 데이터 형식입니다. JSON은 로그 파일 또는 Microsoft Azure Cosmos DB와 같은 NoSQL 데이터베이스에 구조화되지 않은 데이터를 저장하는 데에도 사용됩니다. 많은 REST 웹 서비스에서 JSON 텍스트로 형식이 지정된 결과를 반환하거나 JSON으로 형식이 지정된 데이터를 허용합니다. 예를 들어 Azure Search, Azure Storage, Azure Cosmos DB 등 대부분의 Azure 서비스에는 JSON을 반환하거나 사용하는 REST 엔드포인트가 있습니다. 또한 JSON은 AJAX 호출을 사용하여 웹 페이지와 웹 서버 간에 데이터를 교환하는 기본 형식입니다. 

SQL Server의 JSON 함수를 사용하면 NoSQL과 관계형 개념을 동일한 데이터베이스에서 결합할 수 있습니다. 이제 기본 관계형 열을 동일한 테이블에서 JSON 텍스트로 형식이 지정된 문서를 포함하는 열과 결합하여 관계형 구조로 JSON 문서를 구문 분석하고 가져오거나 관계형 데이터를 JSON 텍스트로 형식을 지정할 수 있습니다. 다음 비디오에서 JSON 함수가 SQL Server 및 Azure SQL 데이터베이스에서 관계형 및 NoSQL 개념을 연결하는 방법을 볼 수 있습니다.

*NoSQL과 관계형 간에 브리지인 JSON*
> [!VIDEO https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds/player]

JSON 텍스트의 예는 다음과 같습니다.

```json
[
  {
    "name": "John",
    "skills": ["SQL", "C#", "Azure"]
  },
  {
    "name": "Jane",
    "surname": "Doe"
  }
]
```

SQL Server 기본 제공 함수 및 연산자를 사용하여 JSON 텍스트로 다음 작업을 수행할 수 있습니다.

- JSON 텍스트를 구문 분석하고 값을 읽거나 수정합니다.  
- JSON 개체의 배열을 테이블 형식으로 변환합니다.  
- 변환된 JSON 개체에서 모든 Transact-SQL 쿼리를 실행합니다.  
- JSON 형식으로 Transact-SQL 쿼리의 결과 서식을 지정합니다.  
  
![기본 제공 JSON 지원 개요](../../relational-databases/json/media/jsonslides1overview.png "기본 제공 JSON 지원 개요")  
  
## <a name="key-json-capabilities-of-sql-server-and-sql-database"></a>SQL Server 및 SQL Database의 주요 JSON 기능

다음 섹션에서는 SQL Server에서 기본 제공 JSON 지원을 통해 제공하는 주요 기능을 설명합니다. 다음 동영상에서 JSON 함수 및 연산자를 사용하는 방법을 볼 수 있습니다.

*SQL Server 2016 및 JSON 지원*
> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support/player?WT.mc_id=dataexposed-c9-niner]

### <a name="extract-values-from-json-text-and-use-them-in-queries"></a>JSON 텍스트에서 값을 추출하여 쿼리에서 사용

데이터베이스 테이블에 저장된 JSON 텍스트가 있는 경우 다음과 같은 기본 제공 함수를 사용하여 JSON 텍스트의 값을 읽거나 수정할 수 있습니다.  

- [ISJSON(Transact-SQL)](../../t-sql/functions/isjson-transact-sql.md)은 문자열에 유효한 JSON이 포함되어 있는지 여부를 테스트합니다.
- [JSON_VALUE(Transact-SQL)](../../t-sql/functions/json-value-transact-sql.md)는 JSON 문자열에서 스칼라 값을 추출합니다.
- [JSON_QUERY(Transact-SQL)](../../t-sql/functions/json-query-transact-sql.md)는 JSON 문자열에서 개체 또는 배열을 추출합니다.
- [JSON_MODIFY(Transact-SQL)](../../t-sql/functions/json-modify-transact-sql.md)는 JSON 문자열에 있는 값을 변경합니다.

**예제**

다음 예제에서 쿼리는 테이블의 관계형 및 JSON 데이터(`jsonCol` 열에 저장됨)를 모두 사용합니다.  
  
```sql  
SELECT Name, Surname,
  JSON_VALUE(jsonCol, '$.info.address.PostCode') AS PostCode,
  JSON_VALUE(jsonCol, '$.info.address."Address Line 1"') + ' '
  + JSON_VALUE(jsonCol, '$.info.address."Address Line 2"') AS Address,
  JSON_QUERY(jsonCol, '$.info.skills') AS Skills
FROM People
WHERE ISJSON(jsonCol) > 0
  AND JSON_VALUE(jsonCol, '$.info.address.Town') = 'Belgrade'
  AND Status = 'Active'
ORDER BY JSON_VALUE(jsonCol, '$.info.address.PostCode')
```  
  
애플리케이션 및 도구는 스칼라 테이블 열에서 가져온 값과 JSON 열에서 가져온 값 간의 차이점을 표시하지 않습니다. Transact-SQL 쿼리의 모든 부분(WHERE, ORDER BY, GROUP BY 절, 창 집계 등 포함)에서 JSON 텍스트 값을 사용할 수 있습니다. JSON 함수는 JavaScript 형식의 구문을 사용하여 JSON 텍스트 내의 값을 참조합니다.

자세한 내용은 [기본 함수를 사용하여 JSON 데이터 유효성 검사, 쿼리, 변경(SQL Server)](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md), [JSON_VALUE(Transact-SQL)](../../t-sql/functions/json-value-transact-sql.md) 및 [JSON_QUERY(Transact-SQL)](../../t-sql/functions/json-query-transact-sql.md)를 참조하세요.  
  
### <a name="change-json-values"></a>JSON 값 변경

JSON 텍스트의 일부를 수정해야 하는 경우 [JSON_MODIFY(Transact-SQL)](../../t-sql/functions/json-modify-transact-sql.md) 함수를 사용하여 JSON 문자열에서 속성 값을 업데이트하고 업데이트된 JSON 문자열을 반환할 수 있습니다. 다음 예제에서는 JSON이 포함된 변수에서 속성 값을 업데이트합니다.  
  
```sql
DECLARE @json NVARCHAR(MAX);
SET @json = '{"info": {"address": [{"town": "Belgrade"}, {"town": "Paris"}, {"town":"Madrid"}]}}';
SET @json = JSON_MODIFY(@json, '$.info.address[1].town', 'London');
SELECT modifiedJson = @json;
```

**결과**

|modifiedJson|  
|--------|  
|{"info":{"address":[{"town":"Belgrade"},{"town":"London"},{"town":"Madrid"}]}|  
  
### <a name="convert-json-collections-to-a-rowset"></a>JSON 컬렉션을 행 집합으로 변환

SQL Server의 JSON 쿼리에는 사용자 지정 쿼리 언어가 필요 없습니다. JSON 데이터를 쿼리하려면 표준 T-SQL을 사용하면 됩니다. JSON 데이터에 대한 쿼리 또는 보고서를 만들어야 하는 경우 **OPENJSON** 행 집합 함수를 호출하여 JSON 데이터를 행 및 열로 쉽게 변환할 수 있습니다. 자세한 내용은 [OPENJSON을 사용하여 JSON 데이터를 행과 열로 변환(SQL Server)](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)을 참조하세요.  
  
다음 예제에서는 **OPENJSON** 을 호출하고 `@json` 변수에 저장된 개체 배열을 표준 SQL **SELECT** 문을 사용하여 쿼리할 수 있는 행 집합으로 변환합니다.  
  
```sql  
DECLARE @json NVARCHAR(MAX);
SET @json = N'[
  {"id": 2, "info": {"name": "John", "surname": "Smith"}, "age": 25},
  {"id": 5, "info": {"name": "Jane", "surname": "Smith"}, "dob": "2005-11-04T12:00:00"}
]';

SELECT *
FROM OPENJSON(@json)
  WITH (
    id INT 'strict $.id',
    firstName NVARCHAR(50) '$.info.name',
    lastName NVARCHAR(50) '$.info.surname',
    age INT,
    dateOfBirth DATETIME2 '$.dob'
  );
```

**결과**

|ID|firstName|lastName|age|dateOfBirth|  
|--------|---------------|--------------|---------|-----------------|  
|2|John|Smith|25||  
|5|Jane|Smith||2005-11-04T12:00:00|  
  
**OPENJSON** 은 JSON 개체 배열을 테이블로 변환합니다. 각 개체는 하나의 행으로 표현되고 키/값 쌍은 셀로 반환됩니다. 출력은 다음 규칙을 준수합니다.

- **OPENJSON** 은 JSON 값을 **WITH** 절에 지정된 형식으로 변환합니다.
- **OPENJSON** 은 기본 키:값 쌍과 계층적으로 구성된 중첩된 개체를 모두 처리할 수 있습니다.
- JSON 텍스트에 포함된 모든 필드를 반환할 필요가 없습니다.
- **OPENJSON** 은 JSON 값이 없을 경우 NULL 값을 반환합니다.
- 중첩된 속성을 참조하거나 다른 이름의 속성을 참조하려면 형식 지정 후 필요에 따라 경로를 지정할 수 있습니다.
- 경로에서 선택적 **strict** 접두사는 지정된 속성의 값이 JSON 텍스트에 있어야 하도록 지정합니다.

자세한 내용은 [OPENJSON을 사용하여 JSON 데이터를 행과 열로 변환(SQL Server)](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md) 및 [OPENJSON(Transact-SQL)](../../t-sql/functions/openjson-transact-sql.md)을 참조하세요.  

JSON 문서에는 표준 관계형 열에 직접 매핑할 수 없는 하위 요소 및 계층적 데이터가 있을 수 있습니다. 이 경우 하위 배열과 부모 엔터티를 조인하여 JSON 계층 구조를 평면화할 수 있습니다.

다음 예제에서 배열의 두 번째 개체에는 사람 기술을 나타내는 하위 배열이 있습니다. 모든 하위 개체는 추가 `OPENJSON` 함수 호출을 사용하여 구문 분석할 수 있습니다.

```sql  
DECLARE @json NVARCHAR(MAX);
SET @json = N'[  
  {"id": 2, "info": {"name": "John", "surname": "Smith"}, "age": 25},
  {"id": 5, "info": {"name": "Jane", "surname": "Smith", "skills": ["SQL", "C#", "Azure"]}, "dob": "2005-11-04T12:00:00"}  
]';

SELECT *  
FROM OPENJSON(@json)  
  WITH (
    id INT 'strict $.id',
    firstName NVARCHAR(50) '$.info.name',
    lastName NVARCHAR(50) '$.info.surname',  
    age INT,
    dateOfBirth DATETIME2 '$.dob',
    skills NVARCHAR(MAX) '$.info.skills' AS JSON
  )
OUTER APPLY OPENJSON(skills)
  WITH (skill NVARCHAR(8) '$');
```

**기술** 배열은 첫 번째 `OPENJSON`에서 원래 JSON 텍스트 조각으로 반환되고 `APPLY` 연산자를 사용하여 다른 `OPENJSON` 함수로 전달됩니다. 두 번째 `OPENJSON` 함수는 JSON 배열을 구분 분석하고 문자열 값을 첫 번째 `OPENJSON`의 결과와 조인될 단일 열 행 집합으로 반환합니다.
이 쿼리의 결과는 다음 표에 표시됩니다.

**결과**

|ID|firstName|lastName|age|dateOfBirth|skill|  
|--------|---------------|--------------|---------|-----------------|----------|  
|2|John|Smith|25|||  
|5|Jane|Smith||2005-11-04T12:00:00|SQL|
|5|Jane|Smith||2005-11-04T12:00:00|C#|
|5|Jane|Smith||2005-11-04T12:00:00|Azure|

`OUTER APPLY OPENJSON`은 하위 배열과 첫 번째 수준 엔터티를 조인하고, 결과 집합을 평면화합니다. JOIN으로 인해 모든 기술에 대해 두 번째 행이 반복됩니다.

### <a name="convert-sql-server-data-to-json-or-export-json"></a>SQL Server 데이터를 JSON으로 변환하거나 JSON 내보내기

>[!NOTE]
>Azure Synapse Analytics 데이터를 JSON으로 변환하거나 JSON을 내보낼 수 없습니다.

**SELECT** 문에 **FOR JSON** 절을 추가하여 SQL Server 데이터 또는 SQL 쿼리 결과를 JSON으로 서식 지정합니다. **FOR JSON** 을 사용하여 JSON 출력의 형식을 클라이언트 애플리케이션에서 SQL Server로 위임합니다. 자세한 내용은 [FOR JSON을 사용하여 쿼리 결과 서식을 JSON으로 지정(SQL Server)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)을 참조하세요.  
  
다음 예제에서는 **FOR JSON** 절에서 PATH 모드를 사용합니다.  
  
```sql  
SELECT id, firstName AS "info.name", lastName AS "info.surname", age, dateOfBirth AS dob
FROM People
FOR JSON PATH;
```

이 **SELECT** 절은 JSON을 이해하는 모든 응용 프로그램에 제공될 수 있는 JSON 텍스트로 SQL 결과의 형식을 지정합니다. PATH 옵션은 SELECT 절에서 점으로 구분된 별칭을 사용하여 쿼리 결과에 개체를 중첩합니다.  
  
**결과**

```json  
[
  {
    "id": 2,
    "info": {
      "name": "John",
      "surname": "Smith"
    },
    "age": 25
  },
  {
    "id": 5,
    "info": {
      "name": "Jane",
      "surname": "Smith"
    },
    "dob": "2005-11-04T12:00:00"
  }
]
```  
  
자세한 내용은 [FOR JSON을 사용하여 쿼리 결과 서식을 JSON으로 지정(SQL Server)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md) 및 [FOR 절(Transact-SQL)](../../t-sql/queries/select-for-clause-transact-sql.md)을 참조하세요.  

## <a name="use-cases-for-json-data-in-sql-server"></a>SQL Server에서 JSON 데이터에 대한 사용 사례

SQL Server 및 Azure SQL Database의 JSON 지원을 통해 관계형 및 NoSQL 개념을 결합할 수 있습니다. 관계형을 반구조화된 데이터로 쉽게 변환하거나 반대로 변환할 수 있습니다. 하지만 JSON은 기존 관계형 모델에 대한 대체입니다. SQL Server와 SQL Database의 JSON 지원을 활용하는 몇 가지 특정 사용 사례는 다음과 같습니다.

### <a name="simplify-complex-data-models"></a>복잡한 데이터 모델 간소화

여러 자식 테이블 대신 JSON 필드를 사용하여 데이터 모델을 비정규화하는 것이 좋습니다.

### <a name="store-retail-and-e-commerce-data"></a>소매 및 전자 상거래 데이터 저장

유연성을 위해 정규화되지 않은 모델에서 다양한 범위의 변수 특성을 사용하여 제품에 대한 정보를 저장합니다.

### <a name="process-log-and-telemetry-data"></a>로그 및 원격 분석 데이터 처리

Transact-SQL 언어의 모든 기능을 사용하여 JSON 파일로 저장된 로그 데이터를 로드, 쿼리 및 분석합니다.

### <a name="store-semi-structured-iot-data"></a>반구조화된 IoT 데이터 저장

IoT 데이터의 실시간 분석이 필요할 때 들어오는 데이터를 스토리지 위치에 준비하는 대신 데이터베이스에 직접 로드합니다.

### <a name="simplify-rest-api-development"></a>REST API 개발 간소화

데이터베이스의 관계형 데이터를 웹 사이트 지원 REST API에서 사용하는 JSON 형식으로 쉽게 변환합니다.

## <a name="combine-relational-and-json-data"></a>관계형 및 JSON 데이터 결합

SQL Server는 표준 Transact-SQL 언어를 사용하여 관계형 및 JSON 데이터를 저장하고 처리할 수 있는 하이브리드 모델을 제공합니다. JSON 문서 컬렉션을 테이블 단위로 구성하고, 둘 간의 관계를 설정하고, 테이블에 저장된 강력한 형식의 스칼라 열을 JSON 열에 저장된 유연한 키/값 쌍과 결합하고, 전체 Transact-SQL을 사용하여 하나 이상의 테이블에서 스칼라 값과 JSON 값을 모두 쿼리할 수 있습니다.

JSON 텍스트는 `VARCHAR` 또는 `NVARCHAR` 열에 저장되며 일반 텍스트 형식으로 인덱싱됩니다. 텍스트를 지원하는 모든 SQL Server 기능 또는 구성 요소는 JSON을 지원하므로 JSON 및 기타 SQL Server 기능 간의 상호 작용에 제한이 거의 없습니다. JSON을 메모리 내 또는 임시 테이블에 저장할 수 있으며 행 수준 보안 조건자를 JSON 텍스트 등에 적용할 수 있습니다.

JSON 문서를 처리하기 위해 사용자 지정된 쿼리 언어를 사용하려는 순수 JSON 워크로드가 있는 경우 Microsoft Azure [Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)를 사용하는 것이 좋습니다.  
  
다음은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 기본 제공 JSON 지원을 사용하는 방법을 보여 주는 몇 가지 사용 사례입니다.  

## <a name="store-and-index-json-data-in-sql-server"></a>SQL Server에서 JSON 데이터 저장 및 인덱싱

JSON은 텍스트 형식이므로 JSON 문서는 SQL Database의 `NVARCHAR` 열에 저장될 수 있습니다. 모든 SQL Server 하위 시스템에서 `NVARCHAR` 형식이 지원되므로 OPENROWSET 또는 PolyBase를 사용하여 읽을 수 있는 **CLUSTERED COLUMNSTORE** 인덱스가 있는 테이블, **메모리 최적화** 테이블 또는 외부 파일이 있는 테이블에 JSON 문서를 넣을 수 있습니다.

SQL Server에서 JSON 데이터를 저장, 인덱싱 및 최적화하는 옵션에 대해 자세히 알아보려면 다음 문서를 참조하세요.

- [SQL Server 또는 SQL Database에 JSON 문서 저장](store-json-documents-in-sql-tables.md)
- [JSON 데이터 인덱싱](index-json-data.md)
- [메모리 내 OLTP를 통해 JSON 처리 최적화](optimize-json-processing-with-in-memory-oltp.md)

### <a name="load-json-files-into-sql-server"></a>SQL Server로 JSON 파일 로드  

표준 JSON 또는 행으로 구분된 JSON으로 파일에 저장된 정보의 형식을 지정할 수 있습니다. SQL Server는 JSON 파일의 콘텐츠를 가져와 **OPENJSON** 또는 **JSON_VALUE** 함수를 사용하여 구문 분석하고 테이블에 로드할 수 있습니다.  
  
-   JSON 문서가 로컬 파일, 공유 네트워크 드라이브 또는 SQL Server에서 액세스할 수 있는 Azure Files 위치에 저장된 경우 대량 가져오기를 사용하여 JSON 데이터를 SQL Server로 로드할 수 있습니다.
  
-   행으로 구분된 JSON 파일이 Azure Blob Storage 또는 Hadoop 파일 시스템에 저장된 경우 PolyBase를 사용하여 JSON 텍스트를 로드하고 Transact-SQL 코드에서 구문 분석한 후 테이블에 로드할 수 있습니다.  

### <a name="import-json-data-into-sql-server-tables"></a>SQL Server 테이블로 JSON 데이터 가져오기

외부 서비스에서 SQL Server로 JSON 데이터를 로드해야 하는 경우 애플리케이션 계층에서 데이터를 구문 분석하는 대신 **OPENJSON** 을 사용하여 데이터를 SQL Server로 가져올 수 있습니다.  
  
```sql  
DECLARE @jsonVariable NVARCHAR(MAX);

SET @jsonVariable = N'[
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
]';

-- INSERT INTO <sampleTable>  
SELECT SalesOrderJsonData.*
FROM OPENJSON (@jsonVariable, N'$')
  WITH (
    Number VARCHAR(200) N'$.Order.Number',
    Date DATETIME N'$.Order.Date',
    Customer VARCHAR(200) N'$.AccountNumber',
    Quantity INT N'$.Item.Quantity'
  ) AS SalesOrderJsonData;
```

JSON 변수의 콘텐츠를 외부 REST 서비스에서 제공하거나, 클라이언트 쪽 JavaScript 프레임워크에서 매개 변수로 전송하거나, 외부 파일에서 로드할 수 있습니다. JSON 텍스트의 결과를 SQL Server 테이블에 손쉽게 삽입, 업데이트 또는 병합할 수 있습니다.

## <a name="analyze-json-data-with-sql-queries"></a>SQL 쿼리를 사용하여 JSON 데이터 분석

보고를 위해 JSON 데이터를 필터링하거나 집계해야 하는 경우 **OPENJSON** 을 사용하여 JSON을 관계형 형식으로 변환할 수 있습니다. 그런 다음, 표준 [!INCLUDE[tsql](../../includes/tsql-md.md)] 및 기본 제공 함수를 사용하여 보고서를 작성할 수 있습니다.  
  
```sql
SELECT Tab.Id, SalesOrderJsonData.Customer, SalesOrderJsonData.Date
FROM SalesOrderRecord AS Tab
CROSS APPLY OPENJSON (Tab.json, N'$.Orders.OrdersArray')
  WITH (
    Number VARCHAR(200) N'$.Order.Number',
    Date DATETIME N'$.Order.Date',
    Customer VARCHAR(200) N'$.AccountNumber',
    Quantity INT N'$.Item.Quantity'
  ) AS SalesOrderJsonData
WHERE JSON_VALUE(Tab.json, '$.Status') = N'Closed'
ORDER BY JSON_VALUE(Tab.json, '$.Group'), Tab.DateModified;
```  
  
같은 쿼리에서 표준 테이블 열과 JSON 텍스트의 값을 모두 사용할 수 있습니다. `JSON_VALUE(Tab.json, '$.Status')` 식에서 인덱스를 추가하여 쿼리 성능을 개선할 수 있습니다. 자세한 내용은 [JSON 데이터 인덱싱](../../relational-databases/json/index-json-data.md)를 참조하세요.

## <a name="return-data-from-a-sql-server-table-formatted-as-json"></a>SQL Server 테이블에서 JSON으로 서식이 지정된 데이터 반환

데이터베이스 계층에서 데이터를 가져와서 JSON 형식으로 반환하는 웹 서비스가 있거나 JSON 형식의 데이터를 허용하는 JavaScript 프레임워크 또는 라이브러리가 있는 경우 SQL 쿼리에서 직접 JSON 출력의 형식을 지정할 수 있습니다. 테이블 형식 쿼리 결과와 직렬화 개체를 차례로 JSON 형식으로 변환하기 위해 코드를 작성하거나 라이브러리를 포함하는 대신, **FOR JSON** 을 사용하여 JSON 형식 지정을 SQL Server에 위임할 수 있습니다.  
  
예를 들어 OData 사양을 준수하는 JSON 출력을 생성할 수 있습니다. 웹 서비스에는 다음과 같은 형식의 요청 및 응답이 필요합니다. 
  
- 요청: `/Northwind/Northwind.svc/Products(1)?$select=ProductID,ProductName`  

- 응답: `{"@odata.context": "https://services.odata.org/V4/Northwind/Northwind.svc/$metadata#Products(ProductID,ProductName)/$entity", "ProductID": 1, "ProductName": "Chai"}`  
  
다음 OData URL은 ProductID 및 ProductName 열에서 `ID`가 1인 제품에 대한 요청을 나타냅니다. **FOR JSON** 을 사용하여 SQL Server에 필요한 형식으로 출력 형식을 지정할 수 있습니다.  
  
```sql  
SELECT 'https://services.odata.org/V4/Northwind/Northwind.svc/$metadata#Products(ProductID,ProductName)/$entity' AS '@odata.context',
  ProductID,
  Name as ProductName
FROM Production.Product
WHERE ProductID = 1
FOR JSON AUTO;
```  
  
이 쿼리의 출력은 OData 사양을 완벽하게 준수하는 JSON 텍스트입니다. 형식 지정 및 이스케이프는 SQL Server에서 처리됩니다. SQL Server는 OData JSON 또는 GeoJSON과 같은 형식으로 쿼리 결과의 형식을 지정할 수 있습니다.  
  
## <a name="test-drive-built-in-json-support-with-the-adventureworks-sample-database"></a>AdventureWorks 예제 데이터베이스를 사용하여 드라이브 기본 제공 JSON 지원 시험 사용

AdventureWorks 샘플 데이터베이스를 가져오려면 [GitHub](https://github.com/microsoft/sql-server-samples/releases/tag/adventureworks)에서 적어도 데이터베이스 파일과 샘플 및 스크립트 파일을 다운로드합니다.

샘플 데이터베이스를 SQL Server 2016 인스턴스로 복원한 후에 샘플 파일을 추출한 다음, JSON 폴더에서 *JSON 샘플 쿼리 프로시저 뷰 및 indexes.sql* 파일을 엽니다. 이 파일의 스크립트를 실행하여 일부 기존 데이터의 서식을 JSON 데이터로 다시 지정하고, JSON 데이터에 대한 샘플 쿼리 및 보고서를 테스트하고, JSON 데이터를 인덱싱하고, JSON을 가져오고 내보냅니다.  
  
파일에 포함된 스크립트를 통해 수행할 수 있는 작업은 다음과 같습니다.  
  
- 기존 스키마를 비정규화하여 JSON 데이터의 열을 만듭니다.

  - SalesReasons, SalesOrderDetails, SalesPerson, Customer 및 기타 판매 주문 관련 정보가 JSON 열에 포함된 테이블의 정보를 SalesOrder_json 테이블에 저장합니다.  
  
  - EmailAddresses/PersonPhone 테이블의 정보를 JSON 개체 배열로 Person_json 테이블에 저장합니다.  
  
- JSON 데이터를 쿼리하는 프로시저 및 뷰를 만듭니다.  
  
- JSON 데이터 인덱싱 JSON 속성의 인덱스 및 전체 텍스트 인덱스를 만듭니다.  
  
- JSON 가져오기 및 내보내기 Person 및 SalesOrder 테이블의 콘텐츠를 JSON 결과로 내보내고, JSON 입력을 사용하여 Person 및 SalesOrder 테이블을 가져오고 업데이트하는 프로시저를 만들고 실행합니다.  
  
- 쿼리 예제 실행 2단계와 4단계에서 만든 저장 프로시저 및 뷰를 호출하는 몇 가지 쿼리를 실행합니다.  
  
- 스크립트 정리 2단계와 4단계에서 만든 저장 프로시저 및 뷰를 유지하려면 이 부분을 실행하지 마세요.  
  
## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>SQL Server 및 Azure SQL Database에서 JSON에 대한 자세한 정보  
  
### <a name="microsoft-videos"></a>Microsoft 비디오

SQL Server 및 Azure SQL Database에서 기본 제공 JSON 지원에 대한 시각적 소개는 다음 비디오를 참조하세요.

*SQL Server 2016 및 Azure SQL Database에서 JSON 사용*
> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database/player?WT.mc_id=dataexposed-c9-niner]

*JSON 함수를 사용하여 SQL Server로 REST API 빌드하기*
> [!VIDEO https://www.youtube.com/embed/0m6GXF3-5WI]

### <a name="reference-articles"></a>참조 문서

- [FOR 절(Transact-SQL)](../../t-sql/queries/select-for-clause-transact-sql.md)(FOR JSON)  
- [OPENJSON(Transact-SQL)](../../t-sql/functions/openjson-transact-sql.md)  
- [JSON 함수(Transact-SQL)](../../t-sql/functions/json-functions-transact-sql.md)  
  - [ISJSON(Transact-SQL)](../../t-sql/functions/isjson-transact-sql.md)  
  - [JSON_VALUE(Transact-SQL)](../../t-sql/functions/json-value-transact-sql.md)  
  - [JSON_QUERY(Transact-SQL)](../../t-sql/functions/json-query-transact-sql.md)  
  - [JSON_MODIFY(Transact-SQL)](../../t-sql/functions/json-modify-transact-sql.md)  
