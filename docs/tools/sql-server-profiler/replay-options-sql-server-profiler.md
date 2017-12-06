---
title: "재생 옵션 (SQL Server Profiler) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- traces [SQL Server], replaying
- replaying traces
- health monitor [SQL Server]
- Replay Configuration dialog box
ms.assetid: 58761a25-a84f-4a90-9c61-97700bc5ad9c
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1e3f6fd0521be0b607a35fe2fd05089e116c9d54
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="replay-options-sql-server-profiler"></a>재생 옵션(SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]캡처된 추적을 재생 하기 전에 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]에서 재생 옵션을 지정 된 **재생 구성** 대화 상자. 이 대화 상자를 열려면 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]에서 추적 파일이나 테이블을 연 다음 **재생** 메뉴에서 **시작**을 클릭합니다. 추적 재생에 필요한 권한에 대한 자세한 내용은 [Permissions Required to Run SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)을 참조하십시오.  
  
 이 항목에서는 **재생 구성** 대화 상자에서 지정할 수 있는 옵션에 대해 설명합니다.  
  
> [!NOTE]  
>  리소스를 많이 사용하는 OLTP 응용 프로그램(활성 동시 연결 수가 많거나 처리량이 많음)을 재생하는 데는 Distributed Replay Utility를 사용하는 것이 좋습니다. Distributed Replay Utility는 여러 컴퓨터의 추적 데이터를 재생할 수 있으므로 중요한 작업을 효율적으로 시뮬레이션할 수 있습니다. 자세한 내용은 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)을 참조하세요.  
  
## <a name="basic-replay-options"></a>기본 재생 옵션  
 **서버 재생**  
 서버는 추적을 재생할 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다. 서버는 [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md)에서 설명하는 재생 요구 사항을 충족해야 합니다.  
  
 **파일에 저장**  
 나중에 볼 수 있도록 추적 재생의 결과가 기록되는 출력 파일입니다. 기본적으로 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 는 추적 재생의 결과만 화면에 표시합니다.  
  
 **테이블에 저장**  
 나중에 볼 수 있도록 추적 재생의 결과가 기록되는 데이터베이스 테이블입니다.  
  
 **재생 스레드 수**  
 동시에 사용할 재생 스레드 수를 지정합니다. 지정한 수가 클수록 재생 중에 리소스가 많이 사용되지만 재생은 빨라집니다. 여러 스레드를 사용하면 이벤트 순서가 유지되지 않을 수도 있습니다.  
  
 **추적한 순서대로 이벤트를 재생합니다.**  
 각 추적을 단계별로 실행하는 것과 같은 디버깅 방법을 사용할 수 있습니다. 이 옵션을 선택하지 않으면 이벤트가 원래 캡처된 순서와 일치하는 순서로 재생되도록 보장할 수 없습니다.  
  
 **여러 스레드를 사용하여 이벤트를 재생합니다.**  
 성능을 최적화하고 디버깅할 수 없도록 합니다. 이벤트는 특정 서버 프로세스 ID(SPID)에 기록된 순서로 재생되지만 SPID의 순서는 보장되지 않습니다.  
  
 **재생 결과 표시**  
 재생 결과를 표시합니다. 이 옵션이 기본 옵션입니다. 재생 중인 추적의 용량이 클 경우에는 이 옵션을 해제하여 디스크 공간을 절약할 수 있습니다.  
  
> [!NOTE]  
>  최고의 재생 성능을 위해 여러 스레드를 사용하여 이벤트를 재생하고 재생 결과는 표시하지 않도록 선택하는 것이 좋습니다.  
  
## <a name="advanced-replay-options"></a>고급 재생 옵션  
 **시스템 SPID 재생**  
 모든 SPID를 재생합니다. 이 옵션이 기본 옵션입니다.  
  
 **한 SPID만 재생**  
 목록에서 선택한 SPID 번호만 재생합니다.  
  
 **날짜 및 시간별 재생 제한**  
 지정된 **시작 시간** 과 **종료 시간**에 대한 추적을 재생합니다.  
  
 **상태 모니터 대기 간격**  
 상태 모니터에서 프로세스를 종료하기 전에 프로세스가 실행될 수 있는 시간을 설정합니다.  
  
 **상태 모니터 폴링 간격**  
 상태 모니터에서 종료 후보에 대해 폴링하는 간격을 설정합니다.  
  
 **SQL Server 차단된 프로세스 모니터 설정**  
 차단된 프로세스 모니터에서 차단되었거나 차단 중인 프로세스를 검색하는 빈도를 설정합니다.  
  
## <a name="about-the-health-monitor"></a>상태 모니터 정보  
 상태 모니터는 추적 재생의 시뮬레이션된 프로세스를 모니터링하고 재생 내에서 차단된 프로세스를 종료하는 응용 프로그램 스레드입니다. **재생 구성** 대화 상자의 **고급 재생 옵션** 탭에서 차단된 프로세스를 끝내기 전에 상태 모니터가 대기해야 하는 시간(**상태 모니터 대기 간격**)을 초 단위로 지정할 수 있습니다. 이 간격을 0으로 설정하면 상태 모니터가 재생 추적에서 시뮬레이션된 차단 프로세스를 종료하지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [추적 재생](../../tools/sql-server-profiler/replay-traces.md)   
 [재생 요구 사항](../../tools/sql-server-profiler/replay-requirements.md)   
 [추적 재생에 대한 고려 사항&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/considerations-for-replaying-traces-sql-server-profiler.md)  
  
  
