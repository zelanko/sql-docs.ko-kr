---
title: "데이터베이스 엔진의 새로운 기능 - SQL Server 2017 | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 42f45b23-6509-45e8-8ee7-76a78f99a920
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: e4a6157cb56c6db911406585f841046a431eef99
ms.openlocfilehash: e3d06068b28a6870a5c34286f073c32519428e39
ms.contentlocale: ko-kr
ms.lasthandoff: 08/16/2017

---
# <a name="whats-new-in-database-engine---sql-server-2017"></a>데이터베이스 엔진의 새로운 기능 - SQL Server 2017
[!INCLUDE[tsql-appliesto-ssvNxt-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

이 문서에서는 향상된 [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)]용 [!INCLUDE[ssdenoversion-md](../includes/ssdenoversion-md.md)] 기능에 대해 설명합니다. 각 항목에 대한 자세한 내용은 아래 링크를 클릭하세요.

> [!NOTE]  
> SQL Server 2017에는 SQL Server 2016 서비스 팩에 추가된 기능도 포함되어 있습니다. 해당 항목에 대해서는 [SQL Server 2016(데이터베이스 엔진)의 새로운 기능](../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md)을 참조하세요.


## <a name="sql-server-database-engine-rc1"></a>SQL Server 데이터베이스 엔진(RC1)  
- 이제 CTP 2.0에 설명된 `clr strict security` 기능에 대한 해결 방법으로 CLR 어셈블리를 허용 목록에 추가할 수 있습니다. 신뢰할 수 있는 어셈블리의 허용 목록을 지원하기 위해 [sp_add_trusted_assembly](../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md), [sp_drop_trusted_assembly](../relational-databases/system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md) 및 [sys.trusted_asssemblies](../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)가 추가되었습니다.

## <a name="sql-server-database-engine-previous-ctps"></a>SQL Server 데이터베이스 엔진(이전의 CTP)  
- CLR은 더 이상 보안 경계로 지원되지 않는 .NET Framework의 CAS(코드 액세스 보안)를 사용합니다. `PERMISSION_SET = SAFE`로 만든 CLR 어셈블리에서 외부 시스템 리소스에 액세스하고, 비관리 코드를 호출하고, sysadmin 권한을 얻을 수 있습니다. [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)]부터 CLR 어셈블리의 보안을 강화하기 위해 `clr strict security`라는 `sp_configure` 옵션이 도입되었습니다. `clr strict security`는 기본적으로 사용되며 `SAFE` 및 `EXTERNAL_ACCESS` 어셈블리가 `UNSAFE`로 표시된 것처럼 처리됩니다. `clr strict security` 옵션은 이전 버전과의 호환성을 위해 사용하지 않도록 설정할 수 있지만 권장하지는 않습니다. 모든 어셈블리는 master 데이터베이스에서 `UNSAFE ASSEMBLY` 권한이 부여된 해당 로그인이 포함된 인증서 또는 비대칭 키로 서명하는 것이 좋습니다. 자세한 내용은 [CLR strict security](configure-windows/clr-strict-security.md)를 참조하세요.  
- [sys.dm_db_log_stats](../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md) DMF가 트랜잭션 로그 파일에 대한 요약 수준 특성 및 정보를 표시하기 위해 새로 도입되었으며, 트랜잭션 로그의 상태를 모니터링하는 데 유용합니다.  
- 다시 시작 가능한 온라인 인덱스 다시 작성 - 다시 시작 가능한 온라인 인덱스 다시 작성을 사용하면 오류(예: 복제본으로 장애 조치 또는 디스크 공간 부족)가 발생한 후 중지된 위치에서 온라인 인덱스 다시 작성 작업을 다시 시작할 수 있습니다. 또한 온라인 인덱스 다시 작성 작업을 일시 중지했다가 나중에 다시 시작할 수도 있습니다. 예를 들어 우선 순위가 높은 작업을 실행하기 위해 시스템 리소스를 일시적으로 비우거나, 사용 가능한 유지 관리 시간이 큰 테이블에 비해 너무 짧은 경우 또 다른 유지 관리 기간에서 인덱스 다시 작성하여 완료해야 할 수 있습니다. 마지막으로 다시 시작 가능한 온라인 인덱스 다시 작성에는 상당한 로그 공간이 필요하지 않으므로 이 작업이 실행되는 동안 로그 잘림을 수행할 수 있습니다. [ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md) 및 [온라인 인덱스 작업에 대한 지침](../relational-databases/indexes/guidelines-for-online-index-operations.md)을 참조하세요.
- **ALTER DATABASE SCOPED CONFIGURATION에 대한 IDENTITY_CACHE 옵션** - IDENTITY_CACHE 옵션이 `ALTER DATABASE SCOPED CONFIGURATION` T-SQL 문에 새로 추가되었습니다. 이 옵션을 `OFF`로 설정하면 서버가 예기치 않게 다시 시작되거나 보조 서버로 장애 조치되는 경우 데이터베이스 엔진에서 ID 열 값 차이가 발생하지 않도록 방지할 수 있습니다. [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)을 참조하세요.   
-  [!INCLUDE[ssnoversion](../includes/ssnoversion.md)]는 이제 다대다 관계를 모델링 하는 그래프 데이터베이스 기능을 제공합니다. 여기에는 노드 및 가장자리 테이블을 만들기 위한 새로운 [CREATE TABLE](../t-sql/statements/create-table-sql-graph.md) 구문과 쿼리에 대한 [MATCH](../t-sql/queries/match-sql-graph.md) 키워드가 포함됩니다. 자세한 내용은 [SQL Server 2017에서 그래프 처리](../relational-databases/graphs/sql-graph-overview.md)를 참조하세요.   
- 자동 튜닝은 잠재적 쿼리 성능 문제에 대한 정보를 제공하고, 솔루션을 권장하며, 식별된 문제를 자동으로 해결하는 데이터베이스 기능입니다. [!INCLUDE[ssnoversion](../includes/ssnoversion.md)]의 자동 튜닝은 잠재적인 성능 문제를 검색할 때마다 알려주고, 정정 작업을 적용하거나 [!INCLUDE[ssde-md](../includes/ssde-md.md)]에서 자동으로 성능 문제를 해결할 수 있도록 합니다. 자세한 내용은 [자동 튜닝](../relational-databases/automatic-tuning/automatic-tuning.md)을 참조하세요.
- 메모리 최적화 테이블에 대한 비클러스터형 인덱스 작성 성능 향상 - 데이터베이스 복구 중에 MEMORY_OPTIMIZED 테이블에 대한 bwtree(비클러스터형) 인덱스를 다시 작성하는 성능이 상당히 최적화되었습니다. 이에 따라 비클러스터형 인덱스를 사용하는 경우 데이터베이스 복구 시간을 크게 줄여줍니다.  
- [sys.dm_os_sys_info](../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)에는 새로운 3개 열, 즉 socket_count, cores_per_socket 및 numa_node_count가 있습니다.
- [sys.dm_db_file_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)에 modified_extent_page_count\, 열이 새로 추가되어 데이터베이스의 각 데이터베이스 파일에 대한 차등 변경 내용을 추적합니다. 새로운 modified_extent_page_count 열을 사용하면 데이터베이스에서 변경된 페이지 백분율이 임계값(예: 70-80 %) 미만인 경우 차등 백업을 수행하고, 그렇지 않은 경우 전체 데이터베이스 백업을 수행하는 스마트 백업 솔루션을 빌드할 수 있습니다.
- SELECT INTO … ON FileGroup - [SELECT INTO](../t-sql/queries/select-into-clause-transact-sql.md)는 이제 SELECT INTO TSQL 구문에 추가된 **ON** 키워드 지원을 사용하여 사용자의 기본 파일 그룹이 아닌 파일 그룹에 테이블을 로드하도록 지원합니다.
- Tempdb 설정 향상 - 파일 크기가 1GB보다 큰 값으로 설정되고 IFI를 사용하도록 설정되지 않은 경우 이 설정을 통해 고객에 대한 경고 메시지와 함께 파일당 초기 tempdb 파일 크기를 **256GB(262,144MB)**까지 지정할 수 있습니다. 지정된 tempdb 데이터 파일의 초기 크기에 따라 설치 시간이 기하급수적으로 증가할 수 있는 IFI(인스턴트 파일 초기화)를 사용하지 않도록 설정하는 의미를 이해해야 합니다. IFI는 트랜잭션 로그 크기에 적용할 수 없으므로 SQL Server 서비스 계정에 대한 IFI 설정과 관계없이 설치 중에 tempdb를 시작하는 동안 더 큰 값의 트랜잭션 로그를 지정하면 설치 시간이 항상 증가할 수 있습니다.
- 새로운 [sys.dm_tran_version_store_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-space-usage.md) DMV가 데이터베이스당 버전 저장소 사용량을 추적하기 위해 도입되었습니다. 이 새로운 DMV는 프로덕션 서버에서 실행되는 성능 비용이나 오버헤드 없이 데이터베이스당 버전 저장소 사용량 요구 사항을 기반으로 하여 tempdb 크기 조정을 사전에 계획하기 위해 버전 저장소 사용량에 대하여 tempdb를 모니터링하는 데 유용합니다.
- 새로운 [sys.dm_db_log_info](../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md) DMF가 DBCC LOGINFO와 비슷한 VLF 정보를 표시하여 고객이 경험한 VLF 수, VLF 크기 또는 축소 파일 문제로 인해 발생할 수 있는 잠재적인 트랜잭션 로그 문제를 모니터링, 경고 및 방지하기 위해 도입되었습니다.
- 최첨단 서버의 소형 데이터베이스에 대해 향상된 백업 성능 - SQL Server에서 데이터베이스 백업을 수행하는 동안 백업 프로세스는 진행 중인 I/O를 비우기 위해 버퍼 풀을 여러 번 반복해야 합니다. 결과적으로 백업 시간은 데이터베이스 크기의 기능일 뿐만 아니라 활성 버퍼 풀 크기의 기능이기도 합니다. SQL Server 2017에서 백업은 버퍼 풀을 여러 번 반복하지 않도록 최적화되어 중소형 데이터베이스의 백업 성능이 크게 향상되었습니다. 백업 및 백업 I/O에 대한 페이지가 버퍼 풀 반복에 비해 더 많은 시간이 소모되므로 데이터베이스 크기가 증가할수록 성능이 저하됩니다.  
- 쿼리 저장소는 이제 대기 통계 요약 정보를 추적합니다. 쿼리 저장소에서 쿼리당 대기 통계 범주를 추적하면 다음 단계의 성능 문제 해결 환경을 통해 워크로드 성능 및 병목 현상에 대한 정보를 더 자세히 제공하는 한편 쿼리 저장소의 주요 이점을 유지할 수 있습니다.  
- 시스템 버전의 임시 테이블은 이제 CASCADE DELETE 및 CASCADE UPDATE를 지원합니다.  
- 간접 검사점 성능 개선 사항
- 클러스터 없는 가용성 그룹 지원이 추가되었습니다.
- 최소 복제본 커밋 가용성 그룹 설정이 추가되었습니다.
- 이제 가용성 그룹은 Windows-Linux 간에 원활하게 작동되므로 OS 간 마이그레이션 및 테스트가 가능합니다.
- 임시 테이블 보존 정책 지원이 추가되었습니다.
- 새로운 DMV SYS.DM_DB_STATS_HISTOGRAM
- 온라인 비클러스터형 columnstore 인덱스 작성 및 다시 작성 지원이 추가되었습니다.
- [sys.dm_db_stats_histogram(TRANSACT-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) 이 통계 검사를 위해 추가되었습니다.
- SQL Server Management Studio 버전 16.4와 함께 릴리스된 DTA(데이터베이스 튜닝 관리자)에서는 SQL Server 2016 이상에서 분석을 수행할 때 추가적인 옵션을 제공합니다.    
   - 성능 향상. 자세한 내용은 [DTA(데이터베이스 엔진 튜닝 관리자) 권장 사항을 사용한 성능 향상](../relational-databases/performance/performance-improvements-using-dta-recommendations.md)을 참조하세요.
   - columnstore 인덱스의 권장 사항을 허용하는 `-fc` 옵션. 자세한 내용은 [DTA 유틸리티](../tools/dta/dta-utility.md) 및 [DTA(데이터베이스 엔진 튜닝 관리자)의 Columnstore 인덱스 권장 사항](../relational-databases/performance/columnstore-index-recommendations-in-database-engine-tuning-advisor-dta.md)을 참조하세요.  
   - DTA에서 쿼리 저장소의 작업을 검토하기 위한 `-iq` 옵션. 자세한 내용은 [쿼리 저장소의 작업을 사용하여 데이터베이스 튜닝](../relational-databases/performance/tuning-database-using-workload-from-query-store.md)을 참조하세요.  
- 메모리 내 기능의 경우 메모리 최적화 테이블 및 고유하게 컴파일된 함수에 대해 향상된 추가 기능을 사용할 수 있습니다. 이러한 향상된 기능을 보여주는 코드 샘플은 [메모리 내 OLTP를 통해 JSON 처리 최적화](../relational-databases/json/optimize-json-processing-with-in-memory-oltp.md)를 참조하세요.
    - 계산 열의 인덱스를 비롯하여 메모리 액세스에 최적화된 테이블의 계산 열에 대한 지원
    - 고유하게 컴파일된 모듈과 CHECK 제약 조건의 JSON 함수에 대한 전체 지원  
    - 고유하게 컴파일된 모듈의`CROSS APPLY` 연산자   
- 새 문자열 함수 [CONCAT_WS](../t-sql/functions/concat-ws-transact-sql.md), [TRANSLATE](../t-sql/functions/translate-transact-sql.md)및 [TRIM](../t-sql/functions/trim-transact-sql.md) 이 추가되었습니다.   
- `WITHIN GROUP` STRING_AGG [함수에 대해 이제](../t-sql/functions/string-agg-transact-sql.md) 절이 지원됩니다.
- 새로운 두 일본어 데이터 정렬 패밀리(Japanese_Bushu_Kakusu_140 및 Japanese_XJIS_140)가 추가되었고, 데이터 정렬 옵션 Variation-selector-sensitive(_VSS)가 일본어 데이터 정렬에서 사용을 위해 추가되었습니다. 자세한 내용은 [데이터 정렬 및 유니코드 지원](../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.   
- 새로운 대량 액세스 옵션([BULK INSERT](../t-sql/statements/bulk-insert-transact-sql.md) 및 [OPENROWSET(BULK...)](../t-sql/functions/openrowset-transact-sql.md))을 사용하면 CSV 형식으로 지정된 파일과 Azure Blob 저장소에 저장된 파일에서 [EXTERNAL DATA SOURCE](../t-sql/statements/create-external-data-source-transact-sql.md)의 새로운 `BLOB_STORAGE` 옵션을 통해 데이터에 직접 액세스할 수 있습니다.
- 데이터베이스 **COMPATIBILITY_LEVEL** 140이 추가되었습니다.   이 수준에서 실행하는 고객에게는 최신 언어 기능 및 쿼리 최적화 프로그램 동작이 제공됩니다. 여기에는 Microsoft에서 릴리스하는 각 시험판 버전의 변경 내용이 포함됩니다.
- 증분 통계 업데이트 임계값을 계산하는 방식이 향상되었습니다(140 호환성 모드 필요).
- [sys.dm_exec_query_statistics_xml](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md) 이 추가되었습니다.
- Memory-Optimized 객체에 대해 향상된 몇 가지 성능 및 언어 기능이 추가되었습니다.
    - `sp_spaceused`가 이제 메모리 최적화 테이블에서 지원됩니다.
    - `sp_rename`이 이제 메모리 최적화 테이블과 고유하게 컴파일된 T-SQL 모듈에서 지원됩니다.
    - `CASE` 식이 이제 고유하게 컴파일된 T-SQL 모듈에서 지원됩니다.
    - 메모리 최적화 테이블에 대한 8개 인덱스 제한이 제거되었습니다.
    - `TOP (N) WITH TIES`가 이제 고유하게 컴파일된 T-SQL 모듈에서 지원됩니다.
    - 메모리 최적화 테이블에 대한 `ALTER TABLE`이 이제 일반적으로 훨씬 빠릅니다.
    - 메모리 최적화 테이블의 트랜잭션 로그 다시 실행이 이제 병렬로 수행됩니다. 이는 복구 시간을 줄이고 AlwaysOn 가용성 그룹 구성의 지속적인 처리량을 크게 향상시킵니다.
    - 이제 메모리 최적화 파일 그룹 파일을 Azure Storage에 저장할 수 있습니다. Azure Storage의 메모리 최적화 파일 백업/복원 기능도 이제 사용할 수 있습니다.
- 클러스터형 Columnstore 인덱스가 LOB 열(nvarchar(max), varchar(max), varbinary(max))을 지원합니다.
- [STRING_AGG](../t-sql/functions/string-agg-transact-sql.md) 집계 함수가 추가되었습니다.  
- 새 권한: 이제 `DATABASE SCOPED CREDENTIAL` 은 보안 개체 클래스로서, `CONTROL`, `ALTER`, `REFERENCES`, `TAKE OWNERSHIP`, `VIEW DEFINITION` 권한을 지원합니다. SQL Database로 제한되는 `ADMINISTER DATABASE BULK OPERATIONS`가 이제 `sys.fn_builtin_permissions`에 표시됩니다.   
- [sys.dm_os_host_info](../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md) DMV가 추가되어 Windows 및 Linux 둘 다에 대한 운영 체제 정보를 제공합니다.   
- R Services로 데이터베이스 역할을 만들어 패키지와 관련된 권한을 관리합니다. 자세한 내용은 [SQL Server에 대한 R 패키지 관리](../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)를 참조하세요.


