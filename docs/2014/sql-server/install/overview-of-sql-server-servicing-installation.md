---
title: SQL Server 서비스 설치 개요 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 6a9fd19b-2367-4908-b638-363b1e929e1e
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 65797fdf770196723a74510501d381fb608ad2ff
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53369065"
---
# <a name="overview-of-sql-server-servicing-installation"></a>SQL Server 서비스 설치 개요
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 제공하는 업데이트를 통해 설치된 모든 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 구성 요소에 업데이트를 적용할 수 있습니다. 기존 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 구성 요소의 버전 수준이 업데이트 버전 수준보다 최신 상태이면 설치 프로그램을 통한 업데이트 작업에서 해당 구성 요소가 제외됩니다. 업데이트 서비스를 적용 하는 방법은 참조 하십시오 [SQL Server 2014 서비스 업데이트 설치](../../database-engine/install-windows/install-sql-server-servicing-updates.md)합니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업데이트를 설치할 때는 다음 사항을 고려해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 한 인스턴스에 속하는 모든 기능을 동시에 업데이트해야 합니다. 예를 들어 [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 업데이트할 때 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소가 동일한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 일부로 설치되어 있으면 함께 업데이트해야 합니다. 관리 도구, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]와 같은 공유 기능은 항상 최신 업데이트로 업데이트해야 합니다. 기능 트리에서 구성 요소나 인스턴스를 선택하지 않으면 해당 구성 요소나 인스턴스는 업데이트되지 않습니다.  
  
