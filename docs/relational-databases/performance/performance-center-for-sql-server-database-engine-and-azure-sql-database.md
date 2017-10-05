---
title: "SQL Server 데이터베이스 엔진 및 Azure SQL Database에 대한 성능 센터 | Microsoft 문서"
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 04/08/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.service: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 14
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 6490c2356c0753f68e7ef5261ede3d699a08b863
ms.contentlocale: ko-kr
ms.lasthandoff: 09/27/2017

---
# <a name="performance-center-for-sql-server-database-engine-and-azure-sql-database"></a>SQL Server 데이터베이스 엔진 및 Azure SQL 데이터베이스에 대한 성능 센터
  이 페이지에서는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 및 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]의 성능에 대해 필요한 정보를 찾는 데 도움이 되는 링크를 제공합니다.  
  
 **범례**  
  
 ![security-center-legend](../../relational-databases/performance/media/security-center-legend.PNG "security-center-legend")  
  
## <a name="this-is-a-work-in-process-does-this-performance-center-help-you-how-can-we-improve-it"></a>진행 중인 작업입니다. 이 성능 센터가 도움이 되나요? 어떻게 하면 개선할 수 있을까요?  
 어떤 정보를 찾고 계세요? 정보를 찾으셨나요? 어떤 정보가 누락되었나요? 여기에 어떤 정보가 표시되기를 원하세요? 여러분의 의견은 문서의 내용을 개선하는 데 많은 도움이 됩니다. 의견이 있으면 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Temporal%20Tables%20page)  
  
## <a name="configuration-options-for-performance"></a>성능에 대한 구성 옵션  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 수준의 다양한 구성 옵션을 통해 데이터베이스 엔진 성능에 영향을 줄 수 있는 기능을 제공합니다. [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]을 사용할 경우 Microsoft에서 전부는 아니지만 이러한 최적화를 대부분 자동으로 수행합니다.  
  
