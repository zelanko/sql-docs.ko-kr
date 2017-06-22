---
title: "데모: 메모리 내 OLTP 성능 향상 | Microsoft 문서"
ms.custom: 
ms.date: 08/19/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c6def45d-d2d4-4d24-8068-fab4cd94d8cc
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6a6edd38b5efb5b617308b9359eea8d255daeb8d
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="demonstration-performance-improvement-of-in-memory-oltp"></a>데모: 메모리 내 OLTP 성능 향상
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  이 항목의 코드 예제는 메모리 액세스에 최적화된 테이블의 빠른 성능 향상을 보여줍니다. 이러한 성능 향상은 메모리 액세스에 최적화된 테이블의 데이터가 기존의 해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 액세스될 때 두드러집니다. 이러한 성능 향상은 메모리 액세스에 최적화된 테이블의 데이터가 고유하게 컴파일된 저장 프로시저(NCSProc)에서 액세스될 때 더욱 커집니다.  
 
메모리 내 OLTP의 잠재적인 성능 향상에 대한 보다 포괄적인 데모를 보려면 [메모리 내 OLTP 성능 데모 v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)을 참조하세요. 
  
 이 문서의 코드 예제는 단일 스레드이며 메모리 내 OLTP의 동시성 이점을 활용하지 않습니다. 동시성을 사용하는 작업에서는 더 큰 성능 향상이 가능합니다. 코드 예제는 성능 향상의 한 가지 측면인 삽입을 위한 데이터 액세스 효율성만 보여 줍니다.  
  
 메모리 액세스에 최적화된 테이블로 제공되는 성능 향상은 메모리 액세스에 최적화된 테이블의 데이터가 NCSProc에서 액세스될 때 완벽하게 실현됩니다.  
  
## <a name="code-example"></a>코드 예  
 다음 하위 섹션에서는 각 단계에 대해 설명합니다.  
  
### <a name="step-1a-prerequisite-if-using-includessnoversionincludesssnoversion-mdmd"></a>1a 단계: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 첫 번째 하위 섹션의 단계는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행 중인 경우에 적용되고 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]에서 실행 중인 경우에는 적용되지 않습니다. 다음을 수행합니다.  
  
1.  SQL Server Management Studio(SSMS.exe)를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하세요. 또는 SSMS.exe와 유사한 도구를 사용해도 됩니다.  
  
2.  이름이 **C:\data\\\**인 디렉터리를 수동으로 만듭니다. 샘플 Transact SQL 코드를 위해서는 미리 존재하는 디렉터리가 필요합니다.  
  
3.  짧은 T-SQL을 실행하여 데이터베이스 및 메모리 액세스에 최적화된 파일 그룹을 생성하십시오.  
  
```tsql  
go  
CREATE DATABASE imoltp;    --  Transact-SQL  
go  
  
ALTER DATABASE imoltp ADD FILEGROUP [imoltp_mod]  
    CONTAINS MEMORY_OPTIMIZED_DATA;  
  
ALTER DATABASE imoltp ADD FILE  
    (name = [imoltp_dir], filename= 'c:\data\imoltp_dir')  
    TO FILEGROUP imoltp_mod;  
go  
  
USE imoltp;  
go  
```  
  
### <a name="step-1b-prerequisite-if-using-includesssdsfullincludessssdsfull-mdmd"></a>1b 단계: [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]  
 이 하위 섹션은 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]를 사용하는 경우에만 적용됩니다. 다음을 수행합니다.  
  
1.  코드 예제로 사용할 기존 테스트 데이터베이스를 결정합니다.  
  
