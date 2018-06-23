---
title: 어떤&#39;SQL Server 2014의 새로운 s | Microsoft Docs
ms.custom: ''
ms.date: 05/25/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- database-engine
- integration-services
- master-data-services
- replication
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- new features [SQL Server]
- SQL Server, what's new
- SQL Server 2008 what's new
- what's new [SQL Server]
- sql server 2014 sp1
- sql server 2014 sp2
ms.assetid: 6a428023-e3cc-4626-a88a-4c13ccbd7db0
caps.latest.revision: 70
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9144eeb653649e36cfed3551e4ec465d403ffdcb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088307"
---
# <a name="what39s-new-in-sql-server-2014"></a>어떤&#39;의 새로운 SQL Server 2014
  이 항목에서는의 새로운 기능에 대 한 자세한 링크 요약 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 하 고 서비스 팩에 대 한 요약 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 
**사용해 보기:** ![Azure 가상 컴퓨터 작은](./media/what-s-new-in-sql-server-2016/azure-virtual-machine-small.png) Azure 계정이 있으세요?  이동 하 여 **[여기](https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2014sp1EnterpriseWindowsServer2012R2)** 를 이미 설치 된 SQL Server 2014 서비스 팩 1 (SP1)로 가상 컴퓨터를 스핀 합니다. 
  
