---
title: "기능 &#39;의 새로운 SQL Server 2017 | Microsoft Docs"
ms.custom: 
ms.date: 05/23/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0b57f375-9242-4bb2-9d4b-c560d5a93524
caps.latest.revision: 71
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 1d363db8e8bd0e1460cdea3c3a7add68e48714c9
ms.openlocfilehash: 25d81efe1b915f0e4ddc5eab2feb4142ad2ceb8f
ms.contentlocale: ko-kr
ms.lasthandoff: 06/05/2017

---
# <a name="what39s-new-in-sql-server-2017"></a>기능 &#39;의 새로운 SQL Server 2017
SQL Server 2017 Linux, Linux 기반 Docker 컨테이너와 창에 SQL Server의 기능을 전환 하 여 개발 언어, 데이터 형식, 온-프레미스 및 클라우드 및 운영 체제에서 선택 사항을 제공 하는 플랫폼 때문에 SQL Server 하기 위한 주요 단계를 나타냅니다.

이 항목은 가장 최근의 커뮤니티 기술 미리 보기 (CTP) 릴리스 및 자세한 특정 기능 영역에 대 한 새로운 정보에 대 한 링크의 새로운 기능을 요약 합니다.

![info_tip](../sql-server/media/info-tip.png) Linux에서 SQL Server 실행! 참조 항목:
-  [SQL Server 2017 linux에 대 한 새로운 기능](https://docs.microsoft.com/sql/linux/sql-server-linux-whats-new)
-  [SQL Server on Linux Documentation](https://docs.microsoft.com/sql/linux/)


**사용해보기:**    
   -   [![평가 센터에서 다운로드](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477) ** [SQL Server 2017 Community Technology Preview 다운로드](http://go.microsoft.com/fwlink/?LinkID=829477)**

## <a name="whats-new-in-sql-server-2017-ctp-21-may-2017"></a>SQL Server 2017 CTP 2.1 (2017 년 5 월)의 새로운 기능
### <a name="sql-server-database-engine"></a>SQL Server 데이터베이스 엔진  
- 새 DMF [sys.dm_db_log_stats](../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md), 요약 수준 특성 및 트랜잭션 로그 파일에 대 한 정보를 노출 하는 도입 된 않으면 트랜잭션 로그의 상태를 모니터링 하는 데 유용 합니다.  
- 이 CTP에는 버그 수정 및 데이터베이스 엔진에 대 한 성능 향상 기능이 포함 되어 있습니다.
- 2017의 세부 목록을 참조 하는 이전 CTP 릴리스에서 향상 된 기능 CTP [SQL Server 2017 (데이터베이스 엔진)의 새로운](../database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md)합니다.

### <a name="sql-server-reporting-services-ssrs"></a>SSRS(SQL Server Reporting Services)
- SQL Server Reporting Services는 더 이상 CTP 2.1을 기준으로 SQL Server 설치 프로그램을 통해 설치할 수 없습니다.
- 주석은 보고서에 사용할 수 있습니다. 메모를 사용 하 여 보고서에 포함 된 내용에 큐브 뷰를 추가 하 고 다른 사용자와 조직에서 공동 작업을 수행할 수 있습니다. 또한 사용자 메모와 함께 첨부 파일을 포함할 수 있습니다.
- 이전 릴리스의 세부 정보를 포함하여 SSRS의 새로운 기능에 대한 자세한 내용은 [의 새로운 기능](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)을 참조하세요. 
- Power BI 보고서 서버에 대 한 정보를 참조 하십시오. [Power BI 보고서 서버와 함께 시작](https://powerbi.microsoft.com/documentation/reportserver-get-started/)합니다.

### <a name="sql-server-machine-learning-services"></a>SQL Server 컴퓨터 학습 서비스
- 이 CTP의 새로운 컴퓨터 학습 서비스 기능이 없는 있습니다.
- 자세한 시스템 학습 서비스의 이전 Ctp의 세부 정보를 포함 하 여 새 정보를 보게 [SQL Server 컴퓨터 학습 서비스의 새로운](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md)합니다.  

### <a name="sql-server-analysis-services-ssas"></a>SSAS(SQL Server Analysis Services)
- 이 CTP에는 새로운 SSAS 기능이 없습니다.  
- 향상 된 기능 및 버그 수정이 릴리스에 대 한 자세한 내용은 참조 하십시오. [SQL Server 2017 Analysis Services의 새로운](../analysis-services/what-s-new-in-sql-server-analysis-services-2017.md)합니다.  

### <a name="sql-server-integration-services-ssis"></a>SSIS(SQL Server Integration Services)
-   이제 사용할 수 있습니다는 **Use32BitRuntime** 매개 변수입니다.
-   로깅의 성능이 향상 되었습니다.
- 자세한 SSIS의 이전 Ctp의 세부 정보를 포함 하 여 새 정보를 보게 [SQL Server 2017 Integration Services의 새로운](../integration-services/what-s-new-in-integration-services-in-sql-server-2017.md)합니다.  

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="whats-new-in-sql-server-2017-ctp-20-april-2017"></a>SQL Server 2017 CTP 2.0 (2017 년 4 월)의 새로운 기능
### <a name="sql-server-database-engine"></a>SQL Server 데이터베이스 엔진
- **다시 시작 가능한 온라인 인덱스 다시 작성**합니다. 다시 시작 가능한 온라인 인덱스 다시 작성을 사용 하면 오류가 발생 한 후 중지 된 곳에서 온라인 인덱스 다시 작성 작업을 다시 시작할 수 있습니다. 예를 들어 장애 조치를 복제본 또는 충분 한 디스크 공간 상황입니다. 또한 일시 중지 수 있으며 그런 온라인 인덱스 다시 작성 작업을 다시 시작할 수 있습니다. 예를 들어 우선 순위가 높은 작업을 실행 하거나 사용 가능한 유지 관리 기간 대형 테이블 부족할 경우 다른 miniatous 창에 인덱스 다시 작성을 완료 하기 위해 시스템 리소스를 일시적으로 해제 해야 합니다. 마지막으로 다시 시작 가능한 온라인 인덱스 다시 작성은 상당한 로그 공간을 다시 시작 가능한 다시 작성 작업이 실행 되는 동안 로그 잘림을 수행 하 여 필요 하지 않습니다. 참조 [ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md) 및 [온라인 인덱스 작업에 대 한 지침이](../relational-databases/indexes/guidelines-for-online-index-operations.md)합니다.
- **ALTER DATABASE SCOPED CONFIGURATION IDENTITY_CACHE 옵션**합니다. 새로운 옵션 IDENTITY_CACHE ALTER 데이터베이스 범위 구성 T-SQL 문에 추가 되었습니다. 이 옵션을 OFF로 설정 하는 경우 서버 예기치 않게 다시 시작 되거나 서버에서 보조 서버로 장애 조치 경우 id 열의 값에 간격이 피할 수 있습니다. 참조 [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)합니다.  
- CLR 보안 경계로 더 이상 지원 되지 않는.NET Framework의 코드 액세스 보안 (CA)를 사용 합니다. 사용 하 여 만든 CLR 어셈블리 `PERMISSION_SET = SAFE` 외부 시스템 리소스에 액세스, 비관리 코드를 호출 및 시스템 관리자 권한을 얻을 수 있습니다. 부터는 [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)], `sp_configure` 이라는 옵션 `clr strict security` 는 CLR 어셈블리의 보안을 강화 하기 위해 도입 되었습니다. `clr strict security`기본적으로 사용 하며 처리 `SAFE` 및 `EXTERNAL_ACCESS` 어셈블리도 표시 된 것 처럼 경우 `UNSAFE`합니다. `clr strict security` 이전 버전과 호환성에 대 한 옵션을 사용할 수 있지만 권장 되지 않습니다. 인증서 또는 비대칭 키에 부여 된 해당 로그인으로 모든 어셈블리를 서명 하는 것이 좋습니다 `UNSAFE ASSEMBLY` master 데이터베이스에 대 한 사용 권한입니다. 자세한 내용은 참조 [CLR 엄격한 보안](../database-engine/configure-windows/clr-strict-security.md)합니다.  
- 그래프 모델 다 대 다 관계를 설정할 데이터베이스 기능입니다. 여기에 새로운 [CREATE TABLE](../t-sql/statements/create-table-sql-graph.md) 노드 및 가장자리 테이블과 키워드를 만들기 위한 구문을 [일치](../t-sql/queries/match-sql-graph.md) 쿼리에 대 한 합니다. 자세한 내용은 참조 [그래프 SQL Server 2017을 사용 하 여 처리](../relational-databases/graphs/sql-graph-overview.md)합니다.   
- 성능 문제 잠재적 쿼리에 대 한 정보를 제공 하는 데이터베이스 기능 자동 튜닝이, 솔루션을 권장할 수 있습니다 및 수정 프로그램 문제를 식별 하는 자동으로 합니다. 자동 조정 [!INCLUDE[ssnoversion](../includes/ssnoversion.md)], 잠재적인 성능 문제를 발견 하 고 수정 동작을 적용할 수 있습니다 때마다 공지 또는 수는 [!INCLUDE[ssde](../includes/ssde-md.md)] 자동으로 성능 문제를 해결 합니다. 자세한 내용은 참조 [자동 튜닝](../relational-databases/automatic-tuning/automatic-tuning.md)합니다.  
-    일괄 처리 모드 적응에 조인 (아래에서 데이터베이스 호환성 140) 계획의 품질을 개선 합니다.
-    데이터베이스 호환성 140) (아래 계획의 품질을 개선 하기 위해 다중 문 T-SQL Tvf에 대 한 인터리브 방식된으로 실행 합니다.
- 쿼리 저장소 이제 추적 대기 통계에 대 한 요약 정보입니다. 추적 쿼리 저장소에 대 한 쿼리당 대기 통계 범주는 다음 문제 해결 환경을, 더욱, 워크 로드 성능 및 쿼리 저장소 장점이 계속 사용 하면서 해당 병목 상태에 대 한 정보를 제공 하는 성능 수준의 수 있습니다.
- DTC 동일한 인스턴스에 포함 된 데이터베이스에 대 한 포함 하 여 가용성 그룹의 일부인 데이터베이스 간의 모든 데이터베이스 간 트랜잭션에 대 한 Always On 가용성 그룹에 대 한 지원. 자세한 내용은 참조 [트랜잭션-Always On 가용성 그룹 및 데이터베이스 미러링](../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)
- 새 열 **modified_extent_page_count** 에 도입 된 [sys.dm_db_file_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md) 데이터베이스의 각 데이터베이스 파일에 차등 변경 내용을 추적 하도록 합니다.
- [SELECT INTO](../t-sql/queries/select-into-clause-transact-sql.md) 이제 테이블을 사용 하 여 사용자의 기본 파일 그룹 이외의 파일 그룹으로 로드를 지원는 **ON** 키워드입니다.
- SQL Server 설치 프로그램에서는 초기 tempdb 파일 크기를 지정할 수 있으므로 최대 **256GB (262, 144 MB)** 파일 크기 보다 큰 값으로 설정 되 면 경고와 함께 파일당 **1GB** IFI을 해제 하 고 합니다.
- 새로운 동적 관리 뷰 (DMV) [sys.dm_tran_version_store_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-space-usage.md) 데이터베이스당 버전 저장소 사용량을 추적 하는 도입 되었습니다.
- 새로운 DMV [sys.dm_db_log_info](../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md) DBCC LOGINFO 비슷합니다 VLF 정보를 표시 하는 도입 되었습니다.
- DBCC CLONEDATABASE 데이터베이스 복제본에서 쿼리 저장소 런타임 통계 누락 되지 않도록 하기 위해 복제 하는 동안 런타임 통계를 플러시합니다. 이외에 DBCC CLONEDATABASE가 더 보기 좋게 꾸밀 지원 하 고 전체 텍스트 인덱스를 복제 합니다.
- 이제 시스템 버전 임시 테이블 모두 삭제 하 고 모두 업데이트를 지원합니다.
- 이 CTP에는 데이터베이스 엔진에 대한 버그 수정이 포함되어 있습니다.
- 2017의 세부 목록을 참조 하는 이전 CTP 릴리스에서 향상 된 기능 CTP [SQL Server 2017 (데이터베이스 엔진)의 새로운](../database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md)합니다.   

### <a name="sql-server-machine-learning-services"></a>SQL Server 컴퓨터 학습 서비스
- SQL Server R Services에는 CTP 2.0에서 Python 언어 지원이 반영 되도록 새 이름을 있습니다. 이제 SQL Server에서 Python 또는 R 스크립트를 실행할 SQL Server 컴퓨터 학습 Services (In-database)를 사용할 수 있습니다. 또는 배포 하 고 SQL Server를 요구 하지 않는 R 및 Python 모델을 사용 하려면 Microsoft 컴퓨터 학습 서버 (독립 실행형)를 설치 합니다. 
- 두 플랫폼 모두는 분산된 기계 학습, 및 Microsoft R (9.1.0 버전)의 최신 버전에 대 한 새 MicrosoftML 알고리즘이 있습니다.
- 자세한 내용은 참조 [기계 학습에 대 한 새로운](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md)합니다.

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="whats-new-in-sql-server-2017-ctp-14-march-2017"></a>SQL Server 2017 CTP 1.4의에서 새로운 기능 (2017 년 3 월)
### <a name="sql-server-database-engine"></a>SQL Server 데이터베이스 엔진
- 이 CTP에는 새로운 데이터베이스 엔진 기능이 없습니다.
- 이 CTP에는 데이터베이스 엔진에 대한 버그 수정이 포함되어 있습니다.
- 2017의 세부 목록을 참조 하는 이전 CTP 릴리스에서 향상 된 기능 CTP [SQL Server 2017 (데이터베이스 엔진)의 새로운](../database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md)합니다.

### <a name="sql-server-r-services"></a>SQL Server R Services
- 이 CTP에는 새로운 R Services 기능이 없습니다.
- 이전 CTP의 세부 정보를 포함하여 R Services의 새로운 기능에 대한 자세한 내용은 [SQL Server R Services의 새로운 기능](../advanced-analytics/r-services/what-s-new-in-sql-server-r-services.md)을 참조하세요.  

### <a name="sql-server-reporting-services-ssrs"></a>SSRS(SQL Server Reporting Services)
- 이 CTP에는 새로운 SSRS 기능이 없습니다.
- 이전 릴리스의 세부 정보를 포함하여 SSRS의 새로운 기능에 대한 자세한 내용은 [의 새로운 기능](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)을 참조하세요. 

### <a name="sql-server-analysis-services-ssas"></a>SSAS(SQL Server Analysis Services)
- 이 CTP에는 새로운 SSAS 기능이 없습니다.  
- SSDT 및 SSMS의 최신 미리 보기 릴리스에서 Analysis Services에 대 한 새로운 포함 한 정보를 참조 하세요. [What's New in Analysis Services 2017](../analysis-services/what-s-new-in-sql-server-analysis-services-2017.md)합니다.  

### <a name="sql-server-integration-services-ssis"></a>SSIS(SQL Server Integration Services)
- 이 CTP에는 새로운 SSIS 기능이 없습니다.
- 자세한 SSIS의 이전 Ctp의 세부 정보를 포함 하 여 새 정보를 보게 [What's New in Integration Services 2017](../integration-services/what-s-new-in-integration-services-in-sql-server-2017.md)합니다.  

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="whats-new-in-sql-server-2017-ctp-13-february-2017"></a>1.3 SQL Server 2017 CTP의 새로운 기능 (2017 년 2 월)
### <a name="sql-server-database-engine"></a>SQL Server 데이터베이스 엔진
- 간접 검사점 성능 개선 사항
- 클러스터 없는 가용성 그룹 지원이 추가되었습니다.
- 최소 복제본 커밋 가용성 그룹 설정이 추가되었습니다.
- 이제 가용성 그룹은 Windows-Linux 간에 원활하게 작동되므로 OS 간 마이그레이션 및 테스트가 가능합니다.
- 임시 테이블 보존 정책 지원 추가 합니다. 자세한 내용은 참조 [관리 기록 데이터의 보존 시스템 버전 임시 테이블에서](../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md#using-temporal-history-retention-policy-approach)합니다.
- 새로운 DMV SYS.DM_DB_STATS_HISTOGRAM
- 온라인 비클러스터형 columnstore 인덱스를 빌드 및 지원이 추가 다시 작성
- Linux 프로세스에 대한 정보를 반환하는&5;개의 새로운 동적 관리 뷰. 자세한 내용은 [Linux 프로세스 동적 관리 뷰](../relational-databases/system-dynamic-management-views/linux-process-dynamic-management-views-transact-sql.md)를 참조하세요.   
- [sys.dm_db_stats_histogram(TRANSACT-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) 이 통계 검사를 위해 추가되었습니다.

### <a name="sql-server-analysis-services-ssas-ctp-13"></a>SSAS(SQL Server Analysis Services)(CTP 1.3)
- 인코딩 힌트 - 대규모 메모리 내 테이블 형식 모델의 처리(데이터 새로 고침)를 최적화하는 데 사용하는 고급 기능입니다. 자세한 내용은 참고 [What's New in Analysis Services 2017](../analysis-services/what-s-new-in-sql-server-analysis-services-2017.md)합니다. 


![horizontal_bar](../sql-server/media/horizontal-bar.png)

##  <a name="infotipsql-servermediainfo-tippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) SQL Server 엔지니어링 팀에 문의 
- [Stack Overflow(태그 sql-server)](http://stackoverflow.com/questions/tagged/sql-server)
- [MSDN 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect - 버그 보고 및 기능 요청](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit - R에 대한 일반 토론](https://www.reddit.com/r/SQLServer/)

## <a name="see-also"></a>참고 항목    
- ![릴리스 정보](../analysis-services/instances/install-windows/media/ssrs-fyi-note.png) [SQL Server 2017 릴리스 정보](../sql-server/sql-server-2017-release-notes.md)합니다. 
- [버전에서 지원하는 기능](https://msdn.microsoft.com/library/cc645993.aspx)
- [설치 하드웨어 및 소프트웨어 요구 사항](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
- [SQL Server 설치 마법사](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)
- [업데이트를 처리 하는 SQL Server 설치](http://msdn.microsoft.com/library/6df72a78-6b36-4bc1-948e-04b4ebe46094)
 
 ![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)

