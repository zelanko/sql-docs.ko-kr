---
title: 성능 모니터링 및 튜닝 도구 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- tools [SQL Server], monitoring performance
- monitoring server performance [SQL Server], tools
- monitoring performance [SQL Server], tools
- database performance [SQL Server], tools
- tuning databases [SQL Server], tools
- database monitoring [SQL Server], tools
- performance [SQL Server], monitoring tools
- server performance [SQL Server], tools
ms.assetid: 31529dfe-68e7-49f7-b3c2-39fcecf33a95
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 30cc668487299677bb2874300d660d09d1dedd22
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85635444"
---
# <a name="performance-monitoring-and-tuning-tools"></a>성능 모니터링 및 튜닝 도구
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이벤트를 모니터링하고 물리적 데이터베이스 디자인을 튜닝하는 여러 가지 도구를 제공합니다. 도구를 선택하는 기준은 수행된 모니터링 또는 튜닝 유형과 모니터링할 이벤트에 따라 결정됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 모니터링 및 튜닝 도구는 다음과 같습니다.  
  
|도구|Description|  
|----------|-----------------|  
|[기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)|기본 제공 함수는 서버가 시작된 이후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업에 대한 스냅샷 통계를 표시하며 이러한 통계는 미리 정의된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 카운터에 저장됩니다. 예를 들어 **\@\@CPU_BUSY**에는 CPU가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 코드를 실행한 시간이 포함되고 **\@\@CONNECTIONS**에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 수나 시도 횟수가 포함되며 **\@\@PACKET_ERRORS**에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결에서 발생한 네트워크 패킷 수가 포함됩니다.|  
|[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)|DBCC(데이터베이스 콘솔 명령) 문을 사용하면 성능 통계 및 데이터베이스의 논리적, 물리적 일관성을 검사할 수 있습니다.|  
|[DTA(데이터베이스 엔진 튜닝 관리자)](../../relational-databases/performance/database-engine-tuning-advisor.md)|데이터베이스 엔진 튜닝 관리자는 튜닝할 데이터베이스에 대해 실행된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 성능 영향을 분석합니다. 데이터베이스 엔진 튜닝 관리자는 인덱스, 인덱싱된 뷰 및 분할의 추가, 제거 또는 수정에 대한 권장 구성을 제공합니다.|  
|[DEA(데이터베이스 실험 도우미)](https://www.microsoft.com/download/details.aspx?id=54090)|DEA(데이터베이스 실험 도우미)는 SQL Server용 새 A/B 테스트 솔루션입니다. 지정된 워크로드에 대한 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 대상 버전의 평가를 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이전 버전([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]로 시작)에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 모든 최신 버전으로 업그레이드할 때 DEA는 비교 분석 메트릭을 제공할 수 있습니다.|
|오류 로그|Windows 애플리케이션 이벤트 로그는 Windows Server 및 Windows 운영 체제 전체에서 발생하는 이벤트뿐만 아니라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트의 이벤트와 전체 텍스트 검색을 전반적으로 보여 줍니다. 이 이벤트 로그에는 다른 곳에서 사용할 수 없는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 이벤트 정보가 포함됩니다. 오류 로그에 있는 정보를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 관련 있는 문제를 해결할 수 있습니다.|  
|[확장 이벤트](../../relational-databases/extended-events/extended-events.md)|확장 이벤트는 성능 리소스를 적게 사용하는 간단한 성능 모니터링 시스템입니다. 확장 이벤트는 세 가지 그래픽 사용자 인터페이스(새 세션 마법사, 새 세션 및 XE 프로파일러)를 제공하여 세션 데이터를 작성, 수정, 표시 및 분석할 수 있습니다.|  
|[실행 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)|실행 관련 DMV를 사용하면 실행 관련 정보를 검색할 수 있습니다.|
|[LQS(활성 쿼리 통계)](../../relational-databases/performance/live-query-statistics.md)|쿼리 실행 단계에 대한 실시간 통계를 표시합니다. 이 데이터는 쿼리를 실행하는 동안 사용할 수 있으므로 이 실행 통계는 쿼리 성능 문제를 디버깅할 때 매우 유용합니다.|  
|[리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)|시스템 모니터는 주로 사용 중인 버퍼 관리자 페이지 요청 수 같은 리소스 사용을 추적하므로 이벤트를 모니터링할 미리 정의된 개체와 카운터 또는 사용자 정의된 카운터를 사용하여 서버 성능과 작업을 모니터링할 수 있습니다. 시스템 모니터(Microsoft Windows NT 4.0의 성능 모니터)는 이벤트에 대한 데이터(예: 메모리 사용량, 활성 트랜잭션 수, 차단된 잠금 수 또는 CPU 작업)보다는 개수와 속도를 수집합니다. 특정 카운터에 대해 운영자에게 경고 메시지를 보내도록 임계값을 설정할 수도 있습니다.<br /><br /> 시스템 모니터는 Microsoft Windows Server 및 Windows 운영 체제에서 작동합니다. 시스템 모니터는 Windows NT 4.0 이상에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 원격 또는 로컬로 모니터링할 수 있습니다.<br /><br /> [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 및 시스템 모니터의 주요 차이점은 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 는 데이터베이스 엔진 이벤트를 모니터링하지만 시스템 모니터는 서버 프로세스와 연관된 리소스 사용량을 모니터링하는 것입니다.|  
|[작업 모니터 열기&#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 의 작업 모니터는 현재 활동의 임시 보기에 유용하고 다음에 대한 정보를 그래픽으로 표시합니다.<br /><br />- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 실행 중인 프로세스<br />- 차단된 프로세스<br />- 잠금<br />- 사용자 작업|  
|[성능 대시보드](../../relational-databases/performance/performance-dashboard.md)|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 성능 대시보드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 현재 성능 병목 상태가 있는지 여부를 신속하게 식별하는 데 도움이 됩니다.|  
|[QTA(쿼리 튜닝 도우미)](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)|[쿼리 저장소 사용 시나리오](../../relational-databases/performance/query-store-usage-scenarios.md#CEUpgrade)의 *SQL Server의 최신 버전으로 업그레이드하는 동안 성능 안정성 유지* 섹션에 설명된 대로 QTA(쿼리 튜닝 도우미) 기능은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 최신 버전으로 업그레이드하는 동안 성능 안정성을 유지하기 위해 사용자에게 권장된 워크플로를 안내합니다. |  
|[쿼리 저장소](../..//relational-databases/performance/monitoring-performance-by-using-the-query-store.md)|쿼리 저장소 기능은 사용자에게 쿼리 계획 선택 및 성능에 대한 인사이트를 제공합니다. 쿼리 계획 변경으로 인해 발생하는 성능 차이를 신속하게 찾을 수 있도록 하여 성능 문제 해결을 간소화합니다. 쿼리 저장소는 쿼리, 계획 및 런타임 통계의 기록을 자동으로 캡처하고 사용자 검토를 위해 보관합니다. 데이터를 기간별로 구분하여 데이터베이스 사용 패턴을 파악하고 서버에서 쿼리 계획 변경이 발생한 시기를 이해할 수 있게 해줍니다.|
|[SQL 추적](../../relational-databases/sql-trace/sql-trace.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저는 다음과 같습니다.<br /><br /> [sp_trace_create&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)<br />[sp_trace_generateevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)<br />[sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)<br />[sp_trace_setfilter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)<br />[sp_trace_setstatus&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)|  
|[SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay는 여러 컴퓨터를 통해 추적 데이터를 재생하여 중요 업무용 워크로드를 시뮬레이트할 수 있습니다.|  
|[sp_trace_setfilter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 는 일괄 처리나 트랜잭션 시작 같은 엔진 프로세스 이벤트를 추적하므로 서버와 데이터베이스 작업(예: 교착 상태, 치명적 오류 또는 로그인 작업)을 모니터링할 수 있습니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블이나 파일에 캡처하여 나중에 분석할 수 있으며, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 캡처된 이벤트를 단계별로 재생하여 발생한 이벤트를 정확히 확인할 수도 있습니다.|  
|[시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)|다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 저장 프로시저는 다양한 모니터링 태스크에 대한 강력한 대체 방법을 제공합니다.<br /><br /> [sp_who&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md):<br />                    현재 실행 중인 문을 포함한 현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자와 프로세스에 대한 스냅샷 정보 및 문의 차단 여부를 보고합니다.<br /><br /> [sp_lock&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md):<br />                    개체 ID, 인덱스 ID, 잠금 유형, 잠금이 적용되는 유형이나 리소스에 대한 스냅샷 정보를 보고합니다.<br /><br /> [sp_spaceused&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md): <br />                    테이블이나 전체 데이터베이스가 사용 중인 현재 예상 디스크 공간의 양을 보여 줍니다.<br /><br /> [sp_monitor&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md):<br />                    **sp_monitor** 가 마지막으로 실행된 이후의 CPU 사용량, I/O 사용량 및 유휴 시간 양을 포함하는 통계를 표시합니다.|  
|[추적 플래그&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)|추적 플래그는 서버에서 특정 작업에 대한 정보를 표시하며 문제점이나 교착 상태 체인과 같은 성능 문제를 진단하는 데 사용됩니다.|  
  
## <a name="choosing-a-monitoring-tool"></a>모니터링 도구 선택  
 모니터링 도구 선택은 모니터링할 이벤트나 작업에 따라 결정됩니다.  
  
|이벤트/작업|확장 이벤트|SQL Server Profiler|Distributed Replay|시스템 모니터|작업 모니터|Transact-SQL|오류 로그|성능 대시보드|  
|-----------------------|-----------------------|-------------------------|------------------------|--------------------|----------------------|-------------------|----------------|----------------|   
|추세 분석|yes|yes||yes|||||  
|캡처한 이벤트 재생||예(단일 컴퓨터에서)|예(여러 컴퓨터에서)||||||  
|임시 모니터링|예<sup>1</sup>|yes|||yes|yes|yes|yes|  
|경고 생성||||yes|||||  
|그래픽 인터페이스|yes|yes||yes|yes||yes|yes|  
|사용자 지정 애플리케이션에서 사용|yes|예<sup>2</sup>||||yes|||  
  
 <sup>1</sup>[SQL Server Management Studio XEvent 프로파일러](../../relational-databases/extended-events/use-the-ssms-xe-profiler.md)   사용  
 <sup>2</sup>[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 시스템 저장 프로시저 사용.  
  
## <a name="windows-monitoring-tools"></a>Windows 모니터링 도구  
 Windows 운영 체제와 Windows Server 2003에서도 다음과 같은 모니터링 도구를 제공합니다.  
  
|도구|Description|  
|----------|-----------------|  
|작업 관리자|시스템에서 실행 중인 프로세스 및 애플리케이션의 개요를 보여 줍니다.|  
|네트워크 모니터 에이전트|네트워크 트래픽을 모니터링합니다.|  
  
 Windows 운영 체제나 Windows Server 도구에 대한 자세한 내용은 Windows 설명서를 참조하십시오.  
  
  
