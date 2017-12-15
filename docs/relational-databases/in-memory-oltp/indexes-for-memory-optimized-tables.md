---
title: "메모리 액세스에 최적화된 테이블의 인덱스 | Microsoft 문서"
ms.custom: 
ms.date: 11/6/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.reviewer: 
ms.service: 
ms.component: in-memory-oltp
ms.suite: sql
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eecc5821-152b-4ed5-888f-7c0e6beffed9
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1679cf30077600cbff38aea1869bc7c8c9edc53e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="indexes-for-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블의 인덱스
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  
이 문서에서는 메모리 최적화 테이블에서 사용할 수 있는 인덱스 유형을 설명합니다. 이 문서에서는 다음 내용을 다룹니다.  
  
- TRANSACT-SQL 구문을 보여 주는 짧은 코드 예제를 제공합니다.  
- 메모리 최적화 인덱스가 기존의 디스크 기반 인덱스와 어떻게 다른지 설명합니다.  
- 메모리 최적화 인덱스 유형이 각각 최고인 상황에 대해 설명합니다.  
  
  
*해시* 인덱스는 [밀접하게 관련된 문서](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md)에서 자세히 설명합니다.  
  
  
*Columnstore* 인덱스에 대해서는 [다른 문서](~/relational-databases/indexes/columnstore-indexes-overview.md)에서 설명합니다.  
  
  
## <a name="a-syntax-for-memory-optimized-indexes"></a>1. 메모리 최적화 인덱스 구문  
  
메모리 최적화 테이블에 대한 각 CREATE TABLE 문은 인덱스를 통해 명시적으로 또는 PRIMAY KEY 또는 UNIQUE 제약 조건을 통해 암시적으로 인덱스를 포함해야 합니다. 인덱스는 다음 중 하나여야 합니다.  
  
- 해시 인덱스  
- 비클러스터형 인덱스(B-트리의 기본 내부 구조를 의미)  
  
  
기본 DURABILITY = SCHEMA_AND_DATA를 사용하여 선언하려면 메모리 최적화 테이블에 기본 키가 있어야 합니다. 다음 CREATE TABLE 문의 PRIMARY KEY NONCLUSTERED 절은 두 가지 요구 사항을 충족합니다.  
  
- CREATE TABLE 문에서 하나의 인덱스의 최소 요구 사항을 충족할 인덱스를 제공합니다.  
- SCHEMA_AND_DATA 절에 필요한 기본 키를 제공합니다.  
  
  
  
    CREATE TABLE SupportEvent  
    (  
        SupportEventId   int NOT NULL  
            PRIMARY KEY NONCLUSTERED,  
        ...  
    ).  
        WITH (  
            MEMORY_OPTIMIZED = ON,  
            DURABILITY = SCHEMA_AND_DATA);  
> [!NOTE]  
>  [!INCLUDE[ssSQL15](../../includes/sssql14-md.md)] 및 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에는 메모리 최적화 테이블 또는 테이블 형식당 8개의 인덱스 제한이 있습니다. [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 및 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터는 메모리 최적화 테이블 및 테이블 형식에 해당하는 인덱스 수 제한이 없어집니다.

  
  
### <a name="a1-code-sample-for-syntax"></a>A.1 구문에 대한 코드 샘플  
  
이 하위 섹션에는 메모리 최적화 테이블에 다양한 인덱스를 만드는 구문을 보여 주는 하는 TRANSACT-SQL 코드 블록이 포함되어 있습니다. 코드에서는 다음을 보여 줍니다.  
  
  
1. 메모리 최적화 테이블을 만듭니다.  
2. ALTER TABLE 문을 사용하여 두 인덱스를 추가합니다.  
3. 데이터 행을 몇 개 삽입합니다.  
  
  
  
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
    ).  
      WITH (  
        MEMORY_OPTIMIZED = ON,  
        DURABILITY = SCHEMA_AND_DATA);  
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
        ('2016-02-25 13:40:41:123', 'Abby', 'Zeke', 2, 'Display problem.'     ),  
        ('2016-02-25 13:40:41:323', 'Ben' , null  , 1, 'Cannot find help.'    ),  
        ('2016-02-25 13:40:41:523', 'Carl', 'Liz' , 2, 'Button is gray.'      ),  
        ('2016-02-25 13:40:41:723', 'Dave', 'Zeke', 2, 'Cannot unhide column.');  
    go  
  
  
  
