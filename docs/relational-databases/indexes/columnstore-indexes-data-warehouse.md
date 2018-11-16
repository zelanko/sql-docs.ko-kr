---
title: Columnstore 인덱스 - 데이터 웨어하우스 | Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 21fd153b-116d-47fc-a926-f1528299a391
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2ce64614e3c2f9d27bfafb9101e54ab49df2089e
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51672622"
---
# <a name="columnstore-indexes---data-warehouse"></a>Columnstore 인덱스 - 데이터 웨어하우스
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Columnstore 인덱스는 분할과 함께 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 웨어하우스를 만들기 위해 필수입니다.  
  
## <a name="whats-new"></a>새로운 기능  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 에서는 columnstore 성능 향상을 위해 다음 기능이 도입되었습니다.  
  
-   Always On은 읽기 가능 복제본에 대한 columnstore 인덱스 쿼리를 지원합니다.  
-   MARS(Multiple Active Result Sets)는 columnstore 인덱스를 지원합니다.  
-   새 동적 관리 뷰 [sys.dm_db_column_store_row_group_physical_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md)는 행 그룹 수준에서 성능 문제 해결 정보를 제공합니다.  
-   Columnstore 인덱스에 대한 단일 스레드 쿼리는 일괄 처리 모드에서 실행할 수 있습니다. 이전에는 다중 스레드 쿼리만이 일괄 처리 모드로 실행할 수 있었습니다.  
-   `SORT` 연산자는 일괄 처리 모드에서 실행됩니다.  
-   다중 `DISTINCT` 연산은 일괄 처리 모드에서 실행됩니다.  
-   이제 창 집계가 데이터베이스 호환성 수준 130 이상에서 일괄 처리 모드로 실행됩니다.  
-   효율적인 집계 처리를 위한 집계 푸시다운입니다. 이는 모든 데이터베이스 호환성 수준에서 지원됩니다.  
-   효율적인 문자열 조건자 처리를 위한 문자열 조건자 푸시다운입니다. 이는 모든 데이터베이스 호환성 수준에서 지원됩니다.  
-   데이터베이스 호환성 수준 130 이상에 대한 스냅숏 격리.  
  
## <a name="improve-performance-by-combining-nonclustered-and-columnstore-indexes"></a>비클러스터형과 columnstore 인덱스를 결합하여 성능 향상  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 클러스터형 columnstore 인덱스에 대해 비클러스터형 인덱스를 정의할 수 있습니다.   
  
### <a name="example-improve-efficiency-of-table-seeks-with-a-nonclustered-index"></a>예: 비클러스터형 인덱스를 사용하여 테이블 검색의 효율성 향상  
 데이터 웨어하우스에서 테이블 검색의 효율성을 개선하려면 테이블 검색을 사용할 때 가장 성능이 좋은 쿼리를 실행하도록 설계된 비클러스터형 인덱스를 만들 수 있습니다. 예를 들어, 일치하는 값을 찾고 작은 범위의 값을 반환하는 쿼리는 columnstore 인덱스보다 B-트리 인덱스에 대해 성능이 더 좋습니다. 왜냐하면 columnstore 인덱스를 통한 전체 테이블 검색이 필요하지 않으며 B-트리 인덱스를 통해 이진 검색을 수행하여 정확한 결과를 더 빠르게 반환하기 때문입니다.  
  
```sql  
--BASIC EXAMPLE: Create a nonclustered index on a columnstore table.  
  
--Create the table  
CREATE TABLE t_account (  
    AccountKey int NOT NULL,  
    AccountDescription nvarchar (50),  
    AccountType nvarchar(50),  
    UnitSold int  
);  
GO  
  
--Store the table as a columnstore.  
CREATE CLUSTERED COLUMNSTORE INDEX taccount_cci ON t_account;  
GO  
  
--Add a nonclustered index.  
CREATE UNIQUE INDEX taccount_nc1 ON t_account (AccountKey);  
```  
  
### <a name="example-use-a-nonclustered-index-to-enforce-a-primary-key-constraint-on-a-columnstore-table"></a>예: 비클러스터형 인덱스를 사용하여 columnstore 테이블에 기본 키 제약 조건 적용  
 기본적으로 columnstore 테이블은 기본 키 제약 조건을 허용하지 않습니다. 이제 columnstore 테이블에 비클러스터형 인덱스를 사용하여 기본 키 제약 조건을 적용할 수 있습니다. 기본 키는 NULL이 아닌 열에 대한 UNIQUE 제약 조건에 해당하며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 UNIQUE 제약 조건을 비클러스터형 인덱스로 구현합니다. 이러한 사실을 결합하여 다음 예제에서는 NULL이 아닌 열 accountkey에 대해 UNIQUE 제약 조건을 정의합니다. 그 결과는 NULL이 아닌 열에 대한 UNIQUE 제약 조건으로 기본 키 제약 조건을 적용하는 비클러스터형 인덱스입니다.  
  
 다음으로, 테이블을 클러스터형 columnstore 인덱스로 변환합니다. 변환 중에 비클러스터형 인덱스는 유지됩니다. 그 결과는 기본 키 제약 조건을 적용하는 비클러스터형 인덱스를 포함한 클러스터형 columnstore 인덱스입니다. Columnstore 테이블에 대한 업데이트 또는 삽입은 비클러스터형 인덱스에도 영향을 미치므로 UNIQUE 제약 조건 및 비 NULL을 위반하는 모든 연산은 전체 연산을 실패하게 만듭니다.  
  
 그 결과는 두 인덱스에 대해 모두 기본 키 제약 조건을 적용하는 비클러스터형 인덱스를 포함한 columnstore 인덱스입니다.  
  
