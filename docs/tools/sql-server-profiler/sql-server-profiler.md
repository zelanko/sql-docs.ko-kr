---
title: SQL Server Profiler
titleSuffix: SQL Server Profiler
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 3ad5f33d-559e-41a4-bde6-bb98792f7f1a
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 11/27/2018
ms.openlocfilehash: afabb7e6509c3e7692b5aaaf4d3fcedcbf4353a9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288118"
---
# <a name="sql-server-profiler"></a>SQL Server Profiler

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]는 추적을 작성 및 관리하고 추적 결과를 분석 및 재생하기 위한 인터페이스입니다. 이벤트는 추적 파일에 저장되며 이 파일은 나중에 분석되거나 문제를 진단할 때 특정 단계를 다시 수행하기 위해 사용할 수 있습니다.  
  
> [!IMPORTANT]
> SQL 추적 및 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]는 사용되지 않습니다. Microsoft SQL Server 추적 및 재생 개체를 포함하는 *Microsoft.SqlServer.Management.Trace* 네임스페이스도 더 이상 사용되지 않습니다. 
> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 
> 확장 이벤트를 대신 사용하세요. [확장 이벤트](../../relational-databases/extended-events/extended-events.md)에 대한 자세한 내용은 [빠른 시작: SQL Server의 확장 이벤트](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md) 및 [SSMS XEvent 프로파일러](../../relational-databases/extended-events/use-the-ssms-xe-profiler.md)를 참조하세요.

> [!NOTE]
> Analysis Services 워크로드에는 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]가 계속 사용되며 지원됩니다.

 ## <a name="where-is-the-profiler"></a>프로파일러는 어디에 있나요?
 
다양한 방법으로 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 프로파일러를 시작할 수 있습니다. [다음 항목에서는 프로파일러를 시작할 수 있는 방법을 나열했습니다.](start-sql-server-profiler.md)
  
## <a name="capture-and-replay-trace-data"></a>추적 데이터 캡처 및 재생 
다음 표에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 추적 데이터를 캡처하고 재생하는 데 사용할 수 있는 권장 기능을 보여 줍니다.
  
||||  
|-|-|-|  
|**기능\대상 작업**|**관계형 엔진**|**Analysis Services**|  
|**추적 캡처**|[의 ](../../relational-databases/extended-events/extended-events.md)확장 이벤트[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 그래픽 사용자 인터페이스|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]|  
|**추적 재생**|[Distributed Replay](../distributed-replay/sql-server-distributed-replay.md)|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]|  
  
## <a name="sql-server-profiler"></a>SQL Server Profiler  
Microsoft [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 또는 Analysis Services의 인스턴스를 모니터링하기 위한 SQL 추적에 대한 그래픽 사용자 인터페이스입니다. 각 이벤트에 대한 데이터를 캡처하고 파일이나 테이블에 저장하여 나중에 분석할 수 있습니다. 예를 들어 프로덕션 환경을 모니터링하여 어느 저장 프로시저가 너무 늦게 실행되어 성능을 떨어뜨리고 있는지 볼 수 있습니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]는 다음과 같은 작업에 사용됩니다.  
  
-   문제가 발생한 원인을 찾기 위해 문제 쿼리 실행  
  
-   실행이 느린 쿼리를 찾고 진단
  
-   문제가 발생한 일련의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 포착. 그런 다음 저장된 추적을 사용하여, 문제를 진단할 수 있는 테스트 서버에서 문제를 복제할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 성능을 모니터링하여 작업 튜닝. 데이터베이스 작업에 맞게 물리적 데이터베이스 디자인을 튜닝하는 방법은 [Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)를 참조하세요.  
  
-   문제 진단을 위해 성능 카운터의 상관 관계 지정  
  
또한 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에서 수행되는 동작을 감사하는 기능을 지원합니다. 감사는 보안 관리자가 나중에 검토할 수 있도록 보안 관련 동작을 기록합니다.  
  
## <a name="sql-server-profiler-concepts"></a>SQL Server Profiler 개념  
[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]도구를 사용하려면 도구가 작동하는 방식을 설명하는 용어를 알고 있어야 합니다.  
  
> [!NOTE]
> SQL 추적을 이해하면 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]로 작업할 때 큰 도움이 됩니다. 자세한 내용은 [SQL Trace](../../relational-databases/sql-trace/sql-trace.md)을(를) 참조하세요.  
  
 **이벤트**  
 이벤트는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]인스턴스에서 발생하는 동작으로, 이벤트의 예는 다음과 같습니다.  
  
