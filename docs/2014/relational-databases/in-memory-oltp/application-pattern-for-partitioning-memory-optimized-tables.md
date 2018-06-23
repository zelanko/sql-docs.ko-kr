---
title: 메모리 액세스에 최적화된 테이블 분할을 위한 응용 프로그램 패턴 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3f867763-a8e6-413a-b015-20e9672cc4d1
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: ef7be1ca170df9efb0a4b76ab4b7f451b6742dbf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172407"
---
# <a name="application-pattern-for-partitioning-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블 분할을 위한 응용 프로그램 패턴
  
            [!INCLUDE[hek_2](../../includes/hek-2-md.md)]는 디스크에서 자주 액세스하지 않는 데이터를 처리하는 동안 제한된 양의 활성 데이터를 메모리 최적화 테이블에 유지하는 패턴을 지원합니다. 일반적으로 것 데이터가 저장 되는 시나리오에 따라는 `datetime` 키입니다.  
  
 분할된 테이블과 메모리 최적화 테이블을 공통 스키마로 유지하여 분할된 테이블을 메모리 최적화 테이블로 에뮬레이트할 수 있습니다. 현재 데이터는 메모리 최적화 테이블에 삽입되고 업데이트되는 반면, 자주 액세스하지 않는 데이터는 기존의 분할된 테이블에 유지됩니다.  
  
 활성 데이터가 메모리 최적화 테이블에 있음을 알고 있는 응용 프로그램은 고유하게 컴파일된 저장 프로시저를 사용하여 데이터에 액세스할 수 있습니다. 전체 데이터에 액세스해야 하거나 어떤 테이블에 관련 데이터가 유지되는지 모를 수 있는 작업은 해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 메모리 최적화 테이블을 분할된 테이블과 조인합니다.  
  
 이 파티션 전환은 다음과 같이 설명됩니다.  
  
-   메모리 내 OLTP 테이블의 데이터를 준비 테이블에 삽입합니다. 가능하면 구분 날짜를 사용합니다.  
  
-   메모리 최적화 테이블에서 같은 데이터를 삭제합니다.  
  
-   준비 테이블을 전환합니다.  
  
-   활성 파티션을 추가합니다.  
  
 ![파티션 전환.](../../database-engine/media/hekaton-partitioned-tables.gif "파티션 전환.")  
활성 데이터 유지 관리  
  
 데이터 삭제와 준비 테이블 전환 사이의 시간 중에 누락된 데이터 쿼리가 수행되지 않도록 하려면 활성 주문 삭제로 시작되는 작업을 유지 관리 시간 중에 수행해야 합니다.  
  
 관련 샘플을 보려면 [응용 프로그램 수준 분할](application-level-partitioning.md)을 참조하세요.  
  
## <a name="code-sample"></a>코드 예제  
 다음 예제에서는 분할된 디스크 기반 테이블과 함께 메모리 최적화 테이블을 사용하는 방법을 보여 줍니다. 자주 사용되는 데이터는 메모리에 저장됩니다. 데이터를 디스크에 저장하려면 새 파티션을 만들고 분할된 테이블에 데이터를 복사합니다.  
  
 이 예제의 첫 번째 부분에서는 데이터베이스와 필요한 개체를 만듭니다. 예제의 두 번째 부분에서는 메모리 최적화 테이블에서 분할된 테이블로 데이터를 이동하는 방법을 보여 줍니다.  
  
