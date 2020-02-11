---
title: '데모: 메모리 내 OLTP 성능 향상 | Microsoft 문서'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c6def45d-d2d4-4d24-8068-fab4cd94d8cc
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 8c9477a318d2cb4f9886d67da8a4f8b5967cc180
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63071788"
---
# <a name="demonstration-performance-improvement-of-in-memory-oltp"></a>데모: 메모리 내 OLTP 성능 향상
  이 예제는 메모리 최적화된 테이블과 디스크 기반 테이블에 대해 동일한 Transact-SQL 쿼리를 실행하는 경우 응답 시간의 차이를 비교하여 메모리 내 OLTP 사용 시 성능 향상을 보여줍니다. 또한 고유하게 컴파일된 저장 프로시저가 생성되고(동일한 쿼리를 기반으로) 고유하게 컴파일된 저장 프로시저로 메모리 최적화 테이블을 쿼리하는 경우 일반적으로 최고의 응답 시간을 갖는다는 것을 설명하기 위해 실행됩니다. 이 샘플은 메모리 최적화 테이블에 포함된 데이터에 액세스 하는 경우 성능 향상의 한 가지 측면 즉, 삽입 수행 시 데이터 액세스 효율성만을 보여줍니다. 이 예제는 단일 스레드이며 메모리 내 OLTP의 동시성 이점을 활용하지 않습니다. 동시성을 사용하는 작업에서는 더 큰 성능 향상이 가능합니다.  
  
