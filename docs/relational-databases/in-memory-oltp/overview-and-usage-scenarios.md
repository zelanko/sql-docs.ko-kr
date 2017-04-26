---
title: "개요 및 사용 시나리오 | Microsoft 문서"
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 62c964c5-eae4-4cf1-9024-d5a19adbd652
caps.latest.revision: 5
author: jodebrui
ms.author: jodebrui
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: edf397a4e4922167ae2eafd2c8e78ac97858bd37
ms.lasthandoff: 04/11/2017

---
# <a name="overview-and-usage-scenarios"></a>개요 및 사용 시나리오
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

메모리 내 OLTP는 SQL Server 및 Azure SQL Database에서 트랜잭션 처리, 데이터 수집, 데이터 로드 및 일시적인 데이터 시나리오의 성능을 최적화하기 위해 사용할 수 있는 뛰어난 기술입니다. 이 항목에서는 메모리 내 OLTP의 기술 및 사용 시나리오를 알아봅니다. 이 정보를 사용하여 메모리 내 OLTP가 응용 프로그램에 적합 한지 확인할 수 있습니다. 이 항목에는 메모리 내 OLTP 개체를 보여 주는 예제, 성능 데모에 대한 참조 및 다음 단계에 사용할 수 있는 리소스에 대한 참조가 포함되어 있습니다.