-   로그인 연결, 실패 및 연결 끊김    
-   [!INCLUDE[tsql](../../includes/tsql-md.md)], `SELECT`, `INSERT`, `UPDATE` 및 `DELETE` 문.    
-   RPC(원격 프로시저 호출) 일괄 처리 상태  
-   저장 프로시저의 시작 또는 끝  
-   저장 프로시저에 있는 문의 시작 또는 끝  
-   SQL 일괄 처리의 시작 또는 끝  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 쓴 오류  
-   데이터베이스 개체에서 획득 또는 해제된 잠금  
-   열린 커서  
-   보안 권한 검사  
  
한 이벤트에 의해 생성된 모든 데이터는 추적에서 한 줄에 표시됩니다. 이 행은 이벤트를 자세히 설명하는 데이터 열로 구분됩니다.  
  
 **EventClass**  
 이벤트 클래스는 추적할 수 있는 이벤트 유형입니다. 이벤트 클래스에는 이벤트에서 보고할 수 있는 모든 데이터가 포함됩니다. 이벤트 클래스의 예는 다음과 같습니다.  
  
-   **SQL:BatchCompleted**  
-   **Audit Login**  
-   **Audit Logout**  
-   **Lock:Acquired**  
-   **Lock:Released**  
  
 **EventCategory**  
 이벤트 범주는 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]내에서 이벤트를 그룹화하는 방법을 정의합니다. 예를 들어 모든 잠금 이벤트 클래스는 **Locks** 이벤트 범주 내에서 그룹화됩니다. 그러나 이벤트 범주는 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]내에서만 존재합니다. 이 용어는 엔진 이벤트를 그룹화하는 방법과 관계가 없습니다.  
  
 **DataColumn**  
 데이터 열은 추적에 캡처된 이벤트 클래스의 특성입니다. 이벤트 클래스가 수집할 수 있는 데이터 형식을 결정하기 때문에 모든 데이터 열이 모든 이벤트 클래스에 적용되는 것은 아닙니다. 예를 들어 **Lock:Acquired** 이벤트 클래스를 캡처하는 추적에서 **BinaryData** 데이터 열에는 잠긴 페이지 ID 값이나 행 값이 들어 있지만 캡처하는 이벤트 클래스에 적용할 수 없는 **Integer Data** 데이터 열에는 아무 값도 들어 있지 않습니다.  
  
 **템플릿**  
 템플릿은 추적의 기본 구성을 정의합니다. 특히 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]로 모니터링하려는 이벤트 클래스가 템플릿에 포함됩니다. 예를 들어 사용할 이벤트, 데이터 열 및 필터를 지정하는 템플릿을 만들 수 있습니다. 템플릿은 실행되지 않으며 .tdf 확장명을 가진 파일로 저장됩니다. 템플릿을 저장한 후에는 템플릿에 기반한 추적이 시작될 때 캡처된 추적 데이터를 제어할 수 있습니다.  
  
 **추적**  
 추적은 선택한 이벤트 클래스, 데이터 열 및 필터에 기초하여 데이터를 캡처합니다. 예를 들어 예외 오류를 모니터링하는 추적을 만들 수 있습니다. 이 작업을 수행하려면 **Exception** 이벤트 클래스를 선택하고 **Error**, **State**및 **Severity** 데이터 열을 선택합니다. 추적 결과에서 의미 있는 데이터를 제공하려면 이 3열의 데이터를 수집해야 합니다. 그런 다음 구성된 방식으로 추적을 실행하고 서버에서 발생하는 모든 **Exception** 이벤트에 대한 데이터를 수집합니다. 추적 데이터를 즉시 분석에 사용하거나 저장한 후 나중에 분석할 수 있습니다. 나중에 추적을 재생할 수 있지만 **Exception** 이벤트와 같은 특정 이벤트는 재생할 수 없습니다. 또한 추적을 템플릿으로 저장하여 나중에 유사한 추적을 구성할 수 있습니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은(는) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 추적하는 두 가지 방법을 제공합니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]을(를) 사용하여 추적하거나 시스템 저장 프로시저를 사용하여 추적할 수 있습니다.  
  
 **Filter**  
 추적 또는 템플릿을 만들 때 이벤트가 수집하는 데이터를 필터링할 조건을 정의할 수 있습니다. 추적이 지나치게 커지지 않도록 필터링을 통해 이벤트 데이터의 하위 집합만 수집할 수 있습니다. 예를 들어 추적에서 Microsoft Windows 사용자 이름을 특정 사용자로 제한하여 출력 데이터를 줄일 수 있습니다.  
  
 필터가 설정되어 있지 않으면 선택된 이벤트 클래스의 모든 이벤트가 추적 출력에서 반환됩니다.  
  