2.  새 테스트 데이터베이스를 만들려면 [Azure 포털](http://portal.azure.com) 을 사용하여 이름이 **imoltp**인 데이터베이스를 생성합니다.  
  
 이를 위해 Azure 포털 사용 지침을 확인하려면 [Azure SQL 데이터베이스 시작](http://azure.microsoft.com/documentation/articles/sql-database-get-started)을 참조하십시오.  
  
### <a name="step-2-create-memory-optimized-tables-and-ncsproc"></a>2단계: 메모리 액세스에 최적화된 테이블과 NCSProc 만들기  
 이 단계를 통해 메모리 액세스에 최적화된 테이블 및 고유하게 컴파일된 저장 프로시저(NCSProc)를 만들 수 있습니다. 다음을 수행합니다.  
  
1.  SSMS.exe를 사용하여 새 데이터베이스에 연결합니다.  
  
2.  데이터베이스에서 다음 T-SQL을 실행합니다.  
  
```tsql  
go  
DROP PROCEDURE IF EXISTS ncsp;  
DROP TABLE IF EXISTS sql;  
DROP TABLE IF EXISTS hash_i;  
DROP TABLE IF EXISTS hash_c;  
go  
  
CREATE TABLE [dbo].[sql] (  
  c1 INT NOT NULL PRIMARY KEY,  
  c2 NCHAR(48) NOT NULL  
);  
go  
  
CREATE TABLE [dbo].[hash_i] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
go  
  
CREATE TABLE [dbo].[hash_c] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
go  
  
CREATE PROCEDURE ncsp  
    @rowcount INT,  
    @c NCHAR(48)  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
  AS   
  BEGIN ATOMIC   
  WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  DECLARE @i INT = 1;  
  WHILE @i <= @rowcount  
  BEGIN;  
    INSERT INTO [dbo].[hash_c] VALUES (@i, @c);  
    SET @i += 1;  
  END;  
END;  
go  
```  
  
### <a name="step-3-run-the-code"></a>3단계: 코드 실행  
 이제 메모리 액세스에 최적화된 테이블의 성능을 보여주는 쿼리를 실행합니다. 다음을 수행합니다.  
  
1.  SSMS.exe를 사용하여 데이터베이스에서 다음 T-SQL을 실행합니다.  
  
     첫 번째 실행에서 생성되는 모든 속도 또는 기타 성능 데이터를 무시합니다. 첫 번째 실행에서는 메모리 초기 할당 등 여러 1회성 작업이 수행됩니다.  
  
2.  SSMS.exe를 사용하여 데이터베이스에서 다음 T-SQL을 다시 실행합니다.  
  
```tsql  
go  
SET STATISTICS TIME OFF;  
SET NOCOUNT ON;  
  
-- Inserts, one at a time.  
  
DECLARE @starttime DATETIME2 = sysdatetime();  
DECLARE @timems INT;  
DECLARE @i INT = 1;  
DECLARE @rowcount INT = 100000;  
DECLARE @c NCHAR(48) = N'12345678901234567890123456789012345678';  
  
-- Harddrive-based table and interpreted Transact-SQL.  
  
BEGIN TRAN;  
  WHILE @i <= @rowcount  
  BEGIN;  
    INSERT INTO [dbo].[sql] VALUES (@i, @c);  
    SET @i += 1;  
  END;  
COMMIT;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT 'A: Disk-based table and interpreted Transact-SQL: '  
    + cast(@timems AS VARCHAR(10)) + ' ms';  
  
-- Interop Hash.  
  
SET @i = 1;  
SET @starttime = sysdatetime();  
  
BEGIN TRAN;  
  WHILE @i <= @rowcount  
    BEGIN;  
      INSERT INTO [dbo].[hash_i] VALUES (@i, @c);  
      SET @i += 1;  
    END;  
COMMIT;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT 'B: memory-optimized table with hash index and interpreted Transact-SQL: '  
    + cast(@timems as VARCHAR(10)) + ' ms';  
  
-- Compiled Hash.  
  
SET @starttime = sysdatetime();  
  
EXECUTE ncsp @rowcount, @c;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT 'C: memory-optimized table with hash index and native SP:'  
    + cast(@timems as varchar(10)) + ' ms';  
go  
  
DELETE sql;  
DELETE hash_i;  
DELETE hash_c;  
go  
```  
  
 다음은 두 번째 테스트 실행에서 생성된 출력 시간 통계입니다.  
  
```tsql  
10453 ms , A: Disk-based table and interpreted Transact-SQL.  
5626 ms , B: memory-optimized table with hash index and interpreted Transact-SQL.  
3937 ms , C: memory-optimized table with hash index and native SP.  
```  
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  

