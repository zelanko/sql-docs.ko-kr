---
title: 복제 에이전트 관리 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Snapshot Agent, administering
- Log Reader Agent, administering
- Queue Reader Agent, administering
- shared agents [SQL Server replication]
- Merge Agent, administering
- Distribution Agent, administering
- agents [SQL Server replication], administering
- replication cleanup jobs [SQL Server]
- administering replication, agents
- replication [SQL Server], administering
- independent agents [SQL Server replication]
ms.assetid: f27186b8-b1b2-4da0-8b2b-91f632c2ab7e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 00fc90be42bddd7feb43d96c9110def4db60835c
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54130453"
---
# <a name="replication-agent-administration"></a>복제 에이전트 관리
  복제 에이전트는 스키마와 데이터의 복사본 만들기, 게시자 또는 구독자에서 업데이트 검색, 서버 간에 변경 내용 전파 등 복제와 관련된 많은 태스크를 수행합니다. 기본적으로 복제 에이전트는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 작업 단계에서 실행됩니다. 에이전트는 단순히 실행 파일이므로 명령줄 및 일괄 처리 스크립트에서 직접 호출할 수도 있습니다. 각 응용 프로그램 에이전트는 실행 방식을 제어하는 데 사용되는 일련의 런타임 매개 변수를 지원합니다. 이러한 매개 변수는 에이전트 프로필 또는 명령줄에서 지정됩니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가 설치될 때 사용자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 서비스를 자동으로 시작하도록 명시적으로 선택하지 않으면 기본적으로 이 서비스는 해제됩니다.  
  
 복제 에이전트 파일은 [!INCLUDE[ssInstallPathVar](../../../includes/ssinstallpathvar-md.md)]\COM에 있습니다. 다음 표에서는 복제 실행 파일과 파일 이름을 보여 줍니다. 에이전트에 대한 링크를 클릭하면 해당 매개 변수 참조가 나타납니다.  
  
