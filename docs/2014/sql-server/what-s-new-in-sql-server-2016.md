---
title: 새로운&#39;SQL Server 2014의 새로운 | Microsoft Docs
ms.custom: ''
ms.date: 05/25/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- new features [SQL Server]
- SQL Server, what's new
- SQL Server 2008 what's new
- what's new [SQL Server]
- sql server 2014 sp1
- sql server 2014 sp2
ms.assetid: 6a428023-e3cc-4626-a88a-4c13ccbd7db0
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 26d0c84194f6f2aafb8bc499ff5404a1438ee577
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/07/2019
ms.locfileid: "57578843"
---
# <a name="what39s-new-in-sql-server-2014"></a>새로운&#39;SQL Server 2014의 새로운
  이 항목에서는 새로운 기능에 대 한 링크가 요약 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 하 고 서비스 팩에 대 한 요약 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 
**사용해보기:** ![Azure 가상 머신 소형](./media/what-s-new-in-sql-server-2016/azure-virtual-machine-small.png) Azure 계정이 있으세요?  이동 **[여기](https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2014sp1EnterpriseWindowsServer2012R2)** 이미 설치 된 SQL Server 2014 서비스 팩 1 (SP1)를 사용 하 여 가상 머신을 스핀업 하 합니다. 
  
