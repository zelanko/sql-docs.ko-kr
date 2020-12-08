---
title: 성능 센터
description: SQL Server 데이터베이스 엔진 및 Azure SQL Database의 성능에 대해 알아야 하는 정보를 찾습니다.
ms.custom: seo-dt-2019
ms.date: 12/11/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- Performance (SQL Server)
- Performance (SQL Database)
helpviewer_keywords:
- SQL Server, performance
- performance (SQL Server)
- database performance (SQL Server)
- SQL Database (Performance)
- performance (SQL Database)
- database performance (SQL Database)
ms.assetid: 301204b2-140d-4495-98ed-021a9b5025f5
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: a93a5ba8ecacf9080edba64b31d7760f6b359c48
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505137"
---
# <a name="performance-center-for-sql-server-database-engine-and-azure-sql-database"></a>SQL Server 데이터베이스 엔진 및 Azure SQL 데이터베이스에 대한 성능 센터
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  이 페이지에서는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 및 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]의 성능에 대해 필요한 정보를 찾는 데 도움이 되는 링크를 제공합니다.  
  
 **범례**  
  
 ![기능 가용성 아이콘을 설명하는 범례 스크린샷](../../relational-databases/performance/media/security-center-legend.PNG "security-center-legend")  
  
## <a name="configuration-options-for-performance"></a>성능에 대한 구성 옵션  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 수준의 다양한 구성 옵션을 통해 데이터베이스 엔진 성능에 영향을 줄 수 있는 기능을 제공합니다. [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]을 사용할 경우 Microsoft에서 전부는 아니지만 이러한 최적화를 대부분 자동으로 수행합니다.  
  
