---
title: Linux의 SQL Server 성능 기능 시작
description: 이 문서에서는 SQL Server를 처음 접하는 Linux 사용자를 위한 SQL Server 성능 기능을 소개합니다. 이러한 예제 대부분은 모든 플랫폼에서 작동하지만 이 문서에서는 Linux 컨텍스트를 다룹니다.
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 60036d26-4797-4872-9a9e-3552841c61be
ms.openlocfilehash: fe60b00654d93c6362a8671318a4b7b88ae90a5f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67896158"
---
# <a name="walkthrough-for-the-performance-features-of-sql-server-on-linux"></a>Linux의 SQL Server 성능 기능 연습

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server를 처음 사용하는 Linux 사용자인 경우 다음 작업에서 몇 가지 성능 기능을 안내합니다. 이 보안 작업은 Linux에 고유하거나 특정하지 않으며 추가로 조사할 영역에 대한 아이디어를 제공하는 데 도움이 됩니다. 각 예제에서는 해당 영역의 심층 설명서에 대한 링크가 제공됩니다.

> [!NOTE]
> 다음 예제에서는 AdventureWorks 샘플 데이터베이스를 사용합니다. 이 샘플 데이터베이스를 구하여 설치하는 방법에 대한 지침은 [Windows에서 Linux로 SQL Server 데이터베이스 복원](sql-server-linux-migrate-restore-database.md)을 참조하세요.

## <a name="create-a-columnstore-index"></a>Columnstore 인덱스 만들기
Columnstore 인덱스는 columnstore라는 열 데이터 형식의 대규모 데이터 저장 영역을 저장 및 쿼리하는 기술입니다.  

1. 다음 Transact-SQL 명령을 실행하여 SalesOrderDetail 테이블에 Columnstore 인덱스를 추가합니다.

   ```sql
   CREATE NONCLUSTERED COLUMNSTORE INDEX [IX_SalesOrderDetail_ColumnStore]
      ON Sales.SalesOrderDetail
      (UnitPrice, OrderQty, ProductID)
   GO
   ```

2. Columnstore 인덱스를 사용하여 테이블을 검색하는 다음 쿼리를 실행합니다.

   ```sql
   SELECT ProductID, SUM(UnitPrice) SumUnitPrice, AVG(UnitPrice) AvgUnitPrice,
      SUM(OrderQty) SumOrderQty, AVG(OrderQty) AvgOrderQty
   FROM Sales.SalesOrderDetail
      GROUP BY ProductID
      ORDER BY ProductID
   ```

3. Columnstore 인덱스의 object_id를 조회하고 SalesOrderDetail 테이블의 사용 통계에 표시되는지 확인하여 Columnstore 인덱스를 사용했는지 검토합니다.

   ```sql
   SELECT * FROM sys.indexes WHERE name = 'IX_SalesOrderDetail_ColumnStore'
   GO

   SELECT * 
   FROM sys.dm_db_index_usage_stats
      WHERE database_id = DB_ID('AdventureWorks')
      AND object_id = OBJECT_ID('AdventureWorks.Sales.SalesOrderDetail');
   ```
   
## <a name="use-in-memory-oltp"></a>메모리 내 OLTP 사용
SQL Server는 애플리케이션 시스템의 성능을 크게 향상시킬 수 있는 메모리 내 OLTP 기능을 제공합니다.  평가 가이드의 이 섹션에서는 메모리에 저장된 메모리 최적화 테이블과 컴파일 또는 해석 없이 테이블에 액세스할 수 있는 고유하게 컴파일된 저장 프로시저를 만드는 단계를 안내합니다.

### <a name="configure-database-for-in-memory-oltp"></a>메모리 내 OLTP에 대한 데이터베이스 구성
1. 메모리 내 OLTP를 사용하려면 최소 130의 호환성 수준으로 데이터베이스를 설정하는 것이 좋습니다.  AdventureWorks의 현재 호환성 수준을 확인하려면 다음 쿼리를 사용합니다.  

   ```sql
   USE AdventureWorks
   GO
   SELECT d.compatibility_level
   FROM sys.databases as d
     WHERE d.name = Db_Name();
   GO
   ```
   
   필요한 경우 이 수준을 130으로 업데이트합니다.

   ```sql
   ALTER DATABASE CURRENT
   SET COMPATIBILITY_LEVEL = 130;
   GO
   ```

2. 트랜잭션이 디스크 기반 테이블 및 메모리 최적화 테이블과 관련된 경우, 이러한 트랜잭션에서 메모리 최적화 트랜잭션 부분은 SNAPSHOT이라고 하는 트랜잭션 격리 수준에서 작동해야 합니다.  컨테이너 간 트랜잭션에서 메모리 최적화 테이블에 대해 이 수준을 안정적으로 적용하려면 다음을 실행합니다.

   ```sql
   ALTER DATABASE CURRENT SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON
   GO
   ```

