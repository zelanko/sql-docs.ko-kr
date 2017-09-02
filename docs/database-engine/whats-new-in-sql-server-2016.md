---
title: "데이터베이스 엔진의 새로운 기능 - SQL Server 2016 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
- SQL2016_rc1
ms.date: 07/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- what's new [SQL Server Database Engine]
- Database Engine [SQL Server], what's new
ms.assetid: 8f625d5a-763c-4440-97b8-4b823a6e2439
caps.latest.revision: 431
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: e4a6157cb56c6db911406585f841046a431eef99
ms.openlocfilehash: bc39be67f0d2fba9195fe2f8e372f05994f0d49d
ms.contentlocale: ko-kr
ms.lasthandoff: 08/16/2017

---
# <a name="whats-new-in-database-engine---sql-server-2016"></a>데이터베이스 엔진의 새로운 기능 - SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

이 항목에서는 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 의 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]릴리스에서 소개된 향상된 기능을 요약합니다.  새로운 기능과 향상된 기능은 데이터 저장소 시스템을 디자인, 개발 및 유지 관리하는 설계자, 개발자 및 관리자의 작업 효율성과 생산성을 증대시킵니다.

다른 SQL Server 구성 요소의 새로운 기능을 검토하려면 [SQL Server 2016의 새로운 기능](../sql-server/what-s-new-in-sql-server-2016.md)을 참조하세요.

> [!NOTE]
>  [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]는 64비트 응용 프로그램입니다. 일부 요소는 32비트 구성 요소로 실행되지만 32비트 설치는 중단되었습니다.

#### <a name="try-it-out"></a>사용해보기

