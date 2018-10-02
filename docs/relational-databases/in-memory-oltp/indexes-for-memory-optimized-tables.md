---
title: 메모리 액세스에 최적화된 테이블의 인덱스 | Microsoft 문서
ms.custom: ''
ms.date: 11/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: eecc5821-152b-4ed5-888f-7c0e6beffed9
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 394330d19904e61eb4a339468cd882f09240ff65
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47748931"
---
# <a name="indexes-on-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블의 인덱스
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

행을 함께 연결하는 인덱스이므로 모든 메모리 최적화 테이블에는 하나 이상의 인덱스가 있어야 합니다. 메모리 최적화 테이블에서는 모든 인덱스 또한 메모리 최적화되어 있습니다. 메모리 최적화 테이블의 인덱스와 디스크 기반 테이블의 인덱스는 여러 방식에서 다릅니다.  

- 데이터 행은 페이지에 저장되지 않으므로 테이블의 모든 페이지를 가져오기 위해 참조할 수 있는 페이지 또는 익스텐트의 모음과 파티션 또는 할당 단위가 없습니다. 사용 가능한 인덱스 형식 중 하나에 대한 인덱스 페이지 개념이 있지만 디스크 기반 테이블의 인덱스와 다르게 저장됩니다. fillfactor가 없으므로 페이지 내에서 기존 유형의 조각화가 발생하지 않습니다.
- 데이터 조작 중에 메모리 최적화 테이블의 인덱스에 대한 변경 내용은 디스크에 기록되지 않습니다. 데이터 행 및 데이터 변경 내용만 트랜잭션 로그에 기록됩니다. 
- 데이터베이스가 다시 온라인이 될 때 메모리 액세스에 최적화된 인덱스가 다시 빌드됩니다. 

메모리 최적화 테이블의 모든 인덱스는 데이터베이스 복구 중에 인덱스 정의를 기반으로 만들어집니다.

인덱스는 다음 중 하나여야 합니다.  
  
- 해시 인덱스  
- 메모리 최적화 비클러스터형 인덱스(B-트리의 기본 내부 구조를 의미) 
  