-   [새로운 &#40;데이터베이스 엔진&#41;](../database-engine/whats-new-in-sql-server-2016.md)  
  
-   [Analysis Services 및 Business Intelligence의 새로운 기능](../analysis-services/what-s-new-in-analysis-services.md)  
  
-   [SQL Server 설치의 새로운 기능](install/what-s-new-in-sql-server-installation.md)  
  
 **[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 에 다음에 중요 한 새 기능이 도입 하지 않았습니다.**  
  
-   [새로운 &#40;Integration Services&#41;](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)  
  
-   [새로운 &#40;Reporting Services&#41;](../reporting-services/what-s-new-reporting-services.md)  
  
## <a name="includesssql14includessssql14-mdmd-service-pack-1-sp1"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP1(서비스 팩 1)
[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] (SP1)는 중요 한 새로운 기능을 제공 하지 않았습니다.
-  [SQL Server 2014 서비스 팩 1 릴리스 정보](https://support.microsoft.com/en-us/kb/3058865)합니다.
-  [![서비스 팩 1 다운로드 microsoft?? SQL Server?? 2014](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=46694) [microsoft Service Pack 1 다운로드?? SQL Server?? 2014](https://www.microsoft.com/en-us/download/details.aspx?id=46694).


## <a name="includesssql14includessssql14-mdmd-service-pack-2-sp2"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 서비스 팩 2 (SP2)
- [SQL Server 2014 서비스 팩 2 릴리스 정보](https://support.microsoft.com/en-us/kb/3171021)합니다.
-  [![서비스 팩 2 다운로드 microsoft?? SQL Server?? 2014](./media/what-s-new-in-sql-server-2016/download.png)](https://go.microsoft.com/fwlink/?LinkID=821558) [microsoft 서비스 팩 2 다운로드?? SQL Server?? 2014](https://go.microsoft.com/fwlink/?LinkID=821558).
-  [![SQL Server 2014 SP2 기능 팩 다운로드](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=53164) [SQL Server 2014 SP2 기능 팩 다운로드](https://www.microsoft.com/en-us/download/details.aspx?id=53164)합니다.

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] (SP2) 다음과 같은 개선 사항이 포함 됩니다.

### <a name="performance-and-scalability-improvements"></a>성능 및 확장성 향상 
-   **자동 소프트 NUMA 분할 합니다.** 사용 하 여 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2, 자동 소프트 NUMA 인스턴스를 시작 하는 동안 추적 플래그 8079를 켤 때 사용 됩니다. 추적 플래그 8079를 시작 하는 동안 때 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2는 하드웨어 레이아웃을 조사 하 고 자동으로 NUMA 노드당 8 개 이상의 Cpu를 보고 하는 시스템에 소프트 NUMA를 구성 합니다. 자동, 소프트 NUMA 동작은 하이퍼스레드 (h T/논리 프로세서)를 인식 합니다. 추가 노드를 분할하고 생성하면 수신기 수, 크기 조정 및 네트워크와 암호화 기능을 늘려서 후순위 처리를 조정합니다. 것이 좋습니다 첫 번째 테스트 자동 소프트 NUMA를 사용 하 여 성능 워크 로드를 프로덕션 환경에서 설정 하기 전에 합니다. [자세한 내용은 블로그를 참조 하세요.](https://blogs.msdn.microsoft.com/psssql/2016/03/30/sql-2016-it-just-runs-faster-automatic-soft-numa/)합니다. 
-  **동적 메모리 개체 크기 조정:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 개체 노드 및 최신 하드웨어의 크기를 조정 하는 코어의 수에 따라 메모리를 동적으로 분할 합니다. 동적 승격 목표 병목 현상이 발생 하는 경우 (CMEMTHREAD)는 스레드로부터 안전한 메모리 개체를 자동으로 분할 하는 것입니다. 노드 (파티션 equals 수가 NUMA 노드 수)로 분할 되어야으로 분할 되지 않은 메모리 개체를 동적으로 승격 될 수 있습니다. 및 메모리 노드별로 분할 된 개체에서 작업을 수행할 수 있습니다. 승격 (개수의 파티션 equals CPU 별로 분할할 수 Cpu)입니다. [자세한 내용은 블로그를 참조 하세요.](https://blogs.msdn.microsoft.com/psssql/2016/04/06/sql-2016-it-just-runs-faster-dynamic-memory-object-cmemthread-partitioning/)합니다.
-  **DBCC CHECK에 대 한 MAXDOP 힌트\* 명령:** 이러한 향상 된이 기능을 해결 [connect 피드백 (468694)](https://connect.microsoft.com/SQLServer/feedback/details/468694/maxdop-option-in-dbcc-checkdb)합니다. 이제 사용 하 여 DBCC CHECKDB를 실행할 수 있습니다는 sp_configure 값이 아닌 MAXDOP 설정 합니다. MAXDOP가 Resource Governor로 구성한 값을 초과하면, 데이터베이스 엔진에서 ALTER WORKLOAD GROUP(Transact-SQL)에서 설명한 Resource Governor MAXDOP 값을 사용합니다. max degree of parallelism 구성 옵션에 사용된 모든 의미 체계 규칙을 MAXDOP 쿼리 힌트 사용 시 적용할 수 있습니다. 자세한 내용은 [DBCC CHECKDB (TRANSACT-SQL)](https://msdn.microsoft.com/library/ms176064.aspx)합니다.
-   **설정 > 버퍼 풀에 대 한 8TB:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2에는 버퍼 풀 사용량에 대 한 가상 주소 공간의 128 TB 수 있습니다. 이러한 향상 된이 기능에는 SQL Server 버퍼 풀을 최신 하드웨어에서 8TB 이상으로 확장할 수 있습니다.
-   **SOS_RWLock 스핀 잠금 개선:** SOS_RWLock는 SQL Server 코드 베이스 전체에서 다양 한 위치에서 사용 하는 동기화 기본 형식입니다.  이름에서 알 수 있듯이 여러 공유 (판독기) 또는 단일 (기록기) 소유권 코드가 있을 수 있습니다. SOS_RWLock 스핀 잠금에 대 한 필요를 제거 하 고 대신 메모리 내 OLTP와 유사한 잠금 없는 기술을 사용 하 여 하는 이러한 향상 된이 기능. 이 변경으로 많은 스레드가 서로 차단 하 고 따라서 향상 된 확장성을 제공 하지 않고 병렬로 SOS_RWLock 하 여 보호 된 데이터 구조를 읽을 수 있습니다. 이 변경 전에 spinlock 구현에는 SOS_RWLock 읽기 데이터 구조에도 한 번에 가져오려고 스레드가 하나만 사용할 수 있습니다.  [자세한 내용은 블로그를 참조 하세요.](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/)합니다.
-    **공간 네이티브 구현 합니다.** 도입 된 공간 쿼리 성능이 크게 향상 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 네이티브 구현을 통해 SP2. 자세한 내용은 참조는 [기술 자료 문서 KB3107399](https://support.microsoft.com/en-us/kb/3107399)합니다.

### <a name="supportability-and-diagnostics-improvements"></a>지원 가능성 및 진단 기능 개선
-   **데이터베이스 복제:** 복제 데이터베이스에 기존 프로덕션 데이터베이스 스키마 및 데이터 없이 메타 데이터를 복제 하 여 문제 해결 향상 시키는 새 DBCC 명령입니다. 명령을 사용 하 여 복제본 만들어집니다 `DBCC clonedatabase('source_database_name', 'clone_database_name')`합니다.  **참고:** 복제된 데이터베이스는 프로덕션 환경에서 사용할 수 없습니다. 다음 복제 된 데이터베이스에서 데이터베이스를이 생성 되었는지 확인 명령을 사용 하 여: `select DATABASEPROPERTYEX('clonedb', 'isClone')`합니다. 반환 값 **1** 데이터베이스에서 clonedatabase 하는 동안 만들어지는지 나타냅니다 **0** 복제본 아님을 나타냅니다.
-   **Tempdb 지원 가능성:**  Tempdb 파일 수 및 서버 시작 시 있는 tempdb 데이터 파일의 크기/자동 증가 나타내는 새 errorlog 메시지입니다.
-   **데이터베이스 즉시 파일 초기화 로깅:** 새 errorlog 메시지를 서버 statup, 데이터베이스 인스턴트 파일 초기화 (사용/사용 안 함)의 상태를 나타냅니다.
-   **호출 스택에서 모듈 이름:** Xevent 호출 스택의 모듈 이름 + 오프셋 절대 주소 대신에 이제 포함 됩니다.
-   **증분 통계에 대 한 새 DMF:** 이러한 향상 된이 기능을 해결 [connect 피드백 (797156)](https://connect.microsoft.com/SQLServer/feedback/details/797156/display-sys-dm-db-stats-properties-per-partition-for-incremental-statistics) 파티션 수준에서 증분 통계를 추적을 사용 하도록 설정 합니다. 새 DMF sys.dm_db_incremental_stats_properties는 파티션당 정보에 대 한 증분 통계를 노출 하기 위해 도입 되었습니다.
-   **인덱스 사용 DMV 동작을 업데이트 합니다.** 이러한 향상 된이 기능을 해결 [connect 피드백 (739566)](https://connect.microsoft.com/SQLServer/feedback/details/739566/rebuilding-an-index-clears-stats-from-sys-dm-db-index-usage-stats) 위치는 인덱스를 다시 작성 하는 고객 으로부터 *하지* 해당 인덱스에 대 한 sys.dm_db_index_usage_stats에서 기존 행 항목의 선택을 취소 합니다. 동작을 동일 하 게 SQL 2008 및 SQL Server 2016 됩니다. [자세한 내용은 블로그를 참조 하세요.](https://blogs.msdn.microsoft.com/sql_server_team/index-usage-dmv-behavior-updated/)합니다.
-   **진단 XE와 Dmv 간의 향상 된 상관 관계:** 이러한 향상 된이 기능을 해결 [connect 피드백 (1934583)](https://connect.microsoft.com/SQLServer/feedback/details/1934583/extended-events-query-hash-and-query-plan-hash-data-types)합니다. Query_hash와 query_plan_hash는 쿼리를 고유 하 게 식별 하는 데 사용 됩니다. DMV에서는 이를 varbinary(8)으로 정의하는 반면 XEvent에서는 UINT64로 정의합니다. SQL server "unisigned bigint" 없으므로 캐스팅이 항상 작동 하지 않습니다. 이러한 향상 기능은 query_hash와 query_plan_hash에 해당하는 새 XEvent 작업/필터 열을 소개합니다. 단, XE와 DMV 간에 쿼리의 상관 관계를 지정할 수 있는 INT64로 정의된 경우는 제외합니다.
-   **BULK INSERT 및 BCP에서 u t F-8에 대 한 지원:** 이러한 향상 된이 기능을 해결 [connect 피드백 (370419)](https://connect.microsoft.com/SQLServer/feedback/details/370419/bulk-insert-and-bcp-does-not-recognize-codepage-65001) 내보내기 및 u t F-8 문자 집합으로 인코딩된 데이터의 가져오기에 대 한 지원을 BULK INSERT 및 BCP에서 이제는 합니다.
-   **연산자 당 간단한 쿼리 실행 프로 파일링 합니다.** Showplan 계획에서 연산자의 비용 확인 하 고 쿼리 실행 계획에서 많은 정보를 제공 하지만 실제 방법은 제한적 이지만 쿼리 성능, 문제를 해결 하는 동안 런타임 통계 (CPU, I/O 읽기, 스레드별 경과 된 시간)를 선호 합니다. SQL 2014 SP2에서 실행 계획 뿐만 아니라 XEvent (query_thread_profile)를 지원 쿼리 성능 문제를 해결 하기 위해 연산자 당 이러한 추가 런타임 통계를 소개 합니다. [자세한 내용은 블로그를 참조 하세요.](https://blogs.msdn.microsoft.com/sql_server_team/added-per-operator-level-performance-stats-for-query-processing/)합니다.
-   **변경 내용 추적 정리:** 새 저장 프로시저인 `sp_flush_CT_internal_table_on_demand` 정리에서 변경 내용 추적 내부 테이블 요청 하기 위해 도입 되었습니다.
-   **AlwaysON 임대 시간 제한 로깅** 현재 시간 및 예상된 된 갱신 시간이 기록 되도록 임대 시간 제한 메시지에 대 한 새 로깅 기능을 추가 합니다. 또한 새 메시지의 시간 제한에 대 한 SQL Errorlog에 도입 되었습니다. [자세한 내용은 블로그를 참조 하세요.](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/)합니다.
-   **SQL Server에서 입력된 버퍼를 검색 하기 위한 새 DMF:** 이제 세션/요청(sys.dm_exec_input_buffer)에 대한 입력 버퍼를 검색하기 위한 새 DMF를 사용할 수 있습니다. 이는 DBCC INPUTBUFFER와 기능적으로 동일합니다. [자세한 내용은 블로그를 참조 하세요.](https://blogs.msdn.microsoft.com/sql_server_team/new-dmf-for-retrieving-input-buffer-in-sql-server/)합니다.
-   **과소 평가 하 고 overestimated 메모리 부여에 대 한 완화 합니다.** 추가 된 새 쿼리 힌트 MIN_GRANT_PERCENT 및 MAX_GRANT_PERCENT를 통해 리소스 관리자에 대 한 합니다. 이 옵션을 사용 하면 메모리 경합을 방지 하도록 해당 메모리 부여를 제한 하 여 쿼리를 실행 하는 동안 이러한 힌트를 활용할 수 있습니다. 자세한 내용은 참조 하세요. [KB310740 기술 자료 문서](https://support.microsoft.com/en-us/kb/3107401)
-   **메모리 부여/사용량 진단 향상:** 새 확장된 이벤트를 요청 하 고 부여 메모리 부여를 추적 하려면 SQL Server (query_memory_grant_usage)에서 추적 기능 목록에 추가 되었습니다. 이 메모리 부여와 관련 된 쿼리 실행 문제 해결을 위한 더 나은 추적 및 분석 기능을 제공 합니다. 자세한 내용은 [기술 자료 문서 KB3107173](https://support.microsoft.com/en-us/kb/3107173)합니다.
-   **쿼리 실행 진단 tempdb 분산에 대 한:**-물리적 I/O 통계, 사용 되는 메모리 및 영향을 받는 행을 추적 하는 추가 열이 이제 Hash Warning 및 Sort Warning입니다. 또한 새 hash_spill_details 확장된 이벤트가 도입 되었습니다. 이제 프로그램 해시 및 정렬 경고에 대 한 더 세부적인 정보를 추적할 수 있습니다 ([KB3107172](https://support.microsoft.com/en-us/kb/3107172)). 이러한 향상 기능은 이제 또한 SpillToTempDbType 복합 형식에 새 특성의 형태로 XML 쿼리 계획을 통해 표시 됩니다 ([KB3107400](https://support.microsoft.com/en-us/kb/3107400)). 이제 표시 정렬 작업 테이블 통계의 통계를 설정 합니다. 의 동일한 원격 인스턴스에 있는 경우 master 데이터베이스는 여러 보조 데이터베이스를 사용할 수 있습니다.
-   **잔여 조건자 푸시 다운을 포함 하는 쿼리 실행 계획에 대 한 향상 된 진단:** 읽은 실제 행 이제 쿼리 성능 문제 해결을 개선 하기 위해 쿼리 실행 계획에서 보고 됩니다. SET STATISTICS IO를 별도로 캡처 필요가 없어질 해야이. 이 구문은 이제를 사용 하면 잔여 조건자 푸시 다운 쿼리 계획에 관련 된 정보를 볼 수 있습니다. 자세한 내용은 [기술 자료 문서 KB3107397](https://support.microsoft.com/en-us/kb/3107397)합니다.


## <a name="additional-information"></a>추가 정보  
 [SQL Server 2014 리소스](../2014-toc/books-online-for-sql-server-2014.md)  
  
 [SQL Server 2014 Release Notes](https://go.microsoft.com/fwlink/p/?linkID=296445)  
  
 [SQL Server 2014 Resource Center](https://msdn.microsoft.com/sqlserver/dn135309)  
  
 [SQLCat Web Site](https://go.microsoft.com/fwlink/p/?linkID=220963)  
  
  
