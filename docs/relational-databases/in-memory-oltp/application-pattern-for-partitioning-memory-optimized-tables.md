---
title: 애플리케이션 패턴 - 메모리 최적화 테이블 분할
description: 매모리 최적화 테이블에 있는 현재 활성화된 데이터와 분할된 테이블에 있는 기존 데이터를 저장하는 메모리 내 OLTP 애플리케이션 디자인 패턴에 대해 알아봅니다.
ms.custom: seo-dt-2019,issue-PR=4700-14820
ms.date: 05/03/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 3f867763-a8e6-413a-b015-20e9672cc4d1
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8ff253b9164ca12d8d24dd5f7b362f4dfb47d548
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465444"
---
# <a name="application-pattern-for-partitioning-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블 분할을 위한 애플리케이션 패턴

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

[!INCLUDE[hek_2](../../includes/hek-2-md.md)]는 상대적으로 최신 데이터에 대한 성능 리소스를 많이 사용하는 애플리케이션 디자인 패턴을 지원합니다. 이 패턴은 최신 데이터를 이전 데이터보다 훨씬 자주 읽거나 업데이트할 때 적용할 수 있습니다. 이 경우 최신 데이터가 *활성* 또는 *핫* 하다고 말하며 오래된 데이터는 *콜드* 하다고 합니다.

주요 개념은 메모리 최적화 테이블에 *핫* 데이터를 저장하는 것입니다. 매주 또는 매월 *콜드* 상태가 된 오래된 데이터는 분할된 테이블로 이동됩니다. 분할된 테이블은 메모리가 아닌 디스크 또는 다른 하드 드라이브에 저장된 데이터가 있습니다.

일반적으로 이 디자인은 **datetime** 키를 사용하여 이동 프로세스가 핫 데이터와 콜드 데이터를 효율적으로 구분할 수 있도록 합니다.

## <a name="advanced-partitioning"></a>고급 분할

이 디자인은 역시 하나의 메모리 최적화 파티션이 있는 분할된 테이블을 가지는 경우를 모방하는 목적입니다. 이 디자인이 작동하려면 모든 테이블이 공통 스키마를 공유하도록 해야 합니다. 이 문서의 뒷부분에 나오는 코드 샘플에서 이 기술을 보여 줍니다.

새 데이터는 정의에 따라 핫으로 간주됩니다. 핫 데이터는 메모리 최적화 테이블에 삽입되고 업데이트됩니다. 콜드 데이터는 기존의 분할된 테이블에서 유지 관리됩니다. 저장 프로시저는 주기적으로 새 파티션을 추가합니다. 파티션은 메모리 최적화 테이블에서 이동된 최신 콜드 데이터를 포함합니다.

작업에 핫 데이터만 필요한 경우 고유하게 컴파일된 저장 프로시저를 사용하여 데이터에 액세스할 수 있습니다. 핫 또는 콜드 데이터에 액세스할 수 있는 작업은 해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)]를 사용하여 메모리 최적화 테이블을 분할된 테이블과 조인해야 합니다.

### <a name="add-a-partition"></a>파티션 추가

최근에 콜드가 된 데이터는 분할된 테이블로 이동해야 합니다. 이 주기적인 파티션 교환 단계는 다음과 같습니다.

1. 메모리 최적화 테이블에 있는 데이터의 경우 핫 데이터와 새로운 콜드 데이터 간의 경계 또는 컷오프 날짜/시간을 결정합니다.
2. 메모리 내 OLTP 테이블에서 새로운 콜드 데이터를 *cold\_staging* 테이블에 삽입합니다.
3. 메모리 최적화 테이블에서 같은 콜드 데이터를 삭제합니다.
4. cold\_staging 테이블을 파티션으로 바꿉니다.
5. 파티션을 추가합니다.

#### <a name="maintenance-window"></a>유지 관리 기간

이전 단계 중 하나는 메모리 최적화 테이블에서 새로운 콜드 데이터를 삭제하는 것입니다. 이 삭제와 새 파티션을 추가하는 마지막 단계 사이에는 시간 간격이 있습니다. 이 기간 동안에는 새로운 콜드 데이터를 읽으려고 시도하는 모든 애플리케이션에 오류가 발생합니다.

관련 샘플을 보려면 [애플리케이션 수준 분할](../../relational-databases/in-memory-oltp/application-level-partitioning.md)을 참조하세요.

## <a name="code-sample"></a>코드 예제

