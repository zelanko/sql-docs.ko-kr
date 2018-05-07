---
title: Linux에서 SQL Server의 성능 기능을 시작 | Microsoft Docs
description: 이 문서에서는 SQL Server를 처음 접하는 Linux 사용자에 대 한 SQL Server 성능 기능을 소개 합니다. 이러한 예 중 많은 모든 플랫폼에서 작동 하지만이 문서의 컨텍스트가 Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.component: ''
ms.suite: sql
ms.technology: database-engine
ms.assetid: 60036d26-4797-4872-9a9e-3552841c61be
ms.custom: sql-linux
ms.openlocfilehash: c5a7ec490d1474fc80dd1574cbd6b4c96fe97aef
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="walkthrough-for-the-performance-features-of-sql-server-on-linux"></a>Linux에서 SQL Server의 성능 기능에 대 한 연습

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server에 새로운 Linux 사용자 인 경우 다음 작업에 관한 일부의 성능 기능입니다. 이러한 설정은 고유 하거나 Linux 특정 아니지만 알 수 있는 영역의 추가로 조사를 수행 하는 데 도움이 됩니다. 각 예제에 해당 영역에 대 한 깊이 설명서에는 링크가 제공 됩니다.

> [!NOTE]
> 다음 예제에서는 AdventureWorks 샘플 데이터베이스를 사용합니다. 이 예제 데이터베이스를 설치 하는 방법에 지침은 [Linux에 Windows에서 SQL Server 데이터베이스를 복원](sql-server-linux-migrate-restore-database.md)합니다.

## <a name="create-a-columnstore-index"></a>Columnstore 인덱스 만들기
Columnstore 인덱스는 저장 하 고 큰 columnstore 라는 칼럼 데이터 형식으로 데이터 저장소를 쿼리 하는 기술입니다.  

1. 다음 TRANSACT-SQL 명령을 실행 하 여 SalesOrderDetail 테이블에 Columnstore 인덱스를 추가 합니다.

   ```sql
   CREATE NONCLUSTERED COLUMNSTORE INDEX [IX_SalesOrderDetail_ColumnStore]
      ON Sales.SalesOrderDetail
      (UnitPrice, OrderQty, ProductID)
   GO
   ```

2. Columnstore 인덱스를 사용 하 여 테이블 검색에 다음 쿼리를 실행 합니다.

   ```sql
   SELECT ProductID, SUM(UnitPrice) SumUnitPrice, AVG(UnitPrice) AvgUnitPrice,
      SUM(OrderQty) SumOrderQty, AVG(OrderQty) AvgOrderQty
   FROM Sales.SalesOrderDetail
      GROUP BY ProductID
      ORDER BY ProductID
   ```

3. Columnstore 인덱스에 대 한 object_id를 조회할 및 SalesOrderDetail 테이블에 대 한 사용량 통계에 나타나는지 확인 하 여 Columnstore 인덱스를 사용 했는지 확인 합니다.

   ```sql
   SELECT * FROM sys.indexes WHERE name = 'IX_SalesOrderDetail_ColumnStore'
   GO

   SELECT * 
   FROM sys.dm_db_index_usage_stats
      WHERE database_id = DB_ID('AdventureWorks')
      AND object_id = OBJECT_ID('AdventureWorks.Sales.SalesOrderDetail');
   ```
   
## <a name="use-in-memory-oltp"></a>메모리 내 OLTP를 사용 하 여
SQL Server 응용 프로그램 시스템의 성능을 크게 향상 시킬 수 있는 메모리 내 OLTP 기능을 제공 합니다.  평가 가이드의이 섹션은 메모리와 컴파일하거나 해석할 필요 없이 테이블에 액세스할 수 있는 고유 하 게 컴파일된 저장된 프로시저에 저장 되는 메모리 액세스에 최적화 된 테이블을 만드는 단계를 안내 합니다.

### <a name="configure-database-for-in-memory-oltp"></a>메모리 내 OLTP에 대 한 데이터베이스를 구성 합니다.
1. 데이터베이스 호환성 수준을 메모리 내 OLTP를 사용 하려면 적어도 130 이상으로 설정 하는 것이 좋습니다.  다음 쿼리를 사용 하 여 AdventureWorks의 현재 호환성 수준을 확인 하려면:  

   ```sql
   USE AdventureWorks
   GO
   SELECT d.compatibility_level
   FROM sys.databases as d
     WHERE d.name = Db_Name();
   GO
   ```
   
   필요한 경우 수준을 130으로 업데이트 합니다.

   ```sql
   ALTER DATABASE CURRENT
   SET COMPATIBILITY_LEVEL = 130;
   GO
   ```

2. 트랜잭션이 모두 디스크 기반 테이블 및 메모리 액세스에 최적화 된 테이블을 포함 하는 경우의 필수적이 지는 메모리 액세스에 최적화 된 트랜잭션 부분은 트랜잭션 격리 수준에서 작동 하는 SNAPSHOT을 이라고 합니다.  컨테이너 간 트랜잭션에서 메모리 액세스에 최적화 된 테이블에 대 한이 수준의 안정적으로 적용 하려면 다음을 실행 합니다.

   ```sql
   ALTER DATABASE CURRENT SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON
   GO
   ```

3. 만들려면 먼저 메모리 액세스에 최적화 된 파일 그룹 및 데이터 파일에 대 한 컨테이너 먼저 메모리 액세스에 최적화 된 테이블을 만듭니다.

   ```sql
   ALTER DATABASE AdventureWorks ADD FILEGROUP AdventureWorks_mod CONTAINS memory_optimized_data
   GO  
   ALTER DATABASE AdventureWorks ADD FILE (NAME='AdventureWorks_mod', FILENAME='/var/opt/mssql/data/AdventureWorks_mod') TO FILEGROUP AdventureWorks_mod
   GO
   ```

