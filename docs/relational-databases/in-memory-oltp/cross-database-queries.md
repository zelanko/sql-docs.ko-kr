---
title: "데이터베이스 간 쿼리 | Microsoft 문서"
ms.custom: 
ms.date: 08/04/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a0305f5b-91bd-4d18-a2fc-ec235b062fd3
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: 41b00b196f6cfad66ae0e26bbb1516da2641d9b7
ms.openlocfilehash: 8289b02c3e15f1b299196c343503c9cb87387c6c
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="cross-database-queries"></a>데이터베이스 간 쿼리
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터 메모리 액세스에 최적화된 테이블은 데이터베이스 간 트랜잭션을 지원하지 않습니다. 메모리 액세스에 최적화된 테이블에도 액세스하는 동일한 쿼리 또는 동일한 트랜잭션에서 다른 데이터베이스에 액세스할 수 없습니다. 데이터베이스의 테이블에서 다른 데이터베이스에 있는 메모리 액세스에 최적화된 테이블로 데이터를 쉽게 복사할 수 없습니다.  
  
 테이블 변수는 트랜잭션 변수가 아닙니다. 메모리 액세스에 최적화된 테이블 변수는 데이터베이스 간 쿼리에 사용할 수 있으므로, 데이터베이스의 데이터를 다른 데이터베이스에 있는 메모리 액세스에 최적화된 테이블로 쉽게 이동할 수 있습니다. 두 트랜잭션을 사용할 수 있습니다. 첫 번째 트랜잭션에서 원격 테이블의 데이터를 변수에 삽입합니다. 두 번째 트랜잭션에서 변수의 데이터를 메모리 액세스에 최적화된 로컬 테이블에 삽입합니다.  메모리 액세스에 최적화된 테이블 변수에 대한 자세한 내용은 [메모리 최적화를 사용하여 임시 테이블 및 테이블 변수 성능 향상](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)을 참조하세요.
  
## <a name="example"></a>예제
이 예제에는 한 데이터베이스의 데이터를 다른 데이터베이스에서 메모리 액세스에 최적화된 테이블로 전송하는 방법을 보여 줍니다.

1. 테스트 개체를 만듭니다.  [!INCLUDE[tsql](../../includes/tsql-md.md)] 에서 다음 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]명령을 실행합니다.  

    ```tsql

    USE master;
    GO
    
    SET NOCOUNT ON;
    
    -- Create simple database
    CREATE DATABASE SourceDatabase;
    ALTER DATABASE SourceDatabase SET RECOVERY SIMPLE;
    GO

    -- Create a table and insert a few records
    USE SourceDatabase;
    
    CREATE TABLE SourceDatabase.[dbo].[SourceTable] (
        [ID] [int] PRIMARY KEY CLUSTERED,
        [FirstName] nvarchar(8)
        );
    
    INSERT [SourceDatabase].[dbo].[SourceTable]
    VALUES (1, N'Bob'),
        (2, N'Susan');
    GO

    -- Create a database with a MEMORY_OPTIMIZED_DATA filegroup

    CREATE DATABASE DestinationDatabase
     ON  PRIMARY 
    ( NAME = N'DestinationDatabase_Data', FILENAME = N'D:\DATA\DestinationDatabase_Data.mdf',   SIZE = 8MB), 
     FILEGROUP [DestinationDatabase_mod] CONTAINS MEMORY_OPTIMIZED_DATA  DEFAULT
    ( NAME = N'DestinationDatabase_mod', FILENAME = N'D:\DATA\DestinationDatabase_mod', MAXSIZE = UNLIMITED)
     LOG ON 
    ( NAME = N'DestinationDatabase_Log', FILENAME = N'D:\LOG\DestinationDatabase_Log.ldf', SIZE = 8MB);
    
    ALTER DATABASE DestinationDatabase SET RECOVERY SIMPLE;
    GO
    
    USE DestinationDatabase;
    GO

    -- Create a memory-optimized table
    CREATE TABLE [dbo].[DestTable_InMem] (
        [ID] [int] PRIMARY KEY NONCLUSTERED,
        [FirstName] nvarchar(8)
        )
    WITH ( MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA );
    GO
    ```

2.  데이터베이스 간 쿼리를 시도합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 에서 다음 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]명령을 실행합니다.
  
    ```tsql  
    INSERT [DestinationDatabase].[dbo].[DestTable_InMem]
    SELECT * FROM [SourceDatabase].[dbo].[SourceTable]
    ```  

    다음과 같은 오류 메시지가 나타납니다.
    > 메시지 41317, 수준 16, 상태 5  
    > 메모리 액세스에 최적화된 테이블 또는 고유하게 컴파일된 모듈에 액세스하는 사용자 트랜잭션은 둘 이상의 사용자 데이터베이스 또는 데이터베이스 모델 및 msdb에 액세스할 수 없으며 master에 쓸 수 없습니다.

3.  메모리 액세스에 최적화된 테이블 형식을 만듭니다.  [!INCLUDE[tsql](../../includes/tsql-md.md)] 에서 다음 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]명령을 실행합니다.

    ```tsql
    USE DestinationDatabase;
    GO
    
    CREATE TYPE [dbo].[MemoryType]  
        AS TABLE  
        (  
        [ID] [int] PRIMARY KEY NONCLUSTERED,
        [FirstName] nvarchar(8)
        )  
        WITH  
            (MEMORY_OPTIMIZED = ON);  
    GO
    ```

4.  데이터베이스 간 쿼리를 다시 시도합니다.  이때 원본 데이터가 먼저 메모리 액세스에 최적화된 테이블 변수로 전송됩니다.  그런 다음 테이블 변수의 데이터가 메모리 액세스에 최적화된 테이블에 전송됩니다.
    ```tsql
    -- Declare table variable utilizing the newly created type - MemoryType
    DECLARE @InMem dbo.MemoryType;
    
    -- Populate table variable
    INSERT @InMem SELECT * FROM SourceDatabase.[dbo].[SourceTable];
    
    -- Populate the destination memory-optimized table
    INSERT [DestinationDatabase].[dbo].[DestTable_InMem] SELECT * FROM @InMem;
    GO 
    ```
   
## <a name="see-also"></a>관련 항목:  
 [메모리 내 OLTP로 마이그레이션](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  