## <a name="sql-server-profiler-tasks"></a>SQL Server Profiler 태스크  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|SQL Server에서 특정한 유형의 이벤트를 모니터링하기 위해 제공하는 미리 정의된 템플릿과 추적을 재생하는 데 필요한 사용 권한을 보여 줍니다.|[SQL Server Profiler 템플릿 및 권한](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler를 실행하는 방법에 대해 설명합니다.|[SQL Server 프로파일러 실행에 필요한 권한](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)|  
|추적을 만드는 방법에 대해 설명합니다.|[추적 만들기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)|  
|추적 파일에 대한 이벤트 및 데이터 열을 지정하는 방법에 대해 설명합니다.|[추적 파일에 대해 이벤트 및 데이터 열 지정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)|  
|파일에 추적 결과를 저장하는 방법에 대해 설명합니다.|[추적 결과를 파일에 저장&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md)|  
|테이블에 추적 결과를 저장하는 방법에 대해 설명합니다.|[테이블에 추적 결과 저장&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md)|  
|추적에서 이벤트를 필터링하는 방법에 대해 설명합니다.|[추적에서의 이벤트 필터링&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)|  
|필터 정보를 보는 방법에 대해 설명합니다.|[필터 정보 보기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)|  
|필터를 수정하는 방법에 대해 설명합니다.|[필터 수정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)|  
|추적 파일에 대한 최대 파일 크기를 설정하는 방법을 설명합니다([!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]).|[추적 파일에 최대 파일 크기 설정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-file-size-for-a-trace-file-sql-server-profiler.md)|  
|추적 테이블에 대한 최대 테이블 크기를 설정하는 방법에 대해 설명합니다.|[추적 테이블에 최대 테이블 크기 설정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-table-size-for-a-trace-table-sql-server-profiler.md)|  
|추적을 시작하는 방법에 대해 설명합니다.|[추적 시작](../../tools/sql-server-profiler/start-a-trace.md)|  
|서버에 연결한 후 추적을 자동으로 시작하는 방법에 대해 설명합니다.|[서버 연결 후 자동으로 추적 시작&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)|  
|이벤트 시작 시간을 기반으로 이벤트를 필터링하는 방법에 대해 설명합니다.|[이벤트 시작 시간을 기준으로 이벤트 필터링&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-start-time-sql-server-profiler.md)|  
|이벤트 종료 시간을 기반으로 이벤트를 필터링하는 방법에 대해 설명합니다.|[이벤트 종료 시간 기반의 이벤트 필터링&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-end-time-sql-server-profiler.md)|  
|추적에서 SPID(서버 프로세스 ID)를 필터링하는 방법에 대해 설명합니다.|[추적의 SPID&#40;서버 프로세스 ID&#41; 필터링&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-server-process-ids-spids-in-a-trace-sql-server-profiler.md)|  
|추적을 일시 중지하는 방법에 대해 설명합니다.|[추적 일시 중지&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/pause-a-trace-sql-server-profiler.md)|  
|추적을 중지하는 방법에 대해 설명합니다.|[추적 중지&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/stop-a-trace-sql-server-profiler.md)|  
|추적을 일시 중지하거나 중지했다가 다시 실행하는 방법에 대해 설명합니다.|[일시 중지 또는 중지 후 추적 실행&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/run-a-trace-after-it-has-been-paused-or-stopped-sql-server-profiler.md)|  
|추적 창을 지우는 방법에 대해 설명합니다.|[추적 창 지우기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/clear-a-trace-window-sql-server-profiler.md)|  
|추적 창을 닫는 방법에 대해 설명합니다.|[추적 창 닫기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/close-a-trace-window-sql-server-profiler.md)|  
|추적 정의 기본값을 설정하는 방법에 대해 설명합니다.|[추적 정의 기본값 설정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md)|  
|추적 표시 기본값을 설정하는 방법에 대해 설명합니다.|[추적 표시 기본값 설정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)|  
|추적 파일을 여는 방법에 대해 설명합니다.|[추적 파일 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)|  
|추적 테이블을 여는 방법에 대해 설명합니다.|[추적 테이블 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)|  
|추적 테이블을 재생하는 방법에 대해 설명합니다.|[추적 테이블 재생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)|  
|추적 파일을 재생하는 방법에 대해 설명합니다.|[추적 파일 재생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)|  
|한 번에 하나의 이벤트를 재생하는 방법에 대해 설명합니다.|[단일 이벤트를 한 번에 하나씩 재생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-single-event-at-a-time-sql-server-profiler.md)|  
|중단점까지 재생하는 방법에 대해 설명합니다.|[중단점까지 재생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-breakpoint-sql-server-profiler.md)|  
|커서까지 재생하는 방법을 설명합니다.|[커서까지 재생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-cursor-sql-server-profiler.md)|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 재생하는 방법에 대해 설명합니다.|[Transact-SQL 스크립트 재생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-transact-sql-script-sql-server-profiler.md)|  
|추적 템플릿을 만드는 방법에 대해 설명합니다.|[추적 템플릿 만들기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)|  
|추적 템플릿을 수정하는 방법에 대해 설명합니다.|[추적 템플릿 수정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/modify-a-trace-template-sql-server-profiler.md)|  
|전역 추적 옵션을 설정하는 방법에 대해 설명합니다.|[전역 추적 옵션 설정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-global-trace-options-sql-server-profiler.md)|  
|추적 중에 값 또는 데이터 열을 찾는 방법에 대해 설명합니다.|[추적 중 값 또는 데이터 열 찾기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/find-a-value-or-data-column-while-tracing-sql-server-profiler.md)|  
|실행 중인 추적에서 템플릿을 파생하는 방법에 대해 설명합니다.|[실행 중인 추적으로부터 템플릿 파생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)|  
|추적 파일 또는 추적 테이블에서 템플릿을 파생하는 방법에 대해 설명합니다.|[추적 파일 또는 추적 테이블에서 템플릿 파생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)|  
|추적 실행을 위한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 만드는 방법에 대해 설명합니다.|[추적 실행을 위한 Transact-SQL 스크립트 만들기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-transact-sql-script-for-running-a-trace-sql-server-profiler.md)|  
|추적 템플릿을 내보내는 방법에 대해 설명합니다.|[추적 템플릿 내보내기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/export-a-trace-template-sql-server-profiler.md)|  
|추적 템플릿을 가져오는 방법에 대해 설명합니다.|[추적 템플릿 가져오기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/import-a-trace-template-sql-server-profiler.md)|  
|추적에서 스크립트를 추출하는 방법에 대해 설명합니다.|[추적에서 스크립트 추출&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/extract-a-script-from-a-trace-sql-server-profiler.md)|  
|추적과 Windows 성능 로그 데이터의 상관 관계를 지정하는 방법에 대해 설명합니다.|[추적과 Windows 성능 로그 데이터의 상관 관계 지정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/correlate-a-trace-with-windows-performance-log-data-sql-server-profiler.md)|  
|추적에 표시되는 열을 구성하는 방법에 대해 설명합니다.|[표시된 열 추적으로 구성&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)|  
|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 시작하는 방법에 대해 설명합니다.|[SQL Server Profiler 시작](../../tools/sql-server-profiler/start-sql-server-profiler.md)|  
|추적 및 추적 템플릿을 저장하는 방법에 대해 설명합니다.|[추적 및 추적 템플릿 저장](../../tools/sql-server-profiler/save-traces-and-trace-templates.md)|  
|추적 템플릿을 수정하는 방법에 대해 설명합니다.|[추적 템플릿 수정](../../tools/sql-server-profiler/modify-trace-templates.md)|  
|추적과 Windows 성능 로그 데이터의 상관 관계를 지정하는 방법에 대해 설명합니다.|[Windows 성능 로그 데이터와 추적의 상관 관계 지정](../../tools/sql-server-profiler/correlate-a-trace-with-windows-performance-log-data.md)|  
|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 추적을 보고 분석하는 방법에 대해 설명합니다.|[SQL Server Profiler를 사용하여 추적 보기 및 분석](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md)|  
|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 교착 상태를 분석하는 방법에 대해 설명합니다.|[SQL Server Profiler를 사용하여 교착 상태 분석](../../tools/sql-server-profiler/analyze-deadlocks-with-sql-server-profiler.md)|  
|SQL Server Profiler에서 SHOWPLAN 결과로 쿼리를 분석하는 방법에 대해 설명합니다.|[SQL Server Profiler에서 SHOWPLAN 결과로 쿼리 분석](../../tools/sql-server-profiler/analyze-queries-with-showplan-results-in-sql-server-profiler.md)|  
|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 추적을 필터링하는 방법에 대해 설명합니다.|[SQL Server Profiler로 추적 필터링](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)|  
|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]의 재생 기능을 사용하는 방법을 설명합니다.|[추적 재생](../../tools/sql-server-profiler/replay-traces.md)|  
|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]에 대한 상황에 맞는 도움말 항목이 나열되어 있습니다.|[SQL Server 프로파일러 F1 도움말](../../tools/sql-server-profiler/sql-server-profiler-f1-help.md)|  
|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]에서 성능 및 작업을 모니터링하는 데 사용하는 시스템 저장 프로시저를 보여 줍니다.|[SQL Server Profiler 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)|  
  
## <a name="see-also"></a>참고 항목  
 [잠금 이벤트 범주](../../relational-databases/event-classes/locks-event-category.md)   
 [세션 이벤트 범주](../../relational-databases/event-classes/sessions-event-category.md)   
 [저장 프로시저 이벤트 범주](../../relational-databases/event-classes/stored-procedures-event-category.md)   
 [TSQL 이벤트 범주](../../relational-databases/event-classes/tsql-event-category.md)   
 [서버 성능 및 작업 모니터링](../../relational-databases/performance/server-performance-and-activity-monitoring.md)  
  
  