|||  
|-|-|  
|**디스크 구성 옵션**|-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [디스크 스트라이프 및 RAID](https://technet.microsoft.com/library/ms190764\(v=sql.105\).aspx)|  
|**데이터 및 로그 파일 구성 옵션**|-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [데이터와 로그 파일을 별개의 드라이브에 배치](../../relational-databases/policy-based-management/place-data-and-log-files-on-separate-drives.md)<br />-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [데이터 및 로그 파일의 기본 위치 보기 또는 변경&#40;SQL Server Management Studio&#41;](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md)|  
|**TempDB 구성 옵션**|-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [TempDB의 성능 향상](https://msdn.microsoft.com/library/ms190768.aspx#Anchor_1)<br />-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [데이터베이스 엔진 구성 - TempDB](http://msdn.microsoft.com/library/7aabd304-f3c9-4c2d-bf9d-5479ee2498da)<br />-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [Using SSDs in Azure VMs to store SQL Server TempDB and Buffer Pool Extensions](http://blogs.technet.com/b/dataplatforminsider/archive/2014/09/25/using-ssds-in-azure-vms-to-store-sql-server-tempdb-and-buffer-pool-extensions.aspx)(Azure VM에서 SSD를 사용하여 SQL Server TempDB 및 버퍼 풀 확장 저장)<br />-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [Azure Virtual Machines의 SQL Server용 임시 디스크에 대한 디스크 및 성능 모범 사례](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-performance-best-practices/)|  
|![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") **서버 구성 옵션**|<ul><li>**프로세서 구성 옵션**<br /><br /> <ul><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [affinity mask 서버 구성 옵션](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)</li><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [affinity Input-Output mask 서버 구성 옵션](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md)</li><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [affinity64 mask 서버 구성 옵션](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md)</li><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [affinity64 Input-Output mask 서버 구성 옵션](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md)</li><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [max worker threads 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)</li></ul></li><li>**서버 구성 옵션**<br /><br /> <ul><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [서버 메모리 서버 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md)</li></ul></li><li>**인덱스 구성 옵션**<br /><br /> <ul><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [fill factor 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-fill-factor-server-configuration-option.md)</li><li></li></ul></li><li>**쿼리 구성 옵션**<br /><br /> <ul><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [min memory per query 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-min-memory-per-query-server-configuration-option.md)</li><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [query governor cost limit 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-query-governor-cost-limit-server-configuration-option.md)</li><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [max degree of parallelism 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)</li><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [cost threshold for parallelism 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-cost-threshold-for-parallelism-server-configuration-option.md)</li><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [optimize for ad hoc workloads 서버 구성 옵션](../../database-engine/configure-windows/optimize-for-ad-hoc-workloads-server-configuration-option.md)</li></ul></li><li>**백업 구성 옵션**<br /><br /> <ul><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [backup compression default 서버 구성 옵션 보기 또는 구성](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)</li></ul></li></ul>|  
|**데이터베이스 구성 최적화 옵션**|-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [데이터 압축](../../relational-databases/data-compression/data-compression.md)<br />-   ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") [데이터베이스의 호환성 수준 보기 또는 변경](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)<br />-   ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") [ALTER DATABASE SCOPED CONFIGURATION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)|  
|**테이블 구성 최적화**|-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [분할된 테이블 및 인덱스](../../relational-databases/partitions/partitioned-tables-and-indexes.md)<br />-|  
|**Azure 가상 컴퓨터의 데이터베이스 엔진 성능**|-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [빠른 검사 목록](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-performance-best-practices/)<br />-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [가상 컴퓨터 크기 및 저장소 계정 고려 사항](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-sql-server-performance-best-practices/)<br />-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [디스크 및 성능 고려 사항](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-performance-best-practices/)<br />-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [I/O 성능 고려 사항](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-sql-server-performance-best-practices/)<br />-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [기능 관련 성능 고려 사항](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-performance-best-practices/)|  
  
## <a name="query-performance-options"></a>쿼리 성능 옵션  
  
|||  
|-|-|  
|![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both")  **[인덱스](../../relational-databases/indexes/indexes.md)**|-   [인덱스 다시 구성 및 다시 작성](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)<br />-   [인덱스의 채우기 비율 지정](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)<br />-   [병렬 인덱스 작업 구성](../../relational-databases/indexes/configure-parallel-index-operations.md)<br />-   [인덱스에 대한 SORT_IN_TEMPDB 옵션](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)<br />-   [전체 텍스트 인덱스 성능 향상](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)|  
|![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both")  **[분할된 테이블 및 인덱스](../../relational-databases/partitions/partitioned-tables-and-indexes.md)**|-   [분할의 이점](https://msdn.microsoft.com/library/ms190787.aspx#Anchor_0)|  
|![security-center-both](../stored-procedures/stored-procedures-database-engine.md)|  
|![security-center-both](../user-defined-functions/user-defined-functions.md)|  
|![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") **병렬 처리 최적화**|-   [max worker threads 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)<br />-   [ALTER DATABASE SCOPED CONFIGURATION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)|  
|![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") **쿼리 최적화 프로그램 최적화**|-   [ALTER DATABASE SCOPED CONFIGURATION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)|  
|![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both")  **[통계](../../relational-databases/statistics/statistics.md)**|-   [통계 업데이트 시기](https://msdn.microsoft.com/library/ms190397.aspx#Anchor_3)<br />-   [통계 업데이트](../../relational-databases/statistics/update-statistics.md)|  
|![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both")  **[메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)**|-   [메모리 액세스에 최적화된 테이블](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)<br />-   [고유하게 컴파일된 저장 프로시저](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)<br />-   [고유하게 컴파일된 저장 프로시저의 TempDB에서 테이블 만들기 및 액세스](../../relational-databases/in-memory-oltp/create-and-access-tables-in-tempdb-from-stored-procedures.md)<br />-   [메모리 액세스에 최적화된 해시 인덱스의 일반적인 성능 문제 해결](http://msdn.microsoft.com/library/1954a997-7585-4713-81fd-76d429b8d095)<br />-   [데모: 메모리 내 OLTP 성능 향상](../../relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp.md)|  
  
## <a name="see-also"></a>참고 항목  
 [성능 모니터링 및 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [쿼리 저장소를 사용하여 성능 모니터링](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [단일 데이터베이스에 대한 Azure SQL 데이터베이스 성능 지침](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)   
 [탄력적 풀을 사용하여 Azure SQL 데이터베이스 성능 최적화](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-guidance/)   
 [Azure Query Performance Insight](https://azure.microsoft.com/documentation/articles/sql-database-query-performance/)  
  
  