-   기본적으로 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업데이트 로그 파일은 % Program Files %에 저장 됩니다\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\LOG\\합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에서 이제 원본 미디어를 사용하여 업데이트를 통합할 수 있습니다. 즉, 원본 미디어와 업데이트를 동시에 실행할 수 있습니다. 자세한 내용은 [What's New in SQL Server 설치](../../../2014/sql-server/install/what-s-new-in-sql-server-installation.md)합니다.  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 제공하는 업데이트를 적용하기 전에 데이터를 백업하는 것이 좋습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업데이트는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update를 통해 제공됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 업데이트하고 보안을 적용하기 위해 정기적으로 업데이트를 검색하는 것이 좋습니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SP1은 전체 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치로 제공되고 있습니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RTM 인스턴스에 적용할 패키지 실행 표준 패치에 서비스 팩을 제공하는 대신 이 버전에서는 2개의 파일로 구성된 설치 패키지가 제공됩니다. 설치 패키지를 실행하면 SP1이 미리 설치된 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 설치됩니다.  
  
## <a name="requirements-and-known-issues"></a>요구 사항 및 알려진 문제  
 디스크 공간은 패키지를 설치 및 다운로드하고, 압축을 풀기 위해 패키지 크기의 약 2.5배를 확보하는 것이 좋습니다. 서비스 팩을 설치한 후 다운로드된 패키지를 제거할 수 있습니다. 임시 파일은 자동으로 제거됩니다.  
  
 **알려진된 문제를 검토 합니다.** 현재 버전의 알려진 문제에 대한 자세한 내용은 [SQL Server 릴리스](https://msdn.microsoft.com/f617a0af-92dd-47aa-82c3-f51b1346bcd8)합니다.  
  
## <a name="installation-overview"></a>설치 개요  
 이 섹션에서는 다음을 수행하는 방법을 비롯하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 누적 업데이트 및 서비스 팩 설치에 대해 설명합니다.  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업데이트 설치 준비  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업데이트 설치  
  
-   서비스 및 애플리케이션 다시 시작  
  
### <a name="prepare-for-a-includesscurrentincludessscurrent-mdmd-update-installation"></a>[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업데이트 설치 준비  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업데이트를 설치하기 전에 다음을 수행해야 합니다.  
  
-   **백업에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터베이스** 설치 하기 전에- [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업데이트를 백업 합니다 `master`, `msdb`, 및 `model` 데이터베이스. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업데이트를 설치하면 이러한 데이터베이스가 변경되어 이전 버전의 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]와 호환되지 않습니다. 업데이트를 적용하지 않은 채 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 다시 설치하고 이전 데이터베이스를 계속 사용하려면 이러한 데이터베이스를 백업해야 합니다.  
  
     또한 사용자 데이터베이스도 백업하는 것이 좋습니다.  
  
    > [!IMPORTANT]  
    >  복제 토폴로지에 참여하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 업데이트를 적용할 경우에는 업데이트를 적용하기 전에 복제된 데이터베이스를 시스템 데이터베이스와 함께 백업해야 합니다.  
  
-   **백업 프로그램 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스, 구성 파일 및 리포지토리** 의 인스턴스를 업데이트 하기 전에- [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], 다음을 백업 해야 합니다.  
  
    -   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스. 기본적으로 C:\Program Files에 설치 된 이러한\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSAS12.\< InstanceID > \OLAP\Data\\합니다. WOW 설치의 경우 기본 경로 C:\ProgramFiles (x86) \ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSAS12.\< InstanceID > \OLAP\Data\\합니다.  
  
    -   msmdsrv.ini 구성 파일의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 구성 설정. 기본적으로이에 위치한 파일은 C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSAS12.\< InstanceID > \OLAP\Config\ 디렉터리입니다.  
  
    -   (선택 사항) [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 리포지토리가 포함된 데이터베이스. 이 단계는 DSO(의사 결정 지원 개체) 라이브러리를 사용하도록 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 구성한 경우에만 필요합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스, 구성 파일 및 리포지토리를 백업하지 못하면 업데이트된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스를 이전 버전으로 되돌릴 수 없습니다.  
  
-   **시스템 데이터베이스에 사용 가능한 공간이 충분 한지 확인 하십시오** 에 대 한 자동 증가 옵션을 선택 하지 않으면-합니다 `master` 및 `msdb` 시스템 데이터베이스에 이러한 데이터베이스 각각에 최소한 500KB 이상의 여유 공간이 있어야 합니다. 데이터베이스에 공간이 충분한지 확인하려면 `sp_spaceused` 및 `master` 데이터베이스에서 `msdb` 시스템 저장 프로시저를 실행합니다. 각 데이터베이스의 할당되지 않은 공간이 500KB보다 적은 경우에는 데이터베이스의 크기를 늘려야 합니다.  
  
-   **서비스 및 응용 프로그램 중지** -시스템 다시 시작 방지을 모든 응용 프로그램 및 인스턴스에 연결 된 서비스를 중지 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 업그레이드 중인 설치 하기 전에 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업데이트 합니다. 여기에는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]등이 있습니다. 자세한 내용은 [데이터베이스 엔진, SQL Server 에이전트 또는 SQL Server Browser 서비스 시작, 중지, 일시 중지, 재개 및 다시 시작](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)을 참조하세요.  
  
    > [!NOTE]  
    >  장애 조치(failover) 클러스터 환경에서는 서비스를 중지할 수 없습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 장애 조치(Failover) 클러스터 설치 섹션을 참조하십시오.  
  
-   업데이트 설치 후 컴퓨터를 다시 시작해야 할 필요가 없도록 설치 프로그램에 파일을 잠그는 프로세스 목록이 표시됩니다. 업데이트 설치 프로그램이 설치 중에 특정 서비스를 종료해야 할 경우 설치를 마친 후 해당 서비스를 다시 시작합니다.  
  
-   설치 중에 잠겨 있는 파일이 발견될 경우 설치가 끝난 후 컴퓨터를 다시 시작해야 할 수도 있습니다. 필요한 경우 컴퓨터를 다시 시작하라는 메시지가 표시됩니다.  
  
### <a name="install-includesscurrentincludessscurrent-mdmd-updates"></a>[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업데이트 설치  
 이 섹션에서는 설치 과정에 대해 설명합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업데이트 설치는 업데이트를 설치할 컴퓨터에 대한 관리 권한이 있는 계정으로 수행해야 합니다. 로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용해야 합니다.  
  
#### <a name="starting-a-includesscurrentincludessscurrent-mdmd-update"></a>[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업데이트 시작  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업데이트를 설치하려면 자동 압축 풀기 패키지 파일을 실행합니다.  
  
 누적 업데이트 패키지(CU): \<SQLServer2014 >-KBxxxxxx-*PPP*.exe  
  
 서비스 팩 패키지(PCU): \<SQLServer2014 >\<SPx >-KBxxxxxx-PPP-LLL.exe  
  
-   x는 서비스 팩 번호를 나타냅니다.  
  
-   PPP는 특정 플랫폼을 나타냅니다.  
  
-   LLL은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 언어의 문자 약어를 나타내며, 예를 들어 영어의 LLL은 ENU입니다.  
  
 장애 조치(failover) 클러스터에 속하는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 구성 요소에 업데이트를 적용하려면 장애 조치 클러스터 설치에 대한 섹션을 참조하십시오. 무인 모드로 업데이트 설치를 실행 하는 방법에 대 한 자세한 내용은 참조 하세요. [명령 프롬프트에서 SQL Server 2014 설치](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)합니다.  
  
####  <a name="Slipstream"></a> 제품 업데이트 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치  
 제품 업데이트는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치의 기능입니다. 최신 제품 업데이트를 주 제품 설치와 통합하여 주 제품과 해당 업데이트가 동시에 설치되게 할 수 있습니다. 제품 업데이트는 적용 가능한 업데이트에 대해서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, WSUS(Windows Server Update Services), 로컬 폴더 또는 네트워크 공유를 검색할 수 있습니다.  설치 프로그램에서 최신 버전의 적용 가능한 업데이트를 찾으면 이를 다운로드하고 현재의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로세스와 통합합니다. 제품 업데이트에는 누적 업데이트, 서비스 팩 또는 서비스 팩과 누적 업데이트가 포함될 수 있습니다. 제품 업데이트 기능은 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] PCU1에서 제공한 통합 설치 기능을 확장한 것입니다.  
  
## <a name="updating-a-prepared-image-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 준비 이미지 업데이트  
 준비 인스턴스 구성을 완료하지 않고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 구성되지 않은 준비 인스턴스에 업데이트를 적용할 수 있습니다. 아래에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 준비 인스턴스에 업데이트를 적용하는 다른 방법에 대해 설명합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이전 준비 인스턴스 업데이트  
  
     구성 전에 준비 인스턴스에 대한 업데이트를 적용할 수 있습니다. 업데이트 패키지는 인스턴스가 준비 상태임을 감지하고 구성을 완료하지 않은 상태로 준비 인스턴스에 패치를 적용합니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update를 사용하여 준비 인스턴스 업데이트  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Update를 통해 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의 준비 인스턴스에 업데이트를 적용할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update 패키지는 인스턴스가 준비 상태임을 감지하고 구성을 완료하지 않은 상태로 준비 인스턴스에 패치를 적용합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 준비 이미지를 업데이트하는 경우 InstanceID 매개 변수를 지정해야 합니다. 자세한 내용과 예제 구문을 보려면 [Installing Updates from the Command Prompt](../../database-engine/install-windows/installing-updates-from-the-command-prompt.md)를 참조하십시오.  
  
## <a name="updating-a-completed-image-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 완료 이미지 업데이트  
 완료 및 구성된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스를 업데이트할 때도 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기타 인스턴스와 동일한 프로세스를 따릅니다.  
  
## <a name="rebuilding-a-includesscurrentincludessscurrent-mdmd-failover-cluster-node"></a>[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 장애 조치(failover) 클러스터 노드 다시 작성  
 업데이트를 적용한 후 장애 조치(failover) 클러스터에서 노드를 다시 작성해야 하는 경우에는 다음 단계를 따릅니다.  
  
1.  장애 조치(failover) 클러스터에서 노드를 다시 작성합니다. 노드를 다시 작성하는 방법은 [Recover from Failover Cluster Instance Failure](../failover-clusters/windows/recover-from-failover-cluster-instance-failure.md)를 참조하십시오.  
  
2.  원본 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 프로그램을 실행하여 장애 조치(failover) 클러스터 노드에 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 을 설치합니다.  
  
3.  추가한 노드에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업데이트 설치 프로그램을 실행합니다.  
  
## <a name="restart-services-and-applications"></a>서비스 및 애플리케이션 다시 시작  
 설치 프로그램이 완료되면 컴퓨터를 다시 시작하라는 메시지가 표시될 수 있습니다. 시스템을 다시 시작한 후 또는 컴퓨터를 다시 시작하라는 메시지 없이 설치 프로그램이 완료된 후 제어판에서 **서비스** 노드를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업데이트를 적용하기 전에 중지했던 서비스를 다시 시작합니다. 이러한 서비스에는 Distributed Transaction Coordinator 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Search 서비스 또는 인스턴스별 서비스 등이 있습니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업데이트 설치 프로그램을 실행하기 전에 닫은 응용 프로그램을 다시 시작합니다. 설치가 완료된 다음 업그레이드된 `master`, `msdb` 및 `model` 데이터베이스를 즉시 다시 백업할 수도 있습니다.  
  
## <a name="uninstalling-updates-from-includesscurrentincludessscurrent-mdmd"></a>[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 업데이트 제거  
 제어판의 **프로그램 및 기능**을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 누적 업데이트 또는 서비스 팩을 제거할 수 있습니다. 설치된 업데이트 목록을 보려면 설치된 업데이트를 열고 **시작** 단추, **제어판**, **프로그램**을 차례로 선택한 다음 **프로그램 및 기능**에서 **설치된 업데이트 보기**를 클릭합니다. 각 누적 업데이트는 목록에 개별 항목으로 표시됩니다. 하지만 누적 업데이트보다 버전이 높은 서비스 팩이 설치되어 있는 경우 누적 업데이트 항목은 숨겨지고 서비스 팩을 제거해야만 사용할 수 있게 됩니다.  
  
 서비스 팩과 업데이트를 제거하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 적용된 최신 업데이트 또는 서비스 팩에서 시작하여 낮은 버전으로 진행해야 합니다. 다음 각 예제에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 다른 서비스 팩 또는 업데이트에 대한 제거 작업이 완료된 후 누적 업데이트 1 상태가 됩니다.  
  
-   누적 업데이트 1과 SP1이 설치된 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스에서 SP1을 제거합니다.  
  
-   누적 업데이트 1, SP1 및 누적 업데이트 2가 설치된 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스에서 누적 업데이트 2를 먼저 제거한 다음 SP1을 제거합니다.  
  
## <a name="see-also"></a>관련 항목  
 [명령 프롬프트에서 SQL Server 2014 설치](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
 [SQL Server 2014 서비스 업데이트 설치](../../database-engine/install-windows/install-sql-server-servicing-updates.md)   
 [SQL Server 설치 유효성 검사](../../database-engine/install-windows/validate-a-sql-server-installation.md)   
 [SQL Server 설치 로그 파일 보기 및 읽기](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