-   [새로운 &#40;데이터베이스 엔진&#41;](../database-engine/whats-new-in-sql-server-2016.md)  
  
-   [Analysis Services 및 Business Intelligence의 새로운 기능](../analysis-services/what-s-new-in-analysis-services.md)  
  
-   [SQL Server 설치의 새로운 기능](install/what-s-new-in-sql-server-installation.md)  
  
 **[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 에 다음과 같은 중요 한 새 기능이 도입 하지 않았습니다.**  
  
-   [새로운 &#40;Integration Services&#41;](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)  
  
-   [새로운 &#40;복제&#41;](../relational-databases/replication/what-s-new-replication.md)  
  
-   [새로운 &#40;Reporting Services&#41;](../reporting-services/what-s-new-reporting-services.md)  
  
## <a name="includesssql14includessssql14-mdmd-service-pack-1-sp1"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP1(서비스 팩 1)
[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] (SP1) 중요 한 새로운 기능을 제공 하지 않았습니다.
-  [SQL Server 2014 서비스 팩 1 릴리스 정보 ](https://support.microsoft.com/en-us/kb/3058865)합니다.
-  [![Microsoft® SQL Server® 2014 서비스 팩 1 다운로드](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=46694) [Microsoft® SQL Server® 2014 서비스 팩 1 다운로드](https://www.microsoft.com/en-us/download/details.aspx?id=46694)합니다.


## <a name="includesssql14includessssql14-mdmd-service-pack-2-sp2"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 서비스 팩 2 (SP2)
- [SQL Server 2014 서비스 팩 2 릴리스 정보](https://support.microsoft.com/en-us/kb/3171021)합니다.
-  [![Microsoft® SQL Server® 2014 서비스 팩 2 다운로드](./media/what-s-new-in-sql-server-2016/download.png)](http://go.microsoft.com/fwlink/?LinkID=821558) [Microsoft® SQL Server® 2014 서비스 팩 2 다운로드](http://go.microsoft.com/fwlink/?LinkID=821558)합니다.
-  [![SQL Server 2014 SP2 기능 팩 다운로드](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=53164) [SQL Server 2014 SP2 기능 팩 다운로드](https://www.microsoft.com/en-us/download/details.aspx?id=53164)합니다.

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] (SP2) 다음과 같은 개선 사항이 포함 되어 있습니다.

### <a name="performance-and-scalability-improvements"></a>성능 및 확장성 향상 
-   **자동 SOFT-NUMA 분할:** 와 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2, 소프트 NUMA 자동 인스턴스를 시작 하는 동안 추적 플래그 8079 켜져 있을 때 사용 합니다. 시작 하는 동안 사용 하는 추적 플래그 8079 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] s p 2는 하드웨어 레이아웃을 조사 하 고 자동으로 시스템 보고 NUMA 노드당 8 개 이상의 Cpu에 소프트 NUMA를 구성 합니다. 자동, 소프트 NUMA 동작은 하이퍼스레드 (HT/논리 프로세서)를 인식 합니다. 추가 노드를 분할하고 생성하면 수신기 수, 크기 조정 및 네트워크와 암호화 기능을 늘려서 후순위 처리를 조정합니다. 좋습니다 첫 번째 테스트를 자동 소프트 NUMA를 사용 하 여 성능 작업 프로덕션 환경에서 설정 하기 전에. [자세한 내용은 블로그를 참조 하십시오.](https://blogs.msdn.microsoft.com/psssql/2016/03/30/sql-2016-it-just-runs-faster-automatic-soft-numa/)합니다. 
-  **동적 메모리 개체 크기 조정:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] s p 2의 노드 및 최신 하드웨어 크기를 조정 하는 코어 수에 따라 메모리 개체를 동적으로 분할 합니다. 동적 프로 모션의 목표 병목 현상이 발생 하는 경우 (CMEMTHREAD) 스레드로부터 안전한 메모리 개체를 자동으로 분할 하는 것입니다. 분할 되지 않은 메모리 개체 노드 (파티션 equals 수가 NUMA 노드 수)으로 분할할 수를 동적으로 승격 될 수 있습니다 및 메모리 노드로 분할 된 개체 수에서 추가 CPU (파티션 equals 수가 수에 의해 분할로 승격 Cpu)입니다. [자세한 내용은 블로그를 참조 하십시오.](https://blogs.msdn.microsoft.com/psssql/2016/04/06/sql-2016-it-just-runs-faster-dynamic-memory-object-cmemthread-partitioning/)합니다.
-  **DBCC CHECK를 위해 MAXDOP 힌트\* 명령을:** 이 개선 사항을 해결 [connect 피드백 (468694)](https://connect.microsoft.com/SQLServer/feedback/details/468694/maxdop-option-in-dbcc-checkdb)합니다. 이제과 함께 DBCC CHECKDB를 실행할 수 있습니다는 sp_configure 값이 아닌 MAXDOP 설정 합니다. MAXDOP가 Resource Governor로 구성한 값을 초과하면, 데이터베이스 엔진에서 ALTER WORKLOAD GROUP(Transact-SQL)에서 설명한 Resource Governor MAXDOP 값을 사용합니다. max degree of parallelism 구성 옵션에 사용된 모든 의미 체계 규칙을 MAXDOP 쿼리 힌트 사용 시 적용할 수 있습니다. 자세한 내용은 참조 [DBCC CHECKDB (TRANSACT-SQL)](https://msdn.microsoft.com/library/ms176064.aspx)합니다.
-   **사용 하도록 설정 > 버퍼 풀에 대 한 8TB:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 버퍼 풀 사용량에 대 한 가상 주소 공간의 128 TB를 사용 하도록 설정 합니다. 이러한 향상에 SQL Server 버퍼 풀에 최신 하드웨어 8TB 이상 확장할 수 있습니다.
-   **SOS_RWLock spinlock 개선:** The SOS_RWLock은 전체 SQL Server 코드 베이스에서 다양 한 위치에서 사용 되는 동기화 기본 형식입니다.  이름에서 알 수 있듯이 여러 공유 (판독기) 또는 단일 (기록기) 소유권 코드가 있을 수 있습니다. 이 개선 SOS_RWLock spinlock에 대 한 필요 하지 않으며 대신 메모리 내 OLTP와 유사한 잠금 없는 기술을 사용 하 여 이러한 변경으로 인해 많은 스레드가 서로 차단 하 고 향상 된 확장성을 제공 하지 않고 병렬로 SOS_RWLock에 의해 보호 되는 데이터 구조를 읽을 수 있습니다. 이 변경 전에 spinlock 구현에는 SOS_RWLock 읽을 데이터 구조에도 한 번에 얻으려고 스레드를 하나만 사용할 수 있습니다.  [자세한 내용은 블로그를 참조 하십시오.](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/)합니다.
-    **공간 네이티브 구현:** 에 도입 된 공간 쿼리 성능이 크게 향상 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 네이티브 구현을 통해 SP2. 자세한 내용은 참조는 [기술 자료 문서 KB3107399](https://support.microsoft.com/en-us/kb/3107399)합니다.

### <a name="supportability-and-diagnostics-improvements"></a>지원 가능성 및 진단 기능 개선
-   **데이터베이스 복제:** 클론 데이터베이스 스키마와 데이터 없이 메타 데이터를 복제 하 여 기존 프로덕션 데이터베이스 문제 해결을 개선 하는 새 DBCC 명령입니다. 복제본이 명령으로 만든 `DBCC clonedatabase(‘source_database_name’, ‘clone_database_name’)`합니다.  **참고:** Cloned 데이터베이스 프로덕션 환경에서는 사용할 수 없습니다. 다음 복제 된 데이터베이스에서 데이터베이스를 생성 하는 경우 확인 명령을 사용 하 여: `select DATABASEPROPERTYEX('clonedb', 'isClone')`합니다. 반환 값 **1** 동안 clonedatabase에서 데이터베이스를 만든 나타냅니다 **0** 은 복제본을 의미 합니다.
-   **Tempdb 지원 가능성:** 서버 시작 시 tempdb 파일 수 및 tempdb 데이터의 크기/자동 증가 나타내는 새 오류 로그 메시지 파일이 존재 합니다.
-   **데이터베이스 인스턴트 파일 초기화 로깅:** statup 서버, 데이터베이스 즉시 파일 초기화 (사용/사용 안 함)의 상태를 나타내는 새 오류 로그 메시지입니다.
-   **호출 스택의 모듈 이름:** 모듈 이름 + 절대 주소가 아닌 오프셋 The Xevent 호출 스택 포함 됩니다.
-   **증분 통계에 대 한 새 DMF:** 이 개선 사항을 해결 [connect 피드백 (797156)](https://connect.microsoft.com/SQLServer/feedback/details/797156/display-sys-dm-db-stats-properties-per-partition-for-incremental-statistics) 증분 통계 파티션 수준에서 추적 기능을 합니다. 정보 파티션 증분 통계를 노출 하는 새 DMF sys.dm_db_incremental_stats_properties 도입 되었습니다.
-   **인덱스 사용 DMV 동작 업데이트:** 이 개선 사항을 해결 [connect 피드백 (739566)](https://connect.microsoft.com/SQLServer/feedback/details/739566/rebuilding-an-index-clears-stats-from-sys-dm-db-index-usage-stats) 위치는 인덱스를 다시 고객 으로부터 *하지* sys.dm_db에서 모든 기존 행 항목을 지웁니다 해당 인덱스에 대해 _index_usage_stats 합니다. 동작은 SQL 2008 및 SQL Server 2016 에서도 동일 하 게 됩니다. [자세한 내용은 블로그를 참조 하십시오.](https://blogs.msdn.microsoft.com/sql_server_team/index-usage-dmv-behavior-updated/)합니다.
-   **XE 진단 및 Dmv 간의 상관 관계를 향상:** 이 개선 사항을 해결 [connect 피드백 (1934583)](https://connect.microsoft.com/SQLServer/feedback/details/1934583/extended-events-query-hash-and-query-plan-hash-data-types)합니다. Query_hash와 query_plan_hash 쿼리를 고유 하 게 식별 하는 데 사용 됩니다. DMV에서는 이를 varbinary(8)으로 정의하는 반면 XEvent에서는 UINT64로 정의합니다. SQL server는 "unisigned bigint" 없으므로 캐스팅 항상 작동 하지 않습니다. 이러한 향상 기능은 query_hash와 query_plan_hash에 해당하는 새 XEvent 작업/필터 열을 소개합니다. 단, XE와 DMV 간에 쿼리의 상관 관계를 지정할 수 있는 INT64로 정의된 경우는 제외합니다.
-   **BULK INSERT 및 BCP에서 u t F-8에 대 한 지원:** 이 개선 사항을 해결 [connect 피드백 (370419)](https://connect.microsoft.com/SQLServer/feedback/details/370419/bulk-insert-and-bcp-does-not-recognize-codepage-65001) BULK INSERT 및 BCP에서 u t F-8 문자 집합으로 인코딩된 데이터 가져오기 및 내보내기에 대 한 지원을 활성화 이제 됩니다.
-   **간단한 연산자 쿼리 실행 프로 파일링:** 있지만 실행 계획은 계획에서 쿼리 실행 계획 및 연산자의 비용에 많은 정보를 제공 하지만 실제에 대 한 정보를 제한 된 쿼리 성능 문제를 해결 하는 동안 (CPU, I/O 읽기 경과 시간 스레드 단위)와 같은 런타임 통계입니다. SQL 2014 s p 2에서 실행 계획으로 (query_thread_profile) XEvent 지원 쿼리 성능 문제를 해결 하기 위해 연산자 당 이러한 추가 런타임 통계를 소개 합니다. [자세한 내용은 블로그를 참조 하십시오.](https://blogs.msdn.microsoft.com/sql_server_team/added-per-operator-level-performance-stats-for-query-processing/)합니다.
-   **변경 내용 추적 정리:** 새 저장 프로시저 `sp_flush_CT_internal_table_on_demand` 정리 변경 내용 추적 내부 테이블 주문형를 도입 합니다.
-   **AlwaysON 임대 시간 제한 로깅** 임대 제한 시간 메시지에 대 한 새 로깅 기능을 추가 되므로 현재 시간 및 예상된 갱신 시간이 기록 됩니다. 또한 새 메시지의 시간 제한에 대 한 SQL Errorlog에 도입 되었습니다. [자세한 내용은 블로그를 참조 하십시오.](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/)합니다.
-   **검색 하기 위한 새 DMF 입력 버퍼에서 SQL Server:** 이제 세션/요청 (sys.dm_exec_input_buffer)를 사용할 수에 대 한 입력된 버퍼를 검색 하기 위한 새 DMF 합니다. 이는 DBCC INPUTBUFFER와 기능적으로 동일합니다. [자세한 내용은 블로그를 참조 하십시오.](https://blogs.msdn.microsoft.com/sql_server_team/new-dmf-for-retrieving-input-buffer-in-sql-server/)합니다.
-   **과소 평가 하 고 overestimated 메모리 부여에 대 한 완화:** MIN_GRANT_PERCENT 및 MAX_GRANT_PERCENT를 통해 리소스 관리자에 대 한 새 쿼리 힌트를 추가 합니다. 이 통해 메모리 경합을 방지 하기 위해 해당 메모리 부여 제한 하 여 쿼리를 실행 하는 동안 이러한 힌트를 활용할 수 있습니다. 자세한 내용은 참조 [KB310740 기술 자료 문서](https://support.microsoft.com/en-us/kb/3107401)
-   **향상 된 메모리 사용량 grant/진단:** 새로운 확장된 이벤트를 추적 하려면 SQL Server (query_memory_grant_usage)의 추적 기능 목록에 추가 되었는지 메모리 부여 요청 하 고 부여 합니다. 이 메모리 부여와 관련 된 쿼리 실행 문제 해결을 위한 더 나은 추적 및 분석 기능을 제공 합니다. 자세한 내용은 참조 [기술 자료 문서 KB3107173](https://support.microsoft.com/en-us/kb/3107173)합니다.
-   **Spill tempdb에 대 한 실행 진단 쿼리:**-Hash Warning 및 Sort Warnings 물리적 I/O 통계, 사용 되는 메모리 및 영향을 받는 행을 추적 하는 추가 열 생깁니다. 또한 새 hash_spill_details 확장된 이벤트가 도입 되었습니다. 이제 해시 및 정렬 경고에 대 한 보다 자세한 정보를 추적할 수 있습니다 ([KB3107172](https://support.microsoft.com/en-us/kb/3107172)). 이러한 향상 기능은 이제도 SpillToTempDbType 복합 형식으로 새 특성의 형태로 XML 쿼리 계획을 통해 표시 됩니다 ([KB3107400](https://support.microsoft.com/en-us/kb/3107400)). 이제 표시 정렬 작업 테이블 통계에 통계를 설정 합니다. 의 인스턴스에 액세스할 때마다 SQL Server 로그인을 제공할 필요가 없습니다.
-   **잔여 조건자 푸시 다운을 포함 하는 쿼리 실행 계획에 대 한 진단을 향상:** 읽은 실제 행 쿼리 성능 문제 해결 개선 하는 쿼리 실행 계획에 이제 보고 됩니다. 이 해야을 유지할 필요성이 SET STATISTICS IO를 개별적으로 캡처할 수 있습니다. 이 구문은 이제를 사용 하는 쿼리 계획의 잔여 조건자 푸시 다운와 관련 된 정보를 볼 수 있습니다. 자세한 내용은 참조 [기술 자료 문서 KB3107397](https://support.microsoft.com/en-us/kb/3107397)합니다.


## <a name="additional-information"></a>추가 정보  
 [SQL Server 2014 리소스](../2014-toc/books-online-for-sql-server-2014.md)  
  
 [SQL Server 2014 Release Notes](http://go.microsoft.com/fwlink/p/?linkID=296445)  
  
 [SQL Server 2014 리소스 센터](http://msdn.microsoft.com/sqlserver/dn135309)  
  
 [SQLCat 웹 사이트](http://go.microsoft.com/fwlink/p/?linkID=220963)  
  
  