*해시* 인덱스는 [메모리 최적화 테이블의 해시 인덱스](../../relational-databases/sql-server-index-design-guide.md#hash_index)에서 자세히 설명합니다.
*비클러스터형* 인덱스는 [메모리 최적화 테이블의 비클러스터형 인덱스](../../relational-databases/sql-server-index-design-guide.md#inmem_nonclustered_index)에서 자세히 설명합니다.  
*Columnstore* 인덱스에 대해서는 [다른 문서](../../relational-databases/indexes/columnstore-indexes-overview.md)에서 설명합니다.  

## <a name="syntax-for-memory-optimized-indexes"></a>메모리 최적화 인덱스 구문  
  
메모리 최적화 테이블에 대한 각 CREATE TABLE 문은 인덱스를 통해 명시적으로 또는 PRIMAY KEY 또는 UNIQUE 제약 조건을 통해 암시적으로 인덱스를 포함해야 합니다.
  
기본 DURABILITY = SCHEMA\_AND_DATA를 사용하여 선언하려면 메모리 최적화 테이블에 기본 키가 있어야 합니다. 다음 CREATE TABLE 문의 PRIMARY KEY NONCLUSTERED 절은 두 가지 요구 사항을 충족합니다.  
  
- CREATE TABLE 문에서 하나의 인덱스의 최소 요구 사항을 충족할 인덱스를 제공합니다.  
- SCHEMA\_AND_DATA 절에 필요한 기본 키를 제공합니다.  

    ```sql
    CREATE TABLE SupportEvent  
    (  
        SupportEventId   int NOT NULL  
            PRIMARY KEY NONCLUSTERED,  
        ...  
    )  
        WITH (  
            MEMORY_OPTIMIZED = ON,  
            DURABILITY = SCHEMA\_AND_DATA);  
    ```
> [!NOTE]  
> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 및 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에는 메모리 최적화 테이블 또는 테이블 형식당 8개의 인덱스 제한이 있습니다. [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 이상 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서는 메모리 최적화 테이블 및 테이블 형식에 해당하는 인덱스 수 제한이 없어집니다.
  
### <a name="code-sample-for-syntax"></a>구문에 대한 코드 샘플  
  
이 하위 섹션에는 메모리 최적화 테이블에 다양한 인덱스를 만드는 구문을 보여 주는 하는 TRANSACT-SQL 코드 블록이 포함되어 있습니다. 코드에서는 다음을 보여 줍니다.  
  
1. 메모리 최적화 테이블을 만듭니다.  
2. ALTER TABLE 문을 사용하여 두 인덱스를 추가합니다.  
3. 데이터 행을 몇 개 삽입합니다.  
   
    ```sql
    DROP TABLE IF EXISTS SupportEvent;  
    go  

    CREATE TABLE SupportEvent  
    (  
        SupportEventId   int               not null   identity(1,1)  
        PRIMARY KEY NONCLUSTERED,  

        StartDateTime        datetime2     not null,  
        CustomerName         nvarchar(16)  not null,  
        SupportEngineerName  nvarchar(16)      null,  
        Priority             int               null,  
        Description          nvarchar(64)      null  
    )  
        WITH (  
        MEMORY_OPTIMIZED = ON,  
        DURABILITY = SCHEMA\_AND_DATA);  
    go  
        
        --------------------  
        
    ALTER TABLE SupportEvent  
        ADD CONSTRAINT constraintUnique_SDT_CN  
        UNIQUE NONCLUSTERED (StartDateTime DESC, CustomerName);  
    go  

    ALTER TABLE SupportEvent  
        ADD INDEX idx_hash_SupportEngineerName  
        HASH (SupportEngineerName) WITH (BUCKET_COUNT = 64);  -- Nonunique.  
    go  
        
        --------------------  
        
    INSERT INTO SupportEvent  
        (StartDateTime, CustomerName, SupportEngineerName, Priority, Description)  
        VALUES  
        ('2016-02-23 13:40:41:123', 'Abby', 'Zeke', 2, 'Display problem.'     ),  
        ('2016-02-24 13:40:41:323', 'Ben' , null  , 1, 'Cannot find help.'    ),  
        ('2016-02-25 13:40:41:523', 'Carl', 'Liz' , 2, 'Button is gray.'      ),  
        ('2016-02-26 13:40:41:723', 'Dave', 'Zeke', 2, 'Cannot unhide column.');  
    go 
    ``` 
  
## <a name="duplicate-index-key-values"></a>중복된 인덱스 키 값

중복된 인덱스 키 값은 메모리 최적화 테이블에 대한 작업의 성능에 영향을 줄 수 있습니다. 대부분의 인덱스 작업에서 중복 체인을 순회해야 하므로 중복이 많으면(예: 100 이상) 인덱스 유지 관리 작업이 비효율적입니다. 메모리 최적화 테이블에서 `INSERT`, `UPDATE` 및 `DELETE` 작업에 영향을 줄 수 있습니다. 

이 문제는 해시 인덱스의 경우 더 자주 발생합니다. 해시 인덱스에 대한 작업당 소요되는 더 적은 비용과 해시 충돌 체인이 있는 큰 중복 체인의 간섭 모두가 원인입니다. 인덱스에서 중복을 줄이려면 비클러스터형 인덱스를 사용하고 중복 수를 줄이기 위해 인덱스 키의 끝에 별도 열을 추가합니다(예: 기본 키에서 추가). 해시 충돌에 대한 자세한 내용은 [메모리 최적화 테이블의 해시 인덱스](../../relational-databases/sql-server-index-design-guide.md#hash_index)를 참조하세요.

예를 들어, `CustomerId`의 기본 키가 있는 `Customers` 테이블과 열 `CustomerCategoryID`의 인덱스를 고려합니다. 일반적으로 특정 범주에 많은 고객이 있으므로 지정된 키에 대한 중복 값이 CustomerCategoryID의 인덱스에 많습니다. 이 시나리오에서는 `(CustomerCategoryID, CustomerId)`에 대한 비클러스터형 인덱스를 사용하는 것이 모범 사례입니다. 이 인덱스는 `CustomerCategoryID`를 포함하는 조건자를 사용하는 쿼리에 사용할 수 있고 중복을 포함하지 않으므로 인덱스 유지 관리의 비효율성을 야기하지 않습니다.

다음 쿼리는 샘플 데이터베이스 `CustomerCategoryID` WideWorldImporters `Sales.Customers`의 테이블 [에 있는](../../sample/world-wide-importers/wide-world-importers-documentation.md)에 대한 인덱스와 관련해 중복 인덱스 키 값의 평균 개수를 보여 줍니다.

```sql
SELECT AVG(row_count) FROM
    (SELECT COUNT(*) AS row_count 
        FROM Sales.Customers
        GROUP BY CustomerCategoryID) a
```

고유 테이블 및 인덱스와 관련해 인덱스 키 중복 항목의 평균 개수를 구하려면 `Sales.Customers` 를 테이블 이름으로 바꾸고 `CustomerCategoryID` 를 인덱스 키 열 목록으로 바꿉니다.

## <a name="comparing-when-to-use-each-index-type"></a>각 인덱스 유형을 사용하는 경우 비교  
  
특정 쿼리의 특성에서 인덱스 유형이 적합한 선택인지 결정됩니다.  

해당 기능은 디스크 기반 테이블에서 기존 클러스터형 및 비클러스터형 인덱스의 기능과 유사하므로 기존 응용 프로그램에서 메모리 최적화 테이블을 구현할 때 일반적으로 비클러스트형 인덱스로 시작하는 것이 좋습니다. 
  
### <a name="recommendations-for-nonclustered-index-use"></a>비클러스터형 인덱스 사용에 대한 권장 사항  
  
비클러스터형 인덱스는 다음의 경우 해시 인덱스 전체에서 선호됩니다.  
  
- 쿼리 시 인덱싱된 열에 `ORDER BY` 절이 포함됨  
- 다중 열 인덱스의 선행 열만 테스트하는 위치 쿼리  
- 쿼리에서 `WHERE` 절을 다음과 같이 사용하여 인덱싱된 열 테스트:  
  - 같지 않음: `WHERE StatusCode != 'Done'`  
  - 값 범위 검색: `WHERE Quantity >= 100`  
  
다음 모든 SELECT 문에서는 비클러스터형 인덱스가 해시 인덱스 전체에서 선호됩니다.  

```sql
SELECT CustomerName, Priority, Description 
FROM SupportEvent  
WHERE StartDateTime > DateAdd(day, -7, GetUtcDate());  
    
SELECT CustomerName, Priority, Description 
FROM SupportEvent  
WHERE CustomerName != 'Ben';  
    
SELECT StartDateTime, CustomerName  
FROM SupportEvent  
ORDER BY StartDateTime;  
    
SELECT CustomerName  
FROM SupportEvent  
WHERE StartDateTime = '2016-02-26';  
```
  
### <a name="recommendations-for-hash-index-use"></a>해시 인덱스 사용에 대한 권장 사항   
  
[해시 인덱스](../../relational-databases/sql-server-index-design-guide.md#hash_index)는 주로 포인트 조회에 사용되고 범위 검색에는 사용되지 않습니다.

해시 인덱스는 쿼리에서 같음 조건자를 사용할 경우 비클러스터형 인덱스보다 선호되고 `WHERE` 절은 다음 예제와 같이 모든 인덱스 키 열에 매핑됩니다.  
  
```sql
SELECT CustomerName 
FROM SupportEvent  
WHERE SupportEngineerName = 'Liz';
```  

### <a name="multi-column-index"></a>여러 열 인덱스  
  
여러 열 인덱스는 비클러스터형 인덱스 또는 해시 인덱스일 수 있습니다. 인덱스 열이 col1 및 col2라고 가정해 보겠습니다. 다음 `SELECT` 문이 주어진 경우 비클러스터형 인덱스만 쿼리 최적화 프로그램에 유용합니다.  
  
```sql
SELECT col1, col3  
FROM MyTable_memop  
WHERE col1 = 'dn';  
```

해시 인덱스는 `WHERE` 절이 있어야 해당 키의 각 열에 대해 같음 테스트를 지정할 수 있습니다. 그러지 않으면 해시 인덱스는 쿼리 최적화 프로그램에 유용하지 않습니다.  
  
`WHERE` 절이 인덱스 키의 두 번째 열만 지정하는 경우에는 두 인덱스 형식 모두 유용하지 않습니다.  

### <a name="summary-table-to-compare-index-use-scenarios"></a>인덱스 사용 시나리오를 비교하기 위한 요약 테이블  
  
다음 표에서 다른 인덱스 유형에서 지원 되는 모든 작업을 나열 합니다. *예*는 인덱스가 요청을 효율적으로 처리할 수 있음을 의미하며 *아니요*는 인덱스를 사용하여 요청을 효과적으로 충족할 수 없음을 의미합니다. 
  
| 연산 | 메모리 액세스에 최적화됨, <br/> 해시 | 메모리 액세스에 최적화됨, <br/> 비클러스터형 | 디스크 기반, <br/> (비)클러스터형 |  
| :-------- | :--------------------------- | :----------------------------------- | :------------------------------------ |  
| 색인 검색은 모든 테이블 행을 검색합니다. | 사용자 계정 컨트롤 | 예 | 사용자 계정 컨트롤 |  
| 같음 조건자(=)에서 인덱스 검색 | 사용자 계정 컨트롤 <br/> (전체 키는 필수) | 사용자 계정 컨트롤  | 사용자 계정 컨트롤 |  
| 같지 않음 및 범위 조건자에서 인덱스 검색 <br/> (>, <, <=, >=, `BETWEEN`). | 아니오 <br/> (인덱스 검색의 결과) | 예 <sup>1</sup> | 사용자 계정 컨트롤 |  
| 인덱스 정의와 일치하는 정렬 순서로 행을 검색합니다. | 아니오 | 예 | 사용자 계정 컨트롤 |  
| 인덱스 정의의 역순과 일치하는 정렬 순서로 행을 검색합니다. | 아니오 | 아니오 | 사용자 계정 컨트롤 |  

<sup>1</sup> 메모리 최적화 비클러스터형 인덱스의 경우 인덱스 검색을 수행하는 데 전체 키가 필요하지 않습니다.  

## <a name="automatic-index-and-statistics-management"></a>자동 인덱스 및 통계 관리

[Adaptive Index Defrag](http://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)와 같은 솔루션을 사용하여 하나 이상의 데이터베이스에 대한 인덱스 조각 모음 및 통계 업데이트를 자동으로 관리합니다. 이 절차는 다른 매개 변수 사이에서 조각화 수준에 따라 인덱스를 다시 작성하거나 다시 구성할지 여부를 자동으로 선택하고 통계를 선형 임계값으로 업데이트합니다.

## <a name="Additional_Reading"></a> 참고 항목   
 [SQL Server 인덱스 디자인 가이드](../../relational-databases/sql-server-index-design-guide.md)   
 [메모리 최적화 테이블의 해시 인덱스](../../relational-databases/sql-server-index-design-guide.md#hash_index)   
 [메모리 최적화 테이블의 비클러스터형 인덱스](../../relational-databases/sql-server-index-design-guide.md#inmem_nonclustered_index)    
 [Adaptive Index Defrag](http://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)  