다음 Transact-SQL 샘플은 표시의 편의성을 위해 일련의 작은 코드 블록으로 표시됩니다. 테스트를 위해 이 모두를 하나의 단일 코드 블록에 추가할 수 있습니다.

전반적으로 Transact-SQL 샘플은 분할된 디스크 기반 테이블과 함께 메모리 최적화 테이블을 사용하는 방법을 보여 줍니다.

T-SQL 예제의 첫 번째 단계에서는 데이터베이스를 만든 다음 데이터베이스의 테이블과 같은 개체를 만듭니다. 이후 단계에서는 메모리 최적화 테이블에서 분할된 테이블로 데이터를 이동하는 방법을 보여 줍니다.

### <a name="create-a-database"></a>데이터베이스 만들기

T-SQL 샘플의 이 섹션에서는 테스트 데이터베이스를 만듭니다. 데이터베이스는 메모리 최적화 테이블과 분할된 테이블을 모두 지원하도록 구성되어 있습니다.

```sql
CREATE DATABASE PartitionSample;
GO

-- Add a FileGroup, enabled for In-Memory OLTP.
-- Change file path as needed.

ALTER DATABASE PartitionSample
    ADD FILEGROUP PartitionSample_mod
    CONTAINS MEMORY_OPTIMIZED_DATA;

ALTER DATABASE PartitionSample
    ADD FILE(
        NAME = 'PartitionSample_mod',
        FILENAME = 'c:\data\PartitionSample_mod')
    TO FILEGROUP PartitionSample_mod;
GO
```

### <a name="create-a-memory-optimized-table-for-hot-data"></a>핫 데이터에 대한 메모리 최적화 테이블 만들기

이 섹션에서는 최신 데이터를 보유하는 메모리 최적화 테이블을 만들며, 이는 대부분 핫 데이터입니다.

```sql
USE PartitionSample;
GO

-- Create a memory-optimized table for the HOT Sales Order data.
-- Notice the index that uses datetime2.

CREATE TABLE dbo.SalesOrders_hot (
   so_id INT IDENTITY PRIMARY KEY NONCLUSTERED,
   cust_id INT NOT NULL,
   so_date DATETIME2 NOT NULL INDEX ix_date NONCLUSTERED,
   so_total MONEY NOT NULL,
   INDEX ix_date_total NONCLUSTERED (so_date desc, so_total desc)
) WITH (MEMORY_OPTIMIZED=ON);
GO
```

### <a name="create-a-partitioned-table-for-cold-data"></a>콜드 데이터에 대한 분할된 테이블 만들기

이 섹션에서는 콜드 데이터를 보유하는 분할된 테이블을 만듭니다.

```sql
-- Create a partition and table for the COLD Sales Order data.
-- Notice the index that uses datetime2.

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
) ON [ByDateRange](so_date);
GO
```

### <a name="create-a-table-to-store-cold-data-during-move"></a>이동 중 콜드 데이터를 저장하는 테이블 만들기

이 섹션에서는 cold\_staging 테이블을 만듭니다. 두 테이블에서 핫 데이터와 콜드 데이터를 통합하는 뷰도 만들어집니다.

```sql
-- A table used to briefly stage the newly cold data, during moves to a partition.

CREATE TABLE dbo.SalesOrders_cold_staging (
   so_id INT NOT NULL,
   cust_id INT NOT NULL,
   so_date datetime2 NOT NULL,
   so_total MONEY NOT NULL,
   CONSTRAINT PK_SalesOrders_cold_staging PRIMARY KEY (so_id, so_date),
   INDEX ix_date_total NONCLUSTERED (so_date desc, so_total desc),
   CONSTRAINT CHK_SalesOrders_cold_staging CHECK (so_date >= '1900-01-01')
);
GO

-- A view, for retrieving the aggregation of hot plus cold data.

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
          0 AS 'is_cold'
       FROM dbo.SalesOrders_cold;
GO
```

### <a name="create-the-stored-procedure"></a>저장 프로시저 만들기

이 섹션에서는 정기적으로 실행되는 저장 프로시저를 만듭니다. 이 프로시저는 메모리 최적화 테이블에서 분할된 테이블로 새로 콜드 데이터를 이동합니다.

