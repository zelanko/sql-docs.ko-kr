---
title: SQL Server 구성 요소 모니터링 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e8f1b16b-ea40-4e12-886c-967ebda4e6e4
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 64eb2996426561b4bc83cc246058e4bef7c9c3ac
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="monitor-sql-server-components"></a>SQL Server 구성 요소 모니터링
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 동적 환경에서 서비스를 제공하기 때문에 모니터링이 매우 중요합니다. 응용 프로그램에 있는 데이터가 바뀌고, 사용자가 필요로 하는 액세스 유형이 바뀌고, 사용자가 연결하는 방법이 바뀔 뿐 아니라, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 액세스하는 응용 프로그램의 유형도 바뀔 수 있으나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 메모리나 디스크 공간 같은 시스템 수준의 리소스를 자동으로 관리하므로 시스템 수준의 상세한 수동 튜닝의 필요성은 최소한으로 줄일 수 있습니다. 모니터링을 통해 관리자는 성능 추세를 확인하여 변경이 필요한지 파악할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 구성 요소를 효과적으로 모니터링하려면  
  
1.  모니터링 목표를 결정합니다.  
  
2.  적절한 도구를 선택합니다.  
  
3.  모니터링할 구성 요소를 식별합니다.  
  
4.  모니터링되는 구성 요소의 메트릭을 선택합니다.  
  
5.  서버를 모니터링합니다.  
  
6.  데이터를 분석합니다.  
  
 이러한 각 단계에 대한 설명은 다음과 같습니다.  
  
## <a name="determine-your-monitoring-goals"></a>모니터링 목표 결정  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 효과적으로 모니터링하려면 모니터링하는 이유를 분명하게 식별해야 합니다. 다음과 같은 이유가 있을 수 있습니다.  
  
-   성능에 대한 기준선을 마련합니다.  
  
-   시간에 따라 성능이 어떻게 변하는지 확인합니다.  
  
-   특정 성능 문제를 진단합니다.  
  
-   최적화할 구성 요소나 프로세스를 식별합니다.  
  
-   여러 클라이언트 응용 프로그램의 성능에 대한 영향을 비교해 봅니다.  
  
-   사용자 작업을 감사합니다.  
  
-   서로 다른 부하 상태에서 서버를 테스트합니다.  
  
-   데이터베이스 아키텍처를 테스트합니다.  
  
-   유지 관리 일정을 테스트합니다.  
  
-   백업 및 복원 계획을 테스트합니다.  
  
-   하드웨어 구성을 수정할 시점을 결정합니다.  
  
## <a name="select-the-appropriate-tool"></a>적절한 도구 선택  
 모니터링 이유를 결정했으면 해당 모니터링 유형에 적절한 도구를 선택해야 합니다. Windows 운영 체제와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 트랜잭션이 많은 환경에서 서버를 모니터링할 수 있는 완전한 도구 집합을 제공합니다. 이러한 도구를 통해 SQL Server 데이터베이스 엔진의 인스턴스나 SQL Server Analysis Services 인스턴스의 상태를 분명하게 알 수 있습니다.  
  
 Windows에서는 서버에서 실행되는 응용 프로그램을 모니터링할 수 있는 다음과 같은 도구를 제공합니다.  
  
-   시스템 모니터. 이 도구를 사용하면 메모리, 디스크 및 프로세서 사용 등 작업에 대한 실시간 데이터를 수집하고 확인할 수 있습니다.  
  
-   성능 로그 및 경고  
  
-   작업 관리자  
  
 Windows Server 또는 Windows 도구에 대한 자세한 내용은 Windows 설명서를 참조하십시오.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 구성 요소를 모니터링할 수 있는 다음과 같은 도구를 제공합니다.  
  
-   SQL 추적  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]  
  
-   Distributed Replay Utility  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 작업 모니터  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 그래픽 실행 계획  
  
-   저장 프로시저  
  
-   DBCC(데이터베이스 콘솔 명령)  
  
-   기본 제공 함수  
  
-   추적 플래그  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 모니터링 도구에 대한 자세한 내용은 [성능 모니터링 및 튜닝 도구](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)를 참조하세요.  
  
## <a name="identify-the-components-to-monitor"></a>모니터링할 구성 요소 식별  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 모니터링하기 위한 세 번째 단계는 모니터링할 구성 요소를 식별하는 것입니다. 예를 들어 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하여 서버를 추적할 경우 추적을 정의하여 특정 이벤트에 대한 데이터를 수집할 수 있습니다. 해당 상황에 적용되지 않는 이벤트는 제외할 수도 있습니다.  
  
## <a name="select-metrics-for-monitored-components"></a>모니터링되는 구성 요소의 메트릭 선택  
 모니터링할 구성 요소를 식별했으면 모니터링할 구성 요소의 메트릭을 결정합니다. 예를 들어 추적에 포함할 이벤트를 선택한 후 이벤트에 대한 특정 데이터만 포함하도록 선택할 수 있습니다. 추적에 관련된 데이터로 추적을 제한하면 추적하는 데 필요한 시스템 리소스를 최소한으로 줄일 수 있습니다.  
  
## <a name="monitor-the-server"></a>서버 모니터링  
 서버를 모니터링하려면 구성한 모니터링 도구를 실행하여 데이터를 수집합니다. 예를 들어 추적을 정의한 후에 추적을 실행하여 서버에서 발생한 이벤트에 대한 데이터를 수집할 수 있습니다.  
  