|에이전트 실행 파일|파일 이름|  
|----------------------|---------------|  
|[복제 스냅숏 에이전트](replication-snapshot-agent.md)|snapshot.exe|  
|[Replication Distribution Agent](replication-distribution-agent.md)|distrib.exe|  
|[복제 로그 판독기 에이전트](replication-log-reader-agent.md)|logread.exe|  
|[복제 큐 판독기 에이전트](replication-queue-reader-agent.md)|qrdrsvc.exe|  
|[Replication Merge Agent](replication-merge-agent.md)|replmerg.exe|  
  
 복제 에이전트뿐만 아니라 복제에서도 여러 작업을 통해 예약 유지 관리와 요청 시 유지 관리를 수행할 수 있습니다.  
  
 **에이전트 및 유지 관리 작업을 실행하려면**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 및 복제 모니터: [복제 에이전트 시작 및 중지 &#40;SQL Server Management Studio&#41;](start-and-stop-a-replication-agent-sql-server-management-studio.md)합니다.  
  
-   복제 프로그래밍: [Replication Agent Executables Concepts](../concepts/replication-agent-executables-concepts.md)  
  
## <a name="agent-profiles"></a>에이전트 프로필  
 복제가 구성되면 에이전트 프로필 집합이 배포자에 설치됩니다. 에이전트 프로필에는 에이전트가 실행될 때마다 사용할 매개 변수 집합이 포함됩니다. 각 에이전트는 시작 과정 중에 배포자로 로그인하여 해당 프로필의 매개 변수에 대해 쿼리합니다. 복제는 각 에이전트에 대한 기본 프로필과 로그 판독기 에이전트, 배포 에이전트 및 병합 에이전트에 대한 미리 정의된 추가 프로필을 제공합니다. 제공된 프로필뿐 아니라 애플리케이션 요구 사항에 찾는 프로필을 만들 수 있습니다. 자세한 내용은 [Replication Agent Profiles](replication-agent-profiles.md)을(를) 참조하세요.  
  
 명령줄 매개 변수를 직접 지정하는 방법은 [복제 에이전트 실행 파일 개념](../concepts/replication-agent-executables-concepts.md)을 참조하세요.  
  
## <a name="monitoring-replication-agents"></a>복제 에이전트 모니터링  
 복제 모니터를 사용하여 복제 에이전트에 대한 정보를 보고 복제 에이전트와 연결된 태스크를 수행할 수 있습니다. 다음 목록에는 각 에이전트, 에이전트를 찾을 수 있는 복제 모니터의 탭 및 이러한 탭에 액세스하는 방법을 설명하는 항목에 대한 링크가 포함되어 있습니다.  
  
-   다음 에이전트는 복제 모니터에서 게시와 연결됩니다.  
  
    -   스냅숏 에이전트  
  
    -   로그 판독기 에이전트  
  
    -   큐 판독기 에이전트  
  
     이러한 에이전트와 연결된 정보 및 태스크는 **에이전트** 탭을 통해 액세스할 수 있습니다. 자세한 내용은 [정보 보기 및 태스크 수행 복제 모니터를 사용 하 여](../monitor/view-information-and-perform-tasks-replication-monitor.md)입니다.  
  
-   다음 에이전트는 복제 모니터에서 구독과 연결됩니다.  
  
    -   배포 에이전트  
  
    -   병합 에이전트  
  
     이러한 에이전트와 연결된 정보 및 태스크는 **구독 조사 목록** (각 게시자에 대 한 사용 가능) 또는 **모든 구독** 탭 (각 게시에 대 한 사용 가능). 자세한 내용은 [정보 보기 및 태스크 수행 복제 모니터를 사용 하 여](../monitor/view-information-and-perform-tasks-replication-monitor.md)입니다.  
  
## <a name="independent-and-shared-agents"></a>독립 및 공유 에이전트  
 독립 에이전트는 한 구독에 사용되는 에이전트입니다. 공유 에이전트는 여러 구독을 제공합니다. 동일한 공유 에이전트를 사용하는 여러 구독을 동기화해야 할 경우 기본적으로 여러 구독은 큐에서 대기하고 공유 에이전트가 한 번에 하나씩 구독을 처리합니다. 독립 에이전트는 구독에 동기화가 필요할 때마다 준비가 되어 있기 때문에 이를 사용하면 대기 시간이 줄어듭니다. 병합 복제는 항상 독립 에이전트를 사용하고 트랜잭션 복제는 새 게시 마법사에서 만든 게시에 대해 기본적으로 독립 에이전트를 사용합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 트랜잭션 복제가 기본적으로 공유 에이전트를 사용했습니다.  
  
## <a name="replication-maintenance-jobs"></a>복제 유지 관리 작업  
 복제는 다음 작업을 통해 예약 유지 관리와 요청 시 유지 관리를 수행합니다.  
  
|정리 작업|Description|기본 일정|  
|------------------|-----------------|----------------------|  
|에이전트 기록 정리: 배포|배포 데이터베이스에서 복제 에이전트 기록을 제거합니다.|10분마다 실행|  
|배포 정리: 배포|배포 데이터베이스에서 복제된 트랜잭션을 제거합니다. 최대 배포 보존 기간 내에 동기화되지 않은 구독을 비활성화합니다.|10분마다 실행|  
|만료된 구독 정리|게시 데이터베이스에서 만료된 구독을 검색하여 제거합니다.|매일 오전 1시에 실행|  
|데이터 유효성 검사에 실패한 구독 다시 초기화|데이터 유효성 검사에 실패한 모든 구독을 검색한 다음 다시 초기화하도록 표시합니다. 다음에 병합 에이전트 또는 배포 에이전트가 실행될 때 새 스냅숏이 구독자에 적용됩니다.|기본 일정 없음(기본적으로 사용되지 않음)|  
|복제 에이전트 점검|기록을 로깅하지 않는 복제 에이전트를 검색합니다. 작업 단계가 실패하면 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 이벤트 로그에 기록합니다.|10분마다 실행|  
|배포에 대한 복제 모니터링 리프레셔|복제 모니터에서 사용한 캐시된 쿼리를 새로 고칩니다.|계속 실행|  
  
## <a name="see-also"></a>관련 항목  
 [복제 모니터링](../monitoring-replication.md)  
  
  
