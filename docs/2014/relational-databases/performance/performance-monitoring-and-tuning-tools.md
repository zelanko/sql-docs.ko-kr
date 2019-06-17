---
title: 성능 모니터링 및 튜닝 도구 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 179944412ed72bc0055bf5c47b788a3a929e9844
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150831"
---
# <a name="performance-monitoring-and-tuning-tools"></a>성능 모니터링 및 튜닝 도구
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 이벤트를 모니터링하고 물리적 데이터베이스 디자인을 튜닝하는 여러 가지 도구를 제공합니다. 도구를 선택하는 기준은 수행된 모니터링 또는 튜닝 유형과 모니터링할 이벤트에 따라 결정됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 모니터링 및 튜닝 도구는 다음과 같습니다.  
  
|도구|Description|  
|----------|-----------------|  
|[sp_trace_setfilter&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql)|[!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 는 일괄 처리나 트랜잭션 시작 같은 엔진 프로세스 이벤트를 추적하므로 서버와 데이터베이스 작업(예: 교착 상태, 치명적 오류 또는 로그인 작업)을 모니터링할 수 있습니다. [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블이나 파일에 캡처하여 나중에 분석할 수 있으며, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 캡처된 이벤트를 단계별로 재생하여 발생한 이벤트를 정확히 확인할 수도 있습니다.|  
|[SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay를 사용하면 여러 컴퓨터를 사용해 추적 데이터를 재생하여 중요한 작업을 효율적으로 시뮬레이트할 수 있습니다.|  
|[리소스 사용 모니터링&#40;시스템 모니터&#41;](../performance-monitor/monitor-resource-usage-system-monitor.md)|시스템 모니터는 주로 사용 중인 버퍼 관리자 페이지 요청 수 같은 리소스 사용을 추적하므로 이벤트를 모니터링할 미리 정의된 개체와 카운터 또는 사용자 정의된 카운터를 사용하여 서버 성능과 작업을 모니터링할 수 있습니다. 시스템 모니터(Microsoft Windows NT 4.0의 성능 모니터)는 이벤트에 대한 데이터(예: 메모리 사용량, 활성 트랜잭션 수, 차단된 잠금 수 또는 CPU 작업)보다는 개수와 속도를 수집합니다. 특정 카운터에 대해 운영자에게 경고 메시지를 보내도록 임계값을 설정할 수도 있습니다.<br /><br /> 시스템 모니터는 Microsoft Windows Server 및 Windows 운영 체제에서 작동합니다. 시스템 모니터는 Windows NT 4.0 이상에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 원격 또는 로컬로 모니터링할 수 있습니다.<br /><br /> [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 및 시스템 모니터의 주요 차이점은 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 는 데이터베이스 엔진 이벤트를 모니터링하지만 시스템 모니터는 서버 프로세스와 연관된 리소스 사용량을 모니터링하는 것입니다.|  
|[작업 모니터 열기&#40;SQL Server Management Studio&#41;](../performance-monitor/open-activity-monitor-sql-server-management-studio.md)|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 의 작업 모니터는 현재 활동의 임시 보기에 유용하고 다음에 대한 정보를 그래픽으로 표시합니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 실행 중인 프로세스<br /><br /> 차단된 프로세스<br /><br /> 잠금<br /><br /> 사용자 작업|  
|[SQL 추적](../sql-trace/sql-trace.md)|[!INCLUDE[tsql](../../../includes/tsql-md.md)] 저장 프로시저는 다음과 같습니다.<br /><br /> [sp_trace_create&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql)<br /><br /> [sp_trace_generateevent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql)<br /><br /> [sp_trace_setevent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)<br /><br /> [sp_trace_setfilter&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql)<br /><br /> [sp_trace_setstatus&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)|  
|오류 로그|Windows 애플리케이션 이벤트 로그는 Windows Server 및 Windows 운영 체제 전체에서 발생하는 이벤트뿐만 아니라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트의 이벤트와 전체 텍스트 검색을 전반적으로 보여 줍니다. 이 이벤트 로그에는 다른 곳에서 사용할 수 없는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 이벤트 정보가 포함됩니다. 오류 로그에 있는 정보를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 관련 있는 문제를 해결할 수 있습니다.|  
|[시스템 저장 프로시저&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)|다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 저장 프로시저는 다양한 모니터링 태스크에 대한 강력한 대체 방법을 제공합니다.<br /><br /> [sp_who&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-who-transact-sql): <br />                    현재 실행 중인 문을 포함한 현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자와 프로세스에 대한 스냅숏 정보 및 문의 차단 여부를 보고합니다.<br /><br /> [sp_lock&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-lock-transact-sql): 개체 ID, 인덱스 ID, 잠금 유형, 잠금이 적용되는 유형이나 리소스에 대한 스냅숏 정보를 보고합니다.<br /><br /> [sp_spaceused&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql): 테이블이나 전체 데이터베이스가 사용 중인 현재 예상 디스크 공간의 양을 보여 줍니다.<br /><br /> [sp_monitor&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-monitor-transact-sql): **sp_monitor** 가 마지막으로 실행된 이후의 CPU 사용량, I/O 사용량 및 유휴 시간 양을 포함하는 통계를 표시합니다.|  
|[DBCC&#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-transact-sql)|DBCC(데이터베이스 콘솔 명령) 문을 사용하면 성능 통계 및 데이터베이스의 논리적, 물리적 일관성을 검사할 수 있습니다.|  
|[기본 제공 함수s&#40;Transact-SQL&#41;](/sql/t-sql/functions/functions)|기본 제공 함수는 서버가 시작된 이후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업에 대한 스냅숏 통계를 표시하며 이러한 통계는 미리 정의된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 카운터에 저장됩니다. 예를 들어 **@@CPU_BUSY** 에는 CPU가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 코드를 실행한 시간이 포함되고 **@@CONNECTIONS** 에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 수나 시도 횟수가 포함되며 **@@PACKET_ERRORS** 에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결에서 발생한 네트워크 패킷 수가 포함됩니다.|  
|[추적 플래그&#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)|추적 플래그는 서버에서 특정 작업에 대한 정보를 표시하며 문제점이나 교착 상태 체인과 같은 성능 문제를 진단하는 데 사용됩니다.|  
|[데이터베이스 엔진 튜닝 관리자](database-engine-tuning-advisor.md)|데이터베이스 엔진 튜닝 관리자는 튜닝할 데이터베이스에 대해 실행된 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문의 성능 영향을 분석합니다. 데이터베이스 엔진 튜닝 관리자는 인덱스, 인덱싱된 뷰 및 분할의 추가, 제거 또는 수정에 대한 권장 구성을 제공합니다.|  
  
## <a name="choosing-a-monitoring-tool"></a>모니터링 도구 선택  
 모니터링 도구 선택은 모니터링할 이벤트나 작업에 따라 결정됩니다.  
  
|이벤트/작업|SQL Server 프로파일러|Distributed Replay|시스템 모니터|작업 모니터|Transact-SQL|오류 로그|  
|-----------------------|-------------------------|------------------------|--------------------|----------------------|-------------------|----------------|  
|추세 분석|사용자 계정 컨트롤||사용자 계정 컨트롤||||  
|캡처한 이벤트 재생|예(단일 컴퓨터에서)|예(여러 컴퓨터에서)|||||  
|임시 모니터링|사용자 계정 컨트롤|||예|예|사용자 계정 컨트롤|  
|경고 생성|||사용자 계정 컨트롤||||  
|그래픽 인터페이스|사용자 계정 컨트롤||예|예||사용자 계정 컨트롤|  
|사용자 지정 애플리케이션에서 사용|예 <sup>1</sup>||||사용자 계정 컨트롤||  
  
 <sup>1</sup> 사용 하 여 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 시스템 저장 프로시저입니다.  
  
## <a name="windows-monitoring-tools"></a>Windows 모니터링 도구  
 Windows 운영 체제와 Windows Server 2003에서도 다음과 같은 모니터링 도구를 제공합니다.  
  
|도구|Description|  
|----------|-----------------|  
|작업 관리자|시스템에서 실행 중인 프로세스 및 애플리케이션의 개요를 보여 줍니다.|  
|네트워크 모니터 에이전트|네트워크 트래픽을 모니터링합니다.|  
  
 Windows 운영 체제나 Windows Server 도구에 대한 자세한 내용은 Windows 설명서를 참조하십시오.  
  
  