### <a name="create-a-memory-optimized-table"></a>메모리 액세스에 최적화 된 테이블 만들기
메모리 액세스에 최적화 된 테이블에 대 한 기본 저장소를 주 메모리과 디스크 기반 테이블과 달리 데이터 하지 않아도에서 메모리 버퍼에 디스크에서 읽을 수 있습니다.  메모리 액세스에 최적화 된 테이블을 만들려면 사용는 MEMORY_OPTIMIZED = ON 절.

1. 메모리 액세스에 최적화 된 테이블 dbo를 만들려면 다음 쿼리를 실행 합니다. ShoppingCart 합니다.  기본적으로 데이터는 내구성 목적 (내구성도 스키마만 유지 하도록 설정할 수 있는 참고) 디스크에 유지 됩니다. 

   ```sql
   CREATE TABLE dbo.ShoppingCart ( 
   ShoppingCartId INT IDENTITY(1,1) PRIMARY KEY NONCLUSTERED,
   UserId INT NOT NULL INDEX ix_UserId NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000), 
   CreatedDate DATETIME2 NOT NULL, 
   TotalPrice MONEY
   ) WITH (MEMORY_OPTIMIZED=ON) 
   GO
   ```

2. 테이블에 일부 레코드를 삽입 합니다.

   ```sql
   INSERT dbo.ShoppingCart VALUES (8798, SYSDATETIME(), NULL) 
   INSERT dbo.ShoppingCart VALUES (23, SYSDATETIME(), 45.4) 
   INSERT dbo.ShoppingCart VALUES (80, SYSDATETIME(), NULL) 
   INSERT dbo.ShoppingCart VALUES (342, SYSDATETIME(), 65.4) 
   ```

### <a name="natively-compiled-stored-procedure"></a>고유 하 게 컴파일된 저장 프로시저
SQL Server 메모리 액세스에 최적화 된 테이블에 액세스 하는 고유 하 게 컴파일된 저장된 프로시저를 지원 합니다. T-SQL 문이 기계어 코드로 컴파일되고 빠른 데이터 액세스와 일반 T-SQL 보다 더 효율적인 쿼리 실행을 사용 하도록 설정 하는 네이티브 Dll로 저장 됩니다.   NATIVE_COMPILATION으로 표시된 저장 프로시저는 고유하게 컴파일됩니다. 

1. ShoppingCart 테이블에 많은 수의 레코드를 삽입 하는 고유 하 게 컴파일된 저장된 프로시저를 만들려면 다음 스크립트를 실행 합니다.


   ```sql
   CREATE PROCEDURE dbo.usp_InsertSampleCarts @InsertCount int 
    WITH NATIVE_COMPILATION, SCHEMABINDING AS 
   BEGIN ATOMIC 
   WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')

   DECLARE @i int = 0

   WHILE @i < @InsertCount 
    BEGIN 
     INSERT INTO dbo.ShoppingCart VALUES (1, SYSDATETIME() , NULL) 
     SET @i += 1 
    END
   END 
   ```
2. 1000000 행을 삽입 합니다.

   ```sql
   EXEC usp_InsertSampleCarts 1000000 
   ```

3. 삽입 된 행을 확인 합니다.

   ```sql
   SELECT COUNT(*) FROM dbo.ShoppingCart 
   ```

### <a name="learn-more-about-in-memory-oltp"></a>메모리 내 OLTP에 대 한 자세한 정보
메모리 내 OLTP에 대 한 자세한 내용은 다음 항목을 참조 합니다.

- [빠른 시작 1: 더 빠른 Transact-SQL 성능을 위한 메모리 내 OLTP 기술](../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md)
- [메모리 내 OLTP로 마이그레이션](../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)
- [메모리 최적화를 사용한 더 빠른 임시 테이블 및 테이블 변수](../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)
- [메모리 사용량 모니터링 및 문제 해결](../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md)
- [메모리 내 OLTP(메모리 내 최적화)](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)

## <a name="use-query-store"></a>쿼리 저장소 사용
쿼리 저장소는 쿼리, 실행 계획 및 런타임 통계에 대 한 자세한 성능 정보를 수집합니다.

쿼리 저장소는 기본적으로 활성화 되어 있으며 ALTER DATABASE를 사용 설정할 수 있습니다.

   ```sql
   ALTER DATABASE AdventureWorks SET QUERY_STORE = ON;
   ```

쿼리 저장소에 쿼리 및 계획에 대 한 정보를 반환한 다음 쿼리를 실행 합니다. 

   ```sql
   SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*
   FROM sys.query_store_plan AS Pl
      JOIN sys.query_store_query AS Qry
         ON Pl.query_id = Qry.query_id
      JOIN sys.query_store_query_text AS Txt
         ON Qry.query_text_id = Txt.query_text_id ;
   ```

## <a name="query-dynamic-management-views"></a>쿼리 동적 관리 뷰
동적 관리 뷰는 서버 인스턴스의 상태를 모니터링, 문제를 진단 및 성능 튜닝에 사용할 수 있는 서버 상태 정보를 반환 합니다.

Dm_os_wait stats 동적 관리 뷰를 쿼리 합니다 하:

   ```sql
   SELECT wait_type, wait_time_ms
   FROM sys.dm_os_wait_stats;
   ```