```sql 
--EXAMPLE: Enforce a primary key constraint on a columnstore table.   
  
--Create a rowstore table with a unique constraint.  
--The unique constraint is implemented as a nonclustered index.  
CREATE TABLE t_account (  
    AccountKey int NOT NULL,  
    AccountDescription nvarchar (50),  
    AccountType nvarchar(50),  
    UnitSold int,  
  
    CONSTRAINT uniq_account UNIQUE (AccountKey)  
);  
  
--Store the table as a columnstore.   
--The unique constraint is preserved as a nonclustered index on the columnstore table.  
CREATE CLUSTERED COLUMNSTORE INDEX t_account_cci ON t_account  
  
--By using the previous two steps, every row in the table meets the UNIQUE constraint  
--on a non-NULL column.  
--This has the same end-result as having a primary key constraint  
--All updates and inserts must meet the unique constraint on the nonclustered index or they will fail.  
  
--If desired, add a foreign key constraint on AccountKey.  
  
ALTER TABLE [dbo].[t_account]  
WITH CHECK ADD FOREIGN KEY([AccountKey]) REFERENCES my_dimension(Accountkey); 
```  
  
### <a name="improve-performance-by-enabling-row-level-and-row-group-level-locking"></a>행 수준 및 행 그룹 수준의 잠금을 사용하여 성능 개선  
 Columnstore 인덱스 기능에 대한 비클러스터형 인덱스를 보완하기 위해 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 는 선택, 업데이트 및 삭제 연산에 대해 세분화된 잠금 기능을 제공합니다. 쿼리는 비클러스터형 인덱스에 대한 인덱스 검색에 행 수준 잠금을 사용하고 columnstore 인덱스에 대한 전체 테이블 검색에 행 그룹 수준 잠금을 실행할 수 있습니다. 이 특성을 통해 행 수준 및 행 그룹 수준 잠금을 적절히 사용하여 더 높은 읽기/쓰기 동시성을 달성합니다.  
  
```sql  
--Granular locking example  
--Store table t_account as a columnstore table.  
CREATE CLUSTERED COLUMNSTORE INDEX taccount_cci ON t_account  
GO  
  
--Add a nonclustered index for use with this example  
CREATE UNIQUE INDEX taccount_nc1 ON t_account (AccountKey);  
GO  
  
--Look at locking with access through the nonclustered index  
SET TRANSACTION ISOLATION LEVEL repeatable read;  
GO  
  
BEGIN TRAN  
    -- The query plan chooses a seek operation on the nonclustered index  
    -- and takes the row lock  
    SELECT * FROM t_account WHERE AccountKey = 100;  
END TRAN  
```  
  
### <a name="snapshot-isolation-and-read-committed-snapshot-isolations"></a>스냅숏 격리 및 커밋된 읽기 스냅숏 격리  
 트랜잭션 일관성을 보장하려면 스냅숏 격리(SI)를 사용하고 columnstore 인덱스에 대한 쿼리의 문 수준 일관성을 보장하려면 커밋된 읽기 스냅숏 격리(RCSI)를 사용합니다. 이렇게 하면 데이터 기록기를 차단하지 않고 쿼리를 실행할 수 있습니다. 이 비차단 동작 덕분에 복잡한 트랜잭션에 대한 교착 상태의 가능성이 크게 줄어듭니다. 자세한 내용은 MSDN의 [SQL Server에서의 스냅숏 격리](https://msdn.microsoft.com/library/tcbchxcb\(v=vs.110\).aspx) 를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Columnstore 인덱스 디자인 지침](../../relational-databases/indexes/columnstore-indexes-design-guidance.md)   
 [Columnstore 인덱스 데이터 로드 지침](../../relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)   
 [Columnstore 인덱스 쿼리 성능](../../relational-databases/indexes/columnstore-indexes-query-performance.md)   
 [실시간 운영 분석을 위한 Columnstore 시작](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
 [Columnstore 인덱스 조각 모음](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)  
 [Columnstore 인덱스 아키텍처](../../relational-databases/sql-server-index-design-guide.md#columnstore_index) 
  
