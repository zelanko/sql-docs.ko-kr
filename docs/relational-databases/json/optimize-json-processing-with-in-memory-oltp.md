---
title: "메모리 내 OLTP를 통해 JSON 처리 최적화 | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
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
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: bb35a5255b35b93cd42e83bd17d9efdcf751bc84
ms.contentlocale: ko-kr
ms.lasthandoff: 07/31/2017

---
# <a name="optimize-json-processing-with-in-memory-oltp"></a>메모리 내 OLTP를 통해 JSON 처리 최적화
[!INCLUDE[tsql-appliesto-ssvNxt-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-asdb-xxxx-xxx.md)]

SQL Server 및 Azure SQL Database를 통해 JSON으로 서식이 지정된 텍스트로 작업할 수 있습니다. JSON 데이터를 처리하는 쿼리의 성능을 향상하려면 표준 문자열 열(NVARCHAR 형식)을 사용하여 메모리 최적화 테이블에 JSON 문서를 저장할 수 있습니다. 메모리 최적화 테이블에 JSON 데이터를 저장하면 잠금 해제된 메모리 내 데이터 액세스를 활용하여 쿼리 성능이 향상됩니다.

## <a name="store-json-in-memory-optimized-tables"></a>메모리 최적화 테이블에 JSON 저장
다음 예제에서는 `Tags`와 `Data`라는 두 개의 JSON 열이 있는 메모리 최적화 `Product` 테이블을 보여 줍니다.

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

## <a name="optimize-json-processing-with-additional-in-memory-features"></a>추가 메모리 내 기능을 통해 JSON 처리 최적화
SQL Server 및 Azure SQL Database에서 사용할 수 있는 기능을 통해 기존의 메모리 내 OLTP 기술과 JSON 기능을 완벽하게 통합할 수 있습니다. 예를 들어 다음과 같은 작업을 수행할 수 있습니다.
 - 고유하게 컴파일된 CHECK 제약 조건을 사용하여 메모리 최적화 테이블에 저장된 [JSON 문서 구조의 유효성을 검사](#validate)합니다.
 - 계산 열을 사용하여 JSON 문서에 저장된 [값을 노출하고 강력하게 형식화](#computedcol)합니다.
 - 메모리 최적화 인덱스를 사용하여 JSON 문서의 [값을 인덱싱](#index)합니다.
 - JSON 문서의 값을 사용하거나 JSON 텍스트로 결과의 서식을 지정하는 [SQL 쿼리를 고유하게 컴파일](#compile)합니다.

## <a name="validate"></a> JSON 열의 유효성 검사
SQL Server 및 Azure SQL Database를 사용하면 문자열 열에 저장된 JSON 문서 내용의 유효성을 검사하는 고유하게 컴파일된 CHECK 제약 조건을 추가할 수 있습니다. 고유하게 컴파일된 JSON CHECK 제약 조건을 사용하여 메모리 최적화 테이블에 저장된 JSON 텍스트의 서식이 올바르게 지정되었는지 확인할 수 있습니다.

다음 예제에서는 JSON 열 `Tags`가 있는 `Product` 테이블을 만듭니다. `Tags` 열에는 `ISJSON` 함수를 사용하여 열에 있는 JSON 텍스트의 유효성을 검사하는 CHECK 제약 조건이 있습니다.

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

JSON 열이 포함된 기존 테이블에 고유하게 컴파일된 CHECK 제약 조건을 추가할 수도 있습니다.

```sql
ALTER TABLE xtp.Product
    ADD CONSTRAINT [Data should be JSON]
        CHECK (ISJSON(Data)=1)
```

## <a name="computedcol"></a> 계산 열을 사용하여 JSON 값 노출
계산 열을 사용하면 JSON 텍스트에서 값을 노출할 수 있으며 JSON 텍스트에서 값을 가져오거나 JSON 구조를 다시 구문 분석하지 않고도 해당 값에 액세스할 수 있습니다. 이 방식으로 노출된 값은 강력한 형식이며 실제로 계산 열에 유지됩니다. 지속형 계산 열을 사용하여 JSON 값에 액세스하면 JSON 문서의 값에 직접 액세스하는 것보다 더 빠릅니다.

다음 예제에서는 JSON `Data` 열에서 다음과 같은 두 값을 노출하는 방법을 보여 줍니다.
-   제품이 만들어진 국가.
-   제품 제조 비용.

이 예에서 계산 열 `MadeIn` 및 `Cost`는 `Data` 열에 저장된 JSON 문서가 변경될 때마다 업데이트됩니다.

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

## <a name="index"></a> JSON 열의 값 인덱싱
SQL Server 및 Azure SQL Database를 사용하면 메모리 최적화 인덱스를 사용하여 JSON 열의 값을 인덱싱할 수 있습니다. 이전 예제에서 설명한 대로 인덱싱되는 JSON 값은 계산 열을 사용하여 노출되고 강력하게 형식화되어야 합니다.

JSON 열의 값은 표준 NONCLUSTERED 및 HASH 인덱스를 사용하여 인덱싱할 수 있습니다.
-   NONCLUSTERED 인덱스는 일부 JSON 값에 따라 행 범위를 선택하고 JSON 값에 따라 결과를 정렬하는 쿼리를 최적화합니다.
-   HASH 인덱스는 찾을 값을 정확히 지정하여 단일 행 또는 몇 개 행을 선택하는 쿼리를 최적화합니다.

다음 예제에서는 두 개의 계산 열을 사용하여 JSON 값을 노출하는 테이블을 만듭니다. 이 예제에서는 하나의 JSON 값에는 NONCLUSTERED 인덱스, 다른 값에는 HASH 인덱스를 만듭니다.

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

## <a name="compile"></a> JSON 쿼리의 네이티브 컴파일
프로시저, 함수 및 트리거에 기본 제공 JSON 함수를 사용하는 쿼리가 포함되어 있는 경우 네이티브 컴파일은 이러한 쿼리의 성능을 향상하고 쿼리를 실행하는 데 필요한 CPU 주기를 줄입니다.

다음 예제에서는 **JSON_VALUE**, **OPENJSON** 및 **JSON_MODIFY**라는 여러 가지 JSON 함수를 사용하는 고유하게 컴파일된 프로시저를 보여 줍니다.

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

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>SQL Server의 기본 제공 JSON 지원에 대한 자세한 정보  
많은 특정 솔루션, 사용 사례 및 권장 사항은 Microsoft 프로그램 관리자인 Jovan Popovic이 제공하는 SQL Server 및 Azure SQL Database의 [기본 제공 JSON 지원에 대한 블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)을 참조하세요.

