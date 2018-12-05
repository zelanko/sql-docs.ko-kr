---
title: SQL Server Distributed Replay | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- Distributed Replay
- SQL Server Distributed Replay
ms.assetid: 58ef7016-b105-42c2-90a0-364f411849a4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 900fdcafe18c2a885ea7191ce8619e46e8f0f963
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52531821"
---
# <a name="sql-server-distributed-replay"></a>SQL Server Distributed Replay
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 기능을 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업그레이드에 따르는 영향을 쉽게 평가할 수 있습니다. 또한 하드웨어 및 운영 체제 업그레이드와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 튜닝에 따르는 영향도 쉽게 평가할 수 있습니다.  
  
## <a name="benefits-of-distributed-replay"></a>Distributed Replay의 이점  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]와 마찬가지로 Distributed Replay를 사용하면 캡처된 추적을 업그레이드된 테스트 환경에 대해 재생할 수 있습니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]와 달리 Distributed Replay는 여러 컴퓨터의 작업을 재생할 수 있습니다.  
  
 Distributed Replay는 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]보다 확장성이 뛰어난 솔루션을 제공합니다. Distributed Replay를 사용하면 여러 컴퓨터의 작업을 재생하고 중요한 작업을 효율적으로 시뮬레이션할 수 있습니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 기능은 여러 컴퓨터를 사용하여 추적 데이터를 재생하고 중요 업무용 작업을 시뮬레이트할 수 있습니다. 응용 프로그램 호환성 테스트, 성능 테스트 또는 용량 계획에 Distributed Replay를 사용할 수 있습니다.  
  
## <a name="when-to-use-distributed-replay"></a>Distributed Replay를 사용하는 경우  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 와 Distributed Replay는 기능이 일부 중복됩니다.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하면 캡처된 추적을 업그레이드된 테스트 환경에 대해 재생할 수 있습니다. 재생 결과를 분석하여 잠재적인 기능 및 성능 관련 비호환성 문제가 있는지도 검토할 수 있습니다. 그러나 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 는 단일 컴퓨터에서만 작업을 재생할 수 있습니다. 리소스를 많이 사용하는 OLTP 응용 프로그램(활성 동시 연결 수가 많거나 처리량이 많음)을 재생할 때는 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 로 인해 리소스 병목 상태가 야기될 수 있습니다.  
  
 Distributed Replay는 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]보다 확장성이 뛰어난 솔루션을 제공합니다. Distributed Replay를 사용하면 여러 컴퓨터의 작업을 재생하고 중요한 작업을 효율적으로 시뮬레이션할 수 있습니다.  
  
 다음 표에서는 각 도구를 사용하는 경우에 대해 설명합니다.  
  
|도구|사용 시기...|  
|----------|---------------|  
|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]|단일 컴퓨터에서 기본 재생 메커니즘을 사용하려는 경우. 특히 **단계**, **커서까지 실행**및 **중단점 설정/해제** 명령과 같은 줄 단위 디버깅 기능이 필요합니다.<br /><br /> [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 추적을 재생하려는 경우|  
|Distributed Replay|응용 프로그램 호환성을 평가하려는 경우. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 운영 체제 업그레이드 시나리오, 하드웨어 업그레이드 또는 인덱스 튜닝을 테스트하려는 경우입니다.<br /><br /> 캡처된 추적의 동시성이 너무 높아 단일 재생 클라이언트로는 시뮬레이션할 수 없는 경우|  
  
## <a name="distributed-replay-concepts"></a>Distributed Replay 개념  
 Distributed Replay 환경을 구성하는 요소는 다음과 같습니다.  
  
-   **Distributed Replay 관리 도구**: Distributed Replay Controller와 통신하는 데 사용되는 콘솔 응용 프로그램 **DReplay.exe**. 관리 도구를 사용하여 Distributed Replay를 제어할 수 있습니다.  
  
-   **Distributed Replay Controller**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller라는 Windows 서비스를 실행하는 컴퓨터. Distributed Replay Controller는 Distributed Replay Client의 동작을 조정합니다. 각 Distributed Replay 환경에는 컨트롤러 인스턴스가 하나만 있을 수 있습니다.  
  
-   **Distributed Replay Client**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client라는 Windows 서비스를 실행하는 하나 이상의 컴퓨터(물리적 또는 가상). 여러 Distributed Replay Client가 함께 작동하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대해 작업을 시뮬레이션합니다. 각 Distributed Replay 환경에 하나 이상의 클라이언트가 있을 수 있습니다.  
  
-   **대상 서버**: Distributed Replay Client가 추적 데이터를 재생하는 데 사용할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스. 테스트 환경에 대상 서버를 배치하는 것이 좋습니다.  
  
 Distributed Replay 관리 도구, Controller 및 Client를 서로 다른 컴퓨터에 설치하거나 동일한 컴퓨터에 설치할 수 있습니다. Distributed Replay Controller 또는 Client 서비스 인스턴스는 동일한 컴퓨터에서 하나만 실행할 수 있습니다.  
  
 다음 그림은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 물리적 아키텍처를 보여 줍니다.  
  
 ![Distributed Replay 아키텍처](../../tools/distributed-replay/media/distributedreplayarch.gif "Distributed Replay 아키텍처")  
  
## <a name="distributed-replay-tasks"></a>Distributed Replay 태스크  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|Distributed Replay를 구성하는 방법에 대해 설명합니다.|[Distributed Replay 구성](../../tools/distributed-replay/configure-distributed-replay.md)|  
|입력 추적 데이터를 준비하는 방법에 대해 설명합니다.|[입력 추적 데이터 준비](../../tools/distributed-replay/prepare-the-input-trace-data.md)|  
|추적 데이터를 재생하는 방법에 대해 설명합니다.|[추적 데이터 재생](../../tools/distributed-replay/replay-trace-data.md)|  
|Distributed Replay 추적 데이터 결과를 검토하는 방법에 대해 설명합니다.|[재생 결과 검토](../../tools/distributed-replay/review-the-replay-results.md)|  
|관리 도구를 사용하여 컨트롤러에서 작업을 시작, 모니터링 및 취소하는 방법에 대해 설명합니다.|[관리 도구 명령줄 옵션&#40;Distributed Replay Utility&#41;](../../tools/distributed-replay/administration-tool-command-line-options-distributed-replay-utility.md)|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Distributed Replay 포럼](https://social.technet.microsoft.com/Forums/sl/sqldru/)   
 [Distributed Replay를 사용하여 SQL Server 테스트 로드 - 2단계](https://blogs.msdn.com/b/mspfe/archive/2012/11/14/using-distributed-replay-to-load-test-your-sql-server-part-2.aspx)   
 [Distributed Replay를 사용하여 SQL Server 테스트 로드 - 1단계](https://blogs.msdn.com/b/mspfe/archive/2012/11/08/using-distributed-replay-to-load-test-your-sql-server-part-1.aspx)  
  
  