이 문서에서는 SQL Server와 Azure SQL Database의 메모리 내 OLTP 기술에 대해 설명합니다. 다음 블로그 게시물에서는 Azure SQL Database의 성능 및 리소스 사용률 이점에 대해 자세히 설명합니다. 
- [Azure SQL Database의 메모리 내 OLTP](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

## <a name="in-memory-oltp-overview"></a>메모리 내 OLTP 개요

메모리 내 OLTP는 올바른 워크로드에 대해 상당한 성능 향상을 제공할 수 있습니다. 하나의 고객은 SQL Server 2016을 실행하는 단일 컴퓨터에서 메모리 내 OLTP를 사용하여 [초당 120만 요청을 달성](https://blogs.msdn.microsoft.com/sqlcat/2016/10/26/how-bwin-is-using-sql-server-2016-in-memory-oltp-to-achieve-unprecedented-performance-and-scale/) 하려는 bwin입니다. 또 다른 고객은 Azure SQL Database에서 메모리 내 OLTP를 활용하여 [리소스 사용률을 70%로 줄이는 동시에](https://customers.microsoft.com/en-US/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)워크로드를 두 배로 늘리려는 Quorum입니다. 고객이 일부 경우에 최대 30배의 성능 향상을 얻었지만 워크로드에 따라 정도가 다릅니다.

그렇다면 이러한 성능 향상은 어디에서 이루어지는 것일까요? 기본적으로 메모리 내 OLTP는 데이터 액세스 및 트랜잭션 실행을 보다 효율적으로 만들고, 동시 실행 트랜잭션 간에 잠금 및 래치 경합을 제거하여 트랜잭션 처리 성능을 개선합니다. 한편으로는 메모리 내 작업이기 때문에 빠르지 않지만 다른 한편으로는 메모리 내 데이터를 중심으로 최적화되기 때문에 빠릅니다. 메모리 내 및 높은 동시성 컴퓨팅의 최신 개선 사항을 활용하기 위해 데이터 저장소, 액세스 및 처리 알고리즘이 처음부터 다시 설계되었습니다.

이제 데이터가 메모리 내에 있다는 것은 오류 시 손실되지 않음을 의미하는 것이 아닙니다. 기본적으로 모든 트랜잭션이 완전히 내구적입니다. 즉, SQL Server의 다른 테이블과 동일한 내구성이 보장됩니다. 트랜잭션 커밋의 일부로 모든 변경 내용이 디스크의 트랜잭션 로그에 기록됩니다. 트랜잭션 커밋 후 언제든 오류가 발생한 경우 데이터베이스가 다시 온라인 상태로 전환되면 데이터가 그대로 유지됩니다. 또한 메모리 내 OLTP는 AlwaysOn, 백업/복원 등 SQL Server의 모든 고가용성 및 재해 복구 기능와 함께 작동합니다.

데이터베이스에서 메모리 내 OLTP를 활용하려면 다음과 같은 유형의 개체 중 하나 이상을 사용합니다.

- *메모리 액세스에 최적화된 테이블* 은 사용자 데이터를 저장하는 데 사용됩니다. 메모리 액세스에 최적화되도록 할 테이블은 만들 때 선언합니다.
- *비영구 테이블* 은 캐싱 또는 중간 결과 집합의 임시 데이터에 사용됩니다(기존의 임시 테이블 대체). 비영구 테이블은 DURABILITY=SCHEMA_ONLY로 선언된 메모리 액세스에 최적화된 테이블입니다. 이러한 테이블의 변경 내용은 IO를 유발하지 않습니다. 따라서 내구성이 중요하지 않은 경우 로그 IO 리소스 소모를 방지할 수 있습니다.
- *메모리 액세스에 최적화된 테이블 형식* 은 TVP(테이블 반환 매개 변수) 및 저장 프로시저의 중간 결과 집합에 사용됩니다. 기존 테이블 형식 대신 사용할 수 있습니다. 메모리 액세스에 최적화된 테이블 형식을 사용하여 선언된 테이블 변수 및 TVP는 비영구 메모리 액세스에 최적화된 테이블의 이점(효율적인 데이터 액세스 및 IO 없음)을 상속합니다.
- *고유하게 컴파일된 T-SQL 모듈* 은 작업을 처리하는 데 필요한 CPU 주기를 줄여 개별 트랜잭션에 소요되는 시간을 더 단축하는 데 사용됩니다. 고유하게 컴파일할 TRANSACT-SQL 모듈은 만들 때 선언합니다. 이 시점에서 고유하게 컴파일할 수 있는 T-SQL 모듈은 저장 프로시저, 트리거 및 사용자 정의 스칼라 함수입니다.

메모리 내 OLTP는 SQL Server 및 Azure SQL Database에 기본 제공됩니다. 또한 이러한 개체는 기존 개체와 매우 유사하게 동작하기 때문에 데이터베이스 및 응용 프로그램에 대한 최소한의 변경으로 성능 이점을 얻을 수 있습니다. 뿐만 아니라 메모리 액세스에 최적화된 테이블과 기존 디스크 기반 테이블을 동일한 데이터베이스에서 함께 사용하고 둘 간에 쿼리를 실행할 수 있습니다. 이러한 유형의 각 개체에 대한 예제를 보여 주는 TRANSACT-SQL 스크립트는 이 항목의 아래쪽에서 확인할 수 있습니다.

## <a name="usage-scenarios-for-in-memory-oltp"></a>메모리 내 OLTP에 대한 사용 시나리오

메모리 내 OLTP는 마법의 단추가 아니고 모든 워크로드에 적합한 것도 아닙니다. 예를 들어 메모리 액세스에 최적화된 테이블은 대부분의 쿼리가 큰 데이터 범위에서 집계를 수행하는 경우 실제로 CPU 사용률을 낮추지 않습니다. 이 시나리오에는 Columnstore 인덱스가 도움이 됩니다.

다음은 메모리 내 OLTP를 성공적으로 사용한 고객의 시나리오 및 응용 프로그램 패턴 목록입니다.

### <a name="high-throughput-and-low-latency-transaction-processing"></a>높은 처리량 및 낮은 대기 시간의 트랜잭션 처리

이는 실제로 메모리 내 OLTP를 구축한 핵심 시나리오입니다. 개별 트랜잭션에 대해 일관성 있게 낮은 대기 시간으로 대량의 트랜잭션을 지원합니다.

일반적인 워크로드 시나리오는 금융 상품 거래, 스포츠 베팅, 모바일 게임, 광고 전달 등입니다. 또 다른 일반적인 패턴은 자주 읽거나 업데이트하는 "카탈로그"입니다. 예를 들어 대용량 파일이 있고 각 파일이 클러스터의 여러 노드에 분산된 경우 메모리 액세스에 최적화된 테이블에서 각 파일의 분할 위치에 대한 카탈로그를 작성합니다.

#### <a name="implementation-considerations"></a>구현 고려 사항

핵심 트랜잭션 테이블, 즉 성능이 가장 중요한 트랜잭션이 있는 테이블에 메모리 액세스에 최적화된 테이블을 사용합니다. 비즈니스 트랜잭션과 관련된 논리 실행을 최적화하려면 고유하게 컴파일된 저장 프로시저를 사용합니다. 데이터베이스에 저장 프로시저로 푸시할 수 있는 논리가 많을수록 메모리 내 OLTP에서 더 많은 이점을 얻을 수 있습니다.

기존 응용 프로그램에서 시작하려면 다음을 수행합니다.
1. [트랜잭션 성능 분석 보고서](https://msdn.microsoft.com/library/dn205133.aspx) 를 사용하여 마이그레이션할 개체를 식별합니다. 
2. [메모리 최적화](https://msdn.microsoft.com/library/dn284308.aspx) 및 [네이티브 컴파일](https://msdn.microsoft.com/library/dn358355.aspx) Advisor를 사용하여 마이그레이션에 대한 도움을 얻습니다.

#### <a name="customer-case-studies"></a>고객 사례 연구

- CMC Markets는 SQL Server 2016에서 메모리 내 OLTP를 활용하여 일관된 짧은 대기 시간을 달성합니다. [1초도 기다리기에 너무 긴 시간이기 때문에 이 금융 서비스 회사는 현재 거래 소프트웨어를 업데이트하고 있습니다.](https://customers.microsoft.com/en-us/story/because-a-second-is-too-long-to-wait-this-financial-services-firm-is-updating-its-trading-software)
- Derivco는 SQL Server 2016에서 메모리 내 OLTP를 활용하여 증가된 처리량을 지원하고 워크로드의 급증을 처리합니다. [온라인 게임 회사는 향후 위험을 원치 않을 때 SQL Server 2016에 투자합니다.](https://customers.microsoft.com/en-us/story/when-an-online-gaming-company-doesnt-want-to-risk-its-future-it-bets-on-sql-server-2016)


### <a name="data-ingestion-including-iot-internet-of-things"></a>IoT(사물 인터넷)를 비롯한 데이터 수집

메모리 내 OLTP는 다양한 원본에서 동시에 많은 양의 데이터를 수집하는 데 매우 유용합니다. 또한 다른 대상보다 SQL Server Database로 데이터를 수집하는 데 유용한 경우가 많습니다. SQL은 데이터에 대한 쿼리를 매우 빠르게 실행하고 실시간 통찰력을 제공하기 때문입니다.

일반적인 응용 프로그램 패턴은, 센서 판독값 및 이벤트를 수집하여 알림 및 기록 분석을 지원하는 것입니다. 동시 읽기 워크로드에 대한 영향을 최소화하면서 여러 원본에서 일괄 처리 업데이트를 관리합니다.

#### <a name="implementation-considerations"></a>구현 고려 사항

메모리 액세스에 최적화된 테이블을 데이터 수집에 사용합니다. 수집이 업데이트보다 주로 삽입으로 구성되고 메모리 내 OLTP 저장소의 데이터 공간이 중요한 경우 다음 중 하나를 수행합니다.

- [을 수행하는 작업을 사용하여](https://msdn.microsoft.com/library/gg492088.aspx)클러스터형 Columnstore 인덱스 `INSERT INTO <disk-based table> SELECT FROM <memory-optimized table>`가 있는 디스크 기반 테이블에 데이터를 정기적으로 일괄 오프로드합니다.
- [임시 메모리 액세스에 최적화된 테이블](https://msdn.microsoft.com/library/mt590207.aspx) 을 사용하여 기록 데이터를 관리합니다. 이 모드에서는 기록 데이터가 디스크에 있으며, 데이터 이동이 시스템에 의해 관리됩니다.

SQL Server 샘플 리포지토리에는 임시 메모리 액세스에 최적화된 테이블, 메모리 액세스에 최적화된 테이블 형식 및 고유하게 컴파일된 저장 프로시저를 사용하여 센서 데이터의 메모리 내 OLTP 저장소 공간을 관리하는 동시에 데이터 수집을 가속화하는 스마트 그리드 응용 프로그램이 포함되어 있습니다. 

 - [smart-grid-release](https://github.com/Microsoft/sql-server-samples/releases/tag/iot-smart-grid-v1.0) 
 - [smart-grid-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/applications/iot-smart-grid)
 
#### <a name="customer-case-studies"></a>고객 사례 연구

- [Quorum은 Azure SQL Database에서 메모리 내 OLTP를 활용하여 사용률을 70%로 낮추는 동시에 주요 데이터베이스의 워크로드를 두 배로 늘립니다.](http://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)
- EdgeNet은 SQL Server 2014에서 메모리 내 OLTP를 사용하여 일괄 처리 데이터 로드 성능을 개선하고 다중 계층 캐시를 유지 관리해야 하는 필요성을 제거했습니다. [데이터 서비스 회사에서 메모리 내 기술을 사용하여 제품 데이터에 대한 실시간 액세스 실현](https://customers.microsoft.com/en-us/story/data-services-firm-gains-real-time-access-to-product-d)
- Beth Israel Deaconess Medical Center는 SQL Server 2014에서 메모리 내 OLTP를 사용하여 도메인 컨트롤러에서 데이터 수집률을 획기적으로 개선하고 워크로드의 급증을 처리할 수 있었습니다[https://customers.microsoft.com/en-us/story/strengthening-data-security-and-creating-more-time-for].

### <a name="caching-and-session-state"></a>캐싱 및 세션 상태

메모리 내 OLTP 기술은 SQL의 세션 상태 유지 관리(예: ASP.NET 응용 프로그램) 및 캐싱 기능을 크게 향상시킵니다.

ASP.NET 세션 상태는 메모리 내 OLTP의 매우 성공적인 사용 사례입니다. 한 고객은 SQL Server를 사용하여 초당 120만 요청을 달성하려고 했습니다. 그 동안 엔터프라이즈의 모든 중간 계층 응용 프로그램의 캐싱 요구 사항을 위해 메모리 내 OLTP를 사용하기 시작했습니다. 세부 정보: [bwin에서 SQL Server 2016 메모리 내 OLTP을 사용하여 전례 없는 성능 및 확장성을 달성하는 방법](https://blogs.msdn.microsoft.com/sqlcat/2016/10/26/how-bwin-is-using-sql-server-2016-in-memory-oltp-to-achieve-unprecedented-performance-and-scale/)

#### <a name="implementation-considerations"></a>구현 고려 사항

varbinary(max) 열에 BLOB을 저장하여 영구 메모리 액세스에 최적화된 테이블을 간단한 키-값 저장소로 사용할 수 있습니다. 또는 SQL Server 및 Azure SQL Database에서 [JSON 지원](https://azure.microsoft.com/blog/json-support-is-generally-available-in-azure-sql-database/) 을 사용하여 반구조화된 캐시를 구현할 수 있습니다. 마지막으로, 다양한 데이터 형식 및 제약 조건 등 완전한 관계형 스키마를 사용하여 비영구 테이블을 통해 완전한 관계형 캐시를 만들 수 있습니다.

GitHub에 게시된 스크립트에서 기본 제공 SQL Server 세션 상태 제공자가 만든 개체를 대체하여 메모리 최적화 ASP.NET 세션 상태를 시작해 보세요.

- [aspnet-session-state](https://github.com/Microsoft/sql-server-samples/tree/master/samples/applications/aspnet-session-state)

#### <a name="customer-case-studies"></a>고객 사례 연구

- bwin은 SQL Server 2014에서 메모리 내 OLTP를 사용하여 처리량을 획기적으로 늘리고 ASP.NET 세션 상태에 대한 하드웨어 공간을 크게 줄일 수 있었습니다. [게임 사이트에서 초당 25만 요청으로 확장하고 플레이어 경험 개선](https://customers.microsoft.com/en-us/story/gaming-site-can-scale-to-250000-requests-per-second-an)
- bwin은 SQL Server 2016에서 메모리 내 OLTP를 사용하여 ASP.NET 세션 상태 처리량을 늘리고 엔터프라이즈 수준의 다중 계층 캐싱 시스템을 구현했습니다. [bwin에서 SQL Server 2016 메모리 내 OLTP를 사용하여 전례 없는 성능 및 확장성을 달성하는 방법](https://blogs.msdn.microsoft.com/sqlcat/2016/10/26/how-bwin-is-using-sql-server-2016-in-memory-oltp-to-achieve-unprecedented-performance-and-scale/)

### <a name="tempdb-object-replacement"></a>Tempdb 개체 대체

비영구 테이블 및 메모리 액세스에 최적화된 테이블 형식을 활용하여 기존 tempdb 기반 #temp 테이블, 테이블 변수 및 TVP(테이블 반환 매개 변수)를 대체할 수 있습니다.

메모리 액세스에 최적화된 테이블 변수 및 비영구 테이블은 일반적으로 기존 테이블 변수 및 #temp 테이블과 비교할 때 CPU를 줄이고 로그 IO를 완전히 제거합니다.



#### <a name="implementation-considerations"></a>구현 고려 사항

시작하려면 [메모리 최적화를 사용하여 임시 테이블 및 테이블 변수 성능 향상](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/21/improving-temp-table-and-table-variable-performance-using-memory-optimization/)을 참조하세요.

#### <a name="customer-case-studies"></a>고객 사례 연구

- 한 고객은 기존 TVP를 메모리 액세스에 최적화된 TVP로 바꾼 것만으로 성능을 40% 개선할 수 있었습니다. [Azure에서 메모리 내 OLTP를 사용하여 고속 IoT 데이터 수집](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/04/07/a-technical-case-study-high-speed-iot-data-ingestion-using-in-memory-oltp-in-azure/)


### <a name="etl-extract-transform-load"></a>ETL(추출, 변환, 로드)

ETL 워크플로에는 종종 준비 테이블로 데이터 로드, 데이터 변환 및 최종 테이블에 로드가 포함됩니다.

#### <a name="implementation-considerations"></a>구현 고려 사항

데이터 준비에 비영구 메모리 액세스에 최적화된 테이블을 사용합니다. 모든 IO가 완전히 제거되고 데이터 액세스 효율성이 향상됩니다.

워크플로의 일환으로 준비 테이블에서 변환을 수행하는 경우 고유하게 컴파일된 저장 프로시저를 사용하여 이러한 변환을 가속화할 수 있습니다. 이러한 변환을 동시에 수행할 수 있으면 메모리 최적화에서 추가적인 확장 이점을 얻을 수 있습니다.

## <a name="sample-script"></a>예제 스크립트

메모리 내 OLTP 사용을 시작하기 전에 먼저 MEMORY_OPTIMIZED_DATA 파일 그룹을 만들어야 합니다. 또한 데이터베이스 호환성 수준 130 이상을 사용하고 데이터베이스 옵션 MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT을 ON으로 설정하는 것이 좋습니다.

다음 위치에서 스크립트를 사용하여 기본 데이터 폴더에 파일 그룹을 만들고 권장 설정을 구성할 수 있습니다.

- [enable-in-memory-oltp.sql](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/enable-in-memory-oltp.sql)

다음 스크립트는 데이터베이스에서 만들 수 있는 메모리 내 OLTP 개체를 보여 줍니다.
  
     -- configure recommended DB option
     ALTER DATABASE CURRENT SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON
     GO
     -- memory-optimized table
     CREATE TABLE dbo.table1
     ( c1 INT IDENTITY PRIMARY KEY NONCLUSTERED,
       c2 NVARCHAR(MAX))
     WITH (MEMORY_OPTIMIZED=ON)
     GO
     -- non-durable table
     CREATE TABLE dbo.temp_table1
     ( c1 INT IDENTITY PRIMARY KEY NONCLUSTERED,
       c2 NVARCHAR(MAX))
     WITH (MEMORY_OPTIMIZED=ON,
           DURABILITY=SCHEMA_ONLY)
     GO
     -- memory-optimized table type
     CREATE TYPE dbo.tt_table1 AS TABLE
     ( c1 INT IDENTITY,
       c2 NVARCHAR(MAX),
       is_transient BIT NOT NULL DEFAULT (0),
       INDEX ix_c1 HASH (c1) WITH (BUCKET_COUNT=1024))
     WITH (MEMORY_OPTIMIZED=ON)
     GO
     -- natively compiled stored procedure
     CREATE PROCEDURE dbo.usp_ingest_table1
       @table1 dbo.tt_table1 READONLY
     WITH NATIVE_COMPILATION, SCHEMABINDING
     AS
     BEGIN ATOMIC
         WITH (TRANSACTION ISOLATION LEVEL=SNAPSHOT,
               LANGUAGE=N'us_english')
     
       DECLARE @i INT = 1
     
       WHILE @i > 0
       BEGIN
         INSERT dbo.table1
         SELECT c2
         FROM @table1
         WHERE c1 = @i AND is_transient=0
     
         IF @@ROWCOUNT > 0
           SET @i += 1
         ELSE
         BEGIN
           INSERT dbo.temp_table1
           SELECT c2
           FROM @table1
           WHERE c1 = @i AND is_transient=1
     
           IF @@ROWCOUNT > 0
             SET @i += 1
           ELSE
             SET @i = 0
         END
       END
     
     END
     GO
     -- sample execution of the proc
     DECLARE @table1 dbo.tt_table1
     INSERT @table1 (c2, is_transient) VALUES (N'sample durable', 0)
     INSERT @table1 (c2, is_transient) VALUES (N'sample non-durable', 1)
     EXECUTE dbo.usp_ingest_table1 @table1=@table1
     SELECT c1, c2 from dbo.table1
     SELECT c1, c2 from dbo.temp_table1
     GO
   

## <a name="resources-to-learn-more"></a>참조 리소스:

- [빠른 시작 1: 더 빠른 T-SQL 성능을 위한 메모리 내 OLTP 기술](http://msdn.microsoft.com/library/mt694156.aspx)
- 메모리 내 OLTP 사용에 대한 성능 데모는 [in-memory-oltp-perf-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)에서 확인할 수 있습니다.
- [메모리 내 OLTP를 설명하고 데모를 보여 주는 17분 분량의 비디오](https://www.youtube.com/watch?v=l5l5eophmK4) (데모는 8분 25초에서 시작)
- [메모리 내 OLTP를 사용하도록 설정하고 권장 옵션을 설정하는 스크립트](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/enable-in-memory-oltp.sql)
- [기본 메모리 내 OLTP 설명서](https://msdn.microsoft.com/library/dn133186.aspx)
- [Azure SQL Database의 메모리 내 OLTP 성능 및 리소스 사용률 이점](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)
- [메모리 최적화를 사용하여 임시 테이블 및 테이블 변수 성능 향상](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/21/improving-temp-table-and-table-variable-performance-using-memory-optimization/)
[SQL Database에서 메모리 내 기술을 사용하여 성능 최적화](https://docs.microsoft.com/azure/sql-database/sql-database-in-memory)
- [메모리 액세스에 최적화된 테이블을 포함한 시스템 버전 임시 테이블](https://msdn.microsoft.com/library/mt590207.aspx)
- [메모리 내 OLTP – 자주 사용되는 작업 패턴 및 마이그레이션 고려 사항](http://msdn.microsoft.com/library/dn673538.aspx) 