## <a name="b-nature-of-memory-optimized-indexes"></a>2. 메모리 최적화 인덱스 특성  
  
메모리 최적화 테이블에서는 모든 인덱스 또한 메모리 최적화되어 있습니다. 메모리 최적화 테이블의 인덱스와 디스크 기반 테이블의 인덱스는 여러 방식에서 다릅니다.  
  
각 메모리 최적화 인덱스는 활성 메모리에만 존재합니다. 인덱스는 디스크에 표시되지 않습니다.  
  
- 데이터베이스가 다시 온라인이 될 때 메모리 액세스에 최적화된 인덱스가 다시 빌드됩니다.  
  
  
SQL UPDATE 문에서 메모리 최적화 테이블의 데이터를 수정하는 경우 인덱스에 대한 해당 변경 내용이 로그에 기록되지 않습니다.  
  
  
메모리 최적화 인덱스의 항목에는 테이블 행에 대한 직접 메모리 주소가 포함되어 있습니다.  
  
- 반면 디스크의 기존 B-트리 인덱스의 항목에는 연결된 테이블 행에 대한 메모리 주소를 찾는 데 시스템에서 처음 사용해야 하는 키 값이 포함됩니다.  
  
  
메모리 액세스에 최적화된 인덱스에는 디스크 기반 인덱스와 마찬가지로 고정된 페이지가 없습니다.  
  
- fillfactor가 없으므로 페이지 내에서 기존 유형의 조각화가 발생하지 않습니다.  
  
## <a name="c-duplicate-index-key-values"></a>3. 중복된 인덱스 키 값

중복된 인덱스 키 값은 메모리 최적화 테이블에 대한 작업의 성능에 영향을 줄 수 있습니다. 대부분의 인덱스 작업에서 중복 체인을 순회해야 하므로 중복이 많으면(예: 100 이상) 인덱스 유지 관리 작업이 비효율적입니다. 메모리 최적화 테이블에서 INSERT, UPDATE 및 DELETE 작업에 영향을 줄 수 있습니다. 이 문제는 해시 인덱스에 대한 작업당 적은 비용 및 해시 충돌 체인이 있는 큰 중복 체인의 간섭으로 인해 해시 인덱스의 경우에 더 잘 나타납니다. 인덱스에서 중복을 줄이려면 비클러스터형 인덱스를 사용하고 중복 수를 줄이기 위해 인덱스 키의 끝에 별도 열을 추가합니다(예: 기본 키에서 추가).

CustomerId에 대한 기본 키가 있고 CustomerCategoryID 열에 대한 인덱스가 있는 Customers 테이블을 예로 들어봅시다. 일반적으로 특정 범주에 많은 고객이 있으므로 지정된 키에 대한 중복 값이 CustomerCategoryID의 인덱스에 많습니다. 이 시나리오에서는 (CustomerCategoryID, CustomerId)에 대한 비클러스터형 인덱스를 사용하는 것이 가장 좋습니다. 이 인덱스는 CustomerCategoryID를 포함하는 조건자를 사용하는 쿼리에 사용할 수 있고 중복을 포함하지 않기 때문에 인덱스 유지 관리에서 비효율성을 초래하지 않습니다.

