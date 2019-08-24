---
title: 메모리 최적화 테이블 변수 | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: bd102e95-53e2-4da6-9b8b-0e4f02d286d3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 485f481819a9712f822f969c04d8e7050ad43bae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62774430"
---
# <a name="memory-optimized-table-variables"></a>메모리 액세스에 최적화된 테이블 변수
  효율적인 데이터 액세스를 위한 메모리 최적화 테이블 및 효율적인 쿼리 처리 및 비즈니스 논리 실행을 위한 고유하게 컴파일된 저장 프로시저 이외에 [!INCLUDE[hek_2](../includes/hek-2-md.md)]은 메모리 최적화 테이블 형식이라는 세 번째 개체를 도입했습니다. 메모리 최적화 테이블 형식을 사용하여 만든 테이블 변수가 메모리 최적화 테이블 변수입니다.  
  
 메모리 액세스에 최적화된 테이블 변수는 디스크 기반 테이블 변수에 비해 다음과 같은 이점을 제공합니다.  
  
-   변수가 메모리에만 저장됩니다. 특히 변수가 고유하게 컴파일된 저장 프로시저에서 사용될 경우, 메모리 최적화 테이블 형식은 메모리 최적화 테이블에 사용된 것과 동일한 메모리 최적화 알고리즘 및 데이터 구조를 사용하므로 데이터 액세스가 더 효율적입니다.  
  
-   메모리 최적화 테이블 변수를 사용하면 tempdb가 사용되지 않습니다. 테이블 변수는 tempdb에 저장되지 않으므로 tempdb에서 리소스를 사용하지 않습니다.  
  
 메모리 최적화 테이블 변수에 대한 일반적인 사용 시나리오는 다음과 같습니다.  
  
-   중간 결과를 저장하고 고유하게 컴파일된 저장 프로시저에 있는 여러 쿼리를 기반으로 단일 결과 집합을 만듭니다.  
  
-   테이블 반환 매개 변수를 고유하게 컴파일된 저장 프로시저와 해석된 저장 프로시저에 전달합니다.  
  
-   디스크 기반 테이블 변수를 바꾸고 경우에 따라 저장 프로시저에 로컬인 #temp 테이블을 교체합니다. 시스템에서 tempdb 경합이 많은 경우에 특히 유용합니다.  
  