|||  
|-|-|  
|**디스크 구성 옵션**|:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [디스크 스트라이프 및 RAID](https://technet.microsoft.com/library/ms190764\(v=sql.105\).aspx)|  
|**데이터 및 로그 파일 구성 옵션**|:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [데이터와 로그 파일을 별개의 드라이브에 배치](../../relational-databases/policy-based-management/place-data-and-log-files-on-separate-drives.md)<br />:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [데이터 및 로그 파일의 기본 위치 보기 또는 변경&#40;SQL Server Management Studio&#41;](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md)|  
|**TempDB 구성 옵션**|:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [TempDB의 성능 향상](../databases/tempdb-database.md)<br />:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [데이터베이스 엔진 구성 - TempDB](../../database-engine/install-windows/install-sql-server.md)<br />:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [Azure VM에서 SSD를 사용하여 SQL Server TempDB 및 버퍼 풀 확장 저장](https://cloudblogs.microsoft.com/sqlserver/2014/09/25/using-ssds-in-azure-vms-to-store-sql-server-tempdb-and-buffer-pool-extensions/)<br />:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [Azure 가상 컴퓨터의 SQL Server용 임시 디스크에 대한 디스크 및 성능 모범 사례](/aspnet/core/performance/performance-best-practices)|  
|**서버 구성 옵션**|**프로세서 구성 옵션**<br /><br />:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [affinity mask 서버 구성 옵션](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)<br />:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [affinity Input-Output mask 서버 구성 옵션](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md)<br />:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [affinity64 mask 서버 구성 옵션](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md)<br />:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [affinity64 Input-Output mask 서버 구성 옵션](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md)<br />:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [max worker threads 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)<br /><br />**서버 구성 옵션**<br /><br />:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [서버 메모리 서버 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md)<br /><br />**인덱스 구성 옵션**<br /><br />:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [fill factor 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-fill-factor-server-configuration-option.md)<br /><br />**쿼리 구성 옵션**<br /><br />:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [쿼리당 최소 메모리 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-min-memory-per-query-server-configuration-option.md)<br />:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [query governor cost limit 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-query-governor-cost-limit-server-configuration-option.md)<br />:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [max degree of parallelism 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)<br />:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [cost threshold for parallelism 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-cost-threshold-for-parallelism-server-configuration-option.md)<br />:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [optimize for ad hoc workloads 서버 구성 옵션](../../database-engine/configure-windows/optimize-for-ad-hoc-workloads-server-configuration-option.md)<br /><br />**백업 구성 옵션**<br /><br />:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [backup compression default 서버 구성 옵션 보기 또는 구성](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)|  
|**데이터베이스 구성 최적화 옵션**|:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [데이터 압축](../../relational-databases/data-compression/data-compression.md)<br />:::image type="icon" source="../../relational-databases/performance/media/security-center-both.png"::: [데이터베이스의 호환성 수준 보기 또는 변경](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)<br />:::image type="icon" source="../../relational-databases/performance/media/security-center-both.png"::: [데이터베이스 범위 구성 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)|  
|**테이블 구성 최적화**|:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)|  
|**Azure 가상 머신의 데이터베이스 엔진 성능**|:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [빠른 검사 목록](/aspnet/core/performance/performance-best-practices)<br />:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [가상 머신 크기 및 스토리지 계정 고려 사항](/aspnet/core/performance/performance-best-practices)<br />:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [디스크 및 성능 고려 사항](/aspnet/core/performance/performance-best-practices)<br />:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [I/O 성능 고려 사항](/aspnet/core/performance/performance-best-practices)<br />:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [기능 관련 성능 고려 사항](/aspnet/core/performance/performance-best-practices)| 
|**Linux의 SQL Server에 대한 성능 모범 사례 및 구성 지침**|:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [SQL Server 구성](../../linux/sql-server-linux-performance-best-practices.md#sql-server-configuration)<br />:::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [Linux OS 구성](../../linux/sql-server-linux-performance-best-practices.md#linux-os-configuration)|

> [!IMPORTANT]
> 추가 고려 사항은 다음에서 제공됩니다.    
> -  [고성능 워크로드를 사용하는 SQL Server 2012 및 SQL Server 2014에 대한 권장 업데이트 및 구성 옵션](https://support.microsoft.com/help/2964518)
> -  [고성능 워크로드를 사용하는SQL Server 2017 및 2016에 대한 권장 업데이트 및 구성 옵션](https://support.microsoft.com/help/4465518)

## <a name="query-performance-options"></a>쿼리 성능 옵션  
  
|||  
|-|-|  
|:::image type="icon" source="../../relational-databases/performance/media/security-center-both.png"::: **[인덱스](../../relational-databases/indexes/indexes.md)**|[인덱스 다시 구성 및 다시 작성](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)<br />[인덱스의 채우기 비율 지정](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)<br />[병렬 인덱스 작업 구성](../../relational-databases/indexes/configure-parallel-index-operations.md)<br />[인덱스에 대한 SORT_IN_TEMPDB 옵션](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)<br />[전체 텍스트 인덱스 성능 향상](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)<br />[쿼리당 최소 메모리 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-min-memory-per-query-server-configuration-option.md)<br />[인덱스 생성 메모리 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md)|  
|:::image type="icon" source="../../relational-databases/performance/media/security-center-both.png"::: **[분할된 테이블 및 인덱스](../../relational-databases/partitions/partitioned-tables-and-indexes.md)**|[분할의 이점](../partitions/partitioned-tables-and-indexes.md)|  
|:::image type="icon" source="../../relational-databases/performance/media/security-center-both.png"::: **[조인](../../relational-databases/performance/joins.md)**|[조인 기본 사항](../../relational-databases/performance/joins.md#fundamentals)<br />[중첩 루프 조인](../../relational-databases/performance/joins.md#nested_loops)<br />[병합 조인](../../relational-databases/performance/joins.md#merge)<br />[HASH 조인](../../relational-databases/performance/joins.md#hash)|  
|:::image type="icon" source="../../relational-databases/performance/media/security-center-both.png"::: **[하위 쿼리](../../relational-databases/performance/subqueries.md)**|[하위 쿼리 기본 사항](../../relational-databases/performance/subqueries.md#fundamentals)<br />[상관 하위 쿼리](../../relational-databases/performance/subqueries.md#correlated)<br />[하위 쿼리 유형](../../relational-databases/performance/subqueries.md#types)|  
|:::image type="icon" source="../../relational-databases/performance/media/security-center-both.png"::: **[저장 프로시저](../stored-procedures/stored-procedures-database-engine.md)**|[CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md#best-practices)|  
|:::image type="icon" source="../../relational-databases/performance/media/security-center-both.png"::: **[사용자 정의 함수](../user-defined-functions/user-defined-functions.md)**|[CREATE FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md#best-practices)<br />[사용자 정의 함수 만들기&#40;데이터베이스 엔진&#41;](../user-defined-functions/create-user-defined-functions-database-engine.md)|  
|:::image type="icon" source="../../relational-databases/performance/media/security-center-both.png"::: **병렬 처리 최적화**|[max worker threads 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)<br />[데이터베이스 범위 구성 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)|  
|:::image type="icon" source="../../relational-databases/performance/media/security-center-both.png"::: **쿼리 최적화 프로그램 최적화**|[데이터베이스 범위 구성 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)<br />[USE HINT 쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md#use_hint)|  
|:::image type="icon" source="../../relational-databases/performance/media/security-center-both.png"::: **[통계](../../relational-databases/statistics/statistics.md)**|[통계 업데이트 시기](../statistics/statistics.md)<br />[통계 업데이트](../../relational-databases/statistics/update-statistics.md)|  
|:::image type="icon" source="../../relational-databases/performance/media/security-center-both.png"::: **[메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)**|[메모리 최적화 테이블](../in-memory-oltp/sample-database-for-in-memory-oltp.md)<br />[고유하게 컴파일된 저장 프로시저](../in-memory-oltp/a-guide-to-query-processing-for-memory-optimized-tables.md)<br />[고유하게 컴파일된 저장 프로시저의 TempDB에서 테이블 만들기 및 액세스](../../relational-databases/in-memory-oltp/create-and-access-tables-in-tempdb-from-stored-procedures.md)<br />[메모리 액세스에 최적화된 해시 인덱스의 일반적인 성능 문제 해결](/previous-versions/sql/sql-server-2016/dn589805(v=sql.130))<br />[데모: 메모리 내 OLTP의 성능 향상](../../relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp.md)|
|:::image type="icon" source="../../relational-databases/performance/media/security-center-both.png"::: **[인텔리전트 쿼리 처리](../../relational-databases/performance/intelligent-query-processing.md)**|[지능형 쿼리 처리](../../relational-databases/performance/intelligent-query-processing.md)|
  
## <a name="see-also"></a>참고 항목  
 [성능 모니터링 및 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [관련된 뷰, 함수 및 프로시저](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [단일 데이터베이스에 대한 Azure SQL 데이터베이스 성능 지침](/azure/azure-sql/database/performance-guidance)   
 [탄력적 풀을 사용하여 Azure SQL 데이터베이스 성능 최적화](/azure/azure-sql/database/elastic-pool-overview)   
 [Azure SQL Database에 대한 Query Performance Insight](/azure/azure-sql/database/query-performance-insight-use)  
 [인덱스 디자인 가이드](../../relational-databases/sql-server-index-design-guide.md)  
 [메모리 관리 아키텍처 가이드](../../relational-databases/memory-management-architecture-guide.md)  
 [페이지 및 익스텐트 아키텍처 가이드](../../relational-databases/pages-and-extents-architecture-guide.md)  
 [마이그레이션 후 유효성 검사 및 최적화 가이드](../../relational-databases/post-migration-validation-and-optimization-guide.md)  
 [쿼리 처리 아키텍처 가이드](../../relational-databases/query-processing-architecture-guide.md)  
 [SQL Server 트랜잭션 잠금 및 행 버전 관리 지침](../sql-server-transaction-locking-and-row-versioning-guide.md)  
 [SQL Server 트랜잭션 로그 아키텍처 및 관리 가이드](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)  
 [스레드 및 태스크 아키텍처 가이드](../../relational-databases/thread-and-task-architecture-guide.md) 
