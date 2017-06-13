---
title: "메모리 액세스에 최적화된 테이블의 해시 인덱스 | Microsoft 문서"
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 06/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e922cc3a-3d6e-453b-8d32-f4b176e98488
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: b1acbcd97dfabfa5d23fa82e55d4eb01101233aa
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="hash-indexes-for-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블의 해시 인덱스
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  
이 문서에서는 메모리 액세스에 최적화된 테이블에서 사용할 수 있는 *해시* 형식의 인덱스를 설명합니다. 이 문서에서는 다음 내용을 다룹니다.  
  
- TRANSACT-SQL 구문을 보여 주는 짧은 코드 예제를 제공합니다.  
- 해시 인덱스의 기본 사항에 대해 설명합니다.  
- [적절한 버킷 수를 계산하는 방법](#configuring_bucket_count)에 대해 설명합니다.  
- 해시 인덱스를 디자인하고 관리하는 방법을 설명합니다.  
  
  
#### <a name="prerequisite"></a>필수 구성 요소  
  
이 문서를 이해하는 데 중요한 컨텍스트 정보는 다음 항목에서 확인할 수 있습니다.  
  
- [메모리 액세스에 최적화된 테이블의 인덱스](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)  
  
  
  
## <a name="a-syntax-for-memory-optimized-indexes"></a>1. 메모리 액세스에 최적화된 인덱스 구문  
  
  
### <a name="a1-code-sample-for-syntax"></a>A.1 구문에 대한 코드 샘플  
  
이 하위 섹션에는 메모리 액세스에 최적화된 테이블에 해시 인덱스를 만드는 데 사용할 수 있는 구문을 보여 주는 하는 TRANSACT-SQL 코드 블록이 포함되어 있습니다.  
  
- 샘플에는 해시 인덱스가 CREATE TABLE 문 내에 선언되어 있습니다.  
  - 대신 별도의 [ALTER TABLE...ADD INDEX](#h3-b2-declaration-limitations) 문에 해시 인덱스를 선언할 수 있습니다.  
  
  
  
    DROP TABLE IF EXISTS SupportEventHash;  
    go  
      
    CREATE TABLE SupportIncidentRating_Hash  
    (  
      SupportIncidentRatingId   int      not null   identity(1,1)  
        PRIMARY KEY NONCLUSTERED,  
      
      RatingLevel          int           not null,  
      
      SupportEngineerName  nvarchar(16)  not null,  
      Description          nvarchar(64)      null,  
      
      INDEX ix_hash_SupportEngineerName  
        HASH (SupportEngineerName) WITH (BUCKET_COUNT = 100000)  
    ).  
      WITH (  
        MEMORY_OPTIMIZED = ON,  
        DURABILITY = SCHEMA_ONLY);  
    go  
  

사용 중인 데이터의 `BUCKET_COUNT` 가 올바른지 확인하려면 [해시 인덱스 버킷 수 구성](#configuring_bucket_count)을 참조하세요. 
  
## <a name="b-hash-indexes"></a>2. 해시 인덱스  
  
  
### <a name="b1-performance-basics"></a>B.1 성능 기본 사항  
  
해시 인덱스의 성능은 다음과 같습니다.  
  
- WHERE 절에서 해시 인덱스 키의 각 열에 대한 *정확한* 값을 지정할 때 뛰어납니다.  
- WHERE 절에서 인덱스 키에 있는 값 *범위* 를 찾을 때 저하됩니다.  
- WHERE 절에서 두 열로 된 해시 인덱스 키에서 첫 번째 열에 특정 값을 지정하지만 키의 *두 번째* 열에 값을 지정하지 않으면 저하됩니다.  
  
  
<a name="h3-b2-declaration-limitations"></a>  
  
### <a name="b2-declaration-limitations"></a>B.2 선언 제한 사항  
  
해시 인덱스는 메모리 액세스에 최적화된 테이블에 대해서만 존재할 수 있습니다. 디스크 기반 테이블에는 있을 수 없습니다.  
  
해시 인덱스를 다음으로 선언할 수 있습니다.  
  
- UNIQUE(또는 Nonunique를 기본값으로 설정할 수 있음)  
- NONCLUSTERED, 기본값입니다.   
  
  
다음은 CREATE TABLE 문 외부에 해시 인덱스를 만드는 구문의 예입니다.  
  
  
    ALTER TABLE MyTable_memop  
      ADD INDEX ix_hash_Column2 UNIQUE  
        HASH (Column2) WITH (BUCKET_COUNT = 64);  
  
  
  
### <a name="b3-buckets-and-hash-function"></a>B.3 버킷 및 해시 함수  
  
해시 인덱스는 *버킷* 배열이라고 하는 키 값을 앵커합니다.  
  
- 각 버킷은 8바이트이며, 키 항목의 링크 목록의 메모리 주소를 저장하는 데 사용됩니다.  
- 각 항목은 인덱스 키와, 기본 메모리 액세스에 최적화된 테이블에서 해당 행의 주소에 대한 값입니다.  
  - 각 항목은 항목의 링크 목록에서 현재 버킷에 연결된 그 다음 항목을 가리킵니다.  
  
  
해싱 알고리즘은 모든 고유 키 값을 해당 버킷 간에 균등하게 분산하려고 시도하지만 완벽한 균일성은 달성하기 힘든 이상적인 상황입니다. 주어진 키 값의 모든 인스턴스는 동일한 버킷에 연결됩니다. 버킷은 다른 키 값의 모든 인스턴스에서도 혼합될 수 있습니다.  
  
- 이 혼합을 *해시 충돌*이라고 합니다. 충돌은 일반적으로 발생하지만 좋은 현상은 아닙니다.  
- 현실적인 목표는 버킷의 30%에 2개의 서로 다른 키 값을 포함하는 것입니다.  
  
  
해시 인덱스에서 보유할 수 있는 버킷 수를 결정합니다.  
  
- 테이블 행 또는 고유 값에 대한 버킷 비율이 낮을 수록 평균 버킷 링크 목록이 길어집니다.  
- 링크 목록이 짧을 경우 성능 속도가 훨씬 빠릅니다.  
  
  
SQL Server에는 모든 해시 인덱스에 사용할 하나의 해시 함수가 있습니다.  
  
- 해시 함수는 결정적으로, 동일한 입력 키 값이 제공되면 동일한 버킷 슬롯을 일관되게 출력합니다.  
- 반복된 호출이 있을 경우 해시 함수는 출력 시 평평한 선형 분포가 아닌 포아송 또는 벨 곡선 분포를 형성하는 경향이 있습니다.  
  
  
해시 인덱스와 버킷의 상호 작용은 다음 그림에 요약되어 있습니다.  
  
  
![hekaton_tables_23d](../../relational-databases/in-memory-oltp/media/hekaton-tables-23d.png "인덱스 키, 해시 함수에 입력, 체인의 헤드를 가리키는 해시 버킷의 주소인 출력")  
  
  
  
### <a name="b4-row-versions-and-garbage-collection"></a>B.4 행 버전 및 가비지 수집  
  
  
메모리 액세스에 최적화된 테이블에서 행이 SQL UPDATE의 영향을 받을 경우 테이블에서는 행의 업데이트된 버전을 만듭니다. 업데이트 트랜잭션 동안 다른 세션에서는 이전 버전의 행을 읽을 수 있어 행 잠금과 관련 있는 성능 속도가 느려지는 것을 방지할 수 있습니다.  
  
해시 인덱스에는 업데이트를 수용하기 위해 서로 다른 버전의 항목이 있을 수도 있습니다.  
  
나중에 이전 버전이 더 이상 필요 없게 되면 GC(가비지 수집) 스레드가 버킷과 링크 목록을 트래버스하여 이전 항목을 정리합니다. 링크 목록 체인 길이가 짧은 경우 GC 스레드 성능은 향상됩니다.   
  
<a name="configuring_bucket_count"></a>
  
## <a name="c-configuring-the-hash-index-bucket-count"></a>3. 해시 인덱스 버킷 수 구성  
  
해시 인덱스 버킷 수는 인덱스를 만들 때 지정되며, ALTER TABLE...ALTER INDEX REBUILD 구문을 사용하여 변경할 수 있습니다.  
  
대부분의 경우 버킷 수는 인덱스 키에 있는 고유한 값 수의 1~2배 사이여야 합니다.   
특정 인덱스 키에 얼마나 많은 값이 지정될지 항상 예측할 수 있는 것은 아닙니다. 성능은 일반적으로 **BUCKET_COUNT** 값이 실제 키 값 수의 10배 이내인 경우에 적절하게 유지되며 과대 평가하는 것이 과소 평가하는 것보다 더 좋습니다.  
  
버킷이 너무 *적으면* 다음과 같은 단점이 있습니다.  
  
- 고유 키 값의 해시 충돌이 더 많아 집니다.  
  - 각 고유 값에서 다른 고유 값과 동일한 버킷을 강제로 공유합니다.  
  - 버킷 당 평균 체인 길이가 증가합니다.  
  - 버킷 체인이 길어질수록 인덱스에서 같음 조회 속도는 느려집니다.  
  
버킷이 너무 *많으면* 다음과 같은 단점이 있습니다.  
  
- 버킷 수가 너무 높으면 빈 버킷이 더 많이 생성될 수 있습니다.  
  - 빈 버킷은 전체 인덱스 검색 성능에 영향을 줍니다. 전체 인덱스 검색을 정기적으로 수행하는 경우 고유한 인덱스 키 값의 수에 가까운 버킷 수를 선택하는 것이 좋습니다.  
  - 각 버킷은 8바이트만 사용하지만 빈 버킷도 메모리를 사용합니다.  
    
  
> [!NOTE]
> 버킷을 더 많이 추가한다고 해서 중복 값을 공유하는 항목 연결이 줄어들지는 않습니다. 값 중복 속도는 버킷 수를 계산하기 위함이 아니라 해시가 적절한 인덱스 유형인지 결정하는 데 사용됩니다.  
  
  
  
### <a name="c1-practical-numbers"></a>C.1 실제 수  
  
**BUCKET_COUNT** 가 기본 범위에서 약간 위에 있거나 약간 아래에 있더라도 해시 인덱스의 성능은 지속할 수 있거나 허용 가능합니다. 문제가 되는 상황은 발생하지 않습니다.  
  
메모리 액세스에 최적화된 테이블에서 증가할 것으로 예측되는 행 수와 비교적 동일한 **BUCKET_COUNT** 를 해시 인덱스에 지정합니다.  
  
테이블에서 2백만 개의 행이 있고 계속 증가하고 있다고 가정하면 10배로 수량이 증가할 경우 2천만 개의 행을 예측합니다. 이 경우 테이블의 행 수보다 10배 많은 버킷 수로 시작됩니다. 이렇게 하면 증가하는 행 수를 위한 공간이 확보됩니다.  
  
- 이상적으로는 행 수가 초기 버킷 수에 도달할 때 버킷 수를 늘리는 것이 좋습니다.  
- 행 수가 버킷 수 보다 5배로 더 많아지더라도 대부분의 경우 성능은 여전히 적절히 유지됩니다.  
  
해시 인덱스에 고유 키 값이 천만 개 있다고 가정하면  
  
- 2백만 개의 버킷 수가 허용할 수 있는 최저 수치입니다. 성능 저하도 견딜 수 있는 정도입니다.  
  
### <a name="c2-too-many-duplicate-values-in-the-index"></a>C.2 인덱스에 중복 값이 너무 많은 경우?  
  
해시 인덱스 값에 중복 비율이 높은 경우에는 해시 버킷은 늘어난 체인을 경험합니다.  
  
이전 T-SQL 구문 코드 블록에서 동일한 SupportEvent 테이블이 있다고 가정합니다. 다음 T-SQL 코드에서는 *모든* 값 대 *고유* 값의 비율을 찾아 표시하는 방법을 보여 줍니다.  
  
        -- Calculate ratio of:  Rows / Unique_Values.  
    DECLARE @allValues float(8) = 0.0, @uniqueVals float(8) = 0.0;  
      
    SELECT @allValues = Count(*) FROM SupportEvent;  
      
    SELECT @uniqueVals = Count(*) FROM  
      (SELECT DISTINCT SupportEngineerName  
         FROM SupportEvent) as d;  
      
        -- If (All / Unique) >= 10.0, use a nonclustered index, not a hash.   
    SELECT Cast((@allValues / @uniqueVals) as float) as [All_divby_Unique];  
    go  
  
- 비율이 10.0 이상이면 해시의 인덱스 유형이 좋지 않다는 것을 의미합니다. 대신 비클러스터형 인덱스를 사용하는 것이 좋습니다.   
  
## <a name="d-troubleshooting-hash-index-bucket-count"></a>4. 해시 인덱스 버킷 수 문제 해결  
  
이 섹션에서는 해시 인덱스 버킷 수에 대한 문제를 해결하는 방법을 설명합니다.  
  
### <a name="d1-monitor-statistics-for-chains-and-empty-buckets"></a>D.1 체인 및 빈 버킷 통계 모니터링  
  
다음 T-SQL SELECT를 실행하여 해시 인덱스의 통계 상태를 모니터링할 수 있습니다. SELECT는 **sys.dm_db_xtp_hash_index_stats**라는 DMV(Data Management View)를 사용합니다.  
  
  
```t-sql
  SELECT  
    QUOTENAME(SCHEMA_NAME(t.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(h.object_id)) as [table],   
    i.name                   as [index],   
    h.total_bucket_count,  
    h.empty_bucket_count,  
      
    FLOOR((  
      CAST(h.empty_bucket_count as float) /  
        h.total_bucket_count) * 100)  
                             as [empty_bucket_percent],  
    h.avg_chain_length,   
    h.max_chain_length  
  FROM  
         sys.dm_db_xtp_hash_index_stats  as h   
    JOIN sys.indexes                     as i  
            ON h.object_id = i.object_id  
           AND h.index_id  = i.index_id  
    JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
    JOIN sys.tables t on h.object_id=t.object_id
  WHERE ia.type=1
  ORDER BY [table], [index];  
```
  
  
다음 통계 지침과 SELECT 결과를 비교합니다.  
  
- 빈 버킷:  
  - 33%가 정상 목표 값이지만 좀 더 높아도 괜찮습니다(90%).  
  - 버킷 수가 고유 키 값 수와 일치하면 대략 버킷의 33% 정도 비어 있는 것입니다.  
  - 값이 10% 이하면 너무 낮습니다.  
- 버킷 내 체인:  
  - 중복 인덱스 키 값이 없는 경우 평균 체인 길이 1이 이상적입니다. 체인 길이는 주로 최대 10까지 허용됩니다.  
  - 평균 체인 길이가 10보다 크고 빈 버킷 백분율이 10%보다 크면 데이터에 너무 많은 중복이 있어 해시 인덱스가 가장 적합한 형식이 아닐 수도 있습니다.  
  

  
### <a name="d2-demonstration-of-chains-and-empty-buckets"></a>D.2 체인 및 빈 버킷 데모  
  
  
다음 T-SQL 코드 블록을 사용하여 `SELECT * FROM sys.dm_db_xtp_hash_index_stats;`을 간편하게 테스트할 수 있습니다. 코드 블록은 1분 내에 완료됩니다. 다음은 아래 코드 블록의 절입니다.  
  
  
1. 몇 개의 해시 인덱스가 있는 메모리 액세스에 최적화된 테이블을 만듭니다.  
2. 수천 개의 행으로 테이블을 채웁니다.  
    1. 모듈로 연산자는 StatusCode 열에서 중복 값의 비율을 구성하는 데 사용됩니다.  
    2. 약 1분 내에 루프에서 행을 262144개 삽입합니다.  
3. **sys.dm_db_xtp_hash_index_stats**에서 이전 SELECT를 실행하라는 메시지가 인쇄됩니다.  
  
  
```t-sql
    DROP TABLE IF EXISTS SalesOrder_Mem;  
    go  
      
      
    CREATE TABLE SalesOrder_Mem  
    (  
      SalesOrderId   uniqueidentifier  NOT NULL  DEFAULT newid(),  
      OrderSequence  int               NOT NULL,  
      OrderDate      datetime2(3)      NOT NULL,  
      StatusCode     tinyint           NOT NULL,  
      
      PRIMARY KEY NONCLUSTERED  
          HASH (SalesOrderId)  WITH (BUCKET_COUNT = 262144),  
      
      INDEX ix_OrderSequence  
          HASH (OrderSequence) WITH (BUCKET_COUNT = 20000),  
      
      INDEX ix_StatusCode  
          HASH (StatusCode)    WITH (BUCKET_COUNT = 8),  
      
      INDEX ix_OrderDate       NONCLUSTERED (OrderDate DESC)  
    )  
      WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
    go  
      
        --------------------  
      
    SET NoCount ON;  
      
      -- Same as PK bucket_count.  68 seconds to complete.  
    DECLARE @i int = 262144;  
      
    BEGIN TRANSACTION;  
      
    WHILE @i > 0  
    Begin  
      
      INSERT SalesOrder_Mem  
          (OrderSequence, OrderDate, StatusCode)  
        Values  
          (@i, GetUtcDate(), @i % 8);  -- Modulo technique.  
      
      SET @i -= 1;  
    End  
    COMMIT TRANSACTION;  
      
    PRINT 'Next, you should query:  sys.dm_db_xtp_hash_index_stats .';  
    go  
```  
  
  
이전의 INSERT 루프는 다음을 수행합니다.  
  
- 기본 키 인덱스 및 IX_OrderSequence에 고유한 값을 삽입합니다.  
- StatusCode에 대해 8개의 고유 값만 표시하는 수백 만 개의 행을 삽입합니다. 따라서 인덱스 ix_StatusCode에는 값 중복 비율이 높습니다.  
  
버킷 수가 최적이 아닌 경우 문제 해결을 위해 **sys.dm_db_xtp_hash_index_stats**에서 다음 SELECT 출력을 확인합니다. 이러한 결과에 대해 섹션 D.1에서 복사한 SELECT에 `WHERE Object_Name(h.object_id) = 'SalesOrder_Mem'` 를 추가했습니다.  
  
  
  
SELECT 결과는 향상된 표시를 위해 보다 좁은 두 개의 결과 테이블로 분할되어 코드 위에 표시됩니다.  
  
- *버킷 수*에 대한 결과는 다음과 같습니다.  
  
  
| IndexName | total_bucket_count | empty_bucket_count | EmptyBucketPercent |  
| :-------- | -----------------: | -----------------: | -----------------: |  
| IX_OrderSequence | 32768 | 13 | 0 |  
| ix_StatusCode | 8 | 4 | 50 |  
| PK_SalesOrd_B14003... | 262144 | 96525 | 36 |  
  
  
- 다음은 *체인 길이*에 대한 결과입니다.  
  
  
| IndexName | avg_chain_length | max_chain_length |  
| :-------- | ---------------: | ---------------: |  
| IX_OrderSequence | 8 | 26 |  
| ix_StatusCode | 65536 | 65536 |  
| PK_SalesOrd_B14003... | 1 | 8 |  
  
  
  
  
3개의 해시 인덱스에 대한 위의 결과 테이블을 해석해 보겠습니다.  
  
*ix_StatusCode*  
  
- 버킷의 50%가 비어 있으며 상태가 정상입니다.  
- 하지만 평균 체인 길이가 65536으로 매우 깁니다.  
  - 이것은 중복 값 비율이 높다는 것을 나타냅니다.  
  - 따라서 이 경우 해시 인덱스를 사용하는 것은 적합하지 않습니다. 대신 비클러스터형 인덱스를 사용해야 합니다.  
  
*IX_OrderSequence*  
  
- 버킷의 0%가 비어 있으며 너무 낮습니다.  
- 이 인덱스에 있는 모든 값은 고유하더라도 평균 체인 길이가 8입니다.  
  - 따라서 평균 체인 길이가 2 또는 3으로 줄어들 수 있도록 버킷 수를 늘려야 합니다.  
- 인덱스 키에 262,144개의 고유한 값이 있으므로 버킷 수가 적어도 262,144개가 되어야 합니다.  
  - 향후에 더 성장할 것으로 예상된다면 버킷 수를 더 높여야 합니다.  
  
*기본 키 인덱스(PK__SalesOrd_…)*  
  
- 버킷의 36%가 비어 있으며 상태가 정상입니다.  
- 평균 체인 길이가 1이면 좋습니다. 변경할 필요가 없습니다.  
  
  
### <a name="d3-balancing-the-trade-off"></a>D.3 상충 관계 균형 조정  
  
OLTP는 작업 시 개별 행에 중점을 둡니다. 일반적으로 전체 테이블 검색은 OLTP 작업에서 성능이 중요한 경로에 두지 않습니다. 따라서 다음 상충 관계에서 서로 균형을 조정해야 합니다.  
  
- 메모리 사용률 vs.  
- 같음 테스트 및 삽입 작업의 성능  
  
  
*메모리 사용률이 더 큰 문제일 경우*  
  
- 인덱스 키 레코드의 수에 가까운 버킷 수를 선택합니다.  
- 버킷 수가 인덱스 키 값 수보다 너무 적으면 안 됩니다. 이 경우 대부분의 DML 작업과 서버 재시작 후 데이터베이스를 복구하는 시간에 영향이 있습니다.  
  
  
*같음 테스트의 성능이 더 큰 문제일 경우*  
  
- 버킷 수를 고유한 인덱스 값 수보다 2-3배 많이 지정하는 것이 좋습니다. 더 높은 수는 다음을 의미합니다.  
  - 하나의 특정 값을 찾을 때 더 빠르게 검색됩니다.  
  - 메모리 사용률이 증가합니다.  
  - 해시 인덱스의 전체 검색에 필요한 시간이 늘어납니다.  
  
  
  
  
## <a name="e-strengths-of-hash-indexes"></a>5. 해시 인덱스의 장점  
  
  
해시 인덱스는 다음과 같은 상황에서 비클러스터형 인덱스에서 선호됩니다.  
  
- 쿼리에서 WHERE 절을 다음과 같이 같음으로 사용하여 인덱싱된 열 테스트  
  
  
  
    SELECT col9 FROM TableZ  
        WHERE Z_Id = 2174;  
  
  
  
### <a name="e1-multi-column-hash-index-keys"></a>E.1 다중 열 해시 인덱스 키  
  
  
2열 인덱스는 비클러스터형 인덱스 또는 해시 인덱스일 수 있습니다. 인덱스 열이 col1 및 col2라고 가정해 보겠습니다. 다음 SQL SELECT 문이 주어진 경우 비클러스터형 인덱스만 쿼리 최적화 프로그램에 유용합니다.  
  
  
    SELECT col1, col3  
        FROM MyTable_memop  
        WHERE col1 = 'dn';  
  
  
해시 인덱스는 WHERE 절이 있어야 해당 키의 각 열에 대한 같음 테스트를 지정할 수 있습니다. 그렇지 않으면 해시 인덱스는 최적화 프로그램에 유용하지 않습니다.  
  
WHERE 절이 인덱스 키의 두 번째 열만 지정하는 경우에는 두 인덱스 유형 모두 유용하지 않습니다.  