```tsql  
CREATE DATABASE partitionsample;  
GO  
  
-- enable for In-Memory OLTP - change file path as needed  
ALTER DATABASE partitionsample ADD FILEGROUP partitionsample_mod CONTAINS MEMORY_OPTIMIZED_DATA  
ALTER DATABASE partitionsample ADD FILE( NAME = 'partitionsample_mod' , FILENAME = 'c:\data\partitionsample_mod') TO FILEGROUP partitionsample_mod;  
GO  
  
USE partitionsample;  
GO  
  
-- frequently used portion of the SalesOrders - memory-optimized  
  
CREATE TABLE dbo.SalesOrders_hot (  
   so_id INT IDENTITY PRIMARY KEY NONCLUSTERED,  
   cust_id INT NOT NULL,  
   so_date DATETIME2 NOT NULL INDEX ix_date NONCLUSTERED,  
   so_total MONEY NOT NULL,  
   INDEX ix_date_total NONCLUSTERED (so_date desc, so_total desc)  
) WITH (MEMORY_OPTIMIZED=ON)  
GO  
  
-- cold portion of the SalesOrders - partitioned disk-based table  
CREATE PARTITION FUNCTION [ByDatePF](datetime2) AS RANGE RIGHT   
   FOR VALUES();  
GO  
  
CREATE PARTITION SCHEME [ByDateRange]   
   AS PARTITION [ByDatePF]   
   ALL TO ([PRIMARY]);  
GO  
  
CREATE TABLE dbo.SalesOrders_cold (  
   so_id INT NOT NULL,  
   cust_id INT NOT NULL,  
   so_date DATETIME2 NOT NULL,  
   so_total MONEY NOT NULL,  
   CONSTRAINT PK_SalesOrders_cold PRIMARY KEY (so_id, so_date),  
   INDEX ix_date_total NONCLUSTERED (so_date desc, so_total desc)  
) ON [ByDateRange](so_date)  
GO  
  
-- table for temporary partitions  
CREATE TABLE dbo.SalesOrders_cold_staging (  
   so_id INT NOT NULL,  
   cust_id INT NOT NULL,  
   so_date datetime2 NOT NULL,  
   so_total MONEY NOT NULL,  
   CONSTRAINT PK_SalesOrders_cold_staging PRIMARY KEY (so_id, so_date),  
   INDEX ix_date_total NONCLUSTERED (so_date desc, so_total desc),  
   CONSTRAINT CHK_SalesOrders_cold_staging CHECK (so_date >= '1900-01-01')  
)  
GO  
  
-- aggregate view of the hot and cold data  
CREATE VIEW dbo.SalesOrders  
AS SELECT so_id,  
   cust_id,  
   so_date,  
   so_total,  
   1 AS 'is_hot'  
   FROM dbo.SalesOrders_hot  
   UNION ALL  
   SELECT so_id,  
          cust_id,  
          so_date,  
          so_total,  
          0 AS 'is_hot'  
          FROM dbo.SalesOrders_cold;  
GO  
  
-- move all sales orders up to the split date to cold storage  
CREATE PROCEDURE dbo.usp_SalesOrdersOffloadToCold @splitdate datetime2  
   AS  
   BEGIN  
      BEGIN TRANSACTION;  
      -- create new heap based on the hot data to be moved to cold storage  
      INSERT INTO dbo.SalesOrders_cold_staging WITH( TABLOCKX)  
      SELECT so_id , cust_id , so_date , so_total  
         FROM dbo.SalesOrders_hot WITH ( serializable)  
         WHERE so_date <= @splitdate;  
  
      -- remove moved data  
      DELETE FROM dbo.SalesOrders_hot WITH( SERIALIZABLE)  
         WHERE so_date <= @splitdate;  
  
      -- update partition function, and switch in new partition  
      ALTER PARTITION SCHEME [ByDateRange] NEXT USED [PRIMARY];  
  
      DECLARE @p INT = ( SELECT MAX( partition_number) FROM sys.partitions WHERE object_id = OBJECT_ID( 'dbo.SalesOrders_cold'));  
      EXEC sp_executesql N'alter table dbo.SalesOrders_cold_staging  
         SWITCH TO dbo.SalesOrders_cold partition @i' , N'@i int' , @i = @p;  
  
      ALTER PARTITION FUNCTION [ByDatePF]()  
      SPLIT RANGE( @splitdate);  
  
      -- modify constraint on staging table to align with new partition  
      ALTER TABLE dbo.SalesOrders_cold_staging DROP CONSTRAINT CHK_SalesOrders_cold_staging;  
  
      DECLARE @s nvarchar( 100) = CONVERT( nvarchar( 100) , @splitdate , 121);  
      DECLARE @sql nvarchar( 1000) = N'alter table dbo.SalesOrders_cold_staging   
         add constraint CHK_SalesOrders_cold_staging check (so_date > ''' + @s + ''')';  
      PRINT @sql;  
      EXEC sp_executesql @sql;  
  
      COMMIT;  
END;  
GO  
  
-- insert sample values in the hot table  
INSERT INTO dbo.SalesOrders_hot VALUES(1,SYSDATETIME(), 1);   
GO  
  
INSERT INTO dbo.SalesOrders_hot VALUES(1, SYSDATETIME(), 1);  
GO  
  
INSERT INTO dbo.SalesOrders_hot VALUES(1, SYSDATETIME(), 1);  
GO  
  
-- verify contents of the table  
SELECT *  FROM dbo.SalesOrders;  
GO  
  
-- offload all sales orders to date to cold storage  
DECLARE  @t datetime2 = SYSDATETIME();  
EXEC dbo.usp_SalesOrdersOffloadToCold @t;  
  
-- verify contents of the tables  
SELECT * FROM dbo.SalesOrders;  
GO  
  
-- verify partitions  
SELECT OBJECT_NAME( object_id) , * FROM sys.dm_db_partition_stats ps  
   WHERE object_id = OBJECT_ID( 'dbo.SalesOrders_cold');  
  
-- insert more rows in the hot table  
INSERT INTO dbo.SalesOrders_hot VALUES(2, SYSDATETIME(), 1);  
GO  
  
INSERT INTO dbo.SalesOrders_hot VALUES(2, SYSDATETIME(), 1);  
GO  
  
INSERT INTO dbo.SalesOrders_hot VALUES(2, SYSDATETIME(), 1);  
GO  
  
-- verify contents of the tables  
SELECT * FROM dbo.SalesOrders;  
GO  
  
-- offload all sales orders to date to cold storage  
DECLARE @t datetime2 = SYSDATETIME();  
EXEC dbo.usp_SalesOrdersOffloadToCold @t;  
  
-- verify contents of the tables  
SELECT * FROM dbo.SalesOrders;  
GO  
  
-- verify partitions  
SELECT OBJECT_NAME( object_id) , partition_number , row_count  FROM sys.dm_db_partition_stats ps  
  WHERE object_id = OBJECT_ID( 'dbo.SalesOrders_cold') AND index_id = 1;  
```  
  
## <a name="see-also"></a>관련 항목  
 [메모리 액세스에 최적화된 테이블](memory-optimized-tables.md)  
  
  