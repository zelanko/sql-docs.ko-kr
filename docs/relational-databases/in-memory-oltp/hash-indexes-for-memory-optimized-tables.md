---
title: 메모리 최적화 테이블의 해시 인덱스 문제 해결
ms.custom: seo-dt-2019
ms.date: 12/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e922cc3a-3d6e-453b-8d32-f4b176e98488
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6216e8e008bff92ce502aa6dda8025c5ef63f0ba
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "74412663"
---
# <a name="troubleshooting-hash-indexes-for-memory-optimized-tables"></a>메모리 최적화 테이블의 해시 인덱스 문제 해결
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

## <a name="prerequisite"></a>필수 요소  
  
이 문서를 이해하는 데 중요한 컨텍스트 정보는 다음 항목에서 확인할 수 있습니다.  
  
- [메모리 액세스에 최적화된 테이블의 인덱스](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)
- [메모리 액세스에 최적화된 테이블의 해시 인덱스](../../relational-databases/sql-server-index-design-guide.md#hash_index) 
 
## <a name="practical-numbers"></a>실제 수  
  
메모리 최적화 테이블의 해시 인덱스를 만들 때 생성 시 버킷 수를 지정해야 합니다. 대부분의 경우 버킷 수는 인덱스 키에 있는 고유한 값 수의 1~2배 사이여야 합니다. 

그러나 **BUCKET_COUNT**가 기본 범위에서 약간 위에 있거나 약간 아래에 있더라도 해시 인덱스의 성능은 지속할 수 있거나 허용 가능합니다. 최소한 메모리 최적화 테이블에서 증가할 것으로 예측되는 행 수와 비교적 동일한 **BUCKET_COUNT**를 해시 인덱스에 지정하는 것이 좋습니다.  
테이블에서 2백만 개의 행이 있고 계속 증가하고 있다고 가정하지만 테이블이 10배인 2천만 개로 증가할 것으로 예측합니다. 이 경우 테이블의 행 수보다 10배 많은 버킷 수로 시작됩니다. 이렇게 하면 증가하는 행 수를 위한 공간이 확보됩니다.  
  
- 이상적으로는 행 수가 초기 버킷 수에 도달할 때 버킷 수를 늘리는 것이 좋습니다.  
- 행 수가 버킷 수 보다 5배로 더 많아지더라도 대부분의 경우 성능은 여전히 적절히 유지됩니다.  
  
해시 인덱스에 고유 키 값이 천만 개 있다고 가정하면  
  
- 2백만 개의 버킷 수가 허용할 수 있는 최저 수치입니다. 성능 저하도 견딜 수 있는 정도입니다.  
  
## <a name="too-many-duplicate-values-in-the-index"></a>인덱스에 중복 값이 너무 많은 경우  
  
해시 인덱스 값에 중복 비율이 높은 경우에는 해시 버킷은 늘어난 체인을 경험합니다.  
  
이전 T-SQL 구문 코드 블록에서 동일한 SupportEvent 테이블이 있다고 가정합니다. 다음 T-SQL 코드에서는 *모든* 값 대 *고유* 값의 비율을 찾아 표시하는 방법을 보여 줍니다.  
  
```sql
-- Calculate ratio of:  Rows / Unique_Values.  
DECLARE @allValues float(8) = 0.0, @uniqueVals float(8) = 0.0;  
  
SELECT @allValues = Count(*) FROM SupportEvent;  
  
SELECT @uniqueVals = Count(*) FROM  
  (SELECT DISTINCT SupportEngineerName  
      FROM SupportEvent) as d;  
  
    -- If (All / Unique) >= 10.0, use a nonclustered index, not a hash.   
SELECT Cast((@allValues / @uniqueVals) as float) as [All_divby_Unique];  
go  
```
  
- 비율이 10.0 이상이면 해시의 인덱스 유형이 좋지 않다는 것을 의미합니다. 대신 비클러스터형 인덱스를 사용하는 것이 좋습니다.   
  
## <a name="troubleshooting-hash-index-bucket-count"></a>해시 인덱스 버킷 수 문제 해결  
  
이 섹션에서는 해시 인덱스 버킷 수에 대한 문제를 해결하는 방법을 설명합니다.  
  
### <a name="monitor-statistics-for-chains-and-empty-buckets"></a>체인 및 빈 버킷 통계 모니터링  
  
다음 T-SQL SELECT를 실행하여 해시 인덱스의 통계 상태를 모니터링할 수 있습니다. SELECT는 **sys.dm_db_xtp_hash_index_stats**라는 DMV(Data Management View)를 사용합니다.  
  
```sql
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
  
### <a name="demonstration-of-chains-and-empty-buckets"></a>체인 및 빈 버킷 데모  
  
다음 T-SQL 코드 블록을 사용하여 `SELECT * FROM sys.dm_db_xtp_hash_index_stats;`을 간편하게 테스트할 수 있습니다. 코드 블록은 1분 내에 완료됩니다. 다음은 아래 코드 블록의 절입니다.  
  
1. 몇 개의 해시 인덱스가 있는 메모리 최적화 테이블을 만듭니다.  
2. 수천 개의 행으로 테이블을 채웁니다.  
    a. 모듈로 연산자는 StatusCode 열에서 중복 값의 비율을 구성하는 데 사용됩니다.  
    b. 약 1분 이내에 루프에서 26만 2,144개의 행을 삽입합니다.  
3. **sys.dm_db_xtp_hash_index_stats**에서 이전 SELECT를 실행하라는 메시지가 인쇄됩니다.  

```sql
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
  
SET NOCOUNT ON;  
  
-- Same as PK bucket_count.  68 seconds to complete.  
DECLARE @i int = 262144;  
  
BEGIN TRANSACTION;  
  
WHILE @i > 0  
BEGIN  
  
  INSERT SalesOrder_Mem  
      (OrderSequence, OrderDate, StatusCode)  
    Values  
      (@i, GetUtcDate(), @i % 8);  -- Modulo technique.  
  
  SET @i -= 1;  
END  
COMMIT TRANSACTION;  
  
PRINT 'Next, you should query:  sys.dm_db_xtp_hash_index_stats .';  
go  
```  
  
이전의 `INSERT` 루프는 다음을 수행합니다.  
  
- 기본 키 인덱스 및 *ix_OrderSequence*에 고유한 값을 삽입합니다.  
- `StatusCode`에 대해 8개의 고유 값만 표시하는 수백만 개의 행을 삽입합니다. 따라서 인덱스 *ix_StatusCode*에는 값 중복 비율이 높습니다.  
  
버킷 수가 최적이 아닌 경우 문제 해결을 위해 **sys.dm_db_xtp_hash_index_stats**에서 다음 SELECT 출력을 확인합니다. 이러한 결과에 대해 섹션 D.1에서 복사한 SELECT에 `WHERE Object_Name(h.object_id) = 'SalesOrder_Mem'` 를 추가했습니다.  
  
`SELECT` 결과는 향상된 표시를 위해 좀 더 좁은 두 개의 결과 테이블로 분할되어 코드 뒤에 표시됩니다.  
  
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
  
### <a name="balancing-the-trade-off"></a>상충 관계 균형 조정  
  
OLTP는 작업 시 개별 행에 중점을 둡니다. 일반적으로 전체 테이블 검색은 OLTP 작업에서 성능이 중요한 경로에 두지 않습니다. 따라서 **메모리 사용 수량**과 **같음 테스트 및 삽입 작업의 성능** 간에 균형을 맞추어야 합니다.  
  
**메모리 사용률이 더 큰 문제일 경우**  
  
- 인덱스 키 레코드의 수에 가까운 버킷 수를 선택합니다.  
- 버킷 수가 인덱스 키 값 수보다 너무 적으면 안 됩니다. 이 경우 대부분의 DML 작업과 서버 재시작 후 데이터베이스를 복구하는 시간에 영향이 있습니다.  
  
**같음 테스트의 성능이 더 큰 문제일 경우**  
  
- 버킷 수를 고유한 인덱스 값 수보다 2-3배 많이 지정하는 것이 좋습니다. 더 높은 수는 다음을 의미합니다.  
  - 하나의 특정 값을 찾을 때 더 빠르게 검색됩니다.  
  - 메모리 사용률이 증가합니다.  
  - 해시 인덱스의 전체 검색에 필요한 시간이 늘어납니다.  
  

##  <a name="additional-reading"></a><a name="Additional_Reading"></a> 더 보기  
 [메모리 최적화 테이블의 해시 인덱스](../../relational-databases/sql-server-index-design-guide.md#hash_index)   
 [메모리 최적화 테이블의 비클러스터형 인덱스](../../relational-databases/sql-server-index-design-guide.md#inmem_nonclustered_index)  
