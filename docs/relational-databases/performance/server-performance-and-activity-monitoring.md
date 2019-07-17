---
title: 서버 성능 및 작업 모니터링 | Microsoft 문서
ms.custom: ''
ms.date: 11/27/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- activity monitoring [SQL Server]
- traces [SQL Server], how-to topics
- monitoring server performance [SQL Server], activity monitoring
- stored procedures [SQL Server], traces
- performance [SQL Server], servers
- servers [SQL Server], performance
- SQL Server Profiler, how-to topics
- SQL Server Management Studio [SQL Server], monitoring system
- Profiler [SQL Server Profiler], how-to topics
ms.assetid: f9abe48d-d6e9-4c38-a355-fc5eb5a95a25
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 6bca272809116f41a16ef033814fb354ffe46ce2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62936830"
---
# <a name="server-performance-and-activity-monitoring"></a>서버 성능 및 작업 모니터링
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  데이터베이스 모니터링의 목표는 서버의 성능을 평가하는 것입니다. 효과적인 모니터링을 위해서는 현재 성능에 대한 스냅샷을 정기적으로 만들어 문제를 일으키는 프로세스를 격리하고 데이터를 지속적으로 수집하여 성능 경향을 추적해야 합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 운영 체제에서는 데이터베이스의 현재 상태를 확인하고 상태 변화에 따른 성능을 추적할 수 있는 유틸리티를 제공합니다.  
  
 다음 섹션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 Windows의 성능 및 작업 모니터링 도구 사용 방법을 설명합니다. 다음 항목이 포함됩니다.  
  
## <a name="to-perform-monitoring-tasks-with-windows-tools"></a>Windows 도구로 모니터링 태스크를 수행 
  
