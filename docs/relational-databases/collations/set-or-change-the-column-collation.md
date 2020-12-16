---
description: 열 데이터 정렬 설정 또는 변경
title: 열 데이터 정렬 설정 또는 변경 | Microsoft 문서
ms.custom: ''
ms.date: 12/05/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- tempdb database [SQL Server], collations
- collations [SQL Server], column
ms.assetid: d7a9638b-717c-4680-9b98-8849081e08be
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3f408175a59484aa162c0db654ebf4b1d5656901
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460586"
---
# <a name="set-or-change-the-column-collation"></a>열 데이터 정렬 설정 또는 변경
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  특정 테이블의 열에 대해 다른 데이터 정렬을 지정하고 다음 중 하나를 사용하여 **char**, **varchar**, **text**, **nchar**, **nvarchar** 및 **ntext** 데이터의 데이터베이스 데이터 정렬을 재정의할 수 있습니다.  
  
-   아래 예제와 같이 [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) 및 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)의 COLLATE 절. 

    -   **바로 변환.** 아래 정의된 기존 테이블 중 하나를 고려합니다.

        ```sql
        -- NVARCHAR column is encoded in UTF-16 because a supplementary character enabled collation is used
        CREATE TABLE dbo.MyTable (CharCol NVARCHAR(50) COLLATE Latin1_General_100_CI_AI_SC);

        -- VARCHAR column is encoded the Latin code page and therefore is not Unicode capable
        CREATE TABLE dbo.MyTable (CharCol VARCHAR(50) COLLATE Latin1_General_100_CI_AI);
        ```

        UTF-8을 사용하기 위해 열을 바로 변환하려면 필요한 데이터 형식과 UTF-8 사용 가능 데이터 정렬을 설정하는 `ALTER COLUMN` 문을 실행합니다.

        ```sql 
        ALTER TABLE dbo.MyTable 
        ALTER COLUMN CharCol VARCHAR(50) COLLATE Latin1_General_100_CI_AI_SC_UTF8
        ```

        이 방법은 구현하기 쉽지만, 큰 테이블 및 많이 사용하는 애플리케이션에 문제가 될 수 있는 차단 작업일 수 있습니다.

    -   **복사 및 바꾸기.** 아래 정의된 기존 테이블 중 하나를 고려합니다.

        ```sql
        -- NVARCHAR column is encoded in UTF-16 because a supplementary character enabled collation is used
        CREATE TABLE dbo.MyTable (CharCol NVARCHAR(50) COLLATE Latin1_General_100_CI_AI_SC);
        GO

        -- VARCHAR column is encoded using the Latin code page and therefore is not Unicode capable
        CREATE TABLE dbo.MyTable (CharCol VARCHAR(50) COLLATE Latin1_General_100_CI_AI);
        GO
        ```

        열을 변환하여 UTF-8을 사용하려면 대상 열이 이미 필요한 데이터 형식 및 UTF-8 사용 가능 데이터 정렬인 새 테이블에 데이터를 복사한 다음, 이전 테이블을 다음과 같이 바꿉니다.

        ```sql
        CREATE TABLE dbo.MyTableNew (CharCol VARCHAR(50) COLLATE Latin1_General_100_CI_AI_SC_UTF8);
        GO
        INSERT INTO dbo.MyTableNew 
        SELECT * FROM dbo.MyTable;
        GO
        DROP TABLE dbo.MyTable;
        GO
        EXEC sp_rename 'dbo.MyTableNew', 'dbo.MyTable';
        GO
        ```

        이 방법은 바로 변환보다 훨씬 더 빠르지만, 많은 종속성(FK, PK, 트리거, DF)을 포함하는 복잡한 스키마를 처리하고 테이블의 뒷부분을 동기화(데이터베이스를 사용 중인 경우)하는 데 더 많은 계획이 필요합니다.
        
    자세한 내용은 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 자세한 내용은 [열 수정(데이터베이스 엔진)](../../relational-databases/tables/modify-columns-database-engine.md#SSMSProcedure)을 참조하세요.  
  
-   SMO( **Management Objects)의** Column.Collation [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 속성 사용  
  
 다음 중 하나가 현재 참조하고 있는 열의 데이터 정렬은 변경할 수 없습니다.  
  
-   계산 열  
-   인덱스  
-   자동으로 또는 `CREATE STATISTICS` 문에 의해 생성된 배포 통계  
-   CHECK 제약 조건  
-   FOREIGN KEY 제약 조건  
  
 **tempdb** 를 사용할 때 [COLLATE](~/t-sql/statements/collations.md) 절은 *database_default* 옵션을 포함하여 임시 테이블에 있는 열이 **tempdb** 의 데이터 정렬 대신 현재 사용자 데이터베이스의 데이터 정렬 기본값을 연결에 사용하도록 지정합니다.  
  
## <a name="collations-and-text-columns"></a>데이터 정렬 및 텍스트 열  
 **text** 열에는 데이터 정렬이 데이터베이스 기본 데이터 정렬의 코드 페이지와 다른 값을 삽입하거나 업데이트할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 값을 열의 데이터 정렬로 암시적으로 변환합니다.  
  
## <a name="collations-and-tempdb"></a>데이터 정렬 및 tempdb  
 **tempdb** 데이터베이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 시작될 때마다 작성되며 **model** 데이터베이스와 같은 기본 데이터 정렬을 사용합니다. 이는 일반적으로 인스턴스의 기본 데이터 정렬과 같습니다. 사용자 데이터베이스를 만들고 **model** 과 다른 기본 데이터 정렬을 지정하면 사용자 데이터베이스는 **tempdb** 와 다른 기본 데이터 정렬을 사용합니다. 모든 임시 저장 프로시저나 임시 테이블은 **tempdb** 에서 생성되고 저장됩니다. 즉, 임시 테이블의 모든 암시적 열과 임시 저장 프로시저의 모든 강제 기본 상수, 변수 및 매개 변수는 영구 테이블 및 저장 프로시저에서 만들어진 유사 개체와는 다른 데이터 정렬을 사용합니다.  
  
 이로 인해 사용자 정의 데이터베이스와 시스템 데이터베이스 개체 간에 데이터 정렬 불일치 문제가 발생할 수 있습니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서는 Latin1_General_CS_AS 데이터 정렬을 사용하는데 다음 문을 실행합니다.  
  
```sql  
CREATE DATABASE TestDB COLLATE Estonian_CS_AS;  
USE TestDB;  
CREATE TABLE TestPermTab (PrimaryKey int PRIMARY KEY, Col1 nchar );  
```  
  
 이 시스템에서 **tempdb** 데이터베이스는 코드 페이지 1252를 포함하는 Latin1_General_CS_AS 데이터 정렬을 사용하고 `TestDB` 및 `TestPermTab.Col1` 은 코드 페이지 1257을 포함하는 `Estonian_CS_AS` 데이터 정렬을 사용합니다. 예를 들면 다음과 같습니다.  
  
```sql  
USE TestDB;  
GO  
-- Create a temporary table with the same column declarations  
-- as TestPermTab  
CREATE TABLE #TestTempTab (PrimaryKey int PRIMARY KEY, Col1 nchar );  
INSERT INTO #TestTempTab  
         SELECT * FROM TestPermTab;  
GO  
```  
  
 이전 예에서 **tempdb** 데이터베이스는 Latin1_General_CS_AS 데이터 정렬을 사용하고 `TestDB` 및 `TestTab.Col1` 은 `Estonian_CS_AS` 데이터 정렬을 사용합니다. 예를 들면 다음과 같습니다.  
  
```sql  
SELECT * FROM TestPermTab AS a INNER JOIN #TestTempTab on a.Col1 = #TestTempTab.Col1;  
```  
  
 **tempdb** 는 기본 서버 데이터 정렬을 사용하고 `TestPermTab.Col1` 은 다른 데이터 정렬을 사용하므로 SQL Server는 "같음 작업에서 'Latin1_General_CI_AS_KS_WS'과(와) 'Estonian_CS_AS' 간의 데이터 정렬 충돌을 해결할 수 없습니다"라는 오류를 반환합니다.  
  
 이 오류를 방지하는 데 사용할 수 있는 방법은 다음과 같습니다.  
  
-   임시 테이블 열이 **tempdb** 가 아닌 사용자 데이터베이스의 기본 데이터 정렬을 사용하도록 지정합니다. 이렇게 하면 시스템에서 요구할 경우 임시 테이블은 여러 데이터베이스에 있는 유사한 형식의 테이블로 작업할 수 있습니다.  
  
    ```sql  
    CREATE TABLE #TestTempTab  
       (PrimaryKey int PRIMARY KEY,  
        Col1 nchar COLLATE database_default  
       );  
    ```  
  
-   `#TestTempTab` 열에 대해 올바른 데이터 정렬을 지정합니다.  
  
    ```sql  
    CREATE TABLE #TestTempTab  
       (PrimaryKey int PRIMARY KEY,  
        Col1 nchar COLLATE Estonian_CS_AS  
       );  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [서버 데이터 정렬 설정 또는 변경](../../relational-databases/collations/set-or-change-the-server-collation.md)   
 [데이터베이스 데이터 정렬 설정 또는 변경](../../relational-databases/collations/set-or-change-the-database-collation.md)   
 [데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  