## <a name="analyze-the-data"></a>데이터 분석  
 추적을 마친 후에 데이터를 분석하여 모니터링 목표가 이루어졌는지 확인할 수 있습니다. 목표가 이루어지지 않았으면 서버를 모니터링하는 데 사용한 구성 요소나 메트릭을 수정합니다.  
  
 다음은 이벤트 데이터를 캡처하고 사용하는 데 관련된 프로세스를 요약하여 설명한 것입니다.  
  
1.  필터를 적용하여 수집한 이벤트 데이터를 제한합니다.  
  
     이벤트 데이터를 제한하면 모니터링 시나리오에 맞는 특정 이벤트에 시스템의 포커스를 맞출 수 있습니다. 예를 들어 처리 속도가 느린 쿼리를 모니터링할 때는 응용 프로그램에서 실행한 쿼리가 특정 데이터베이스에 대해 실행되는 데 30초 이상 걸리는 경우만 모니터링하는 필터를 사용할 수 있습니다. 자세한 내용은 [추적 필터 설정&#40;Transact-SQL&#41;](../../relational-databases/sql-trace/set-a-trace-filter-transact-sql.md) 및 [추적에서의 이벤트 필터링&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)을 참조하세요.  
  
2.  이벤트를 모니터링(캡처)합니다.  
  
     모니터링을 설정하면 활성 모니터링은 지정한 응용 프로그램, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스 또는 운영 체제에서 데이터를 즉시 캡처합니다. 예를 들어 시스템 모니터를 사용하여 디스크 작업을 모니터링하면 디스크 읽기 및 쓰기 같은 이벤트 데이터가 캡처되고 해당 데이터가 화면에 표시됩니다. 자세한 내용은 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)을 참조하세요.  
  
3.  캡처한 이벤트 데이터를 저장합니다.  
  
     캡처한 이벤트 데이터를 저장하면 나중에 분석하거나 Distributed Replay Utility 또는 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 재생할 수도 있습니다. 캡처한 이벤트 데이터는 원래 분석용으로 만든 도구로 다시 로드할 수 있는 파일에 저장됩니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 는 이벤트 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 저장할 수 있습니다. 캡처한 이벤트 데이터를 저장하는 것은 성능 기준선을 만들 때 중요합니다. 성능 기준선 데이터를 저장하면 최근 캡처한 이벤트 데이터와 비교하여 성능이 최적인지 확인할 수 있습니다. 자세한 내용은 [SQL Server Profiler 템플릿 및 권한](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)을 참조하세요.  
  
4.  이벤트를 캡처하도록 설정이 지정된 추적 템플릿을 만듭니다.  
  
     추적 템플릿에는 이벤트 자체, 이벤트 데이터 및 데이터를 캡처하는 데 사용하는 필터에 대한 정보가 포함됩니다. 이 템플릿을 사용하면 나중에 특정 이벤트 집합을 모니터링할 때 이벤트, 이벤트 데이터 및 필터를 다시 정의할 필요가 없습니다. 예를 들어 교착 상태 수와 교착 상태에 있는 사용자 수를 모니터링할 경우 해당 이벤트, 이벤트 데이터 및 이벤트 필터를 정의하는 템플릿을 만들어 저장해 두면 다음에 교착 상태를 모니터링할 때 해당 필터를 다시 적용할 수 있습니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 는 추적 템플릿을 이 용도로 사용합니다. 자세한 내용은 [추적 정의 기본값 설정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md) 및 [추적 템플릿 만들기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)를 참조하세요.  
  
5.  캡처한 이벤트 데이터를 분석합니다.  
  
     데이터 분석을 위해 캡처한 이벤트 데이터가 해당 데이터를 캡처한 응용 프로그램으로 로드됩니다. 예를 들어 확인 및 분석을 위해 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에서 캡처한 추적을 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 로 다시 로드할 수 있습니다. 자세한 내용은 [SQL Server Profiler를 사용하여 추적 보기 및 분석](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md)을 참조하세요.  
  
     이벤트 데이터를 분석하면 발생한 이벤트와 발생 원인을 알 수 있습니다. 이 정보를 사용하면 수행된 분석 유형에 따라 메모리를 추가하거나 인덱스를 변경하거나 Transact-SQL 문 또는 저장 프로시저의 코딩 문제를 수정하는 등 성능 향상에 필요한 사항을 변경할 수 있습니다. 예를 들어 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자를 사용하여 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에서 캡처한 추적을 분석하고 결과에 따라 인덱스 권장 구성을 만들 수 있습니다.  
  
6.  캡처한 이벤트 데이터를 재생합니다.  
  
     이벤트 재생을 사용하면 데이터를 캡처한 데이터베이스 환경의 테스트 복사본을 만들고 캡처한 이벤트를 실제 시스템에서 원래 발생했던 대로 반복할 수 있습니다. 이 기능은 Distributed Replay Utility나 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 통해서만 사용할 수 있습니다. 이벤트 재생 속도는 이벤트가 원래 발생한 속도와 같게 하거나 최대한 빠르게 하거나 한 번에 한 단계씩 재생하여 각 이벤트가 발생한 후 시스템을 분석할 수도 있습니다. 같은 이벤트를 테스트 환경에서 분석하여 프로덕션 시스템에 발생할 수 있는 해로운 상황을 미리 방지할 수 있습니다. 자세한 내용은 [추적 재생](../../tools/sql-server-profiler/replay-traces.md)을 참조하세요.  
  
  