- [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]을 다운로드하려면 **[평가 센터](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**![다운로드](../analysis-services/media/download.png "다운로드")로 이동하세요.

- Azure 계정이 있으세요?  계정이 있는 경우 **[여기](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/)** 로 이동하여 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 이 이미 설치된 가상 컴퓨터를 실행해 보세요.

![참고](../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "참고") 현재 릴리스 정보는 [SQL Server 2016 릴리스 정보](../sql-server/sql-server-2016-release-notes.md)를 참조하세요.
  
## <a name="sql-server-2016-service-pack-1-sp1"></a>SQL Server 2016 서비스 팩 1(SP1)  
-  이제`CREATE OR ALTER <object>` 구문은 [프로시저](../t-sql/statements/create-procedure-transact-sql.md), [뷰](../t-sql/statements/create-view-transact-sql.md), [함수](../t-sql/statements/create-function-transact-sql.md)및 [트리거](../t-sql/statements/create-trigger-transact-sql.md)에 사용할 수 있습니다.
-   `OPTION (USE HINT('<hint1>', '<hint2>'))`같은 보다 일반적인 쿼리 힌트 모델에 대한 지원이 추가되었습니다. 자세한 내용은 [쿼리 힌트(Transact-SQL)](../t-sql/queries/hints-transact-sql-query.md)를 참조하세요.  
- [sys.dm_exec_valid_use_hints](../relational-databases/system-dynamic-management-views/sys-dm-exec-valid-use-hints-transact-sql.md) DMV가 목록 힌트에 추가됩니다.  
- [sys.dm_exec_query_statistics_xml](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md) DMV이 추가되어 실행 계획 XML 임시 통계를 반환합니다.  
- [sys.dm_db_incremental_stats_properties](../relational-databases/system-dynamic-management-views/sys-dm-db-incremental-stats-properties-transact-sql.md) DMV가 지정된 테이블에 대한 증분 통계에 추가됩니다.  
- `instant_file_initialization_enabled` 열이 [sys.dm_server_services](../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md)에 추가됩니다.  
- `estimated_read_row_count` 열이 [sys.dm_exec_query_profiles](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)에 추가됩니다.  
-  `sql_memory_model` 및 `sql_memory_model_desc` 열이 [sys.dm_os_sys_info](../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md) 에 추가되어 메모리 페이지의 잠금 모델에 대한 정보를 제공합니다.
-  더 많은 버전에서 다양한 기능을 지원합니다. 예를 들면 행 수준 보안, Always Encrypted, 동적 데이터 마스킹, 데이터베이스 감사, 메모리 내 OLTP 등 기타 몇몇 다른 기능이 모든 버전에 추가되었습니다. 자세한 내용은 [SQL Server 2016의 버전과 지원하는 기능](../sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.   
-  [sp_refresh_parameter_encryption](../relational-databases/system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md) 을 사용하면 상시 암호화를 사용하여 암호화된 개체가 다시 정의될 때 상시 암호화 기능을 통해 메타데이터를 업데이트할 수 있습니다.  


##  <a name="Feature"></a> SQL Server 2016 RTM
이 섹션에 포함된 하위 섹션은 아래와 같습니다.

-   [Columnstore 인덱스](#columnstore)
-   [데이터베이스 범위 구성](#scopedconfiguration)
-   [메모리 내 OLTP](#InMemory)
-   [쿼리 최적화 프로그램](#QueryOptimizer)
-   [활성 쿼리 통계](#LiveStats)
-   [쿼리 저장소](#QueryStore)
-   [임시 테이블](#TT)
-   [Microsoft Azure Blob Storage에 대한 스트라이프 백업](#StripedBackupToAzure)
-   [Microsoft Azure Blob Storage에 대한 파일-스냅숏 백업](#FileSnapshotBackup)
-   [Managed Backup](#ManagedBackup)
-   [TempDB 데이터베이스](#multipleTempDB)
-   [기본 제공 JSON 지원](#ForJson)
-   [PolyBase](#bkPolyBase)
-   [Stretch Database](#stretch)
-   [UTF-8에 대한 지원](#UTF8)
-   [새로운 기본 데이터베이스 크기 및 자동 증가 값](#DefaultDB)
-   [향상된 Transact-SQL 기능](#TSQL)
-   [향상된 시스템 뷰 기능](#SystemTable)
-   [향상된 보안 기능](#Security)
-   [향상된 고가용성 기능](#HighAvailability)
-   [향상된 복제 기능](#Repl)
-   [향상된 도구 기능](#Tools)

####  <a name="columnstore"></a> Columnstore 인덱스

이 릴리스에서는 업데이트 가능한 비클러스터형 columnstore 인덱스, 메모리 내 테이블의 columnstore 인덱스 및 다양한 운영 분석용 새 기능을 비롯하여 columnstore 인덱스에 대한 향상 기능을 제공합니다.

- 읽기 전용 비클러스터형 columnstore 인덱스는 업그레이드한 후 업데이트할 수 있습니다.  업데이트 가능하게 설정하도록 인덱스를 다시 빌드할 필요가 없습니다.

- columnstore 인덱스에 대한 분석 쿼리 성능이 향상되었고, 특히 집계 및 문자열 조건자의 성능이 향상되었습니다.

- DMV 및 XEvent의 지원 가능성이 향상되었습니다.

자세한 내용은 온라인 설명서의 [Columnstore 인덱스 가이드](../relational-databases/indexes/columnstore-indexes-overview.md) 섹션을 참조하세요.

- [Columnstore 인덱스 버전형 기능 요약](~/relational-databases/indexes/columnstore-indexes-what-s-new.md) – 새로운 기능을 포함합니다.

- [Columnstore 인덱스 데이터 로드](../relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)

- [Columnstore 인덱스 쿼리 성능](~/relational-databases/indexes/columnstore-indexes-query-performance.md)

- [실시간 운영 분석을 위한 Columnstore 시작](../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)

- [데이터 웨어하우스용 Columnstore 인덱스](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)

- [Columnstore 인덱스 조각 모음](~/relational-databases/indexes/columnstore-indexes-defragmentation.md)


####  <a name="scopedconfiguration"></a> 데이터베이스 범위 구성


새 [ALTER DATABASE SCOPED CONFIGURATION&#40;Transact-SQL&#41;](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) 문을 사용하면 특정 데이터베이스의 특정 구성을 제어할 수 있습니다. 구성 설정은 응용 프로그램 동작에 영향을 줍니다.

새 문은 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 및 [!INCLUDE[sqldbesa](../includes/sqldbesa-md.md)]에서 모두 사용할 수 있습니다.



####  <a name="InMemory"></a> 메모리 내 OLTP


##### <a name="storage-format-change"></a>저장소 형식 변경

SQL Server 2014 및 2016 간 메모리 액세스에 최적화된 테이블의 저장소 형식이 변경되었습니다. SQL Server 2014에서의 업그레이드 및 연결/복원의 경우 데이터베이스가 복구되는 동안 새 저장소 형식이 직렬화되고 데이터베이스가 한 번 다시 시작됩니다.

- [SQL Server 2016으로 업그레이드](../database-engine/install-windows/upgrade-sql-server.md)


##### <a name="alter-table-is-log-optimized-and-runs-in-parallel"></a>ALTER TABLE은 로그에 최적화되고 병렬로 실행됨.

이제 메모리 액세스에 최적화된 테이블에서 ALTER TABLE 문을 실행하면 메타데이터 변경 내용만 로그에 기록됩니다. 이렇게 하면 로그 IO가 현저하게 줄어듭니다. 또한 이제 대부분의 ALTER TABLE 시나리오가 병렬로 실행되어 문의 실행 시간을 크게 단축할 수 있습니다.

- LOB를 포함한 비 병렬 예외에 대한 자세한 내용은 [메모리 액세스에 최적화된 테이블 변경](../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md)을 참조하세요.



##### <a name="statistics"></a>통계

[메모리 액세스에 최적화된](../relational-databases/in-memory-oltp/statistics-for-memory-optimized-tables.md) 테이블에 대한 통계는 이제 자동으로 업데이트됩니다. 또한 이제 통계를 수집하는 데 비용이 많이 드는 전체 검사 방법 대신 샘플링 방식이 지원됩니다.


##### <a name="parallel-and-heap-scan-for-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블의 병렬 및 힙 검색

메모리 액세스에 최적화된 테이블과, 메모리 액세스에 최적화된 테이블의 모든 인덱스는 이제 병렬 검색을 지원합니다. 그 결과로 분석 쿼리 성능이 향상됩니다.

또한 힙 검색이 지원되어 병렬로 수행할 수 있습니다. 메모리 액세스에 최적화된 테이블의 경우 힙 검색은 행을 저장하는 데 사용되는 메모리 내 힙 데이터 구조를 사용하여 테이블에서 모든 행 검색을 참조합니다. 전체 테이블 검색의 경우 힙 검색이 인덱스를 사용하는 것보다 더 효율적입니다.

##### <a name="transact-sql-improvements-for-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블에 대한 Transact-SQL 개선 사항

SQL Server 2014의 메모리 액세스에 최적화된 테이블에 지원되지 않았던 몇 가지 Transact-SQL 요소가 이제 SQL Server 2016에서 다음과 같이 지원됩니다.


- UNIQUE 제약 조건 및 인덱스가 지원됩니다.


- 메모리 액세스에 최적화된 테이블 간의 FOREIGN KEY 참조가 지원됩니다.
  - 이러한 외래 키는 기본 키만 참조할 수 있으며 고유 키는 참조할 수 없습니다.


- CHECK 제약 조건이 지원됩니다.

- 비고유 인덱스에서 해당 키에 NULL 값을 허용할 수 있습니다.

- TRIGGER가 메모리 액세스에 최적화된 테이블에서 지원됩니다.
  - AFTER 트리거만 지원됩니다. INSTEADOF 트리거는 지원되지 않습니다.
  - 메모리 액세스에 최적화된 테이블의 모든 트리거는 WITH NATIVE_COMPILATION을 사용해야 합니다.

- 메모리 액세스에 최적화된 테이블과 고유하게 컴파일된 T-SQL 모듈에서 인덱스와 다른 아티팩트를 사용하여 모든 SQL Server 코드 페이지와 데이터 정렬에 대한 전체 검색입니다.


- [메모리 액세스에 최적화된 테이블 변경](../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md)지원:
  - 인덱스 추가 및 삭제 해시 인덱스의 bucket_count를 변경합니다.
  - 스키마 변경합니다(열 추가/삭제/변경, 제약 조건 추가/삭제).

- 이제 메모리 액세스에 최적화된 테이블에 결합된 길이가 8060바이트 페이지의 길이보다 긴 여러 개의 열이 있을 수 있습니다. `nvarchar(4000)`형식의 열이 3 개 있는 테이블이 한 예입니다. 이러한 예에서 일부 열은 이제 행 외부에 저장됩니다. 쿼리에서 열이 행 내부 또는 행 외부에 있는지 알지 못합니다.

- [LOB(Large Object) 형식](../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md) `varbinary(max)`, `nvarchar(max)`및 `varchar(max)` 는 메모리 액세스에 최적화된 테이블에서 지원되지 않습니다.


전체 내용을 보려면 다음을 참조하세요.

- [메모리 내 OLTP에서 지원되지 않는 Transact-SQL 구문](../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)
- [메모리 내 OLTP에 대해 지원되지 않는 SQL Server 기능](~/relational-databases/in-memory-oltp/unsupported-sql-server-features-for-in-memory-oltp.md)


##### <a name="transact-sql-improvements-for-natively-compiled-modules"></a>고유하게 컴파일된 모듈에 대한 Transact-SQL 개선 사항

SQL Server 2014의 고유하게 컴파일된 모듈에 지원되지 않았던 몇 가지 Transact-SQL 요소가 이제 SQL Server 2016에서 다음과 같이 지원됩니다.


- 쿼리 구문:
  - UNION 및 UNION ALL
  - SELECT DISTINCT
  - OUTER JOIN
  - SELECT의 하위 쿼리


- 이제 INSERT, UPDATE 및 DELETE 문에는 [OUTPUT 절](../t-sql/queries/output-clause-transact-sql.md)이 포함될 수 있습니다.

- 이제 기본 프로시저에서 LOB를 다음과 같이 사용할 수 있습니다.
  - 변수 선언
  - 수신한 입력 매개 변수
  - 기본 프로시저에서 문자열 함수(예: LTrim 또는 Substring)에 전달된 매개 변수


- 이제 인라인(단일 문) TVF(테이블 반환 함수)가 고유하게 컴파일될 수 있습니다.

- 이제 스칼라 UDF(사용자 정의 함수)가 고유하게 컴파일될 수 있습니다.

- 호출할 기본 프로시저에서 향상된 지원:
  - [보안 함수](../t-sql/functions/security-functions-transact-sql.md)기본 제공
  - [수치 연산 함수](../t-sql/functions/mathematical-functions-transact-sql.md)기본 제공
  - 기본 제공 함수 `@@SPID`입니다.


- EXECUTE AS CALLER가 이제 지원됩니다. 즉 고유하게 컴파일된 T-SQL 모듈을 만드는 경우 EXECUTE AS 절은 더 이상 필요 없습니다.


전체 내용을 보려면 다음을 참조하세요.

- [고유하게 컴파일된 T-SQL 모듈에 대해 지원되는 기능](../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)
- [고유하게 컴파일된 T-SQL 모듈 변경](../relational-databases/in-memory-oltp/altering-natively-compiled-t-sql-modules.md)


##### <a name="performance-and-scaling-improvements"></a>향상된 성능 및 크기 조정 기능

- 더 이상 데이터 크기 제한이 없습니다. [메모리 액세스에 최적화된 테이블에 필요한 메모리 예측](~/relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md)을 참조하세요.

- 이제 여러 동시 스레드가 [메모리 액세스에 최적화된 테이블의 변경 내용을 디스크에 유지](../relational-databases/in-memory-oltp/scalability.md)합니다.

- 병렬 계획은 [해석된 Transact-SQL을 사용하여 메모리 액세스에 최적화된 테이블에 액세스](../relational-databases/in-memory-oltp/accessing-memory-optimized-tables-using-interpreted-transact-sql.md)를 지원합니다.


##### <a name="enhancements-in-sql-server-management-studio"></a>SQL Server Management Studio의 향상된 기능

- [메모리 내 OLTP에 테이블 또는 저장 프로시저를 이식해야 하는지 확인](../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md) 에는 더 이상 데이터 수집기 또는 관리 데이터 웨어하우스의 구성이 필요하지 않습니다. 이제 보고서는 프로덕션 데이터베이스에서 직접 실행될 수 있습니다.

- [데이터베이스에서 여러 개체의 마이그레이션 적합도를 평가하기 위한](../relational-databases/in-memory-oltp/powershell-cmdlet-for-migration-evaluation.md) 마이그레이션 평가용 PowerShell Cmdlet [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 이 향상되었습니다.

- 데이터베이스를 마우스 오른쪽 단추로 클릭하고 작업 > 메모리 내 OLTP 마이그레이션 검사 목록 생성을 선택하여 마이그레이션 검사 목록을 생성합니다.

##### <a name="cross-feature-support"></a>교차 기능 지원

- 메모리 내 OLTP에서 임시 시스템 버전 관리를 사용하도록 지원됩니다. 자세한 내용은 [메모리 액세스에 최적화된 테이블을 포함한 시스템 버전 임시 테이블](../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)을 참조하세요.

- 메모리 내 OLTP 작업에서 네이티브 컴파일 코드에 대한 쿼리 저장소가 지원됩니다. 자세한 내용은 [메모리 내 OLTP와 쿼리 저장소 사용](../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)을 참조하세요.

- [메모리 액세스에 최적화된 테이블의 행 수준 보안](../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md#rls)

- 이제 [MARS&#40;Multiple Active Result Sets&#41; 사용](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) 연결이 메모리 액세스에 최적화된 테이블 및 고유하게 컴파일된 저장 프로시저에 액세스할 수 있습니다.

- [TDE(투명한 데이터 암호화)](../relational-databases/security/encryption/transparent-data-encryption-tde.md) 지원. 데이터베이스의 ENCRYPTION이 사용하도록 구성된 경우 이제 [메모리 액세스에 최적화된 파일 그룹](../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)의 파일도 암호화됩니다.

자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.


####  <a name="QueryOptimizer"></a> 쿼리 최적화 프로그램
##### <a name="compatibility-level-guarantees"></a>호환성 수준 보증
SQL Server 2016으로 데이터베이스를 업그레이드할 때 사용했던 이전 호환성 수준(예를 들어 120 또는 110)을 유지하는 경우 계획 변경이 표시되지 않습니다. 쿼리 최적화 프로그램에 관련된 새로운 기능과 향상된 기능은 이전 호환성 수준에서만 사용할 수 있습니다. 
##### <a name="trace-flag-4199"></a>추적 플래그 4199
이 추적 플래그를 통해 제어되는 대부분 쿼리 최적화 프로그램 동작이 SQL Server 2016의 최신 호환성 수준(130)에서 무조건 사용하도록 설정된 후에는 일반적으로 SQL Server 2016에서 추적 플래그 4199를 사용할 필요가 없습니다.
##### <a name="new-referential-integrity-operator"></a>새 참조 무결성 연산자
각 테이블은 최대 253개의 다른 테이블 및 열을 외래 키(나가는 참조)로 참조할 수 있습니다. [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 에서는 단일 테이블의 열을 참조할 수 있는 다른 테이블 및 열의 수 제한이 253에서 10,000으로 증가합니다. 제한 사항에 대해서는 [Create Foreign Key Relationships](../relational-databases/tables/create-foreign-key-relationships.md)를 참조하세요. 새 참조 무결성 연산자가 호환성 수준 130에서 도입되어 해당 위치에서 참조 무결성 검사를 수행합니다. 이렇게 하면 들어오는 많은 참조를 보관하는 테이블의 UPDATE 및 DELETE 작업에 대한 전반적인 성능이 향상되어 들어오는 많은 참조를 확보할 수 있게 됩니다. 자세한 내용은 [Query Optimizer Additions in SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/23/query-optimizer-additions-in-sql-server/)(SQL Server 2016의 쿼리 최적화 프로그램에서 추가된 기능)을 참조하세요.
##### <a name="parallel-update-of-sampled-statistics"></a>샘플링된 통계의 병렬 업데이트
통계를 작성할 데이터 샘플링이 이제 병렬로 수행되어(호환성 수준 130) 통계 컬렉션의 성능이 개선되었습니다. 자세한 내용은 [통계 업데이트](../t-sql/statements/update-statistics-transact-sql.md)를 참조하세요.
#### <a name="sublinear-threshold-for-update-of-statistics"></a>통계의 업데이트에 대해 선형 폭이 강조되는 임계값
대형 테이블에서 통계의 자동 업데이트가 한층 더 강화되었습니다(호환성 수준 130). 대형 테이블의 경우 SQL Server 2016부터 통계 자동 업데이트를 트리거하는 임계값이 20%가 되어 임계값이 테이블에서 행이 증가한 수만큼 줄어든 상태로 시작됩니다(백분율로 표시). 임계값을 줄이기 위해 2371 추적 플래그를 설정하지 않아도 됩니다. 
##### <a name="other-enhancements"></a>기타 향상된 기능
Insert select 문에서 Insert는 다중 스레드 형식이거나, 병렬 계획일 수 있습니다(호환성 수준 130). 병렬 계획을 가져오려면 INSERT... SELECT 문에서는 TABLOCK 힌트를 사용해야 합니다. 자세한 내용은 참조 [Parallel Insert Select](https://blogs.msdn.microsoft.com/sqlcat/2016/07/06/sqlsweet16-episode-3-parallel-insert-select/)를 참조하세요.

####  <a name="LiveStats"></a> 활성 쿼리 통계
 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 는 활성 쿼리의 활성 실행 계획을 보는 기능을 제공합니다. 이 활성 쿼리 계획을 통해 제어권이 한 쿼리 계획 연산자에서 다른 연산자로 흘러갈 때 쿼리 실행 프로세스를 실시간으로 파악할 수 있습니다. 자세한 내용은 [Live Query Statistics](../relational-databases/performance/live-query-statistics.md)를 참조하세요.

####  <a name="QueryStore"></a> 쿼리 저장소
쿼리 저장소는 DBA에게 쿼리 계획 선택 및 성능에 대한 정보를 제공하는 새로운 기능입니다. 쿼리 계획 변경으로 인해 발생하는 성능 차이를 신속하게 찾을 수 있도록 하여 성능 문제 해결을 간소화합니다. 이 기능은 쿼리, 계획 및 런타임 통계의 기록을 자동으로 캡처하고 검토할 수 있도록 이 기록을 유지합니다. 데이터를 기간별로 구분하여 데이터베이스 사용 패턴을 파악하고 서버에서 쿼리 계획 변경이 발생한 시기를 이해할 수 있게 해줍니다. 쿼리 저장소는 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 대화 상자를 사용하여 정보를 표시하고 이를 통해 선택된 쿼리 계획 중 하나에 쿼리를 적용할 수 있습니다. 자세한 내용은 [Monitoring Performance By Using the Query Store](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)을 참조하세요.


####  <a name="TT"></a> 임시 테이블
[!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 은 이제 시스템 버전 임시 테이블을 지원합니다. 임시 테이블은 언제든지 저장된 팩트에 대한 올바른 정보를 제공하는 새로운 테이블 유형입니다. 각 임시 테이블은 실제로 현재 데이터 및 기록 데이터에 각각 하나씩 해당하는 테이블 두 개로 구성됩니다. 시스템에서는 현재 데이터가 포함된 테이블의 데이터가 변경될 때 이전 값이 기록 테이블에 저장되어 있는지 확인합니다. 이와 같은 복잡한 구조가 사용자에게 표시되지 않도록 쿼리 구문이 제공됩니다. 자세한 내용은 [Temporal Tables](../relational-databases/tables/temporal-tables.md)을 참조하세요.

####  <a name="StripedBackupToAzure"></a> Microsoft Azure Blob Storage에 대한 스트라이프 백업
[!INCLUDE[ssSQL15](../includes/sssql15-md.md)]에서 Microsoft Azure Blob 저장소 서비스를 사용하는 URL에 SQL Server 백업 기능에서 12.8TB의 최대 백업 크기를 지원하는 블록 Blob을 사용하여 스트라이프 백업 세트를 지원합니다. 예를 보려면 [Code Examples](../relational-databases/backup-restore/sql-server-backup-to-url.md#Examples)를 참조하세요.

####  <a name="FileSnapshotBackup"></a> Microsoft Azure Blob Storage에 대한 파일-스냅숏 백업
 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]의 URL에 대한 SQL Server 백업 기능에서는 이제 Azure 스냅숏을 사용하여 모든 데이터베이스 파일이 Microsoft Azure Blob 저장소 서비스를 통해 저장되는 데이터베이스를 백업할 수 있습니다. 자세한 내용은 [Azure의 데이터베이스 파일에 대한 파일-스냅숏 백업](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)을 참조하세요.

####  <a name="ManagedBackup"></a> Managed Backup
Microsoft Azure에 대한 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SQL Server Managed Backup에서는 백업 파일에 새 블록 Blob 저장소를 사용합니다. Managed Backup에 대한 몇 가지 변경 내용과 향상된 기능도 있습니다.

-   자동화된 백업 일정 및 사용자 지정 백업 일정을 둘 다 지원합니다.

-   시스템 데이터베이스에 대한 백업을 지원합니다.

-   단순 복구 모델을 사용 중인 데이터베이스를 지원합니다.

 자세한 내용은 [SQL Server Managed Backup to Microsoft Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)를 참조하세요.

> [!NOTE]
>  [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]의 경우 이 새로운 Managed Backup 기능은 아직 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 UI로 지원되지 않습니다.

####  <a name="multipleTempDB"></a> TempDB 데이터베이스
 TempDB에 대한 몇 가지 향상된 기능이 있습니다.

-   Tempdb에 대한 추적 플래그 1117 및 1118이 필요하지 않습니다. Tempdb 데이터베이스가 여러 개 있을 경우 모든 파일은 증가 설정에 따라 동시에 크기가 증가합니다. 또한 tempdb의 모든 할당에는 단일 익스텐트가 사용됩니다.

-   기본적으로 설치 시 CPU 개수 또는 8개 중 적은 수만큼 tempdb 파일이 추가됩니다.

-   설치하는 동안 SQL Server 설치 마법사의 데이터베이스 엔진 구성 - TempDB 섹션에서 새로운 UI 입력 컨트롤을 사용하여 tempdb 데이터베이스 파일 수, 초기 크기, 자동 증가 및 디렉터리 배치를 구성할 수 있습니다.

-   기본 초기 크기는 8MB이고 기본 자동 증가는 64MB입니다.

-   Tempdb 데이터베이스 파일에 대해 여러 볼륨을 지정할 수 있습니다. 여러 디렉터리가 지정된 경우 tempdb 데이터 파일은 라운드 로빈 방식으로 여러 디렉터리에 분배됩니다.

####  <a name="ForJson"></a> 기본 제공 JSON 지원
SQL Server 2016에서는 JSON 가져오기 및 내보내기와 JSON 문자열 사용에 대한 기본 제공 지원을 추가합니다. 이 기본 제공 지원에는 다음 문과 함수가 포함됩니다.

-   **FOR JSON** 절을 **SELECT** 문에 추가하여 쿼리 결과 서식을 JSON으로 지정하거나 JSON을 내보냅니다. 예를 들어 **FOR JSON** 절을 사용하여 JSON 출력의 서식 지정 작업을 클라이언트 응용 프로그램에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로 위임할 수 있습니다. 자세한 내용은 [FOR JSON을 사용하여 쿼리 결과를 JSON으로 서식 지정&#40;SQL Server&#41;](../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)을 참조하세요.

-   **OPENJSON** 행 집합 공급자 함수를 호출하여 JSON 데이터를 행과 열로 변환하거나 JSON을 가져옵니다. **OPENJSON** 을 사용하여 JSON 데이터를 SQL Server로 가져오거나, JSON 데이터를 현재 JSON을 직접 사용할 수 없는 앱이나 서비스에 대한 행 및 열로 변환합니다. 자세한 내용은 [OPENJSON을 사용하여 JSON 데이터를 행과 열로 변환&#40;SQL Server&#41;](../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)을 참조하세요.

-   **ISJSON** 함수는 문자열에 유효한 JSON이 포함되어 있는지 여부를 테스트합니다. 자세한 내용은 [ISJSON&#40;Transact-SQL&#41;](../t-sql/functions/isjson-transact-sql.md)을 참조하세요.

-   **JSON_VALUE** 함수는 JSON 문자열에서 스칼라 값을 추출합니다. 자세한 내용은 [JSON_VALUE&#40;Transact-SQL&#41;](../t-sql/functions/json-value-transact-sql.md)를 참조하세요.

-   **JSON_QUERY** 함수는 JSON 문자열에서 개체 또는 배열을 추출합니다. 자세한 내용은 [JSON_QUERY&#40;Transact-SQL&#41;](../t-sql/functions/json-query-transact-sql.md)를 참조하세요.

-   **JSON_MODIFY** 함수는 JSON 문자열의 속성 값을 업데이트하고 업데이트된 JSON 문자열을 반환합니다. 자세한 내용은 [JSON_MODIFY &#40;Transact-SQL&#41;](../t-sql/functions/json-modify-transact-sql.md)을 참조하세요.

####  <a name="bkPolyBase"></a> PolyBase
 PolyBase를 사용하면 T-SQL 문을 사용하여 Hadoop 또는 Azure Blob Storage에 저장된 데이터에 액세스하고 임시 방식으로 데이터를 쿼리할 수 있습니다. 또한 반구조적 데이터를 쿼리하고 결과를 SQL Server에 저장된 관계형 데이터 집합과 조인할 수 있습니다. PolyBase는 데이터 웨어하우징 작업에 최적화되고 분석 쿼리 시나리오에 사용됩니다.

 자세한 내용은 [PolyBase 가이드](../relational-databases/polybase/polybase-guide.md)를 참조하세요.

####  <a name="stretch"></a> Stretch Database
 스트레치 데이터베이스는 기록 데이터를 Microsoft Azure 클라우드에 투명하고 안전하게 마이그레이션하는 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 의 새로운 기능입니다. 온-프레미스에 있든 클라우드로 확장되든 상관없이 SQL Server 데이터에 원활하게 액세스할 수 있습니다. 데이터 저장 위치를 결정하는 정책을 설정하면 SQL Server가 백그라운드에서 데이터 이동을 처리합니다. 전체 테이블은 항상 온라인 상태이며 쿼리할 수 있습니다. 또한 스트레치 데이터베이스는 기존 쿼리 또는 응용 프로그램을 변경할 필요가 없습니다. 데이터의 위치가 응용 프로그램에 완전히 투명합니다. 자세한 내용은 [Stretch Database](../sql-server/stretch-database/stretch-database.md)를 참조하십시오.
 
####  <a name="UTF8"></a> UTF-8에 대한 지원
[bcp 유틸리티](../tools/bcp-utility.md), [BULK INSERT](../t-sql/statements/bulk-insert-transact-sql.md) 및 [OPENROWSET](../t-sql/functions/openrowset-transact-sql.md)는 이제 UTF-8 코드 페이지를 지원합니다. 자세한 내용은 해당 항목 및 [서식 파일 만들기&#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md)를 참조하세요.

####  <a name="DefaultDB"></a> 새로운 기본 데이터베이스 크기 및 자동 증가 값
model 데이터베이스의 새 값 및 모델을 기반으로 하는 새 데이터베이스의 기본값이 추가되었습니다. 이제 데이터 및 로그 파일의 초기 크기는 8MB입니다. 이제 데이터 및 로그 파일의 기본 자동 증가는 64MB입니다.


###  <a name="TSQL"></a> 향상된 Transact-SQL 기능
수많은 기능 향상을 통해 이 항목의 다른 섹션에서 설명되는 기능이 지원됩니다. 다음과 같은 향상된 기능이 추가로 제공됩니다.
- 이제 TRUNCATE TABLE 문은 지정된 파티션의 잘림을 허용합니다. 자세한 내용은 [TRUNCATE TABLE&#40;Transact-SQL&#41;](../t-sql/statements/truncate-table-transact-sql.md)을 참조하세요.
- 이제 [ALTER TABLE&#40;Transact-SQL&#41;](../t-sql/statements/alter-table-transact-sql.md)은 테이블을 사용 가능한 상태로 유지하면서 많은 열 변경 작업을 수행할 수 있게 해줍니다.
- 전체 텍스트 인덱스 DMV [sys.dm_fts_index_keywords_position_by_document&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-position-by-document-transact-sql.md)는 문서에서 키워드의 위치를 반환합니다. 이 DMV는 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] SP2 및 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP1에도 추가되었습니다.
- 새 쿼리 힌트 **NO_PERFORMANCE_SPOOL** 은 스풀 연산자가 쿼리 계획에 추가되지 않도록 합니다. 그 결과, 스풀 작업에서 많은 동시 쿼리가 실행 중일 때 성능이 향상될 수 있습니다. 자세한 내용은 [쿼리 힌트&#40;Transact-SQL&#41;](../t-sql/queries/hints-transact-sql-query.md)를 참조하세요.
- [FORMATMESSAGE&#40;Transact-SQL&#41;](../t-sql/functions/formatmessage-transact-sql.md) 문이 msg_string 인수를 적용하도록 향상되었습니다. NONCLUSTERED 인덱스의 최대 인덱스 키 크기가 1700바이트로 증가되었습니다.
- 새 DROP IF 구문이 AGGREGATE, ASSEMBLY, COLUMN, CONSTRAINT, DATABASE, DEFAULT, FUNCTION, INDEX, PROCEDURE, ROLE, RULE, SCHEMA, SECURITY POLICY, SEQUENCE, SYNONYM, TABLE, TRIGGER, TYPE, USER 및 VIEW에 관련된 drop 문에 추가되었습니다. 구문에 대해서는 개별 구문 항목을 참조하세요.
- 병렬 처리 수준을 지정하기 위해 [DBCC CHECKTABLE&#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checktable-transact-sql.md), [DBCC CHECKDB&#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) 및 [DBCC CHECKFILEGROUP&#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md)에 MAXDOP 옵션이 추가되었습니다.
- 이제 SESSION_CONTEXT를 설정할 수 있습니다. [SESSION_CONTEXT&#40;Transact-SQL&#41;](../t-sql/functions/session-context-transact-sql.md) 함수, [CURRENT_TRANSACTION_ID&#40;Transact-SQL&#41;](../t-sql/functions/current-transaction-id-transact-sql.md) 함수 및 [sp_set_session_context&#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md) 프로시저를 포함합니다.
- 고급 분석 확장을 통해 사용자는 R 등의 지원 언어로 기록된 스크립트를 실행할 수 있습니다. [!INCLUDE[tsql](../includes/tsql-md.md)]는 [sp_execute_external_script &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 저장 프로시저 및 [external scripts enabled 서버 구성 옵션](../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)을 도입하여 R을 지원합니다. 자세한 내용은 [SQL Server R Services](../advanced-analytics/r-services/sql-server-r-services.md)를 참조하세요.
- 또한 R을 지원하기 위해 외부 리소스 풀을 만들 수 있습니다. 자세한 내용은 [CREATE EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../t-sql/statements/create-external-resource-pool-transact-sql.md)을 참조하세요.  새 카탈로그 뷰 및 DMV([sys.resource_governor_external_resource_pools&#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md) 및 [sys.dm_resource_governor_external_resource_pool_affinity&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md))입니다. [sp_execute_external_script&#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 및 [CREATE WORKLOAD GROUP&#40;Transact-SQL&#41;](../t-sql/statements/create-workload-group-transact-sql.md)에 추가 인수를 사용할 수 있습니다. 일부 리소스 관리자 카탈로그 뷰 및 DMV에 다른 열이 추가되었습니다.
- 상시 암호화 기능을 지원하도록 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS 옵션을 사용하여 [CREATE USER](../t-sql/statements/create-user-transact-sql.md) 구문이 향상되었습니다. 자세한 내용은 [상시 암호화로 보호되는 중요한 데이터 마이그레이션](../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md)을 참조하세요.
- [COMPRESS&#40;Transact-SQL&#41;](../t-sql/functions/compress-transact-sql.md) 및 [DECOMPRESS&#40;Transact-SQL&#41;](../t-sql/functions/decompress-transact-sql.md) 함수는 값을 GZIP 알고리즘으로 변환하거나, 그 반대로 변환합니다.
- [DATEDIFF_BIG&#40;Transact-SQL&#41;](../t-sql/functions/datediff-big-transact-sql.md) 및 [AT TIME ZONE&#40;Transact-SQL&#41;](../t-sql/queries/at-time-zone-transact-sql.md) 함수와 [sys.time_zone_info&#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-time-zone-info-transact-sql.md) 뷰가 날짜 및 시간 상호 작용을 지원하기 위해 추가되었습니다.
- 이전에 제공된 서버 수준 자격 증명 이외에 이제 데이터베이스 수준에서 자격 증명을 만들 수 있습니다. 자세한 내용은 [CREATE DATABASE SCOPED CREDENTIAL&#40;Transact-SQL&#41;](../t-sql/statements/create-database-scoped-credential-transact-sql.md)을 참조하세요.
- InstanceDefaultDataPath, InstanceDefaultLogPath, ProductBuild, ProductBuildType, ProductMajorVersion, ProductMinorVersion, ProductUpdateLevel 및 ProductUpdateReference라는 8개의 새로운 속성이 [SERVERPROPERTY&#40;Transact-SQL&#41;](../t-sql/functions/serverproperty-transact-sql.md)에 추가되었습니다.
- [HASHBYTES&#40;Transact-SQL&#41;](../t-sql/functions/hashbytes-transact-sql.md) 함수에 대한 8,000바이트 입력 길이 제한이 제거되었습니다.
- 새로운 문자열 함수 [STRING_SPLIT&#40;Transact-SQL&#41;](../t-sql/functions/string-split-transact-sql.md) 및 [STRING_ESCAPE&#40;Transact-SQL&#41;](../t-sql/functions/string-escape-transact-sql.md)가 추가되었습니다.
- 자동 증가 옵션: ALTER DATABASE의 AUTOGROW_SINGLE_FILE 및 AUTOGROW_ALL_FILES 옵션이 추적 플래그 1117을 대체했고 추적 플래그 1117이 아무런 영향을 미치지 않습니다. 자세한 내용은 [ALTER DATABASE 파일 및 파일 그룹 옵션&#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md) 및 [sys.filegroups&#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)의 새 is_autogrow_all_files 열을 참조하세요.
- 혼합 익스텐트 할당: 사용자 데이터베이스에서 개체의 처음 8페이지에 대한 기본 할당이 혼합 페이지 익스텐트 사용에서 단일 익스텐트 사용으로 변경됩니다. ALTER DATABASE의 SET MIXED_PAGE_ALLOCATION 옵션이 추적 플래그 1118을 대체했고 추적 플래그 1118이 아무런 영향을 미치지 않습니다. 자세한 내용은 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-set-options.md) 및 [sys.databases&#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-databases-transact-sql.md)의 새 `is_mixed_page_allocation_on` 열을 참조하세요.


###  <a name="SystemTable"></a> 향상된 시스템 뷰 기능
- 새로운 두 개의 뷰가 행 수준 보안을 지원합니다. 자세한 내용은 [sys.security_predicates&#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md) 및 [sys.security_policies&#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)를 참조하세요.
- 새로운 7개의 뷰가 쿼리 저장소 기능을 지원합니다. 자세한 내용은 [쿼리 저장소 카탈로그 뷰&#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)를 참조하세요.
- 메모리 부여에 대한 정보를 제공하는 새로운 24개의 열이 [sys.dm_exec_query_stats&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)에 추가되었습니다.
- 메모리 부여를 지정하도록 새로운 두 개의 쿼리 힌트(MIN_GRANT_PERCENT 및 MAX_GRANT_PERCENT)가 추가되었습니다. [쿼리 힌트&#40;Transact-SQL&#41;](../t-sql/queries/hints-transact-sql-query.md)를 참조하세요.
- [sys.dm_exec_session_wait_stats&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md)는 서버 전체 [sys.dm_os_wait_stats&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)와 비슷한 세션별 보고서를 제공합니다.
- [sys.dm_exec_function_stats&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-function-stats-transact-sql.md)는 스칼라 반환 함수에 대한 실행 통계를 제공합니다.
- [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]부터 [sys.dm_db_index_usage_stats&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)의 항목은 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 이전의 상태로 유지됩니다.
- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 제출된 문에 대한 정보는 새로운 동적 관리 함수인 [sys.dm_exec_input_buffer&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md)를 통해 반환할 수 있습니다.
- [SQL Server R 서비스](../advanced-analytics/r-services/sql-server-r-services.md)를 지원하는 2개의 새로운 뷰: [sys.dm_external_script_requests](../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) 및 [sys.dm_external_script_execution_stats](../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)가 제공됩니다. 


###  <a name="Security"></a> 향상된 보안 기능

####  <a name="RLS"></a> 행 수준 보안
행 수준 보안에 조건자 기반 액세스 제어가 도입됩니다. 여기에는 유연하고, 중앙 집중적이며, 조건자 기반 평가가 있어 메타데이터(예: 레이블) 또는 관리자가 적절히 판단한 기타 기준을 고려할 수 있습니다. 조건자는 사용자 특성에 따라 사용자가 데이터에 적절하게 액세스하는지의 여부를 결정하는 기준으로 사용됩니다. 조건자 기반 액세스 제어를 사용하여 레이블 기반 액세스 제어를 구현할 수 있습니다. 자세한 내용은 [행 수준 보안](../relational-databases/security/row-level-security.md)을 참조하세요.


####  <a name="TCE"></a> 상시 암호화
상시 암호화를 통해 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 암호화된 데이터에 대한 작업을 실행할 수 있고, 무엇보다 모든 암호화 키는 서버가 아닌 고객의 신뢰할 수 있는 환경 내의 응용 프로그램에 있습니다. 상시 암호화는 고객 데이터를 보호하므로 DBA가 일반 텍스트 데이터에 액세스할 수 없습니다. 데이터의 암호화 및 암호 해독은 드라이버 수준에서 투명하게 수행되므로 기존 응용 프로그램에서 변경해야 하는 내용이 최소화됩니다. 자세한 내용은 [상시 암호화&#40;데이터베이스 엔진#41;](../relational-databases/security/encryption/always-encrypted-database-engine.md)를 참조하세요.


####  <a name="Masking"></a> 동적 데이터 마스킹
동적 데이터 마스킹에서는 권한이 없는 사용자로 마스킹하여 중요한 데이터 노출을 제한합니다. 동적 데이터 마스킹을 사용하면 고객이 응용 프로그램 계층에 미치는 영향을 최소화하고 표시할 중요한 데이터의 양을 지정할 수 있게 하여 중요한 데이터에 대한 무단 액세스를 방지할 수 있습니다. 데이터베이스의 데이터는 변경되지 않으면서 지정된 데이터베이스 필드에 대한 쿼리의 결과 집합에서 중요한 데이터를 숨기는 정책 기반 보안 기능입니다. 자세한 내용은 [Dynamic Data Masking](../relational-databases/security/dynamic-data-masking.md)을 참조하세요.


####  <a name="Perms"></a> 새 사용 권한
- **ALTER ANY SECURITY POLICY** 권한은 행 수준 보안 구현의 일부로 제공됩니다.
- **ALTER ANY MASK** 및 **UNMASK** 권한은 동적 데이터 마스킹 구현의 일부로 제공됩니다.
- **ALTER ANY COLUMN ENCRYPTION KEY**, **VIEW ANY COLUMN ENCRYPTION KEY**, **ALTER ANY COLUMN MASTER KEY DEFINITION**및 **VIEW ANY COLUMN MASTER KEY DEFINITION** 권한은 상시 암호화 기능 구현의 일부로 제공됩니다.
- **ALTER ANY EXTERNAL DATA SOURCE** 및 **ALTER ANY EXTERNAL FILE FORMAT** 권한은 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 에 표시되지만 [!INCLUDE[ssAPS](../includes/ssaps-md.md)] ([!INCLUDE[ssDW](../includes/ssdw-md.md)])에만 적용됩니다.
- **EXECUTE ANY EXTERNAL SCRIPT** 권한은 R 스크립트 지원의 일부로 제공됩니다.
 - **ALTER ANY DATABASE SCOPED CONFIGURATION** 권한은 [ALTER DATABASE SCOPED CONFIGURATION&#40;Transact-SQL&#41;](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) 문 사용에 대한 권한을 부여하기 위해 제공됩니다.

####  <a name="TDE"></a> 투명한 데이터 암호화
- 암호화의 Intel AES-NI 하드웨어 가속이 지원되어 투명한 데이터 암호화가 향상되었습니다. 그 결과, 투명한 데이터 암호화를 켜는 경우 CPU 오버헤드가 감소합니다.

###  <a name="AES"></a> 끝점에 대한 AES 암호화
- 끝점에 대한 기본 암호화가 RC4에서 AES로 변경되었습니다.

####  <a name="newcredentialtype"></a> 새 자격 증명 유형
- 이전에 제공된 서버 수준 자격 증명 이외에 이제 데이터베이스 수준에서 자격 증명을 만들 수 있습니다. 자세한 내용은 [CREATE DATABASE SCOPED CREDENTIAL&#40;Transact-SQL&#41;](../t-sql/statements/create-database-scoped-credential-transact-sql.md)을 참조하세요.


###  <a name="HighAvailability"></a> 향상된 고가용성 기능
이제 SQL Server 2016 Standard Edition은 Always On 기본 가용성 그룹을 지원합니다. 기본 가용성 그룹은 기본 및 보조 복제본을 지원합니다. 이 기능은 고가용성에 대한 오래된 데이터베이스 미러링 기술을 대체합니다. 기본 가용성 그룹과 고급 가용성 그룹의 차이점에 대한 자세한 내용은 [기본 가용성 그룹&#40;Always On 가용성 그룹&#41;](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md)을 참조하세요.

이제 읽기 전용 연결 요청의 부하를 읽기 전용 복제본 집합에 분산할 수 있습니다. 이전 동작은 항상 라우팅 목록에서 처음 사용 가능한 읽기 전용 복제본으로 연결을 전송했습니다. 자세한 내용은 [읽기 전용 복제본에 대한 부하 분산 구성](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md#loadbalancing)을 참조하세요.

 자동 장애 조치(failover)를 지원하는 복제본 수가 두 개에서 세 개로 증가했습니다.

 이제 Always On 장애 조치(failover) 클러스터에 대한 그룹 관리 서비스 계정이 지원됩니다. 자세한 내용은 [그룹 관리 서비스 계정 개요](https://technet.microsoft.com/library/hh831782.aspx)를 참조하세요. Windows Server 2012 R2에서는 암호가 변경된 후 임시 가동 중지 시간을 방지하려면 업데이트가 필요합니다. 업데이트를 가져오려면 [gMSA 기반 서비스 Windows Server 2012 R2 도메인에서 암호 변경 후 로그온 할 수 없습니다](https://support.microsoft.com/kb/2998082/)를 참조하세요.

 [!INCLUDE[ssHADR](../includes/sshadr-md.md)] 은 Windows Server 2016에서 분산 트랜잭션 및 DTC를 지원합니다. 자세한 내용은 [분산 트랜잭션 지원](../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md#dtcsupport)을 참조하세요.

 이제 데이터베이스가 오프라인으로 전환될 때 장애 조치(failover)하도록 [!INCLUDE[ssHADR](../includes/sshadr-md.md)] 을 구성할 수 있습니다. 이렇게 변경하려면 [CREATE AVAILABILITY GROUP&#40;Transact-SQL&#41;](../t-sql/statements/create-availability-group-transact-sql.md) 또는 [ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../t-sql/statements/alter-availability-group-transact-sql.md) 문에서 **DB_FAILOVER** 옵션을 **ON**으로 설정해야 합니다.

이제 Always On은 암호화된 데이터베이스를 지원합니다. 이제 가용성 그룹 마법사에서는 새 가용성 그룹을 만들거나 기존 가용성 그룹에 데이터베이스 또는 복제본을 추가할 때 데이터베이스 마스터 키가 포함된 데이터베이스에 대한 암호를 묻는 메시지를 표시합니다.

이제 두 개의 개별 WSFC(Windows Server 장애 조치(failover) 클러스터)에 있는 두 개의 가용성 그룹을 분산형 가용성 그룹으로 결합할 수 있습니다. 자세한 내용은 [분산된 가용성 그룹&#40;Always On 가용성 그룹&#41;](../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)을 참조하세요.

직접 시드를 사용하여 네트워크를 통해 보조 복제본을 자동으로 시드할 수 있습니다(수동 시드의 경우 대상 데이터베이스의 물리적 백업을 보조 복제본에서 복원해야 함). 직접 시드를 지정하려면 [CREATE AVAILABILITY GROUP&#40;Transact-SQL&#41;](../t-sql/statements/create-availability-group-transact-sql.md) 또는 [ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../t-sql/statements/alter-availability-group-transact-sql.md) 문에서 **SEEDING_MODE=AUTOMATIC**을 설정합니다. 또한 직접 시드에서 사용되는 각 보조 복제본에서 **GRANT CREATE ANY DATABASE** 및 [ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../t-sql/statements/alter-availability-group-transact-sql.md)을 지정해야 합니다.

**성능 향상** – 가용성 그룹의 동기화 처리량은 주 복제본에서 로그 블록의 병렬 및 빠른 압축, 최적화된 동기화 프로토콜, 보조 복제본에서 로그 레코드 다시 실행 및 병렬 압축 풀기를 통해 10배까지 증가되었습니다. 따라서 읽기 가능한 보조 복제본의 새로 고침이 증가되고 장애 조치(failover) 시 데이터베이스 복구 시간이 줄어듭니다. 메모리 액세스에 최적화된 테이블에 대한 다시 실행은 SQL Server 2016에서 아직 병렬로 수행되지 않습니다.

###  <a name="Repl"></a> 향상된 복제 기능
- 이제 메모리 액세스에 최적화된 테이블의 복제가 지원됩니다. 자세한 내용은 [메모리 액세스에 최적화된 테이블 구독자로 복제](../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md)를 참조하세요.
- 이제 [!INCLUDE[ssSDSFull](../includes/sssdsfull-md.md)]에 대한 복제가 지원됩니다. 자세한 내용은 [Replication to SQL Database](../relational-databases/replication/replication-to-sql-database.md)를 참조하세요.

###  <a name="Tools"></a> 향상된 도구 기능

####  <a name="SSMS"></a> Management Studio
최신 [SSMS(SQL Server Management Studio)](https://msdn.microsoft.com/library/mt238290.aspx)를 다운로드

- [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 는 Microsoft Azure에 연결하기 위해 개발 중인 ADAL(Active Directory Authentication Library)을 지원합니다. 이 기능은 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]에서 사용되는 인증서 기반 인증을 대체합니다.
- [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 를 설치하려면 필수 조건으로 .NET 4.6을 설치해야 합니다. .NET 4.6은 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 가 설치될 때 설치 프로그램에 의해 자동으로 설치됩니다.
- 결과 표에서 텍스트를 복사하거나 저장할 때 캐리지 리턴/줄 바꿈(줄 바꿈 문자)을 유지하는 새 쿼리 결과 표 옵션이 지원됩니다. 도구/옵션 메뉴에서 이 옵션을 설정합니다.
- SQL Server 관리 도구는 더 이상 주 기능 트리에서 설치되지 않습니다. 자세한 내용은 [SSMS로 SQL Server 관리 도구 설치](http://msdn.microsoft.com/library/af68d59a-a04d-4f23-9967-ad4ee2e63381)를 참조하세요.
- [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 를 설치하려면 필수 조건으로 .NET 4.6.1을 설치해야 합니다. .NET 4.6.1은 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 가 설치될 때 설치 프로그램에 의해 자동으로 설치됩니다.

####  <a name="UA"></a> 업그레이드 관리자
SQL Server 2016 업그레이드 관리자 Preview는 이전 버전의 사용자가 SQL Server 데이터베이스에 대해 업그레이드 규칙 집합을 실행하여 주요 변경 내용, 동작 변경 내용 및 더 이상 사용되지 않는 기능을 파악하고 스트레치 데이터베이스 등의 새로운 기능을 적용할 때 도움을 제공할 수 있게 하는 독립 실행형 도구입니다.

 [여기](https://www.microsoft.com/en-us/download/details.aspx?id=48119) 에서 업그레이드 관리자 Preview를 다운로드하거나, 웹 플랫폼 설치 관리자를 사용하여 설치할 수 있습니다.

## <a name="see-also"></a>관련 항목:
[SQL Server 2016의 새로운 기능](../sql-server/what-s-new-in-sql-server-2016.md)
 
[SQL Server 2016 릴리스 정보](../sql-server/sql-server-2016-release-notes.md) 
 
[SSMS로 SQL Server 관리 도구 설치](http://msdn.microsoft.com/library/af68d59a-a04d-4f23-9967-ad4ee2e63381)









