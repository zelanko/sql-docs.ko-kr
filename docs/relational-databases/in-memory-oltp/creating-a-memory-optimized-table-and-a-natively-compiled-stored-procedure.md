---
title: 메모리 액세스에 최적화된 테이블 및 고유하게 컴파일된 저장 프로시저 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 48a9a0a3-930f-477b-bd0f-e82e77999ecc
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: f905e088d158803f26110356b1dad3cc29f62ab6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65090391"
---
# <a name="creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure"></a>메모리 액세스에 최적화된 테이블 및 고유하게 컴파일된 저장 프로시저 만들기

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 항목에는 메모리 내 OLTP의 구문을 소개하는 예제가 포함되어 있습니다.  

애플리케이션에서 메모리 내 OLTP를 사용하려면 다음 태스크를 완료해야 합니다.  

-   메모리 최적화 데이터 파일 그룹을 만들고 컨테이너를 파일 그룹에 추가합니다.  
  
-   메모리 최적화 테이블과 인덱스를 만듭니다. 자세한 내용은 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)을 참조하세요.  
  
-   데이터를 로드한 후 컴파일된 저장 프로시저를 만들기 전에 데이터를 메모리 최적화 테이블에 로드합니다. 자세한 내용은 [메모리 액세스에 최적화된 테이블에 대한 통계](../../relational-databases/in-memory-oltp/statistics-for-memory-optimized-tables.md)를 참조하세요.  
  
-   메모리 최적화 테이블의 데이터에 액세스하는 고유하게 컴파일된 저장 프로시저를 만듭니다. 자세한 내용은 [CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)를 참조하세요. 메모리 최적화 테이블에서 기존의 해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용할 수도 있습니다.  
  
-   필요에 따라 기존 테이블에서 메모리 최적화 테이블로 데이터를 마이그레이션합니다.  

## <a name="background-on-in-memory-objects"></a>메모리 내 개체에 대한 배경

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 메모리 최적화 테이블을 만드는 방법에 대한 자세한 내용은 [메모리 내 OLTP에 대한 SQL Server Management Studio 지원](../../relational-databases/in-memory-oltp/sql-server-management-studio-support-for-in-memory-oltp.md)을 참조하세요.  

### <a name="natively-compiled-stored-procedures"></a>고유하게 컴파일된 저장 프로시저

고유하게 컴파일된 저장 프로시저는 네이티브 코드로 컴파일된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저이며 메모리 최적화 테이블에 액세스합니다. 고유하게 컴파일된 저장 프로시저는 쿼리 및 비즈니스 논리가 저장 프로시저에서 효율적으로 실행되도록 해 줍니다. 네이티브 컴파일 프로세스에 대한 자세한 내용은 [Native Compilation of Tables and Stored Procedures](../../relational-databases/in-memory-oltp/native-compilation-of-tables-and-stored-procedures.md)을 참조하세요. 디스크 기반 저장 프로시저를 고유하게 컴파일된 저장 프로시저로 마이그레이션하는 방법은 [고유하게 컴파일된 저장 프로시저의 마이그레이션 문제](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)를 참조하세요.

> [!NOTE]
> 해석된(디스크 기반) 저장 프로시저와 고유하게 컴파일된 저장 프로시저 간의 한 가지 차이점은 해석된 저장 프로시저가 처음 실행할 때 컴파일되는 반면 고유하게 컴파일된 저장 프로시저는 생성할 때 컴파일된다는 것입니다. 고유하게 컴파일된 저장 프로시저를 사용하면 만들 때 많은 오류 조건을 검색하여 고유하게 컴파일된 저장 프로시저 만들기가 실패할 수 있습니다(예: 산술 오버플로, 형식 변환, 일부 0으로 나누기 조건). 해석된 저장된 프로시저를 사용하면 일반적으로 저장 프로시저를 만들 때 이러한 오류 조건으로 인해 오류가 발생하지 않지만 모든 실행이 실패합니다.

## <a name="code-example-in-t-sql"></a>T-SQL 코드 예제

다음 코드 샘플을 사용하려면 c:\Data\라는 디렉터리가 필요합니다.