다음 쿼리는 샘플 데이터베이스 `CustomerCategoryID` WideWorldImporters `Sales.Customers`의 테이블 [에 있는](https://msdn.microsoft.com/library/mt734199(v=sql.1).aspx)에 대한 인덱스와 관련해 중복 인덱스 키 값의 평균 개수를 보여 줍니다.

```Transact-SQL
    SELECT AVG(row_count) FROM
       (SELECT COUNT(*) AS row_count 
        FROM Sales.Customers
        GROUP BY CustomerCategoryID) a
```

고유 테이블 및 인덱스와 관련해 인덱스 키 중복 항목의 평균 개수를 구하려면 `Sales.Customers` 를 테이블 이름으로 바꾸고 `CustomerCategoryID` 를 인덱스 키 열 목록으로 바꿉니다.

## <a name="d-comparing-when-to-use-each-index-type"></a>4. 각 인덱스 유형을 사용하는 경우 비교  
  
  
특정 쿼리의 특성에서 인덱스 유형이 적합한 선택인지 결정됩니다.  

해당 기능은 디스크 기반 테이블에서 기존 클러스터형 및 비클러스터형 인덱스의 기능과 유사하므로 기존 응용 프로그램에서 메모리 최적화 테이블을 구현할 때 일반적으로 비클러스트형 인덱스로 시작하는 것이 좋습니다. 
  
  
### <a name="d1-strengths-of-nonclustered-indexes"></a>D.1 비클러스터형 인덱스의 장점  
  
  
비클러스터형 인덱스는 다음의 경우 해시 인덱스 전체에서 선호됩니다.  
  
- 쿼리 시 인덱싱된 열에 ORDER BY 절이 포함됨  
- 다중 열 인덱스의 선행 열만 테스트하는 위치 쿼리  
- 쿼리에서 WHERE 절을 다음과 같이 사용하여 인덱싱된 열 테스트  
  - 같지 않음: *WHERE StatusCode != '완료'*  
  - 값 범위: *수량 위치 > = 100*  
  
  
다음 모든 SELECT 문에서는 비클러스터형 인덱스가 해시 인덱스 전체에서 선호됩니다.  
  
  
  
    SELECT col2 FROM TableA  
        WHERE StartDate > DateAdd(day, -7, GetUtcDate());  
      
    SELECT col3 FROM TableB  
        WHERE ActivityCode != 5;  
      
    SELECT StartDate, LastName  
        FROM TableC  
        ORDER BY StartDate;  
      
    SELECT IndexKeyColumn2  
        FROM TableD  
        WHERE IndexKeyColumn1 = 42;  
  
  
  
### <a name="d2-strengths-of-hash-indexes"></a>D.2 해시 인덱스의 장점  
  
  
[해시 인덱스](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md) 는 다음과 같은 상황에서 비클러스터형 인덱스에서 선호됩니다.  
  
- 쿼리에서 WHERE 절을 다음과 같이 모든 인덱스 키 열에서 같음으로 사용하여 인덱싱된 열 테스트  
  
  
  
    SELECT col9 FROM TableZ  
        WHERE Z_Id = 2174;  
  
  
  
### <a name="d3-summary-table-to-compare-index-strengths"></a>D.3 인덱스 장점을 비교할 요약 테이블  
  
  
다음 표에서 다른 인덱스 유형에서 지원 되는 모든 작업을 나열 합니다.  
  
  
| 연산 | 메모리 액세스에 최적화됨, <br/> 해시 | 메모리 액세스에 최적화됨, <br/> 비클러스터형 | 디스크 기반, <br/> (비)클러스터형 |  
| :-------- | :--------------------------- | :----------------------------------- | :------------------------------------ |  
| 색인 검색은 모든 테이블 행을 검색합니다. | 예 | 예 | 예 |  
| 같음 조건자(=)에서 인덱스 검색 | 예 <br/> (전체 키는 필수) | 예  | 예 |  
| 같지 않음 및 범위 조건자에서 인덱스 검색 <br/> (>, <, <=, > =, BETWEEN). | 아니요 <br/> (인덱스 검색의 결과) | 예 | 예 |  
| 인덱스 정의와 일치하는 정렬 순서로 행을 검색합니다. | 아니요 | 예 | 예 |  
| 인덱스 정의의 역순과 일치하는 정렬 순서로 행을 검색합니다. | 아니요 | 아니요 | 예 |  
  
  
이 표에서 테이블에서 "예"는 인덱스가 요청을 효율적으로 처리할 수 있음을 의미하며 "아니요"는 인덱스를 사용하여 요청을 효과적으로 충족할 수 없음을 의미합니다.  