-   테이블 변수를 사용하여 고유하게 컴파일된 저장 프로시저에서 커서를 시뮬레이트할 수 있으며, 이를 통해 고유하게 컴파일된 저장 프로시저에서 화면 영역 제한을 해결할 수 있습니다.  
  
 메모리 최적화 테이블과 마찬가지로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 메모리 최적화 테이블 형식별로 하나의 DLL을 생성합니다. (컴파일은 메모리 최적화 테이블 형식을 만들 때, 그리고 호출을 메모리 최적화 테이블 변수를 만드는 데 사용 하는 경우에 없습니다.) 이 DLL은 인덱스에 액세스하고 테이블 변수에서 데이터를 검색하는 함수를 포함합니다. 테이블 형식을 기반으로 메모리 최적화 테이블 변수를 선언할 경우 테이블 형식에 따라 테이블 및 인덱스 구조의 인스턴스가 사용자 세션에 만들어집니다. 이 테이블 변수는 디스크 기반 테이블 변수와 동일한 방법으로 사용할 수 있습니다. 테이블 변수에서 행을 삽입, 업데이트 및 삭제하고 [!INCLUDE[tsql](../includes/tsql-md.md)] 쿼리에서 변수를 사용할 수 있습니다. 변수를 고유하게 컴파일된 저장 프로시저와 해석된 저장 프로시저에 TVP(테이블 반환 매개 변수)로 전달할 수도 있습니다.  
  
 다음 샘플 AdventureWorks 기반 메모리 내 OLTP 샘플에서 메모리 최적화 테이블 형식을 보여 줍니다 ([SQL Server 2014 메모리 내 OLTP 샘플](https://msftdbprodsamples.codeplex.com/releases/view/114491)).  
  
```sql
CREATE TYPE Sales.SalesOrderDetailType_inmem
   AS TABLE
(
   OrderQty         smallint   NOT NULL,
   ProductID        int        NOT NULL,

   SpecialOfferID   int        NOT NULL
      INDEX  IX_SpecialOfferID  NONCLUSTERED,

   LocalID          int        NOT NULL,

   INDEX IX_ProductID HASH (ProductID)
      WITH ( BUCKET_COUNT = 8 )
)
WITH ( MEMORY_OPTIMIZED = ON );
```  
  
 이 예제에서는 다음 사항을 제외하고 메모리 최적화 테이블 형식의 구문이 디스크 기반 테이블 형식과 비슷함을 보여 줍니다.  
  
-   `MEMORY_OPTIMIZED=ON`은 테이블 형식이 메모리 최적화 형식인지 여부를 나타냅니다.  
  
-   이 형식에 적어도 한 개의 인덱스가 있어야 합니다. 메모리 최적화 테이블과 마찬가지로 해시 및 비클러스터형 인덱스를 사용할 수 있습니다.  
  
     해시 인덱스의 경우 버킷 수는 예상 고유 인덱스 키 개수의 약 1~2배 사이여야 합니다. 자세한 내용은 [해시 인덱스에 대 한 올바른 버킷 수를 결정](../relational-databases/indexes/indexes.md)합니다.  
  
-   메모리 최적화 테이블에 대한 데이터 형식 및 제약 조건 제한은 메모리 최적화 테이블 형식에도 적용됩니다. 예를 들어, [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 기본 제약 조건은 지원되지만 CHECK 제약 조건은 지원되지 않습니다.  
  
 메모리 최적화 테이블과 마찬가지로 메모리 최적화 테이블 변수에는 다음과 같은 특징이 있습니다.  
  
-   병렬 계획을 지원하지 않습니다.  
  
-   메모리 크기에 맞아야 하고 디스크 리소스를 사용하지 않습니다.  
  
 디스크 기반 테이블 변수는 tempdb에 있습니다. 메모리 액세스에 최적화된 테이블 변수는 사용자 데이터베이스에 있지만, 스토리지를 사용하지 않으므로 복구되지 않습니다.  
  
 인라인 구문을 사용하여 메모리 최적화 테이블 변수를 만들 수 없습니다. 디스크 기반 테이블 변수와 달리 먼저 형식을 만들어야 합니다.  
  
## <a name="table-valued-parameters"></a>테이블 반환 매개 변수  
 다음 예제 스크립트는 메모리 최적화 테이블 형식 `Sales.SalesOrderDetailType_inmem`으로 테이블 변수를 선언하고, 변수에 세 행을 삽입하고, 변수를 `Sales.usp_InsertSalesOrder_inmem`에 TVP로 전달하는 과정을 보여 줍니다.  
  
```sql  
DECLARE @od Sales.SalesOrderDetailType_inmem,  
  @SalesOrderID uniqueidentifier,  
  @DueDate datetime2 = SYSDATETIME()  
  
INSERT @od (LocalID, ProductID, OrderQty, SpecialOfferID) VALUES  
  (1, 888, 2, 1),  
  (2, 450, 13, 1),  
  (3, 841, 1, 1)  
  
EXEC Sales.usp_InsertSalesOrder_inmem  
  @SalesOrderID = @SalesOrderID,  
  @DueDate = @DueDate,  
 @OnlineOrderFlag = 1,  
  @SalesOrderDetails = @od  
```  
  
 메모리 액세스에 최적화된 테이블 형식을 저장 프로시저 TVP(테이블 반환 매개 변수)에 대한 형식으로 사용하고 디스크 기반 테이블 형식 및 TVP와 동일한 클라이언트에서 참조할 수 있습니다. 따라서 메모리 최적화 TVP를 통한 저장 프로시저 호출 및 고유하게 컴파일된 저장 프로시저 호출 작업은 디스크 기반 TVP를 통한 해석된 저장 프로시저 호출 작업과 동일합니다.  
  
## <a name="temp-table-replacement"></a>#temp 테이블 바꾸기  
 다음 예제에서는 메모리 최적화 테이블 형식 및 테이블 변수를 저장 프로시저에 로컬인 #temp 테이블에 대한 대체 값으로 보여 줍니다.  
  
```sql  
-- Using SQL procedure and temp table  
CREATE TABLE #tempTable (c INT NOT NULL PRIMARY KEY NONCLUSTERED)  
  
CREATE PROCEDURE sqlProc  
AS  
BEGIN  
  TRUNCATE TABLE #tempTable  
  
  INSERT #tempTable VALUES (1)  
  INSERT #tempTable VALUES (2)  
  INSERT #tempTable VALUES (3)  
  SELECT * FROM #tempTable  
END  
GO  
  
-- Using natively compiled stored procedure and table variable  
CREATE TYPE TT AS TABLE (c INT NOT NULL PRIMARY KEY NONCLUSTERED)  
GO  
  
CREATE PROCEDURE NCSPProc  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  DECLARE @tableVariable TT  
  INSERT @tableVariable VALUES (1)  
  INSERT @tableVariable VALUES (2)  
  INSERT @tableVariable VALUES (3)  
  SELECT c FROM @tableVariable  
END  
GO  
```  
  
## <a name="creating-a-single-result-set"></a>단일 결과 집합 만들기  
 다음 예제에서는 중간 결과를 저장하고 고유하게 컴파일된 저장 프로시저에 있는 여러 쿼리를 기반으로 단일 결과 집합을 만드는 방법을 보여 줍니다. 이 예제는 통합 `SELECT c1 FROM dbo.t1 UNION SELECT c1 FROM dbo.t2`를 계산합니다.  
  
```sql  
CREATE DATABASE hk  
GO  
ALTER DATABASE hk ADD FILEGROUP hk_mod CONTAINS MEMORY_OPTIMIZED_DATA  
ALTER DATABASE hk ADD FILE( NAME = 'hk_mod' , FILENAME = 'c:\data\hk_mod') TO FILEGROUP hk_mod;  
  
USE hk  
GO  
  
CREATE TYPE tab1 AS TABLE (c1 INT NOT NULL, INDEX idx NONCLUSTERED(c1)) WITH (MEMORY_OPTIMIZED = ON)  
  
CREATE TABLE dbo.t1 (c1 INT NOT NULL, INDEX idx NONCLUSTERED(c1)) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
CREATE TABLE dbo.t2 (c1 INT NOT NULL, INDEX idx NONCLUSTERED(c1)) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
  
INSERT INTO dbo.t1 VALUES (1), (2)  
INSERT INTO dbo.t2 VALUES (3), (4)  
GO  
  
CREATE PROCEDURE dbo.p1  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
  AS  
  BEGIN ATOMIC WITH ( TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english' )  
  
    DECLARE @t dbo.tab1  
    INSERT @t (c1)  
    SELECT c1 FROM dbo.t1;  
  
    INSERT @t (c1)  
    SELECT c1 FROM dbo.t2;  
  
    SELECT c1 FROM @t;  
  END  
GO  
  
EXEC dbo.p1  
GO  
```  
  
## <a name="memory-consumption-for-table-variables"></a>테이블 변수에 대한 메모리 사용  
 테이블 변수에 대한 메모리 사용은 비클러스터형 인덱스를 제외하고 메모리 최적화 테이블과 유사합니다. 비클러스터형 인덱스를 포함한 메모리 최적화 테이블 변수에 대량의 행을 삽입하고 인덱스 키가 클 경우, 이러한 테이블 변수에는 잘못된 양의 메모리가 사용됩니다. 큰 테이블 변수에 대한 비클러스터형 인덱스는 테이블(인덱스 페이지의 추가 메모리)에 삽입된 동일한 행 수에 대해 비클러스터형 인덱스에 필요한 것보다 더 많은 메모리가 그에 비례하여 필요합니다.  
  
 테이블 변수에 대한 메모리는 데이터베이스의 리소스 관리자 리소스 풀에서 제공됩니다.  
  
 메모리 최적화 테이블과는 달리 테이블 변수에 의해 (삭제된 행을 포함하여) 사용되는 메모리는 테이블 변수가 범위를 벗어날 때 해제됩니다.  
  
 메모리는 데이터베이스의 단일 PGPOOL 메모리 소비자의 일부로 계산됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [메모리 내 OLTP에 대한 Transact-SQL 지원](../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)  
  
  