```sql
-- A stored procedure to move all newly cold sales orders data
-- to its staging location.

CREATE PROCEDURE dbo.usp_SalesOrdersOffloadToCold @splitdate datetime2
   AS
   BEGIN
      BEGIN TRANSACTION;

      -- Insert the cold data as a temporary heap.
      INSERT INTO dbo.SalesOrders_cold_staging WITH (TABLOCKX)
      SELECT so_id , cust_id , so_date , so_total
         FROM dbo.SalesOrders_hot WITH (serializable)
         WHERE so_date <= @splitdate;

      -- Delete the moved data from the hot table.
      DELETE FROM dbo.SalesOrders_hot WITH (SERIALIZABLE)
         WHERE so_date <= @splitdate;

      -- Update the partition function, and switch in the new partition.
      ALTER PARTITION SCHEME [ByDateRange] NEXT USED [PRIMARY];

      DECLARE @p INT = (
        SELECT MAX(partition_number)
            FROM sys.partitions
            WHERE object_id = OBJECT_ID('dbo.SalesOrders_cold'));

      EXEC sp_executesql
        N'ALTER TABLE dbo.SalesOrders_cold_staging
            SWITCH TO dbo.SalesOrders_cold partition @i',
        N'@i int',
        @i = @p;

      ALTER PARTITION FUNCTION [ByDatePF]()
      SPLIT RANGE( @splitdate);

      -- Modify a constraint on the cold_staging table, to align with new partition.
      ALTER TABLE dbo.SalesOrders_cold_staging
         DROP CONSTRAINT CHK_SalesOrders_cold_staging;

      DECLARE @s nvarchar( 100) = CONVERT( nvarchar( 100) , @splitdate , 121);
      DECLARE @sql nvarchar( 1000) = N'alter table dbo.SalesOrders_cold_staging 
         add constraint CHK_SalesOrders_cold_staging check (so_date > ''' + @s + ''')';
      PRINT @sql;
      EXEC sp_executesql @sql;

      COMMIT;
END;
GO
```

### <a name="prepare-sample-data-and-demo-the-stored-procedure"></a>샘플 데이터 준비 및 저장 프로시저 데모

이 섹션에서는 샘플 데이터를 생성하고 삽입한 다음 저장 프로시저를 데모용으로 실행합니다.

```sql
-- Insert sample values into the hot table.
INSERT INTO dbo.SalesOrders_hot VALUES(1,SYSDATETIME(), 1);
GO
INSERT INTO dbo.SalesOrders_hot VALUES(1, SYSDATETIME(), 1);
GO
INSERT INTO dbo.SalesOrders_hot VALUES(1, SYSDATETIME(), 1);
GO

-- Verify that the hot data is in the table, by selecting from the view.
SELECT * FROM dbo.SalesOrders;
GO

-- Treat all data in the hot table as cold data:
-- Run the stored procedure, to move (offload) all sales orders to date to cold storage.
DECLARE @t datetime2 = SYSDATETIME();
EXEC dbo.usp_SalesOrdersOffloadToCold @t;

-- Again, read hot plus cold data from the view.
SELECT * FROM dbo.SalesOrders;
GO

-- Retrieve the name of every partition.
SELECT OBJECT_NAME( object_id) , * FROM sys.dm_db_partition_stats ps
   WHERE object_id = OBJECT_ID( 'dbo.SalesOrders_cold');

-- Insert more data into the hot table.
INSERT INTO dbo.SalesOrders_hot VALUES(2, SYSDATETIME(), 1);
GO
INSERT INTO dbo.SalesOrders_hot VALUES(2, SYSDATETIME(), 1);
GO
INSERT INTO dbo.SalesOrders_hot VALUES(2, SYSDATETIME(), 1);
GO

-- Read hot plus cold data from the view.
SELECT * FROM dbo.SalesOrders;
GO

-- Again, run the stored procedure, to move all sales orders to date to cold storage.
DECLARE @t datetime2 = SYSDATETIME();
EXEC dbo.usp_SalesOrdersOffloadToCold @t;

-- Read hot plus cold data from the view.
SELECT * FROM dbo.SalesOrders;
GO

-- Again, retrieve the name of every partition.
-- The stored procedure can modify the partitions.
SELECT OBJECT_NAME( object_id) , partition_number , row_count
  FROM sys.dm_db_partition_stats ps
  WHERE object_id = OBJECT_ID( 'dbo.SalesOrders_cold')
    AND index_id = 1;
```

### <a name="drop-all-the-demo-objects"></a>모든 데모 개체 삭제하기

테스트 시스템에서 데모 테스트 데이터베이스를 제거해야 합니다.

```sql
-- You must first leave the context of the PartitionSample database.

-- USE <A-Database-Name-Here>;
GO

DROP DATABASE PartitionSample;
GO
```

## <a name="see-also"></a>참고 항목

[메모리 최적화 테이블](./sample-database-for-in-memory-oltp.md)