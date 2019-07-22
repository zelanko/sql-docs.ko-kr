---
title: FROM 또는 하위 쿼리를 사용하여 UPDATE 구현 | Microsoft 문서
ms.custom: ''
ms.date: 11/17/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 138f5b0e-f8a4-400f-b581-8062aebc62b6
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0c41165cf1e4a6b1ad8122cb674f8644f40d8ebe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68050261"
---
# <a name="implementing-update-with-from-or-subqueries"></a>FROM 또는 하위 쿼리를 사용하여 UPDATE 구현

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]



Transact-SQL UPDATE 문에서 기본적으로 컴파일된 T-SQL 모듈에서는 다음 구문 요소가 지원되지 *않습니다*.

- FROM 절
- 하위 쿼리

대조적으로 선행 요소는 SELECT 문에서 기본적으로 컴파일된 모듈에서 지원*됩니다*.

FROM 절이 있는 UPDATE 문은 종종 TVP(테이블 반환 매개 변수)에 따라 테이블의 정보를 업데이트하거나 AFTER 트리거에서 테이블의 열을 업데이트하는 데 사용됩니다.

TVP에 따라 업데이트하는 시나리오의 경우 [고유하게 컴파일된 저장 프로시저에서 MERGE 기능 구현](../../relational-databases/in-memory-oltp/implementing-merge-functionality-in-a-natively-compiled-stored-procedure.md)을 참조하세요. 

다음 샘플에서는 트리거에서 수행되는 업데이트를 보여줍니다. 테이블에서 LastUpdated라는 열은 현재 날짜-시간 AFTER 업데이트로 설정됩니다. 해결 방법은 다음 항목을 사용하여 개별 업데이트를 수행합니다.

- IDENTITY 열이 있는 테이블 변수입니다.
- WHILE 루프는 테이블 변수의 행을 반복합니다.

원래 T-SQL UPDATE 문은 다음과 같습니다.

   ```sql
    UPDATE dbo.Table1  
        SET LastUpdated = SysDateTime()  
        FROM  
            dbo.Table1 t  
            JOIN Inserted i ON t.Id = i.Id;  
   ```

다음 블록의 샘플 T-SQL 코드는 좋은 성능을 제공하는 해결 방법을 보여줍니다. 해결 방법은 고유하게 컴파일된 트리거에서 구현되었습니다. 코드에서 주의해야 할 사항은 다음과 같습니다.  
  
- 메모리 최적화 테이블 형식인 dbo.Type1 형식  
- 트리거의 WHILE 루프.  
  - 루프는 Inserted에서 행을 한 번에 하나씩 검색합니다.  
  
  
  
 ```sql
    DROP TABLE IF EXISTS dbo.Table1;  
    go  
    DROP TYPE IF EXISTS dbo.Type1;  
    go  
    -----------------------------
    -- Table and table type.
    -----------------------------
  
    CREATE TABLE dbo.Table1  
    (  
        Id           INT        NOT NULL  PRIMARY KEY NONCLUSTERED,  
        Column2      INT        NOT NULL,  
        LastUpdated  DATETIME2  NOT NULL  DEFAULT (SYSDATETIME())  
    )  
        WITH (MEMORY_OPTIMIZED = ON);  
    go  
  
  
    CREATE TYPE dbo.Type1 AS TABLE  
    (  
        Id       INT NOT  NULL,  
        
        RowID    INT NOT  NULL  IDENTITY,  
        INDEX ix_RowID HASH (RowID) WITH (BUCKET_COUNT=1024)
    )   
        WITH (MEMORY_OPTIMIZED = ON);  
    go  
    ----------------------------------------
    -- Trigger that contains the workaround
    -- for UPDATE with FROM.
    ----------------------------------------
  
    CREATE TRIGGER dbo.tr_a_u_Table1  
        ON dbo.Table1  
        WITH NATIVE_COMPILATION, SCHEMABINDING  
        AFTER UPDATE  
    AS 
    BEGIN ATOMIC WITH  
        (  
        TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
        LANGUAGE = N'us_english'  
        )  
        
      DECLARE @tabvar1 dbo.Type1;  
    
      INSERT @tabvar1 (Id)   
          SELECT Id FROM Inserted;  
    
      DECLARE  
          @i INT = 1,  @Id INT,  
          @max INT = SCOPE_IDENTITY();  
    
      ---- Loop as a workaround to simulate a cursor.
      ---- Iterate over the rows in the memory-optimized table  
      ----   variable and perform an update for each row.  
    
      WHILE @i <= @max  
      BEGIN  
          SELECT @Id = Id  
              FROM @tabvar1  
              WHERE RowID = @i;  
    
          UPDATE dbo.Table1  
              SET LastUpdated = SysDateTime()  
              WHERE Id = @Id;  
    
          SET @i += 1;  
      END  
    END  
    go  
    ---------------------------------
    -- Test to verify functionality.
    ---------------------------------
  
    SET NOCOUNT ON;  
  
    INSERT dbo.Table1 (Id, Column2)  
        VALUES (1,9), (2,9), (3,600);  
    
    SELECT N'BEFORE-Update' AS [BEFORE-Update], *  
        FROM dbo.Table1  
        ORDER BY Id;  
  
    WAITFOR DELAY '00:00:01';  

    UPDATE dbo.Table1  
        SET   Column2 += 1  
        WHERE Column2 <= 99;  
  
    SELECT N'AFTER--Update' AS [AFTER--Update], *  
        FROM dbo.Table1  
        ORDER BY Id;  
    go  
    -----------------------------  
  
    /**** Actual output:  
  
    BEFORE-Update   Id   Column2   LastUpdated  
    BEFORE-Update   1       9      2016-04-20 21:18:42.8394659  
    BEFORE-Update   2       9      2016-04-20 21:18:42.8394659  
    BEFORE-Update   3     600      2016-04-20 21:18:42.8394659  
  
    AFTER--Update   Id   Column2   LastUpdated  
    AFTER--Update   1      10      2016-04-20 21:18:43.8529692  
    AFTER--Update   2      10      2016-04-20 21:18:43.8529692  
    AFTER--Update   3     600      2016-04-20 21:18:42.8394659  
    ****/  
 ```
