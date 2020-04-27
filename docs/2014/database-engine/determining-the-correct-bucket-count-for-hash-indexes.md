---
title: 해시 인덱스에 대 한 올바른 버킷 수 결정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 6d1ac280-87db-4bd8-ad43-54353647d8b5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b1b79c0908f8639df869d01a8ff862afc5be77cb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62754245"
---
# <a name="determining-the-correct-bucket-count-for-hash-indexes"></a>해시 인덱스에 대한 올바른 버킷 수 결정
  메모리 최적화 테이블을 만들 때 `BUCKET_COUNT` 매개 변수 값을 지정해야 합니다. 이 항목에서는 적절한 `BUCKET_COUNT` 매개 변수 값을 결정하기 위한 권장 사항을 안내합니다. 정확한 버킷 수를 확인할 수 없으면 대신 비클러스터형 인덱스를 사용합니다.  잘못된 `BUCKET_COUNT` 값, 특히 너무 낮은 값을 사용하면 데이터베이스 복구 시간과 작업 성능에 큰 영향을 줄 수 있습니다. 버킷 수를 더 많이 추정하는 것이 좋습니다.  
  
 중복 인덱스 키는 해시 인덱스를 사용하는 경우 동일한 버킷에 해시되어 해당 버킷의 체인이 증가하도록 하기 때문에 성능을 저하시킬 수 있습니다.  
  
 비클러스터형 해시 인덱스에 대한 자세한 내용은 [Hash Indexes](hash-indexes.md) 및 [Guidelines for Using Indexes on Memory-Optimized Tables](../relational-databases/in-memory-oltp/memory-optimized-tables.md)을 참조하세요.  
  
 메모리 최적화 테이블에서 각 해시 인덱스에 대해 한 해시 테이블이 할당됩니다. 인덱스에 할당 된 해시 테이블의 크기는 [CREATE TABLE &#40;transact-sql&#41;](/sql/t-sql/statements/create-table-transact-sql) 또는 `BUCKET_COUNT` [CREATE TYPE &#40;transact-sql&#41;](/sql/t-sql/statements/create-type-transact-sql)매개 변수에 의해 지정 됩니다. 버킷 수는 내부적으로 다음 2의 제곱 수로 반올림됩니다. 예를 들어, 버킷 수를 300,000개로 지정하면 실제 버킷 수가 524,288개가 됩니다.  
  
 버킷 수와 관련한 문서 및 비디오에 대한 링크를 보려면 [해시 인덱스(메모리 내 OLTP)에 대한 올바른 버킷 수를 결정하는 방법](https://www.mssqltips.com/sqlservertip/3104/determine-bucketcount-for-hash-indexes-for-sql-server-memory-optimized-tables/)(영문)을 참조하세요.  
  
## <a name="recommendations"></a>권장 사항  
 대부분의 경우 버킷 수는 인덱스 키에 있는 고유한 값 수의 1~2배 사이여야 합니다. 인덱스 키에 중복 값이 많이 포함되어 있는 경우 평균적으로 각 인덱스 키 값에 대해 10개 이상의 행이 있으므로 대신 비클러스터형 인덱스를 사용하세요.  
  
 특정 인덱스 키에 얼마나 많은 값이 지정될지 항상 예측할 수 있는 것은 아닙니다. `BUCKET_COUNT` 값이 실제 키 값 수의 5배 이내에 해당하는 경우 성능이 적절해야 합니다.  
  
 기존 데이터에 있는 고유한 인덱스 키 수를 확인하려면 다음 예제와 비슷한 쿼리를 사용하세요.  
  
### <a name="primary-key-and-unique-indexes"></a>기본 키 및 고유 인덱스  
 기본 키 인덱스는 고유하므로 키의 고유 값 수가 테이블에 있는 행 수에 해당합니다. 예를 들어, AdventureWorks 데이터베이스의 Sales.SalesOrderDetail 테이블에 있는 (SalesOrderID, SalesOrderDetailID)에 대한 기본 키의 경우 다음 쿼리를 실행하여 테이블의 행 수에 해당하는 고유한 기본 키 값 수를 계산합니다.  
  
```sql  
SELECT COUNT(*) AS [row count]   
FROM Sales.SalesOrderDetail  
```  
  
 이 쿼리는 121,317개의 행 수를 보여 줍니다. 행 수가 크게 변경되지 않을 경우 버킷 수로 240,000개를 사용합니다. 테이블의 판매 주문 수가 4배가 될 것으로 예상되는 경우 버킷 수로 480,000개를 사용합니다.  
  
### <a name="non-unique-indexes"></a>고유하지 않은 인덱스  
 다른 인덱스, 예를 들어 (SpecialOfferID, ProductID)에 대한 다중 열 인덱스의 경우 다음 쿼리를 발행하여 고유한 인덱스 키 값 수를 확인합니다.  
  
```sql  
SELECT COUNT(*) AS [SpecialOfferID_ProductID index key count]  
FROM   
   (SELECT DISTINCT SpecialOfferID, ProductID   
    FROM Sales.SalesOrderDetail) t  
```  
  
 이 쿼리는 (SpecialOfferID, ProductID)에 대한 인덱스 키 수로 484를 반환하여 비클러스터형 해시 인덱스 대신 비클러스터형 인덱스를 사용해야 함을 나타냅니다.  
  
### <a name="determining-the-number-of-duplicates"></a>중복 항목 수 확인  
 인덱스 키 값의 평균 중복 값 수를 확인하려면 총 행 수를 고유한 인덱스 키 값 수로 나눕니다.  
  
 예를 들어, (SpecialOfferID, ProductID)의 경우 이 값은 121317/484 = 251개가 됩니다. 즉, 인덱스 키 값이 평균 251개가 되며 비클러스터형 인덱스여야 합니다.  
  
## <a name="troubleshooting-the-bucket-count"></a>버킷 수 문제 해결  
 메모리 최적화 테이블의 버킷 수 문제를 해결 하려면 [dm_db_xtp_hash_index_stats &#40;transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-hash-index-stats-transact-sql) 를 사용 하 여 빈 버킷 및 행 체인의 길이에 대 한 통계를 가져옵니다. 다음 쿼리는 현재 데이터베이스의 모든 해시 인덱스에 대한 통계를 가져오는 데 사용할 수 있습니다. 데이터베이스에 큰 테이블이 있는 경우 이 쿼리를 실행하는 데 몇 분 정도 걸릴 수 있습니다.  
  
```sql  
SELECT   
   object_name(hs.object_id) AS 'object name',   
   i.name as 'index name',   
   hs.total_bucket_count,  
   hs.empty_bucket_count,  
   floor((cast(empty_bucket_count as float)/total_bucket_count) * 100) AS 'empty_bucket_percent',  
   hs.avg_chain_length,   
   hs.max_chain_length  
FROM sys.dm_db_xtp_hash_index_stats AS hs   
   JOIN sys.indexes AS i   
   ON hs.object_id=i.object_id AND hs.index_id=i.index_id  
```  
  
 해시 인덱스 상태의 두 가지 키 지표는 다음과 같습니다.  
  
 *empty_bucket_percent*  
 *empty_bucket_percent* 는 해시 인덱스에 있는 빈 버킷 수를 나타냅니다.  
  
 *empty_bucket_percent* 가 10% 미만인 경우 버킷 수도 적을 가능성이 큽니다. *empty_bucket_percent* 가 33% 이상이 되는 것이 이상적입니다. 버킷 수가 인덱스 키 값 수와 일치하는 경우 해시 분포로 인해 버킷의 1/3이 비어 있습니다.  
  
 *avg_chain_length*  
 *avg_chain_length* 는 해시 버킷의 평균 행 체인 길이를 나타냅니다.  
  
 *avg_chain_length* 가 10보다 크고 *empty_bucket_percent* 가 10% 이상이면 중복 인덱스 키 값이 많을 수 있으므로 비클러스터형 인덱스가 더 적합합니다. 평균 체인 길이 1이 이상적입니다.  
  
 다음 두 가지 요소가 체인 길이에 영향을 줍니다.  
  
1.  중복 행. 모든 중복 행은 해시 인덱스에 있는 동일한 체인의 일부입니다.  
  
2.  여러 키 값이 동일한 버킷에 매핑됩니다. 버킷 수가 적을수록 여러 값이 매핑되는 버킷이 증가합니다.  
  
 예를 들어, 다음 테이블 및 스크립트를 고려하여 테이블에 샘플 행을 삽입합니다.  
  
```sql  
CREATE TABLE [Sales].[SalesOrderHeader_test]  
(  
   [SalesOrderID] [uniqueidentifier] NOT NULL DEFAULT (newid()),  
   [OrderSequence] int NOT NULL,  
   [OrderDate] [datetime2](7) NOT NULL,  
   [Status] [tinyint] NOT NULL,  
  
PRIMARY KEY NONCLUSTERED HASH ([SalesOrderID]) WITH ( BUCKET_COUNT = 262144 ),  
INDEX IX_OrderSequence HASH (OrderSequence) WITH ( BUCKET_COUNT = 20000),  
INDEX IX_Status HASH ([Status]) WITH ( BUCKET_COUNT = 8),  
INDEX IX_OrderDate NONCLUSTERED ([OrderDate] ASC),  
)WITH ( MEMORY_OPTIMIZED = ON , DURABILITY = SCHEMA_AND_DATA )  
GO  
  
DECLARE @i int = 0  
BEGIN TRAN  
WHILE @i < 262144  
BEGIN  
   INSERT Sales.SalesOrderHeader_test (OrderSequence, OrderDate, [Status]) VALUES (@i, sysdatetime(), @i % 8)  
   SET @i += 1  
END  
COMMIT  
GO  
```  
  
 이 스크립트는 테이블에 262,144개의 행을 삽입합니다. 기본 키 인덱스 및 IX_OrderSequence에 고유한 값을 삽입합니다. IX_Status 인덱스에 다수의 중복 값을 삽입합니다. 이 스크립트는 8개의 고유 값만 생성합니다.  
  
 BUCKET_COUNT 문제 해결 쿼리의 출력은 다음과 같습니다.  
  
|인덱스 이름|total_bucket_count|empty_bucket_count|empty_bucket_percent|avg_chain_length|max_chain_length|  
|----------------|--------------------------|--------------------------|----------------------------|------------------------|------------------------|  
|IX_Status|8|4|50|65536|65536|  
|IX_OrderSequence|32768|13|0|8|26|  
|PK_SalesOrd_B14003C3F8FB3364|262144|96319|36|1|8|  
  
 이 테이블의 경우 3개의 해시 인덱스를 고려하세요.  
  
-   IX_Status: 버킷의 50%가 비어 있으며 좋습니다. 하지만 평균 체인 길이는 매우 깁니다(65,536). 이것은 중복 값이 많다는 것을 나타냅니다. 따라서 이 경우 비클러스터형 해시 인덱스를 사용하는 것은 적합하지 않습니다. 대신 비클러스터형 인덱스를 사용해야 합니다.  
  
-   IX_OrderSequence: 버킷의 0%는 비어 있으며 너무 낮습니다. 또한 평균 체인 길이는 8입니다. 이 인덱스에서 값이 고유하므로 이것은 평균 8개의 값이 각 버킷에 매핑됨을 의미합니다. 버킷 수를 늘려야 합니다. 인덱스 키에 262,144개의 고유한 값이 있으므로 버킷 수가 적어도 262,144개가 되어야 합니다. 향후에 더 성장할 것으로 예상된다면 수를 더 높여야 합니다.  
  
-   기본 키 인덱스 (PK__SalesOrder ...): 버킷의 36%가 비어 있으며이는 정상입니다. 또한 평균 체인 길이가 1이면 좋습니다. 변경할 필요 없습니다.  
  
 메모리 최적화 해시 인덱스 문제 해결에 대한 자세한 내용은 [Troubleshooting Common Performance Problems with Memory-Optimized Hash Indexes](../../2014/database-engine/troubleshooting-common-performance-problems-with-memory-optimized-hash-indexes.md)을 참조하세요.  
  
## <a name="detailed-considerations-for-further-optimization"></a>추가 최적화에 대한 세부 고려 사항  
 이 섹션에서는 버킷 수를 최적화하기 위한 추가 고려 사항을 설명합니다.  
  
 해시 인덱스에서 최상의 성능을 얻으려면 해시 테이블에 할당된 메모리 크기와 인덱스 키에 있는 고유 값의 수가 균형을 이루어야 합니다. 다음과 같이 포인트 조회 및 테이블 검색의 성능도 서로 균형을 이루어야 합니다.  
  
-   버킷 수 값이 높을수록 인덱스에 있을 빈 버킷 수가 더 많아집니다. 각 버킷은 테이블 검색의 일부로 검색되므로 이것은 메모리 사용(버킷당 8바이트)과 테이블 검색 성능에 영향을 미칩니다.  
  
-   버킷 수가 낮을 수록 단일 버킷에 더 많은 값이 할당됩니다. 이렇게 하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 이 검색 조건자에 지정된 값을 찾기 위해 단일 버킷에 여러 값을 순환해야 할 수 있으므로 포인트 조회와 삽입 성능이 줄어듭니다.  
  
 버킷 수가 고유한 인덱스 키 수에 비해 지나치게 적으면 각 버킷에 많은 값이 매핑됩니다. 이로 인해 특히 포인트 조회(개별 인덱스 키의 조회) 및 삽입과 같은 대부분의 DML 작업 성능이 저하됩니다. 예를 들어, WHERE 절에 인덱스 키 열과 일치하는 같음 조건자를 사용하면 UPDATE 및 DELETE 작업과 SELECT 쿼리의 성능이 저하될 수 있습니다. 데이터베이스 시작 시 인덱스가 재생성되므로 버킷 수가 적어도 데이터베이스의 복구 시간에 영향이 있습니다.  
  
### <a name="duplicate-index-key-values"></a>중복된 인덱스 키 값  
 중복 값이 해시 충돌 성능에 미치는 영향이 커질 수 있습니다. 일반적으로 각 인덱스 키에 포함된 중복 항목 수가 적으므로 문제가 되지 않습니다. 하지만 고유한 인덱스 키 수와 테이블 행 수의 차이가 너무 크면 문제가 될 수 있습니다.  
  
 동일한 인덱스 키가 있는 모든 행은 동일한 중복 체인으로 이동합니다. 해시 충돌로 인해 동일한 버킷에 여러 인덱스 키가 있으면 인덱스 스캐너에서 첫 번째 값의 전체 중복 체인을 검색한 다음에야 두 번째 값에 해당하는 첫 번째 행을 찾을 수 있습니다. 또한 중복 키를 사용하면 가비지 컬렉션에서 행을 찾기 더 어려워집니다. 예를 들어 특정 키에 대해 중복이 1000개 있고 행 중 하나가 삭제된 경우 가비지 수집기에서 1000개의 중복 체인을 검색하여 인덱스에서 행의 연결을 해제해야 합니다. 이는 가비지 수집기가 모든 인덱스에서 연결을 해제해야 하므로 삭제된 행을 찾은 쿼리가 더 효율적인 인덱스(기본 키 인덱스)를 사용하여 행을 찾은 경우에도 해당됩니다.  
  
 해시 인덱스의 경우 중복 인덱스 키 값에 의해 발생하는 작업을 줄이는 방법에는 두 가지가 있습니다.  
  
-   대신 비클러스터형 인덱스를 사용합니다. 애플리케이션을 변경하지 않고도 인덱스 키에 열을 추가하여 중복을 줄일 수 있습니다.  
  
-   인덱스에 대해 매우 높은 버킷 수를 지정합니다. 예를 들어, 고유 인덱스 키 수의 20-100배로 지정합니다. 이렇게 하면 해시 충돌이 줄어듭니다.  
  
### <a name="small-tables"></a>작은 테이블  
 작은 테이블의 경우 인덱스의 크기가 전체 데이터베이스 크기에 비해 작으므로 일반적으로 메모리 사용률은 문제가 되지 않습니다.  
  
 이제 원하는 성능에 따라 항목을 선택해야 합니다.  
  
-   인덱스에서 성능이 중요한 작업이 주로 포인트 조회 및/또는 삽입 작업인 경우 높은 버킷 수가 해시 충돌 가능성을 줄이므로 적합합니다. 행 수의 3배 이상이 가장 좋습니다.  
  
-   성능이 중요한 작업이 전체 인덱스 검색인 경우 실제 인덱스 키 값 수에 가까운 버킷 수를 사용합니다.  
  
### <a name="big-tables"></a>큰 테이블  
 큰 테이블의 경우 메모리 사용률이 관심사가 될 수 있습니다. 예를 들어 4 개의 해시 인덱스가 있는 2억5000만 행 테이블을 사용 하는 경우 각각의 버킷 수가 10억 인 경우 해시 테이블에 대 한 오버 헤드는 4 개의 인덱스 \* * 10억 버킷 8 바이트 = 32 gb의 메모리 사용률입니다. 각 인덱스에 대해 2억 5천만 개의 버킷 수를 선택할 때 해시 테이블의 총 오버헤드는 8기가바이트가 됩니다. 이는 8 바이트의 메모리 사용량 외에도 각 인덱스는이 시나리오에서 8gb 인 각 개별 행에 추가 됩니다. 4 개의 인덱스 \* 8 바이트 \* 2억5000만 행입니다.  
  
 일반적으로 전체 테이블 검색은 OLTP 작업에서 성능이 중요한 경로에 해당되지 않습니다. 따라서 포인트 조회 및 삽입 작업 성능과 메모리 사용률 간에 다음과 같이 선택합니다.  
  
-   메모리 사용률이 중요한 경우 버킷 수를 인덱스 키 값 수에 가깝게 선택합니다. 버킷 수가 인덱스 키 값 수보다 너무 적으면 안 됩니다. 이 경우 대부분의 DML 작업과 서버 재시작 후 데이터베이스를 복구하는 시간에 영향이 있습니다.  
  
-   포인트 조회를 위해 성능을 최적화하는 경우 버킷 수를 고유한 인덱스 값 수보다 2-3배 많이 지정하는 것이 좋습니다. 버킷 수가 많다는 것은 메모리 사용률이 증가하고 전체 인덱스 검색에 필요한 시간이 증가한다는 것을 의미합니다.  
  
## <a name="see-also"></a>참고 항목  
 [메모리 액세스에 최적화된 테이블의 인덱스](../../2014/database-engine/indexes-on-memory-optimized-tables.md)  
  
  
