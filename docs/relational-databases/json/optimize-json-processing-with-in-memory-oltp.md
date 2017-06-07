---
title: "메모리 내 OLTP를 통해 JSON 처리 최적화 | Microsoft 문서"
ms.custom: 
ms.date: 02/03/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d9c5adb1-3209-4186-bc10-8e41a26f5e57
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4e0331c288665fd9f69444d0d14366dfa69a668f
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="optimize-json-processing-with-in-memory-oltp"></a>메모리 내 OLTP를 통해 JSON 처리 최적화
[!INCLUDE[tsql-appliesto-ssvNxt-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-asdb-xxxx-xxx.md)]

SQL Server 및 Azure SQL Database를 통해 JSON으로 서식이 지정된 텍스트로 작업할 수 있습니다. JSON 데이터를 처리하는 OLTP 쿼리의 성능을 향상하기 위해 표준 문자열 열(NVARCHAR 형식)을 사용하여 메모리 액세스에 최적화된 테이블에 JSON 문서를 저장할 수 있습니다.

## <a name="store-json-in-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블에 JSON 저장
다음 예제에서는 `Tags`와 `Data`라는 두 개의 JSON 열이 있는 메모리 액세스에 최적화된 `Product` 테이블을 보여 줍니다.

```sql
CREATE SCHEMA xtp;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED, --standard column
    Name nvarchar(400) NOT NULL, --standard column
    Price float, --standard column

    Tags nvarchar(400),--json stored in string column
    Data nvarchar(4000) --json stored in string column

) WITH (MEMORY_OPTIMIZED=ON);
```
메모리 액세스에 최적화된 테이블에 JSON 데이터를 저장하면 잠금 해제된 메모리 내 데이터 액세스를 활용하여 쿼리 성능이 향상됩니다.

## <a name="optimize-json-with-additional-in-memory-features"></a>추가 메모리 내 기능을 통해 JSON 최적화
SQL Server 및 Azure SQL Database에서 사용할 수 있는 새로운 기능을 통해 기존의 메모리 내 OLTP 기술과 JSON 기능을 완벽하게 통합할 수 있습니다. 예를 들어 다음과 같은 작업을 수행할 수 있습니다.
 - 고유하게 컴파일된 CHECK 제약 조건을 사용하여 메모리 액세스에 최적화된 테이블에 저장된 JSON 문서 구조의 유효성을 검사합니다.
 - 계산 열을 사용하여 JSON 문서에 저장된 값을 노출하고 강력하게 형식화합니다.
 - 메모리 액세스에 최적화된 인덱스를 사용하여 JSON 문서의 값을 인덱싱합니다.
 - JSON 문서의 값을 사용하는 SQL 쿼리를 고유하게 컴파일하고 JSON 텍스트로 결과의 서식을 지정합니다.

## <a name="validate-json-columns"></a>JSON 열 유효성 검사
다음 예제와 같이 SQL Server 및 Azure SQL Database를 사용하면 문자열 열에 저장된 JSON 문서 내용의 유효성을 검사하는 고유하게 컴파일된 CHECK 제약 조건을 추가할 수 있습니다.

```sql
DROP TABLE IF EXISTS xtp.Product;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED,
    Name nvarchar(400) NOT NULL,
    Price float,

    Tags nvarchar(400)
            CONSTRAINT [Tags should be formatted as JSON]
                CHECK (ISJSON(Tags)=1),
    Data nvarchar(4000)

) WITH (MEMORY_OPTIMIZED=ON);
```

고유하게 컴파일된 CHECK 제약 조건은 JSON 열이 포함된 기존 테이블에 추가할 수 있습니다.

```sql
ALTER TABLE xtp.Product
    ADD CONSTRAINT [Data should be JSON]
        CHECK (ISJSON(Data)=1)
```

고유하게 컴파일된 JSON CHECK 제약 조건을 사용하여 메모리 액세스에 최적화된 테이블에 저장된 JSON 텍스트의 서식이 올바르게 지정되었는지 확인할 수 있습니다.

## <a name="expose-json-values-using-computed-columns"></a>계산 열을 사용하여 JSON 값 노출
계산 열을 사용하면 JSON 텍스트에서 값을 노출할 수 있으며 JSON 텍스트에서 값을 가져오는 식을 다시 계산하지 않고 JSON 구조를 다시 구문 분석하지 않고도 해당 값에 액세스할 수 있습니다. 노출된 값은 강력한 형식이며 실제로 계산 열에 유지됩니다. 지속형 계산 열을 사용하여 JSON 값에 액세스하면 JSON 문서의 값에 액세스하는 것보다 더 빠릅니다.

다음 예제에서는 JSON `Data` 열에서 다음과 같은 두 값을 노출하는 방법을 보여 줍니다.
-   제품이 만들어진 국가.
-   제품 제조 비용.

