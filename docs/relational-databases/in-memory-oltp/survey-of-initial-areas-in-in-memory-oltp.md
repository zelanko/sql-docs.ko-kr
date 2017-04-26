---
title: "빠른 시작 1: 더 빠른 Transact-SQL 성능을 위한 메모리 내 OLTP 기술 | Microsoft 문서"
ms.custom: 
ms.date: 12/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1c25a164-547d-43c4-8484-6b5ee3cbaf3a
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 82286b0d52ff37697ad9197b88c45935137a8dae
ms.lasthandoff: 04/11/2017

---
# <a name="survey-of-initial-areas-in-in-memory-oltp"></a>메모리 내 OLTP에서 초기 영역 설문 조사
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  
이 문서는 Microsoft SQL Server 및 Azure SQL 데이터베이스의 메모리 내 OLTP 성능 기능의 기본 사항을 급히 알아보려는 개발자를 위해 작성되었습니다.  
  
이 문서에서는 메모리 내 OLTP에 대해 다음 사항을 제공합니다.  
  
- 기능에 대한 빠른 설명  
- 기능을 구현하는 핵심 코드 샘플  
  
  
사소한 점을 제외하고 메모리 내 기술 지원과 관련된 SQL Server와 SQL 데이터베이스의 차이는 거의 없습니다.  
  
  
일부 블로거들은 비공식적으로 메모리 내 OLTP를 *Hekaton*이라고도 합니다.  
  
  
<a name="benefits-of-in-memory-features-21a"></a>  
  
## <a name="benefits-of-in-memory-features"></a>메모리 내 기능의 이점  
  
SQL Server는 많은 응용 프로그램 시스템의 성능을 크게 향상시킬 수 있는 메모리 내 기능을 제공합니다. 이 섹션에서는 가장 명확한 고려 사항에 대해 설명합니다.  
  
  
### <a name="features-for-oltp-online-transactional-processing"></a>OLTP(온라인 트랜잭션 처리) 기능  
  
  
동시에 다수의 SQL INSERT를 처리해야 하는 시스템이 OLTP 기능에 가장 적합합니다.  
  
- 벤치마크 결과에 따르면 메모리 내 기능을 도입할 경우 속도가 5배에서 20배까지 향상됩니다.  
  
  
Transact-SQL 계산을 많이 처리하는 시스템도 적합합니다.  
  
- 복잡한 계산 전용의 저장 프로시저는 최대 99배까지 더 빠르게 실행할 수 있습니다.  
  
  
나중에 메모리 내 OLTP의 성능 향상 데모를 제공하는 다음 문서를 참조하는 것이 좋습니다.  
  
- [Demonstration: Performance Improvement of In-Memory OLTP](../../relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp.md) (데모: 메모리 내 OLTP의 성능 향상)에서는 더 큰 잠재적 성능 향상에 대한 소규모 데모를 제공합니다.  
- [Sample Database for In-Memory OLTP](../../relational-databases/in-memory-oltp/sample-database-for-in-memory-oltp.md) (메모리 내 OLTP에 대한 샘플 데이터베이스)에서는 규모가 더 큰 데모를 제공합니다.  
  
  
  
### <a name="features-for-operational-analytics"></a>운영 분석 기능  
  
메모리 내 분석은 일반적으로 GROUP BY 절을 포함하여 트랜잭션 데이터를 집계하는 SQL SELECT를 가리킵니다. 운영 분석에는 *columnstore* 라는 인덱스 유형이 중요합니다.  
  
다음 두 가지 주요 시나리오가 있습니다.  
  
- *배치 운영 분석* 은 업무 시간 이후 또는 트랜잭션 데이터의 복사본이 있는 보조 하드웨어에서 실행되는 집계 프로세스를 가리킵니다.  
  - [Azure SQL 데이터 웨어하우스](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-overview-what-is/) 도 배치 운영 분석과 관련이 있습니다.  
- *실시간 운영 분석* 은 업무 시간 중 및 트랜잭션 작업에 사용되는 주 하드웨어에서 실행되는 집계 프로세스를 가리킵니다.  
  
  
현재 문서에서는 분석이 아닌 OLTP에 중점을 둡니다. columnstore 인덱스에서 분석을 SQL로 가져오는 방법에 대한 자세한 내용은 다음을 참조하세요.  
  
