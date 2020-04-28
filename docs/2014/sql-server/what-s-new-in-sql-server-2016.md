---
title: SQL Server 2014의 새로운 기능 | Microsoft Docs
ms.custom: ''
ms.date: 12/10/2019
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
ms.openlocfilehash: 23a1392256e103fa1bc112f11b5c5b97f5c398f1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75237710"
---
# <a name="whats-new-in-sql-server-2014"></a>SQL Server 2014의 새로운 기능

이 항목에서는의 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 새로운 기능에 대 한 자세한 링크 및에 대 한 서비스 팩 요약을 요약 합니다.[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 
**사용해 보기:** ![azure Virtual Machine small](./media/what-s-new-in-sql-server-2016/azure-virtual-machine-small.png) 에 azure 계정이 있나요?  SQL Server 2014 https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2014sp1EnterpriseWindowsServer2012R2 SP1 (서비스 팩 1)이 이미 설치 된 가상 컴퓨터를 실행 하려면로 이동 합니다.

> [!TIP]
> SQL Server 2014의 홈 설명서 페이지를 보려면 [여기를 클릭](../2014-toc/index.yml) 하세요.

<!--
Do not let this file's filename fool you.
This filename contains "2016", but nevertheless...
This file, at this exact GitHub path, is dedicated to SQL Server version 2014.
-->

## <a name="whats-new-articles"></a>새로운 기능 문서

-   [새로운 기능 &#40;데이터베이스 엔진&#41;](../database-engine/whats-new-in-sql-server-2016.md)  
  
-   [Analysis Services 및 비즈니스 인텔리전스의 새로운 기능](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services)  
  
-   [SQL Server 설치의 새로운 기능](install/what-s-new-in-sql-server-installation.md)  
  
 **[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]는 다음과 같은 기능에 중요 한 새로운 기능을 도입 하지 않았습니다.**  
  
-   [새로운 기능 &#40;Integration Services&#41;](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)  
  
-   [새로운 기능 &#40;Reporting Services&#41;](../reporting-services/what-s-new-reporting-services.md)  
  
## <a name="sssql14-service-pack-1-sp1"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP1(서비스 팩 1)
[!INCLUDE[ssSQL14](../includes/sssql14-md.md)](SP1)에는 중요 한 새로운 기능이 도입 되지 않았습니다.
-  [2014 서비스 팩 1 릴리스 정보를 SQL Server](https://support.microsoft.com/kb/3058865)합니다.
-  [Microsoft SQL Server 2014 서비스 팩 1 다운로드 Microsoft SQL Server 2014 서비스 팩 1을 다운로드 합니다. ![](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/download/details.aspx?id=46694) [Download Service Pack 1 for Microsoft SQL Server 2014](https://www.microsoft.com/download/details.aspx?id=46694)


## <a name="sssql14-service-pack-2-sp2"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]서비스 팩 2 (SP2)
- [2014 서비스 팩 2 릴리스 정보를 SQL Server](https://support.microsoft.com/kb/3171021)합니다.
-  [Microsoft SQL Server 2014에 대 한 서비스 팩 2 다운로드 Microsoft SQL Server 2014 서비스 팩 2를 다운로드 합니다. ![](./media/what-s-new-in-sql-server-2016/download.png)](https://go.microsoft.com/fwlink/?LinkID=821558) [Download Service Pack 2 for Microsoft SQL Server 2014](https://go.microsoft.com/fwlink/?LinkID=821558)
-  [다운로드 SQL Server 2014 sp2 기능 팩 SQL Server 2014 SP2 기능 팩을 다운로드 합니다. ![](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/download/details.aspx?id=53164) [Download the SQL Server 2014 SP2 Feature Pack](https://www.microsoft.com/download/details.aspx?id=53164)

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]2 에는 다음과 같은 향상 된 기능이 포함 되어 있습니다.

### <a name="performance-and-scalability-improvements"></a>성능 및 확장성 향상 
-   **자동 소프트 NUMA 분할:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] S p 2에서는 인스턴스를 시작 하는 동안 추적 플래그 8079가 설정 되 면 자동 소프트 NUMA가 사용 됩니다. 시작 하는 동안 추적 플래그 8079를 사용 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 하도록 설정 하면 s p 2는 하드웨어 레이아웃을 검사 하 고 NUMA 노드당 8 개 이상의 cpu를 보고 하는 시스템에서 소프트 NUMA를 자동으로 구성 합니다. 자동 소프트 NUMA 동작은 하이퍼스레드 제외 (HT/logical processor)를 인식 합니다. 추가 노드를 분할하고 생성하면 수신기 수, 크기 조정 및 네트워크와 암호화 기능을 늘려서 후순위 처리를 조정합니다. 프로덕션 환경에서 튜닝 하기 전에 먼저 자동 소프트 NUMA를 사용 하 여 성능 작업을 테스트 하는 것이 좋습니다. [자세한 내용은 블로그를 참조](https://blogs.msdn.microsoft.com/psssql/2016/03/30/sql-2016-it-just-runs-faster-automatic-soft-numa/)하세요. 
-  **동적 메모리 개체 배율:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] s p 2는 최신 하드웨어에서 확장할 노드 및 코어 수에 따라 메모리 개체를 동적으로 분할 합니다. 동적 승격의 목표는 병목 상태가 될 경우 CMEMTHREAD (스레드 안전 메모리 개체)를 자동으로 분할 하는 것입니다. 분할 되지 않은 메모리 개체는 노드에 의해 동적으로 분할 될 수 있습니다. 파티션 수는 NUMA 노드 수와 같습니다. 노드당 분할 된 메모리 개체는 CPU를 통해 추가로 분할 될 수 있습니다 (파티션 수는 Cpu 수와 동일). [자세한 내용은 블로그를 참조](https://blogs.msdn.microsoft.com/psssql/2016/04/06/sql-2016-it-just-runs-faster-dynamic-memory-object-cmemthread-partitioning/)하세요.
-  **DBCC\* CHECK 명령에 대 한 MAXDOP 힌트:** 이 향상 기능은 [연결 피드백 (468694)](https://connect.microsoft.com/SQLServer/feedback/details/468694/maxdop-option-in-dbcc-checkdb)을 해결 합니다. 이제 sp_configure 값이 아닌 MAXDOP 설정을 사용 하 여 DBCC CHECKDB를 실행할 수 있습니다. MAXDOP가 Resource Governor로 구성한 값을 초과하면, 데이터베이스 엔진에서 ALTER WORKLOAD GROUP(Transact-SQL)에서 설명한 Resource Governor MAXDOP 값을 사용합니다. max degree of parallelism 구성 옵션에 사용된 모든 의미 체계 규칙을 MAXDOP 쿼리 힌트 사용 시 적용할 수 있습니다. 자세한 내용은 [DBCC CHECKDB (transact-sql)](https://msdn.microsoft.com/library/ms176064.aspx)를 참조 하세요.
-   **버퍼 풀에 대해 8tb를 사용 하도록 설정:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] s p 2는 버퍼 풀 사용에 128 tb의 가상 주소 공간을 사용 하도록 >설정 합니다. 이러한 향상을 통해 SQL Server 버퍼 풀이 최신 하드웨어에서 8TB 이상으로 확장 될 수 있습니다.
-   **SOS_RWLock Spinlock 개선:** SOS_RWLock은 SQL Server 코드 베이스 전체에서 다양 한 위치에 사용 되는 동기화 기본 형식입니다.  이름에서 알 수 있듯이, 코드에 여러 공유 (판독기) 또는 단일 (작성자) 소유권이 있을 수 있습니다. 이러한 향상 된 기능을 통해 SOS_RWLock에 대해 spinlock이 필요 하지 않으며, 대신 메모리 내 OLTP와 유사한 잠금 없는 기술을 사용 합니다. 이와 같이 변경 하면 많은 스레드가 서로를 차단 하지 않고 동시에 SOS_RWLock으로 보호 되는 데이터 구조를 읽을 수 있습니다. 이러한 병렬화는 향상 된 확장성을 제공 합니다. 이러한 변경 전에는 spinlock 구현에서 한 번에 하나의 스레드만 SOS_RWLock 데이터 구조를 읽을 수 있도록 허용 했습니다. [자세한 내용은 블로그를 참조](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/)하세요.
-    **공간 네이티브 구현:** 기본 구현을 통해 SP2에서 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 공간 쿼리 성능이 크게 향상 되었습니다. 자세한 내용은 [기술 자료 문서 KB3107399](https://support.microsoft.com/kb/3107399)를 참조 하세요.

### <a name="supportability-and-diagnostics-improvements"></a>지원 가능성 및 진단 기능 향상
-   **데이터베이스 복제:** 데이터베이스 복제는 데이터 없이 스키마 및 메타 데이터를 복제 하 여 기존 프로덕션 데이터베이스의 문제 해결을 개선 하는 새로운 DBCC 명령입니다. 복제본은 명령을 `DBCC clonedatabase('source_database_name', 'clone_database_name')`사용 하 여 만듭니다.  **참고:** 복제 된 데이터베이스는 프로덕션 환경에서 사용 하면 안 됩니다. 다음 명령을 사용 하 여 복제 된 데이터베이스에서 데이터베이스가 생성 되었는지 확인 `select DATABASEPROPERTYEX('clonedb', 'isClone')`합니다. 반환 값 **1** 은 데이터베이스가 clonedatabase에서 생성 되었음을 나타내며 **0** 은 복제가 아닌 것을 나타냅니다.
-   **Tempdb 지원 가능성:**  Tempdb 파일 수 및 tempdb 데이터 파일의 크기와 자동 증가를 모두 시작 하는 것을 나타내는 새 오류 로그 메시지입니다.
-   **데이터베이스 즉시 파일 초기화 로깅:** 서버 시작 시 데이터베이스 즉시 파일 초기화의 상태 (사용/사용 안 함)를 나타내는 새 오류 로그 메시지입니다.
-   **호출 스택의 모듈 이름:** 이제 XEvent (확장 이벤트) 호출 스택에 절대 주소가 아니라 모듈 이름 및 오프셋이 포함 됩니다.
-   **증분 통계에 대 한 새 DMF:** 이 향상 된 기능은 [연결 피드백 (797156)](https://connect.microsoft.com/SQLServer/feedback/details/797156/display-sys-dm-db-stats-properties-per-partition-for-incremental-statistics) 을 처리 하 여 파티션 수준에서 증분 통계를 추적할 수 있도록 합니다. 증분 통계에 대 한 파티션당 정보를 노출 하기 위해 새 DMF dm_db_incremental_stats_properties가 도입 되었습니다.
-   **인덱스 사용 DMV 동작 업데이트:** 이 향상 된 기능을 통해 인덱스를 다시 작성 해도 해당 인덱스에 대해 dm_db_index_usage_stats의 기존 행 항목이 삭제 *되지 않는* 고객의 [연결 피드백 (739566)](https://connect.microsoft.com/SQLServer/feedback/details/739566/rebuilding-an-index-clears-stats-from-sys-dm-db-index-usage-stats) 이 해결 됩니다. 이 동작은 이제 SQL 2008 및 SQL Server 2016와 동일 합니다. [자세한 내용은 블로그를 참조](https://blogs.msdn.microsoft.com/sql_server_team/index-usage-dmv-behavior-updated/)하세요.
-   **진단 XE와 dmv 간의 상관 관계 향상:** 이 개선 사항은 [연결 피드백 (1934583)](https://connect.microsoft.com/SQLServer/feedback/details/1934583/extended-events-query-hash-and-query-plan-hash-data-types)을 해결 합니다. `Query_hash`및 `query_plan_hash` 는 쿼리를 고유 하 게 식별 하는 데 사용 됩니다. DMV에서는 이를 varbinary(8)으로 정의하는 반면 XEvent에서는 UINT64로 정의합니다. SQL server에는 "unsigned bigint"가 없으므로 캐스팅이 항상 작동 하지는 않습니다. 이 개선 사항에는 새로운 XEvent 작업 및 필터 열이 도입 되었습니다. 열은 INT64로 정의 `query_hash` 된다는 `query_plan_hash`점을 제외 하 고 및와 동일 합니다. INT64 정의는 XE와 Dmv 간의 쿼리를 상호 연결 하는 데 도움이 됩니다.
-   **BULK INSERT 및 BCP에서 u t f-8에 대 한 지원:** 이 개선 사항은 [연결 피드백 (370419)](https://connect.microsoft.com/SQLServer/feedback/details/370419/bulk-insert-and-bcp-does-not-recognize-codepage-65001)을 해결 합니다. 이제 BULK INSERT와 BCP는 UTF-8 문자 집합으로 인코딩된 데이터를 내보내거나 가져올 수 있습니다.
-   **연산자 당 쿼리 실행의 경량 프로 파일링:** 실행 계획에서 각 운영자의 비용에 대 한 정보를 제공 합니다. 그러나 실제 런타임 통계는 CPU, i/o 읽기 및 스레드별 경과 시간 등의 작업에 대해 제한 됩니다. SQL Server 2014 s p 2에서는 실행 계획의 연산자 당 이러한 추가 런타임 통계를 소개 합니다. 또한 R2는 쿼리 성능 문제 `query_thread_profile` 해결을 지원 하기 위해 라는 XEvent를 도입 합니다. [자세한 내용은 블로그를 참조](https://blogs.msdn.microsoft.com/sql_server_team/added-per-operator-level-performance-stats-for-query-processing/)하세요.
-   **변경 내용 추적 정리:** 새 저장 프로시저 `sp_flush_CT_internal_table_on_demand` 를 도입 하 여 요청 시 변경 내용 추적 내부 테이블을 정리 합니다.
-   **AlwaysON 임대 시간 제한 로깅** 현재 시간 및 예상 된 갱신 시간이 기록 될 수 있도록 임대 시간 제한 메시지에 대 한 새 로깅 기능을 추가 했습니다. 또한 시간 제한과 관련 하 여 SQL 오류 로그에 새 메시지가 새로 추가 되었습니다. [자세한 내용은 블로그를 참조](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/)하세요.
-   **SQL Server에서 입력 버퍼를 검색 하기 위한 새 DMF:** 이제 세션/요청 dm_exec_input_buffer (DMF)에 대 한 입력 버퍼를 검색 하기 위한 새로운를 사용할 수 있습니다. 이 DMF는 DBCC INPUTBUFFER와 기능적으로 동일 합니다. [자세한 내용은 블로그를 참조](https://blogs.msdn.microsoft.com/sql_server_team/new-dmf-for-retrieving-input-buffer-in-sql-server/)하세요.
-   **과소 예측 및 과도 하 게 예상 되는 메모리 부여에 대 한 완화:** MIN_GRANT_PERCENT 및 MAX_GRANT_PERCENT를 통해 Resource Governor에 대 한 새 쿼리 힌트가 추가 되었습니다. 이 새 쿼리를 사용 하면 메모리 경합을 방지 하기 위해 메모리 부여를 50, 하 여 쿼리를 실행 하는 동안 이러한 힌트를 활용할 수 있습니다. 자세한 내용은 [기술 자료 문서 KB310740](https://support.microsoft.com/kb/3107401)를 참조 하세요.
-   **더 나은 메모리 부여 및 사용 진단:** SQL Server의 추적 기능 목록 `query_memory_grant_usage` 에 라는 새 확장 이벤트가 추가 되었습니다. 이 이벤트는 요청 및 부여 된 메모리 부여를 추적 합니다. 이 이벤트는 메모리 부여와 관련 된 쿼리 실행 문제를 해결 하기 위한 향상 된 추적 및 분석 기능을 제공 합니다. 자세한 내용은 [기술 자료 문서 KB3107173](https://support.microsoft.com/kb/3107173)를 참조 하세요.
-   **Tempdb 분산을 위한 쿼리 실행 진단:**-해시 경고 및 정렬 경고에는 이제 실제 i/o 통계, 사용 된 메모리 및 영향을 받는 행을 추적 하는 추가 열이 있습니다. 또한 새로운 hash_spill_details 확장 이벤트를 도입 했습니다. 이제 해시 및 정렬 경고 ([KB3107172](https://support.microsoft.com/kb/3107172))에 대 한 더 세부적인 정보를 추적할 수 있습니다. 이러한 향상 된 기능은 이제 새 특성의 형태로 XML 쿼리 계획을 통해 SpillToTempDbType 복합 유형 ([KB3107400](https://support.microsoft.com/kb/3107400))에도 노출 됩니다. Set statistics `ON` 는 이제 sort 작업 테이블 통계를 표시 합니다.
-   **잔여 조건자 푸시 다운을 포함 하는 쿼리 실행 계획에 대 한 진단이 향상 되었습니다.** 이제 쿼리 성능 문제 해결을 개선 하는 데 도움이 되는 실제 행 읽기가 쿼리 실행 계획에 보고 되었습니다. 이러한 행은 SET STATISTICS IO를 별도로 캡처할 필요성을 무효화 합니다. 이러한 행을 사용 하 여 쿼리 계획의 잔여 조건자 푸시와 관련 된 정보를 볼 수도 있습니다. 자세한 내용은 [기술 자료 문서 KB3107397](https://support.microsoft.com/kb/3107397)를 참조 하세요.


## <a name="additional-information"></a>추가 정보  
 [SQL Server 2014 리소스](../2014-toc/index.yml)  
  
 [SQL Server 2014 릴리스 정보](https://go.microsoft.com/fwlink/p/?linkID=296445)  
  
 [SQL Server 2014 리소스 센터](https://msdn.microsoft.com/sqlserver/dn135309)  
  
 [SQLCat 웹 사이트](https://go.microsoft.com/fwlink/p/?linkID=220963)  