```sql
DROP TABLE IF EXISTS xtp.Product;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED,
    Name nvarchar(400) NOT NULL,
    Price float,

    Data nvarchar(4000),

    MadeIn AS CAST(JSON_VALUE(Data, '$.MadeIn') as NVARCHAR(50)) PERSISTED,
    Cost   AS CAST(JSON_VALUE(Data, '$.ManufacturingCost') as float)

) WITH (MEMORY_OPTIMIZED=ON);
```

계산 열 `MadeIn` 및 `Cost`는 `Data` 열에 저장된 JSON 문서가 변경될 때마다 업데이트됩니다.

## <a name="index-values-in-json-columns"></a>JSON 열의 값 인덱싱
SQL Server 및 AAzure SQL Database를 통해 메모리 액세스에 최적화된 인덱스를 사용하여 JSON 열의 값을 인덱싱할 수 있습니다. 다음 예제와 같이 인덱싱되는 JSON 값은 계산 열을 사용하여 노출되고 강력하게 형식화되어야 합니다.

```sql
DROP TABLE IF EXISTS xtp.Product;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED,
    Name nvarchar(400) NOT NULL,
    Price float,

    Data nvarchar(4000),

    MadeIn AS CAST(JSON_VALUE(Data, '$.MadeIn') as NVARCHAR(50)) PERSISTED,
    Cost   AS CAST(JSON_VALUE(Data, '$.ManufacturingCost') as float) PERSISTED,

    INDEX [idx_Product_MadeIn] NONCLUSTERED (MadeIn)

) WITH (MEMORY_OPTIMIZED=ON)

ALTER TABLE Product
    ADD INDEX [idx_Product_Cost] NONCLUSTERED HASH(Cost)
        WITH (BUCKET_COUNT=20000)
```
JSON 열의 값은 표준 NONCLUSTERED 및 HASH 인덱스를 사용하여 인덱싱할 수 있습니다.
-   NONCLUSTERED 인덱스는 일부 JSON 값에 따라 행 범위를 선택하고 JSON 값에 따라 결과를 정렬하는 쿼리를 최적화합니다.
-   HASH 인덱스는 찾으려는 정확한 값을 지정하여 단일 행이나 몇 개의 행을 가져올 때 최적의 성능을 제공합니다.

## <a name="native-compilation-of-json-queries"></a>JSON 쿼리의 네이티브 컴파일
마지막으로 JSON 함수와 함께 쿼리를 포함하는 Transact-SQL 프로시저, 함수 및 트리거의 네이티브 컴파일은 쿼리의 성능을 향상시키고 프로시저를 실행하는 데 필요한 CPU 주기를 줄입니다. 다음 예제에서는 JSON_VALUE, OPENJSON 및 JSON_MODIFY라는 여러 가지 JSON 함수를 사용하는 고유하게 컴파일된 프로시저를 보여 줍니다.

```sql
CREATE PROCEDURE xtp.ProductList(@ProductIds nvarchar(100))
WITH SCHEMABINDING, NATIVE_COMPILATION
AS BEGIN
    ATOMIC WITH (transaction isolation level = snapshot,  language = N'English')

    SELECT ProductID,Name,Price,Data,Tags, JSON_VALUE(data,'$.MadeIn') AS MadeIn
    FROM xtp.Product
        JOIN OPENJSON(@ProductIds)
            ON ProductID = value

END;

CREATE PROCEDURE xtp.UpdateProductData(@ProductId int, @Property nvarchar(100), @Value nvarchar(100))
WITH SCHEMABINDING, NATIVE_COMPILATION
AS BEGIN
    ATOMIC WITH (transaction isolation level = snapshot,  language = N'English')

    UPDATE xtp.Product
    SET Data = JSON_MODIFY(Data, @Property, @Value)
    WHERE ProductID = @ProductId;

END
```

## <a name="next-steps"></a>다음 단계
메모리 내 OLTP 네이티브 모듈의 JSON은 SQL Server 및 Azure SQL Database에서 사용할 수 있는 기본 제공 JSON 기능의 성능을 향상시킵니다.

JSON 사용에 대한 핵심 시나리오에 대해 자세히 알아보려면 다음 리소스 중 일부를 확인하세요.

-   [TechNet 블로그](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
-   [MSDN 설명서](https://msdn.microsoft.com/library/dn921897.aspx)
-   [Channel 9 비디오](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

응용 프로그램과 JSON 통합에 대한 다양한 시나리오에 대해 알아보려면 다음 리소스를 확인하세요.
-   이 [Channel 9 비디오](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)의 데모를 참조하세요.
-   [JSON 블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)의 사용 사례와 일치하는 시나리오를 찾아보세요.
-   [GitHub 리포지토리](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/json/)에서 예제를 찾아보세요.