- [실시간 운영 분석을 위한 Columnstore 시작](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)  
- [Columnstore 인덱스 가이드](../../relational-databases/indexes/columnstore-indexes-overview.md)  
  
  
> [!NOTE]
> 메모리 내 기능에 대한 동영상(2분 소요)은 [Azure SQL Database - In-Memory Technologies](http://channel9.msdn.com/Blogs/Windows-Azure/Azure-SQL-Database-In-Memory-Technologies)(Azure SQL 데이터베이스 - 메모리 내 기술)에서 확인할 수 있습니다. 이 동영상은 2015년 12월에 발표되었습니다.  


### <a name="columnstore"></a>columnstore

일련의 뛰어난 블로그 게시물은 여러 관점에서 columnstore 인덱스에 대해 설명합니다. 대부분의 게시물은 columnstore에서 지원하는 실시간 운영 분석의 개념에 대해 추가로 설명합니다.  이러한 게시물은 2016년 3월 Microsoft의 프로그램 관리자인 Sunil Agarwal이 작성한 것입니다.

#### <a name="real-time-operational-analytics"></a>실시간 운영 분석

1. [메모리 내 기술을 사용하는 실시간 운영 분석](https://blogs.technet.microsoft.com/dataplatforminsider/2015/12/09/real-time-operational-analytics-using-in-memory-technology/)
2. [실시간 운영 분석 - NCCI(비클러스터형 columnstore 인덱스) 개요](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/02/29/real-time-operational-analytics-using-nonclustered-columnstore-index/)
3. [실시간 운영 분석: SQL Server 2016에서 NCCI(비클러스터형 columnstore 인덱스)를 사용하는 간단한 예제](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/02/29/real-time-operational-analytics-simple-example-using-nonclustered-clustered-columnstore-index-ncci/)
4. [실시간 운영 분석: SQL Server 2016의 DML 작업 및 NCCI(비클러스터형 columnstore 인덱스)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/04/real-time-operational-analytics-dml-operations-and-nonclustered-columnstore-index-ncci-in-sql-server-2016/)
5. [실시간 운영 분석: 필터링된 NCCI(비클러스터형 columnstore 인덱스)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-filtered-nonclustered-columnstore-index-ncci/)
6. [실시간 운영 분석: NCCI(비클러스터형 Columnstore 인덱스)의 압축 지연 옵션](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-compression-delay-option-for-nonclustered-columnstore-index-ncci/)
7. [실시간 운영 분석: NCCI의 압축 지연 옵션 및 성능](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-compression-delay-option-with-ncci-and-the-performance/)
8. [실시간 운영 분석: 메모리 액세스에 최적화된 테이블 및 Columnstore 인덱스](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/07/real-time-operational-analytics-memory-optimized-table-and-columnstore-index/)

#### <a name="defragment-a-columnstore-index"></a>Columnstore 인덱스를 조각 모음합니다.

1. [REORGANIZE 명령을 사용하여 Columnstore 인덱스 조각 모음](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/07/columnstore-index-defragmentation-using-reorganize-command/)
2. [REORGANIZE의 Columnstore 인덱스 병합 정책](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/08/columnstore-index-merge-policy-for-reorganize/)

#### <a name="bulk-importation-of-data"></a>데이터 대량 가져오기

1. [클러스터형 열 저장소: 대량 로드](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2014/07/27/clustered-column-store-index-bulk-loading-the-data/)
2. [클러스터형 Columnstore 인덱스: 데이터 로드 최적화 – 최소 로깅](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/10/clustered-columnstore-index-data-load-optimizations-minimal-logging/)
3. [클러스터형 columnstore 인덱스: 데이터 로드 최적화 – 병렬로 대량 가져오기](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/02/28/clustered-columnstore-index-parallel-bulk-import/)





<a name="features-on-in-memory-oltp-13b"></a>  
  
## <a name="features-of-in-memory-oltp"></a>메모리 내 OLTP의 기능  
  
메모리 내 OLTP의 주요 기능을 살펴보겠습니다.  
  
  
#### <a name="memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블  
  
CREATE TABLE 문에서 T-SQL 키워드 MEMORY_OPTIMIZED는 디스크가 아니라 활성 메모리에 있도록 테이블을 만드는 방법입니다.  
  
  
[메모리 액세스에 최적화된 테이블](../../relational-databases/in-memory-oltp/memory-optimized-tables.md) 은 활성 메모리에 포함될 뿐 아니라 디스크에도 보조 복사본이 있습니다.  
  
- 디스크 복사본은 서버 또는 데이터베이스가 종료된 다음 다시 시작한 후 일상적인 복구를 위해 사용됩니다. 이 메모리 및 디스크의 중복성은 사용자와 코드에서 완전히 숨겨집니다.  
  
  
#### <a name="natively-compiled-modules"></a>고유하게 컴파일된 모듈  
  
CREATE PROCEDURE 문에서 T-SQL 키워드 NATIVE_COMPILATION은 네이티브 프로시저를 만드는 방법입니다. 온라인에서 데이터베이스를 순환할 때마다 네이티브 프로시저를 처음 사용할 때 T-SQL 문이 기계어 코드로 컴파일됩니다. T-SQL 명령이 각 명령의 느린 해석을 더 이상 허용하지 않습니다.  
  
- 네이티브 컴파일 결과를 확인하는 데 해석된 프로시저 기간의 1/100 정도밖에 걸리지 않았습니다.  
  
  
네이티브 모듈은 메모리 액세스에 최적화된 테이블만 참조할 수 있으며, 디스크 기반 테이블은 참조할 수 없습니다.  
  
고유하게 컴파일된 모듈에는 다음 세 가지 유형이 있습니다.  
  
- [네이티브 컴파일 저장 프로시저](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
- 네이티브 컴파일 UDF(사용자 정의 함수), 스칼라  
- 네이티브 컴파일 트리거  
  
  
#### <a name="availability-in-azure-sql-database"></a>Azure SQL 데이터베이스의 가용성  
  
메모리 내 OLTP 및 Columnstore를 Azure SQL Database에서 사용할 수 있습니다. 자세한 내용은 [SQL Database에서 메모리 내 기술을 사용하여 성능 최적화](https://docs.microsoft.com/azure/sql-database/sql-database-in-memory)를 참조하세요.
  
  
<a name="ensure-compatibility-level-gteq-130-99c"></a>  
  
## <a name="1-ensure-compatibility-level--130"></a>1. 호환성 수준을 130 이상으로 설정  
  
  
이 섹션의 앞부분에 나오는 번호가 지정된 일련의 섹션에서는 메모리 내 OLTP 기능을 구현하는 데 사용할 수 있는 Transact-SQL 구문을 보여 줍니다.  
  
  
먼저 데이터베이스의 호환성 수준을 적어도 130 이상으로 설정하는 것이 중요합니다. 다음은 현재 데이터베이스에 설정된 현재 호환성 수준을 보여 주는 T-SQL 코드입니다.  
  
  
  
  
  
    SELECT d.compatibility_level  
        FROM sys.databases as d  
        WHERE d.name = Db_Name();  
  
  
  
  
다음은 필요할 경우 수준을 업데이트하는 T-SQL 코드입니다.  
  
  
  
  
    ALTER DATABASE CURRENT  
        SET COMPATIBILITY_LEVEL = 130;  
  
  
  
  
<a name="elevate-to-snapshot-26n"></a>  
  
## <a name="2-elevate-to-snapshot"></a>2. SNAPSHOT으로 권한 상승  
  
  
트랜잭션에 디스크 기반 테이블과 메모리 액세스에 최적화된 테이블이 모두 포함되어 있을 경우 *컨테이너 간 트랜잭션*이라고 합니다. 이러한 트랜잭션에서 메모리 액세스에 최적화된 트랜잭션 부분은 SNAPSHOT이라고 하는 트랜잭션 격리 수준에서 작동해야 합니다.  
  
컨테이너 간 트랜잭션에서 메모리 액세스에 최적화된 테이블에 대해 이 수준을 안정적으로 적용하려면 다음 T-SQL을 실행하여 [데이터베이스 설정을 변경](../../t-sql/statements/alter-database-transact-sql-set-options.md)합니다.  
  
  
  
  
    ALTER DATABASE CURRENT  
        SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;  
  
  
  
  
<a name="create-an-optimized-filegroup-24r"></a>  
  
## <a name="3-create-an-optimized-filegroup"></a>3. 최적화된 FILEGROUP 만들기  
  
  
Microsoft SQL Server에서 메모리 액세스에 최적화된 테이블을 만들려면 먼저 CONTAINS MEMORY_OPTIMIZED_DATA를 선언하는 FILEGROUP을 만들어야 합니다. 이렇게 하면 FILEGROUP이 데이터베이스에 할당됩니다. 자세한 내용은 다음을 참조하세요.  
  
- [메모리 액세스에 최적화된 FILEGROUP](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)  
  
  
Azure SQL 데이터베이스에서는 이러한 FILEGROUP을 만들 수 없으며, 만들 필요도 없습니다.  

다음 샘플 T-SQL 스크립트는 메모리 내 OLTP에 데이터베이스를 사용하고 모든 권장 설정을 구성합니다. 이는 SQL Server와 Azure SQL Database 둘 다에서 작동합니다([enable-in-memory-oltp.sql](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/enable-in-memory-oltp.sql)).
  
  
<a name="create-a-memory-optimized-table-26y"></a>  
  
## <a name="4-create-a-memory-optimized-table"></a>4. 메모리 액세스에 최적화된 테이블 만들기  
  
  
  
  
중요한 Transact-SQL 키워드는 MEMORY_OPTIMIZED 키워드입니다.  
  
  
  
  
    CREATE TABLE dbo.SalesOrder  
    (  
        SalesOrderId   integer        not null  IDENTITY  
            PRIMARY KEY NONCLUSTERED,  
        CustomerId     integer        not null,  
        OrderDate      datetime       not null  
    )  
        WITH  
            (MEMORY_OPTIMIZED = ON,  
            DURABILITY = SCHEMA_AND_DATA);  
  
  
  
  
메모리 액세스에 최적화된 테이블에 대한 Transact-SQL INSERT 및 SELECT 문은 일반 테이블의 경우와 동일합니다.  
  
#### <a name="alter-table-for-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블에 대한 ALTER TABLE  
  
ALTER TABLE... ADD/DROP은 메모리 액세스에 최적화된 테이블 또는 인덱스에서 열을 추가하거나 제거할 수 있습니다.  
  
- CREATE INDEX 및 DROP INDEX는 메모리 액세스에 최적화된 테이블에 대해 실행할 수 없습니다. 대신 ALTER TABLE ... ADD/DROP INDEX를 사용하세요.  
- 자세한 내용은 [메모리 액세스에 최적화된 테이블 변경](../../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md)을 참조하세요.  
  
  
#### <a name="plan-your-memory-optimized-tables-and-indexes"></a>메모리 액세스에 최적화된 테이블과 인덱스 계획  
  
  
- [메모리 액세스에 최적화된 테이블의 인덱스](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)  
- [메모리 내 OLTP에서 지원되지 않는 Transact-SQL 구문](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
  
<a name="create-a-natively-compiled-stored-procedure-native-proc-29u"></a>  
  
## <a name="5-create-a-natively-compiled-stored-procedure-native-proc"></a>5. 네이티브 컴파일 저장 프로시저 만들기(기본 프로시저)  
  
  
중요한 키워드는 NATIVE_COMPILATION입니다.  
  
  
  
  
    CREATE PROCEDURE ncspRetrieveLatestSalesOrderIdForCustomerId  
        @_CustomerId   INT  
        WITH  
            NATIVE_COMPILATION,  
            SCHEMABINDING  
    AS  
    BEGIN ATOMIC  
        WITH  
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
            LANGUAGE = N'us_english')  
      
        DECLARE @SalesOrderId int, @OrderDate datetime;  
      
        SELECT TOP 1  
                @SalesOrderId = s.SalesOrderId,  
                @OrderDate    = s.OrderDate  
            FROM dbo.SalesOrder AS s  
            WHERE s.CustomerId = @_CustomerId  
            ORDER BY s.OrderDate DESC;  
      
        RETURN @SalesOrderId;  
    END;  
  
  
  
  
키워드 SCHEMABINDING은 기본 프로시저가 먼저 삭제되지 않으면 기본 프로시저에서 참조하는 테이블을 삭제할 수 없음을 의미합니다. 자세한 내용은 [네이티브 컴파일 저장 프로시저 만들기](../../relational-databases/in-memory-oltp/creating-natively-compiled-stored-procedures.md)를 참조하세요.  
  
  
<a name="execute-the-native-proc-31e"></a>  
  
## <a name="6-execute-the-native-proc"></a>6. 기본 프로시저 실행  
  
  
테이블을 두 개의 데이터 행으로 채웁니다.  
  
  
  
  
    INSERT into dbo.SalesOrder  
            ( CustomerId, OrderDate )  
        VALUES  
            ( 42, '2013-01-13 03:35:59' ),  
            ( 42, '2015-01-15 15:35:59' );  
  
  
  
  
네이티브 컴파일 저장 프로시저에 대한 EXECUTE 호출이 그 뒤를 따릅니다.  
  
  
  
  
    DECLARE @LatestSalesOrderId int, @mesg nvarchar(128);  
      
    EXECUTE @LatestSalesOrderId =  
        ncspRetrieveLatestSalesOrderIdForCustomerId 42;  
      
    SET @mesg = CONCAT(@LatestSalesOrderId,  
        ' = Latest SalesOrderId, for CustomerId = ', 42);  
    PRINT @mesg;  
      
    -- Here is the actual PRINT output:  
    -- 2 = Latest SalesOrderId, for CustomerId = 42  
  
  
  
  
<a name="guide-to-the-documentation-and-next-steps-32w"></a>  
  
### <a name="guide-to-the-documentation-and-next-steps"></a>설명서와 다음 단계에 대한 가이드  
  
  
앞의 간단한 예제에서는 메모리 내 OLTP의 고급 기능을 학습하기 위한 토대를 제공합니다. 다음 섹션은 특별히 알고 있어야 할 고려 사항과, 각 사항에 대한 세부 정보를 볼 수 있는 위치에 대한 가이드입니다.  
  
  
  
<a name="how-do-in-memory-oltp-features-work-so-much-faster-33v"></a>  
  
## <a name="how-in-memory-oltp-features-work-so-much-faster"></a>메모리 내 OLTP 기능이 훨씬 더 빠르게 작동하는 방법  
  
  
다음 하위 섹션에서는 향상된 성능 제공을 위해 메모리 내 OLTP 기능이 내부에서 작동하는 방법에 대해 간략하게 설명합니다.  
  
  
<a name="how-do-memory-optimized-tables-perform-faster-34q"></a>  
  
### <a name="how-memory-optimized-tables-perform-faster"></a>메모리 액세스에 최적화된 테이블의 성능이 향상되는 방법  
  
  
**이중 특성:** 메모리 액세스에 최적화된 테이블은 활성 메모리에서 표현되고, 하드 디스크에도 표현되는 이중 특성이 있습니다. 각 트랜잭션은 테이블의 두 표현 방식으로 모두 커밋됩니다. 트랜잭션은 그중 더 빠른 활성 메모리 표현에 대해 작동합니다. 메모리 액세스에 최적화된 테이블은 디스크와 비교할 때 더 빨라진 활성 메모리 속도를 활용합니다. 또한 더 빨라진 활성 메모리로 인해 실제로 속도에 최적화된 고급 테이블 구조가 구현됩니다. 고급 구조는 또한 페이징되지 않아 래치 및 스핀 잠금의 오버헤드와 경합을 방지합니다.  
  
  
**잠금 없음:** 메모리 액세스에 최적화된 테이블은 데이터 무결성과 동시성 및 높은 처리량 간 경쟁하는 목표에 *최적* 의 접근 방법을 사용합니다. 트랜잭션 중 테이블은 업데이트된 데이터 행의 어떤 버전에도 잠금을 설정하지 않습니다. 이렇게 하면 일부 고용량 시스템의 경합을 크게 줄일 수 있습니다.  
  
  
**행 버전:** 잠금 대신 메모리 액세스에 최적화된 테이블은 tempdb가 아닌 테이블 자체에 업데이트된 행의 새로운 버전을 추가합니다. 원래 행은 트랜잭션이 커밋될 때까지 유지됩니다. 트랜잭션 중 다른 프로세스에서는 원래 버전의 행을 읽을 수 있습니다.  
  
- 디스크 기반 테이블의 경우 행 버전이 여러 개 만들어 지면 행 버전은 tempdb에 임시로 저장됩니다.  
  
  
**적어진 로깅:** 업데이트된 행의 이전 버전과 이후 버전은 메모리 액세스에 최적화된 테이블에서 유지됩니다. 이러한 행 쌍은 일반적으로 로그 파일에 기록된 정보의 상당 부분을 제공합니다. 이로 인해 시스템에서 기록하는 정보의 양과, 로그에 정보를 기록하는 빈도가 모두 줄어들었습니다. 그럼에도 불구하고 트랜잭션 무결성은 보장됩니다.  
  
  
<a name="how-do-native-procs-perform-faster-35x"></a>  
  
### <a name="how-native-procs-perform-faster"></a>네이티브 프로시저의 성능이 향상되는 방법  
  
일반 해석된 저장 프로시저를 네이티브 컴파일 저장 프로시저로 변환하면 런타임 시 실행하는 명령 수가 크게 줄어듭니다.  
  
  
<a name="trade-offs-of-in-memory-features-36j"></a>  
  
## <a name="trade-offs-of-in-memory-features"></a>메모리 내 기능의 상충 관계  
  
  
전산학에서 일반적인 경우와 마찬가지로 메모리 내 기능을 통해 제공되는 성능 향상은 절충안입니다. 기능이 향상될 수록 기능으로 인한 추가 비용보다 더 가치 있는 혜택이 수반됩니다. 다음에서 상충 관계에 대한 포괄적인 지침을 확인할 수 있습니다.

- [SQL Server에 메모리 내 OLTP 기능 채택 계획](../../relational-databases/in-memory-oltp/plan-your-adoption-of-in-memory-oltp-features-in-sql-server.md)

이 섹션의 나머지 부분에는 몇 가지 주요 계획 및 상충 관계 고려 사항이 나열되어 있습니다.
  
<a name="trade-offs-of-memory-optimized-tables-37d"></a>  
  
### <a name="trade-offs-of-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블의 장단점  
  
  
**메모리 추정:** 메모리 액세스에 최적화된 테이블이 사용하는 활성 메모리 양을 추정할 수 있습니다. 컴퓨터 시스템은 메모리 액세스에 최적화된 테이블을 호스트하는 데 적합한 메모리 용량을 확보해야 합니다. 자세한 내용은 다음을 참조하세요.  
  
- [메모리 사용량 모니터링 및 문제 해결](../../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md)  
- [메모리 액세스에 최적화된 테이블에 필요한 메모리 예측](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md)  
- [메모리 액세스에 최적화된 테이블의 테이블 및 행 크기](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)  
  
  
**큰 테이블 분할:** 많은 활성 메모리에 대한 요구를 충족하는 한 가지 방법은 큰 테이블을 *최근 핫* 데이터 행을 저장하는 메모리 내 부분과, *콜드 레거시* 행(예: 전체가 배송되어 완료된 판매 주문)을 저장하는 디스크 부분으로 분할하는 것입니다. 이 분할은 디자인 및 구현 단계에서 수동으로 처리됩니다. 다음을 참조하십시오.  
  
- [응용 프로그램 수준 분할](../../relational-databases/in-memory-oltp/application-level-partitioning.md)  
- [메모리 액세스에 최적화된 테이블 분할을 위한 응용 프로그램 패턴](../../relational-databases/in-memory-oltp/application-pattern-for-partitioning-memory-optimized-tables.md)  
  
  
<a name="trade-offs-of-native-procs-38p"></a>  
  
### <a name="trade-offs-of-native-procs"></a>기본 프로시저의 상충 관계  
  
  
- 네이티브 컴파일 저장 프로시저는 디스크 기반 테이블 형식에 액세스할 수 없습니다. 기본 프로시저는 메모리 액세스에 최적화된 테이블에만 액세스할 수 있습니다.  
- 서버 또는 데이터베이스가 가장 최근에 온라인 상태로 전환되고 난 후 기본 프로시저가 처음으로 실행될 때 기본 프로시저는 한 번 다시 컴파일해야 합니다. 이 작업으로 인해 기본 프로시저 실행이 시작되기 전에 지연이 발생합니다.  
  
  
<a name="advanced-considerations-for-memory-optimized-tables-39n"></a>  
  
## <a name="advanced-considerations-for-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블에 대한 고급 고려 사항  
  
  
[메모리 액세스에 최적화된 테이블의 인덱스](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md) 는 일부 방식에서 기존 디스크 테이블의 인덱스와 다릅니다.  
  
- [해시 인덱스](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md) 는 메모리 액세스에 최적화된 테이블에서만 사용할 수 있습니다.  
  
  
계획 중인 메모리 액세스에 최적화된 테이블 및 인덱스에 대해 활성 메모리가 충분한지 확인할 계획을 세워야 합니다. 다음을 참조하십시오.  
  
- [메모리 액세스에 최적화된 개체의 저장소 만들기 및 관리](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
DURABILITY = SCHEMA_ONLY를 사용하여 메모리 액세스에 최적화된 테이블을 선언할 수 있습니다.  
  
- 이 구문은 데이터베이스가 오프라인 상태가 될 때 메모리 액세스에 최적화된 테이블에서 데이터를 모두 삭제할 것을 시스템에 알려줍니다. 테이블 정의만 유지됩니다.  
- 데이터베이스가 다시 온라인 상태가 되면 메모리 액세스에 최적화된 테이블은 데이터가 없는 활성 메모리로 다시 로드됩니다.  
- 수천 개의 행이 관련된 경우 SCHEMA_ONLY 테이블이 tempdb의 [#temporary 테이블](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md) 보다 더 효율적일 수 있습니다.  
  
  
테이블 변수를 메모리 액세스에 최적화된 변수로 선언할 수도 있습니다. 다음을 참조하십시오.  
  
- [메모리 최적화를 사용한 더 빠른 임시 테이블 및 테이블 변수](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)  
  
  
  
<a name="advanced-considerations-for-natively-compiled-modules-40k"></a>  
  
## <a name="advanced-considerations-for-natively-compiled-modules"></a>네이티브 컴파일 모듈에 대한 고급 고려 사항  
  
  
TRANSACT-SQL을 통해 사용할 수 있는 네이티브 컴파일 모듈 형식은 다음과 같습니다.  
  
- 네이티브 컴파일 저장 프로시저(네이티브 프로시저)  
- 네이티브 컴파일 [스칼라 사용자 정의 함수](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)  
- 네이티브 컴파일 트리거(네이티브 트리거)  
  - 메모리 액세스에 최적화된 테이블에는 고유하게 컴파일되는 트리거만 허용됩니다.  
- 네이티브 컴파일 [테이블 반환 함수](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)  
  - [메모리 최적화를 사용하여 임시 테이블 및 테이블 변수 성능 향상](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/21/improving-temp-table-and-table-variable-performance-using-memory-optimization/)  
  
  
고유하게 컴파일된 UDF(사용자 정의 함수)는 해석된 UDF보다 더 빠르게 실행됩니다. UDF와 관련해서 고려해야 할 몇 가지 사항은 다음과 같습니다.  
  
- T-SQL SELECT에서 UDF를 사용하는 경우 UDF가 반환된 행마다 한 번씩 항상 호출됩니다.  
  - UDF는 인라인으로 실행되지 않고 대신 항상 호출됩니다.  
  - 컴파일된 차이는 모든 UDF에 내재된 반복 호출의 오버헤드보다 덜 중요합니다.  
  - 하지만 실용적인 수준에서 UDF 호출의 오버헤드가 허용되는 경우도 많습니다.  
  
네이티브 UDF의 성능에 대한 테스트 데이터 및 설명은 다음을 참조하세요.  
  
  - [SQL Server 2016에서 네이티브 컴파일 UDF로 RBAR 영향 완화](https://blogs.msdn.microsoft.com/sqlcat/2016/02/17/soften-the-rbar-impact-with-native-compiled-udfs-in-sql-server-2016/)  
  - [Gail Shaw가 작성하는 블로그 게시물](http://sqlinthewild.co.za/index.php/2016/01/12/natively-compiled-user-defined-functions/)(2016년 1월 게시)  
  
  
<a name="documentation-guide-for-memory-optimized-tables-41z"></a>  
  
## <a name="documentation-guide-for-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블에 대한 설명서 가이드  
  
  
다음은 메모리 액세스에 최적화된 테이블에 대한 특별 고려 사항에 설명하는 다른 문서에 대한 링크입니다.  
  
- [메모리 내 OLTP로 마이그레이션](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  - [메모리 내 OLTP에 테이블 또는 저장 프로시저를 이식해야 하는지 확인](../../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)  
  - SQL Server Management Studio의 트랜잭션 성능 분석 보고서를 사용하면 메모리 내 OLTP로 데이터베이스 응용 프로그램의 성능이 향상될지 평가할 수 있습니다.  
  - [메모리 최적화 관리자](../../relational-databases/in-memory-oltp/memory-optimization-advisor.md) 를 사용하여 디스크 기반 데이터베이스 테이블을 메모리 내 OLTP로 마이그레이션 지원   
- [메모리 액세스에 최적화된 테이블의 백업, 복원 및 복구](http://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)  
  - 메모리 액세스에 최적화된 테이블에서 사용하는 저장소는 메모리의 해당 크기보다 훨씬 클 수 있으며, 이는 데이터베이스 백업의 크기에 영향을 미칩니다.  
- [메모리 액세스에 최적화된 테이블의 트랜잭션](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)  
  - 메모리 액세스에 최적화된 테이블의 트랜잭션과 관련해서 T-SQL의 재시도 논리에 대한 정보를 포함합니다.  
- [메모리 내 OLTP에 대한 Transact-SQL 지원](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)  
  - 메모리 액세스에 최적화된 테이블 및 기본 프로시저에 지원되거나 지원되지 않는 T-SQL 및 데이터 형식  
- [메모리 액세스에 최적화된 테이블이 있는 데이터베이스를 리소스 풀에 바인딩](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)(고급 고려 사항 옵션에 대해 설명)  
  
  
  
<a name="documentation-guide-for-native-procs-42b"></a>  
  
## <a name="documentation-guide-for-native-procs"></a>기본 프로시저에 대한 설명서 가이드  
  
  
  
<a name="related-links-43f"></a>  
  
## <a name="related-links"></a>관련 링크  
  
- 초기 문서: [메모리 내 OLTP(메모리 내 최적화)](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
메모리 내 OLTP를 사용하여 얻을 수 있는 성능 향상을 보여 주는 코드를 제공하는 문서는 다음과 같습니다.  
  
- [Demonstration: Performance Improvement of In-Memory OLTP](../../relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp.md) (데모: 메모리 내 OLTP의 성능 향상)에서는 더 큰 잠재적 성능 향상에 대한 소규모 데모를 제공합니다.  
- [Sample Database for In-Memory OLTP](../../relational-databases/in-memory-oltp/sample-database-for-in-memory-oltp.md) (메모리 내 OLTP에 대한 샘플 데이터베이스)에서는 규모가 더 큰 데모를 제공합니다.  
  
  
  
\<!--  
  
e1328615-6b59-4473-8a8d-4f360f73187d , dn817827.aspx , "실시간 운영 분석을 위한 Columnstore 시작"  
  
f98af4a5-4523-43b1-be8d-1b03c3217839 , gg492088.aspx , "Columnstore 인덱스 가이드"  
  
14dddf81-b502-49dc-a6b6-d18b1ae32d2b , dn133165.aspx , "메모리 액세스에 최적화된 테이블"  
  
d5ed432c-10c5-4e4f-883c-ef4d1fa32366 , dn133184.aspx , "고유하게 컴파일된 저장 프로시저"  
  
14106cc9-816b-493a-bcb9-fe66a1cd4630 , dn639109.aspx , "메모리 액세스에 최적화된 파일 그룹"  
  
f222b1d5-d2fa-4269-8294-4575a0e78636, dn465873.aspx , "메모리 액세스에 최적화된 테이블이 있는 데이터베이스를 리소스 풀에 바인딩"  
  
86805eeb-6972-45d8-8369-16ededc535c7, dn511012.aspx , "메모리 액세스에 최적화된 테이블의 인덱스"  
  
16ef63a4-367a-46ac-917d-9eebc81ab29b, dn133166.aspx , "메모리 액세스에 최적화된 테이블의 인덱스 사용 지침"  
  
e3f8009c-319d-4d7b-8993-828e55ccde11, dn246937.aspx , "메모리 내 OLTP에서 지원되지 않는 Transact-SQL 구문"  
  
2cd07d26-a1f1-4034-8d6f-f196eed1b763, dn133169.aspx , "메모리 액세스에 최적화된 테이블의 트랜잭션"  
참고: mt668425.aspx "메모리 액세스에 최적화된 테이블의 트랜잭션을 위한 동작 및 지침"을 참조하세요.  
f2a35c37-4449-49ee-8bba-928028f1de66, dn169141.aspx , "메모리 액세스에 최적화된 테이블의 트랜잭션에 대한 재시도 논리 지침"  
  
7a458b9c-3423-4e24-823d-99573544c877, dn465869.aspx , "메모리 사용 모니터링 및 문제 해결"  
  
5c5cc1fc-1fdf-4562-9443-272ad9ab5ba8, dn282389.aspx , "메모리 액세스에 최적화된 테이블에 필요한 메모리 예측"  
  
b0a248a4-4488-4cc8-89fc-46906a8c24a1, dn205318.aspx , "메모리 액세스에 최적화된 테이블의 테이블 및 행 크기"  
  
162d1392-39d2-4436-a4d9-ee5c47864c5a, dn296452.aspx , "응용 프로그램 수준 분할"  
  
3f867763-a8e6-413a-b015-20e9672cc4d1, dn133171.aspx , "메모리 액세스에 최적화된 테이블 분할을 위한 응용 프로그램 패턴"  
  
86805eeb-6972-45d8-8369-16ededc535c7, dn511012.aspx , "메모리 액세스에 최적화된 테이블의 인덱스"  
  
d82f21fa-6be1-4723-a72e-f2526fafd1b6, dn465872.aspx , "메모리 액세스에 최적화된 OLTP의 메모리 관리"  
  
622aabe6-95c7-42cc-8768-ac2e679c5089, dn133174.aspx , "메모리 액세스에 최적화된 개체의 저장소 만들기 및 관리"  
  
bd102e95-53e2-4da6-9b8b-0e4f02d286d3, dn535766.aspx , "메모리 액세스에 최적화된 테이블 변수"; "메모리 액세스에 최적화된 테이블의 테이블 변수"  
사용되지 않습니다. 대신 38512a22-7e63-436f-9c13-dde7cf5c2202, mt718711.aspx , "메모리 최적화를 사용한 더 빠른 임시 테이블 및 테이블 변수"  
  
  
f0d5dd10-73fd-4e05-9177-07f56552bdf7, ms191320.aspx , "사용자 정의 함수 만들기(데이터베이스 엔진)"; "테이블 반환 함수"  
  
d2546e40-fdfc-414b-8196-76ed1f124bf5, dn935012.aspx , "메모리 내 OLTP에 대한 사용자 정의 스칼라 함수"; "스칼라 사용자 정의 함수"  
  
405cdac5-a0d4-47a4-9180-82876b773b82, dn247639.aspx , "메모리 내 OLTP로 마이그레이션"  
  
3f083347-0fbb-4b19-a6fb-1818d545e281, dn624160.aspx , "메모리 액세스에 최적화된 테이블 백업, 복원 및 복구"  
  
690b70b7-5be1-4014-af97-54e531997839, dn269114.aspx , "메모리 액세스에 최적화된 테이블 변경"  
  
  
b1cc7c30-1747-4c21-88ac-e95a5e58baac, dn133080.aspx , "메모리 내 OLTP에서 업데이트되거나 새로운 속성, 시스템 뷰, 저장 프로시저, 대기 유형 및 DMV"  
와 다른 방법으로 더 많은 메모리를 사용합니다. 이라고도 합니다. 이라고도 합니다. 이라고도 합니다. 와 다른 방법으로 더 많은 메모리를 사용합니다.  
“메모리 내 OLTP에 대한 Transact-SQL 지원”도 참조하세요.  
  
  
c1ef96f1-290d-4952-8369-2f49f27afee2, dn205133.aspx, "메모리 내 OLTP에 테이블 또는 저장 프로시저를 이식해야 하는지 확인"  
  
181989c2-9636-415a-bd1d-d304fc920b8a, dn284308.aspx, "메모리 최적화 관리자"  
  
55548cb2-77a8-4953-8b5a-f2778a4f13cf, dn452282.aspx, "고유하게 컴파일된 저장 프로시저의 모니터링 성능"  
  
d3898a47-2985-4a08-bc70-fd8331a01b7b, dn358355.aspx, "네이티브 컴파일 관리자"  
  
f43faad4-2182-4b43-a76a-0e3b405816d1, dn296678.aspx, "고유하게 컴파일된 저장 프로시저의 마이그레이션 문제"  
  
e1d03d74-2572-4a55-afd6-7edf0bc28bdb, dn133186.aspx, "메모리 내 OLTP(메모리 내 최적화)"  
  
c6def45d-d2d4-4d24-8068-fab4cd94d8cc, dn530757.aspx, "데모: 메모리 내 OLTP 성능 향상"  
  
405cdac5-a0d4-47a4-9180-82876b773b82, dn247639.aspx , "메모리 내 OLTP로 마이그레이션"  
  
f76fbd84-df59-4404-806b-8ecb4497c9cc, bb522682.aspx, "ALTER DATABASE SET 옵션(Transact-SQL)"  
  
e6b34010-cf62-4f65-bbdf-117f291cde7b, dn452286.aspx, "고유하게 컴파일된 저장 프로시저 만들기"  
  
df347f9b-b950-4e3a-85f4-b9f21735eae3, mt465764.aspx, "메모리 내 OLTP에 대한 예제 데이터베이스"  
  
38512a22-7e63-436f-9c13-dde7cf5c2202, mt718711.aspx, "메모리 최적화를 사용한 더 빠른 임시 테이블 및 테이블 변수"  
  
38512a22-7e63-436f-9c13-dde7cf5c2202, mt718711.aspx, "메모리 최적화를 사용한 더 빠른 임시 테이블 및 테이블 변수"  
  
  
  
  
H1 # 빠른 시작 1: 더 빠른 트랜잭션 작업을 위한 메모리 내 기술  
대문자로 {1c25a164-547d-43c4-8484-6b5ee3cbaf3a}  
MSDN에서 mt718711.aspx  
  
GeneMi , 2016-05-07  00:07am  
-->  
  
  
  