-   [시스템 모니터 시작&#40;Windows&#41;](../../relational-databases/performance/start-system-monitor-windows.md)  
  
-   [Windows 애플리케이션 로그 보기&#40;Windows&#41;](../../relational-databases/performance/view-the-windows-application-log-windows-10.md)  
  
## <a name="to-create-sql-server-database-alerts-with-windows-tools"></a>Windows 도구로 SQL Server 데이터베이스 경고 만들기  
  
-   [SQL Server 데이터베이스 경고 설정&#40;Windows&#41;](../../relational-databases/performance/set-up-a-sql-server-database-alert-windows.md)  

## <a name="to-perform-monitoring-tasks-with-extended-events"></a>확장 이벤트로 모니터링 작업을 수행하려면  
 
 -   [확장 이벤트](../../relational-databases/extended-events/extended-events.md)
 
 -   [빠른 시작: SQL Server의 확장 이벤트](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md)
 
 -   [개체 탐색기에서 이벤트 세션 관리](../../relational-databases/extended-events/manage-event-sessions-in-the-object-explorer.md)
 
 -   [확장 이벤트 세션 변경](../../relational-databases/extended-events/alter-an-extended-events-session.md)
 
 -   [기존 SQL 추적 스크립트를 확장 이벤트 세션으로 변환](../../relational-databases/extended-events/convert-an-existing-sql-trace-script-to-an-extended-events-session.md)
 
 -   [SQL 추적 이벤트 클래스에 해당하는 확장 이벤트 항목 확인](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md)
   
## <a name="to-perform-monitoring-tasks-with-sql-server-management-studio"></a>SQL Server Management Studio로 모니터링 태스크를 수행  
  
-   [SQL Server 오류 로그 보기&#40;SQL Server Management Studio&#41;](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)  
  
-   [작업 모니터 열기&#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)  

-   [쿼리 저장소를 사용하여 성능 모니터링](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)

## <a name="to-perform-monitoring-tasks-with-sql-trace-and-sql-server-profiler"></a>SQL 추적 및 SQL Server 프로파일러로 모니터링 태스크를 수행하려면

> [!IMPORTANT]
> 다음 섹션에서는 SQL 추적 및 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하는 방법을 설명합니다.  
> SQL 추적 및 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]는 사용되지 않습니다. Microsoft SQL Server 추적 및 재생 개체를 포함하는 *Microsoft.SqlServer.Management.Trace* 네임스페이스도 더 이상 사용되지 않습니다.   
> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
> 확장 이벤트를 대신 사용하세요. [확장 이벤트](../../relational-databases/extended-events/extended-events.md)에 대한 자세한 내용은 [빠른 시작: SQL Server의 확장 이벤트](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md) 및 [SSMS XEvent Profiler](../../relational-databases/extended-events/use-the-ssms-xe-profiler.md)를 참조하세요.

> [!NOTE] 
> Analysis Services 워크로드에는 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]가 계속 사용되며 지원됩니다.

### <a name="to-perform-monitoring-tasks-with-sql-trace-by-using-transact-sql-stored-procedures"></a>Transact-SQL 저장 프로시저를 사용하여 SQL 추적으로 모니터링 태스크를 수행  
  
-   [추적 만들기&#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)  
  
-   [추적 필터 설정&#40;Transact-SQL&#41;](../../relational-databases/sql-trace/set-a-trace-filter-transact-sql.md)  
  
-   [기존 추적 수정&#40;Transact-SQL&#41;](../../relational-databases/sql-trace/modify-an-existing-trace-transact-sql.md)  
  
-   [저장된 추적 보기&#40;Transact-SQL&#41;](../../relational-databases/sql-trace/view-a-saved-trace-transact-sql.md)  
  
-   [필터 정보 보기&#40;Transact-SQL&#41;](../../relational-databases/sql-trace/view-filter-information-transact-sql.md)  
  
-   [추적 삭제&#40;Transact-SQL&#41;](../../relational-databases/sql-trace/delete-a-trace-transact-sql.md)  
  
### <a name="to-create-and-modify-traces-by-using-sql-server-profiler"></a>SQL Server Profiler를 사용하여 추적을 만들고 수정  
  
-   [추적 만들기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
-   [전역 추적 옵션 설정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-global-trace-options-sql-server-profiler.md)  
  
-   [추적 파일에 대해 이벤트 및 데이터 열 지정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
-   [추적 실행을 위한 Transact-SQL 스크립트 만들기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-transact-sql-script-for-running-a-trace-sql-server-profiler.md)  
  
-   [추적 결과를 파일에 저장&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md)  
  
-   [추적 파일에 최대 파일 크기 설정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-file-size-for-a-trace-file-sql-server-profiler.md)  
  
-   [테이블에 추적 결과 저장&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md)  
  
-   [추적 테이블에 최대 테이블 크기 설정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-table-size-for-a-trace-table-sql-server-profiler.md)  
  
-   [추적에서의 이벤트 필터링&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)  
  
-   [필터 정보 보기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)  
  
-   [필터 수정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)  
  
-   [이벤트 시작 시간을 기준으로 이벤트 필터링&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-start-time-sql-server-profiler.md)  
  
-   [이벤트 종료 시간 기반의 이벤트 필터링&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-end-time-sql-server-profiler.md)  
  
-   [추적의 SPID&#40;서버 프로세스 ID&#41; 필터링&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-server-process-ids-spids-in-a-trace-sql-server-profiler.md)  
  
-   [표시된 열 추적으로 구성&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)  
  
### <a name="to-start-pause-and-stop-traces-by-using-sql-server-profiler"></a>SQL Server Profiler를 사용하여 추적을 시작, 일시 중지 및 중지  
  
-   [서버 연결 후 자동으로 추적 시작&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)  
  
-   [추적 일시 중지&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/pause-a-trace-sql-server-profiler.md)  
  
-   [추적 중지&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/stop-a-trace-sql-server-profiler.md)  
  
-   [일시 중지 또는 중지 후 추적 실행&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/run-a-trace-after-it-has-been-paused-or-stopped-sql-server-profiler.md)  
  
### <a name="to-open-traces-and-configure-how-traces-are-displayed-by-using-sql-server-profiler"></a>SQL Server Profiler를 사용하여 추적을 열거나 추적 표시 방법을 구성  
  
-   [추적 파일 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)  
  
-   [추적 테이블 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)  
  
-   [추적 창 지우기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/clear-a-trace-window-sql-server-profiler.md)  
  
-   [추적 창 닫기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/close-a-trace-window-sql-server-profiler.md)  
  
-   [추적 정의 기본값 설정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md)  
  
-   [추적 표시 기본값 설정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)  
  
### <a name="to-replay-traces-by-using-sql-server-profiler"></a>SQL Server Profiler를 사용하여 추적 재생  
  
-   [추적 파일 재생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)  
  
-   [추적 테이블 재생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)  
  
-   [단일 이벤트를 한 번에 하나씩 재생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-single-event-at-a-time-sql-server-profiler.md)  
  
-   [중단점까지 재생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-breakpoint-sql-server-profiler.md)  
  
-   [커서까지 재생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-cursor-sql-server-profiler.md)  
  
-   [Transact-SQL 스크립트 재생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-transact-sql-script-sql-server-profiler.md)  
  
### <a name="to-create-modify-and-use-trace-templates-by-using-sql-server-profiler"></a>SQL Server Profiler를 사용하여 추적 템플릿을 생성, 수정 및 사용  
  
-   [추적 템플릿 만들기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)  
  
-   [추적 템플릿 수정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/modify-a-trace-template-sql-server-profiler.md)  
  
-   [실행 중인 추적으로부터 템플릿 파생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)  
  
-   [추적 파일 또는 추적 테이블에서 템플릿 파생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)  
  
-   [추적 템플릿 내보내기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/export-a-trace-template-sql-server-profiler.md)  
  
-   [추적 템플릿 가져오기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/import-a-trace-template-sql-server-profiler.md)  
  
### <a name="to-use-sql-server-profiler-traces-to-collect-and-monitor-server-performance"></a>SQL Server Profiler 추적을 사용하여 서버 성능을 수집 및 모니터링  
  
-   [추적 중 값 또는 데이터 열 찾기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/find-a-value-or-data-column-while-tracing-sql-server-profiler.md)  
  
-   [교착 상태 그래프 저장&#40;SQL Server Profiler&#41;](../../relational-databases/performance/save-deadlock-graphs-sql-server-profiler.md)  
  
-   [Showplan XML 이벤트를 개별적으로 저장&#40;SQL Server Profiler&#41;](../../relational-databases/performance/save-showplan-xml-events-separately-sql-server-profiler.md)  
  
-   [Showplan XML Statistics Profile 이벤트를 개별적으로 저장&#40;SQL Server Profiler&#41;](../../relational-databases/performance/save-showplan-xml-statistics-profile-events-separately-sql-server-profiler.md)  
  
-   [추적에서 스크립트 추출&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/extract-a-script-from-a-trace-sql-server-profiler.md)  
  
-   [추적과 Windows 성능 로그 데이터의 상관 관계 지정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/correlate-a-trace-with-windows-performance-log-data-sql-server-profiler.md)  
  
  