```sql  
CREATE DATABASE imoltp   
GO  
  
--------------------------------------  
-- create database with a memory-optimized
-- filegroup and a container.

ALTER DATABASE imoltp ADD FILEGROUP imoltp_mod
    CONTAINS MEMORY_OPTIMIZED_DATA;

ALTER DATABASE imoltp ADD FILE (
    name='imoltp_mod1', filename='c:\data\imoltp_mod1')
    TO FILEGROUP imoltp_mod;

ALTER DATABASE imoltp
    SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
GO  
  
USE imoltp  
GO  
  
-- Create a durable (data will be persisted) memory-optimized table
-- two of the columns are indexed.

CREATE TABLE dbo.ShoppingCart (   
    ShoppingCartId INT IDENTITY(1,1) PRIMARY KEY NONCLUSTERED,  
    UserId INT NOT NULL INDEX ix_UserId NONCLUSTERED
        HASH WITH (BUCKET_COUNT=1000000),
    CreatedDate DATETIME2 NOT NULL,   
    TotalPrice MONEY  
    ) WITH (MEMORY_OPTIMIZED=ON)   
GO  

-- Create a non-durable table. Data will not be persisted,
-- data loss if the server turns off unexpectedly.

CREATE TABLE dbo.UserSession (   
   SessionId INT IDENTITY(1,1) PRIMARY KEY NONCLUSTERED
        HASH WITH (BUCKET_COUNT=400000),
   UserId int NOT NULL,   
   CreatedDate DATETIME2 NOT NULL,  
   ShoppingCartId INT,  
   INDEX ix_UserId NONCLUSTERED
        HASH (UserId) WITH (BUCKET_COUNT=400000)   
    )   
    WITH (MEMORY_OPTIMIZED=ON, DURABILITY=SCHEMA_ONLY)
GO  
  
-- insert data into the tables  
INSERT dbo.UserSession VALUES (342, SYSDATETIME(), 4);
INSERT dbo.UserSession VALUES (65, SYSDATETIME(), NULL)   
INSERT dbo.UserSession VALUES (8798, SYSDATETIME(), 1)   
INSERT dbo.UserSession VALUES (80, SYSDATETIME(), NULL)   
INSERT dbo.UserSession VALUES (4321, SYSDATETIME(), NULL)   
INSERT dbo.UserSession VALUES (8578, SYSDATETIME(), NULL)   
  
INSERT dbo.ShoppingCart VALUES (8798, SYSDATETIME(), NULL)   
INSERT dbo.ShoppingCart VALUES (23, SYSDATETIME(), 45.4)   
INSERT dbo.ShoppingCart VALUES (80, SYSDATETIME(), NULL)   
INSERT dbo.ShoppingCart VALUES (342, SYSDATETIME(), 65.4)   
GO  
  
-- Verify table contents.

SELECT * FROM dbo.UserSession;
SELECT * FROM dbo.ShoppingCart;
GO  
  
-- Update statistics on memory-optimized tables;

UPDATE STATISTICS dbo.UserSession  WITH FULLSCAN, NORECOMPUTE;
UPDATE STATISTICS dbo.ShoppingCart WITH FULLSCAN, NORECOMPUTE;
GO  
  
-- in an explicit transaction, assign a cart to a session
-- and update the total price.
-- SELECT/UPDATE/DELETE statements in explicit transactions.

BEGIN TRAN;
   UPDATE dbo.UserSession SET ShoppingCartId=3 WHERE SessionId=4;
   UPDATE dbo.ShoppingCart SET TotalPrice=65.84 WHERE ShoppingCartId=3;
COMMIT;
GO   
  
-- Verify table contents.

SELECT *   
    FROM dbo.UserSession u
        JOIN dbo.ShoppingCart s on u.ShoppingCartId=s.ShoppingCartId
    WHERE u.SessionId=4;
 GO  
  
-- Natively compiled stored procedure for assigning
-- a shopping cart to a session.

CREATE PROCEDURE dbo.usp_AssignCart @SessionId int
    WITH NATIVE_COMPILATION, SCHEMABINDING
AS
BEGIN ATOMIC
    WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
        LANGUAGE = N'us_english');
  
  DECLARE @UserId INT,  
          @ShoppingCartId INT;
  
  SELECT @UserId=UserId, @ShoppingCartId=ShoppingCartId
  FROM dbo.UserSession WHERE SessionId=@SessionId;
  
  IF @UserId IS NULL   
    THROW 51000, N'The session or shopping cart does not exist.', 1;
  
  UPDATE dbo.UserSession
    SET ShoppingCartId=@ShoppingCartId WHERE SessionId=@SessionId;
 END   
 GO  
  
 EXEC usp_AssignCart 1;
 GO  
  
-- natively compiled stored procedure for inserting
-- a large number of rows this demonstrates the
-- performance of native procs   
CREATE PROCEDURE dbo.usp_InsertSampleCarts @InsertCount int
    WITH NATIVE_COMPILATION, SCHEMABINDING   
AS
BEGIN ATOMIC   
    WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
        LANGUAGE = N'us_english');
  
  DECLARE @i int = 0;
  
  WHILE @i < @InsertCount   
  BEGIN   
    INSERT INTO dbo.ShoppingCart VALUES (1, SYSDATETIME() , NULL)
    SET @i += 1   
  END  
  
END   
GO  
  
-- insert 1,000,000 rows   
 EXEC usp_InsertSampleCarts 1000000   
 GO  
  
---- verify the rows have been inserted   
 SELECT COUNT(*) FROM dbo.ShoppingCart   
 GO  
  
-- Sample memory-optimized tables for
-- sales orders and sales order details.
CREATE TABLE dbo.SalesOrders   
(  
   so_id INT NOT NULL PRIMARY KEY NONCLUSTERED,  
   cust_id INT NOT NULL,  
   so_date DATE NOT NULL INDEX ix_date NONCLUSTERED,  
   so_total MONEY NOT NULL,  
   INDEX ix_date_total NONCLUSTERED
        (so_date DESC, so_total DESC)  
) WITH (MEMORY_OPTIMIZED=ON);
GO  
  
CREATE TABLE dbo.SalesOrderDetails  
(  
   so_id INT NOT NULL,  
   lineitem_id INT NOT NULL,  
   product_id INT NOT NULL,  
   unitprice MONEY NOT NULL,  
  
   CONSTRAINT PK_SOD PRIMARY KEY NONCLUSTERED
        (so_id,lineitem_id)
) WITH (MEMORY_OPTIMIZED=ON)  
GO  

-- Memory-optimized table type for collecting
-- sales order details.

CREATE TYPE dbo.SalesOrderDetailsType AS TABLE  
(  
   so_id INT NOT NULL,  
   lineitem_id INT NOT NULL,  
   product_id INT NOT NULL,  
   unitprice MONEY NOT NULL,  
  
   PRIMARY KEY NONCLUSTERED (so_id,lineitem_id)  
) WITH (MEMORY_OPTIMIZED=ON)  
GO  
  
-- stored procedure that inserts a sales order,
-- along with its details.

CREATE PROCEDURE dbo.InsertSalesOrder
    @so_id INT, @cust_id INT,
    @items dbo.SalesOrderDetailsType READONLY  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS BEGIN ATOMIC WITH   
(  
   TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
   LANGUAGE = N'us_english'  
)  
   DECLARE @total MONEY  
   SELECT @total = SUM(unitprice) FROM @items  

   INSERT dbo.SalesOrders
        VALUES (@so_id, @cust_id, getdate(), @total)

   INSERT dbo.SalesOrderDetails
        SELECT so_id, lineitem_id, product_id, unitprice
        FROM @items  
END  
GO  
  
-- Insert a sample sales order.
DECLARE @so_id INT = 18,  
       @cust_id INT = 8,  
       @items dbo.SalesOrderDetailsType;

INSERT @items  VALUES   
       (@so_id, 1, 4, 43),   
       (@so_id, 2, 3, 3),   
       (@so_id, 3, 8, 453),   
       (@so_id, 4, 5, 76),   
       (@so_id, 5, 4, 43);

EXEC dbo.InsertSalesOrder @so_id, @cust_id, @items;
GO  
  
-- verify the content of the tables  
SELECT   
       so.so_id,  
       so.so_date,  
       sod.lineitem_id,  
       sod.product_id,  
       sod.unitprice  
FROM dbo.SalesOrders so
    JOIN dbo.SalesOrderDetails sod on so.so_id=sod.so_id  
ORDER BY so.so_id, sod.lineitem_id  
```  
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP 코드 예제](../../relational-databases/in-memory-oltp/in-memory-oltp-code-samples.md)  
  
  