3. 메모리 최적화 테이블을 만들려면 먼저, 데이터 파일에 대해 메모리 최적화 FILEGROUP과 컨테이너를 만들어야 합니다.

   ```sql
   ALTER DATABASE AdventureWorks ADD FILEGROUP AdventureWorks_mod CONTAINS memory_optimized_data
   GO  
   ALTER DATABASE AdventureWorks ADD FILE (NAME='AdventureWorks_mod', FILENAME='/var/opt/mssql/data/AdventureWorks_mod') TO FILEGROUP AdventureWorks_mod
   GO
   ```

### <a name="create-a-memory-optimized-table"></a>메모리 최적화 테이블 만들기
메모리 최적화 테이블의 기본 저장소는 주 메모리이므로 디스크 기반 테이블과 달리 디스크에서 메모리 버퍼로 데이터를 읽을 필요가 없습니다.  메모리 최적화 테이블을 만들려면 MEMORY_OPTIMIZED = ON 절을 사용합니다.

1. 다음 쿼리를 실행하여 메모리 최적화 테이블 dbo.ShoppingCart를 만듭니다.  기본적으로 데이터는 내구성을 위해 디스크에 유지됩니다(스키마만 유지하도록 내구성을 설정할 수도 있음). 

   ```sql
   CREATE TABLE dbo.ShoppingCart ( 
   ShoppingCartId INT IDENTITY(1,1) PRIMARY KEY NONCLUSTERED,
   UserId INT NOT NULL INDEX ix_UserId NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000), 
   CreatedDate DATETIME2 NOT NULL, 
   TotalPrice MONEY
   ) WITH (MEMORY_OPTIMIZED=ON) 
   GO
   ```

2. 테이블에 레코드를 삽입합니다.

   ```sql
   INSERT dbo.ShoppingCart VALUES (8798, SYSDATETIME(), NULL) 
   INSERT dbo.ShoppingCart VALUES (23, SYSDATETIME(), 45.4) 
   INSERT dbo.ShoppingCart VALUES (80, SYSDATETIME(), NULL) 
   INSERT dbo.ShoppingCart VALUES (342, SYSDATETIME(), 65.4) 
   ```

### <a name="natively-compiled-stored-procedure"></a>고유하게 컴파일된 저장 프로시저
SQL Server는 메모리 최적화 테이블에 액세스하는 고유하게 컴파일된 저장 프로시저를 지원합니다. T-SQL 문은 기계어 코드로 컴파일되고 네이티브 DLL로 저장되므로 기존 T-SQL보다 더 빠르게 데이터에 액세스하고 보다 효율적으로 쿼리를 실행할 수 있습니다.   NATIVE_COMPILATION으로 표시된 저장 프로시저는 고유하게 컴파일됩니다. 

1. 다음 스크립트를 실행하여 ShoppingCart 테이블에 많은 수의 레코드를 삽입하는 고유하게 컴파일된 저장 프로시저를 만듭니다.


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
2. 100만개의 행을 삽입하려면 다음을 실행합니다.

   ```sql
   EXEC usp_InsertSampleCarts 1000000 
   ```

3. 다음과 같이 행이 삽입되었는지 확인합니다.

   ```sql
   SELECT COUNT(*) FROM dbo.ShoppingCart 
   ```

### <a name="learn-more-about-in-memory-oltp"></a>메모리 내 OLTP에 대한 자세한 정보
메모리 내 OLTP에 대한 자세한 내용은 다음 항목을 참조하세요.

- [빠른 시작 1: 더 빠른 Transact-SQL 성능을 위한 메모리 내 OLTP 기술](../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md)
- [메모리 내 OLTP로 마이그레이션](../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)
- [메모리 최적화를 사용한 더 빠른 임시 테이블 및 테이블 변수](../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)
- [메모리 사용량 모니터링 및 문제 해결](../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md)
- [메모리 내 OLTP(메모리 내 최적화)](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)

## <a name="use-query-store"></a>쿼리 저장소 사용
쿼리 저장소는 쿼리, 실행 계획 및 런타임 통계에 대한 자세한 성능 정보를 수집합니다.

쿼리 저장소는 기본적으로 활성화되어 있지 않으며 ALTER DATABASE를 사용하여 사용하도록 설정할 수 있습니다.

   ```sql
   ALTER DATABASE AdventureWorks SET QUERY_STORE = ON;
   ```

다음 쿼리를 실행하여 쿼리 저장소의 쿼리 및 계획에 대한 정보를 반환합니다. 

   ```sql
   SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*
   FROM sys.query_store_plan AS Pl
      JOIN sys.query_store_query AS Qry
         ON Pl.query_id = Qry.query_id
      JOIN sys.query_store_query_text AS Txt
         ON Qry.query_text_id = Txt.query_text_id ;
   ```

## <a name="query-dynamic-management-views"></a>쿼리 동적 관리 뷰
동적 관리 뷰는 서버 인스턴스 상태 모니터링, 문제 진단 및 성능 튜닝에 사용할 수 있는 서버 상태 정보를 반환합니다.

dm_os_wait stats 동적 관리 뷰를 쿼리하려면 다음을 실행합니다.

   ```sql
   SELECT wait_type, wait_time_ms
   FROM sys.dm_os_wait_stats;
   ```