> [!NOTE]  
>  메모리 최적화 테이블을 보여 주는 다른 예제는 [SQL Server 2014 메모리 내 OLTP 예제](https://msftdbprodsamples.codeplex.com/releases/view/114491)에 있습니다.  
  
 이 샘플을 완료하려면 다음을 수행합니다.  
  
1.  
  **imoltp** 라는 데이터베이스를 만들고 메모리 내 OLTP를 사용하여 설정하려는 파일 세부 정보를 변경합니다.  
  
2.  샘플에 대한 데이터베이스 개체 즉, 세 테이블 및 고유하게 컴파일된 저장 프로시저를 만듭니다.  
  
3.  다른 쿼리를 실행하고 각 쿼리에 대한 응답 시간을 표시합니다.  
  
 예제에 대한 **imoltp** 데이터베이스를 설치하려면 우선 빈 폴더 **c:\imoltp_data**를 만든 후 다음 코드를 실행합니다.  
  
```sql  
USE master  
GO  
  
-- Create a new database.  
CREATE DATABASE imoltp  
GO  
  
-- Prepare the database for In-Memory OLTP by  
-- adding a memory-optimized filegroup to the database.  
ALTER DATABASE imoltp ADD FILEGROUP imoltp_file_group  
    CONTAINS MEMORY_OPTIMIZED_DATA;  
  
-- Add a file (to hold the memory-optimized data) to the new filegroup.  
ALTER DATABASE imoltp ADD FILE (name='imoltp_file', filename='c:\imoltp_data\imoltp_file')  
    TO FILEGROUP imoltp_file_group;  
GO  
  
```  
  
 그 후, 다음 코드를 실행하여 디스크 기반 테이블, 2개의 (2) 메모리 최적화 테이블, 다른 데이터 액세스 메서드를 보여주는데 사용될 고유하게 컴파일된 저장 프로시를 만듭니다.  
  
```sql  
USE imoltp  
GO  
  
-- If the tables or stored procedure already exist, drop them to start clean.  
IF EXISTS (SELECT NAME FROM sys.objects WHERE NAME = 'DiskBasedTable')  
   DROP TABLE [dbo].[DiskBasedTable]  
GO  
  
IF EXISTS (SELECT NAME FROM sys.objects WHERE NAME = 'InMemTable')  
   DROP TABLE [dbo].[InMemTable]  
GO  
  
IF EXISTS (SELECT NAME FROM sys.objects  WHERE NAME = 'InMemTable2')  
   DROP TABLE [dbo].[InMemTable2]  
GO  
  
IF EXISTS (SELECT NAME FROM sys.objects  WHERE NAME = 'usp_InsertData')  
   DROP PROCEDURE [dbo].[usp_InsertData]  
GO  
  
-- Create a traditional disk-based table.  
CREATE TABLE [dbo].[DiskBasedTable] (  
  c1 INT NOT NULL PRIMARY KEY,  
  c2 NCHAR(48) NOT NULL  
)  
GO  
  
-- Create a memory-optimized table.  
CREATE TABLE [dbo].[InMemTable] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
GO  
  
-- Create a 2nd memory-optimized table.  
CREATE TABLE [dbo].[InMemTable2] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
GO  
  
-- Create a natively-compiled stored procedure.  
CREATE PROCEDURE [dbo].[usp_InsertData]   
  @rowcount INT,  
  @c NCHAR(48)  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
  AS   
  BEGIN ATOMIC   
  WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  DECLARE @i INT = 1;  
  WHILE @i <= @rowcount  
  BEGIN  
    INSERT INTO [dbo].[inMemTable2](c1,c2) VALUES (@i, @c);  
    SET @i += 1;  
  END  
END  
GO  
  
```  
  
 설치가 완료되고 데이터 액세스 메서드 사이의 성능을 비교하여 응답 시간을 표시하는 쿼리를 실행할 준비가 됩니다.  
  
 예제를 완료하려면 다음 코드를 여러 번 실행합니다. 초기 메모리 할당에 의해 부정적인 영향을 받는 첫 번째 실행의 결과를 무시합니다.  
  
```sql  
SET STATISTICS TIME OFF;  
SET NOCOUNT ON;  
  
-- Delete data from all tables to reset the example.  
DELETE FROM [dbo].[DiskBasedTable]   
    WHERE [c1]>0  
GO  
DELETE FROM [dbo].[inMemTable]   
    WHERE [c1]>0  
GO  
DELETE FROM [dbo].[InMemTable2]   
    WHERE [c1]>0  
GO  
  
-- Declare parameters for the test queries.  
DECLARE @i INT = 1;  
DECLARE @rowcount INT = 100000;  
DECLARE @c NCHAR(48) = N'12345678901234567890123456789012345678';  
DECLARE @timems INT;  
DECLARE @starttime datetime2 = sysdatetime();  
  
-- Disk-based table queried with interpreted Transact-SQL.  
BEGIN TRAN  
  WHILE @I <= @rowcount  
  BEGIN  
    INSERT INTO [dbo].[DiskBasedTable](c1,c2) VALUES (@i, @c);  
    SET @i += 1;  
  END  
COMMIT  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT CAST(@timems AS VARCHAR(10)) + ' ms (disk-based table with interpreted Transact-SQL).';  
  
-- Memory-optimized table queried with interpreted Transact-SQL.  
SET @i = 1;  
SET @starttime = sysdatetime();  
  
BEGIN TRAN  
  WHILE @i <= @rowcount  
    BEGIN  
      INSERT INTO [dbo].[InMemTable](c1,c2) VALUES (@i, @c);  
      SET @i += 1;  
    END  
COMMIT  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT CAST(@timems AS VARCHAR(10)) + ' ms (memory-optimized table with interpreted Transact-SQL).';  
  
-- Memory-optimized table queried with a natively-compiled stored procedure.  
SET @starttime = sysdatetime();  
  
EXEC usp_InsertData @rowcount, @c;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT CAST(@timems AS VARCHAR(10)) + ' ms (memory-optimized table with natively-compiled stored procedure).';  
  
```  
  
 예상 결과는 메모리 최적화 테이블과 고유하게 컴파일된 저장 프로시저가 기존의 디스크 기반 테이블에 대해 실행되는 동일한 작업보다 지속적으로 빠른 응답 시간을 보여주는 실제 응답 시간을 제공합니다.  
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP를 보여 주는 AdventureWorks 확장](../../database-engine/extensions-to-adventureworks-to-demonstrate-in-memory-oltp.md)   
 [메모리 내 OLTP는 메모리 내 최적화를 &#40;&#41;](in-memory-oltp-in-memory-optimization.md)   
 [메모리 액세스에 최적화 된 테이블](memory-optimized-tables.md)   
 [고유 하 게 컴파일된 저장 프로시저](natively-compiled-stored-procedures.md)   
 [메모리 액세스에 최적화 된 테이블 사용을 위한 요구 사항](requirements-for-using-memory-optimized-tables.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [ALTER DATABASE 파일 및 파일 그룹 옵션&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)   
 [프로시저 및 메모리 액세스에 최적화 된 테이블 만들기](/sql/t-sql/statements/create-procedure-transact-sql)  
  
  
