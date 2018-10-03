---
title: SQL Server 장애 조치(Failover) 클러스터 인스턴스 업그레이드(설치) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- upgrading clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], creating clusters
- clusters [SQL Server], creating
- failover clustering [SQL Server], upgrading
ms.assetid: ea8b7d66-e5a1-402f-9928-8f7310e84f5c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4d10eb18560574e647c443caf4887b8e893d7501
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48132113"
---
# <a name="upgrade-a-sql-server-failover-cluster-instance-setup"></a>SQL Server 장애 조치(Failover) 클러스터 인스턴스 업그레이드(설치)
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 마법사를 사용하거나 명령 프롬프트에서 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 장애 조치(Failover) 클러스터를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터로 업그레이드할 수 있습니다.  
  
 장애 조치(Failover) 클러스터 업그레이드 도중 작동 중단 시간은 장애 조치(Failover) 시간 및 업그레이드 스크립트 실행에 필요한 시간으로만 제한됩니다. 장애 조치 클러스터 롤링 업그레이드 프로세스를 따르는 경우 작동 중단 시간이 최소화됩니다. 장애 조치 클러스터 노드에 필수 구성 요소가 모두 있는지 여부에 따라 이러한 필수 구성 요소를 설치하는 동안 작동 중단 시간이 추가로 발생할 수도 있습니다. 업그레이드 과정에서 작동 중단 시간을 최소화하는 방법에 대한 자세한 내용은 이 페이지의 [장애 조치(Failover) 클러스터 업그레이드 수행 전 최선의 방법](#BestPractices) 섹션을 참조하십시오.  
  
 업그레이드 하는 방법에 대 한 자세한 내용은 참조 하세요. [Supported Version and Edition Upgrades](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md) 하 고 [SQL Server 2014로 업그레이드](../../../database-engine/install-windows/upgrade-sql-server.md)합니다.  
  
 명령 프롬프트에 사용할 예제 구문에 대 한 자세한 내용은 참조 하세요. [명령 프롬프트에서 SQL Server 2014 설치](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 시작하기 전에 다음과 같은 중요한 정보를 검토하십시오.  
  
-   [장애 조치(Failover) 클러스터링을 설치하기 전에](../install/before-installing-failover-clustering.md)  
  
-   [업그레이드 관리자를 사용 하 여 업그레이드를 준비 하려면](../../install/use-upgrade-advisor-to-prepare-for-upgrades.md)합니다.  
  
-   [데이터베이스 엔진 업그레이드](../../../database-engine/install-windows/upgrade-database-engine.md)  
  
-   설치 프로그램에서는 클러스터링된 운영 체제에 .NET Framework 4.0을 설치합니다. 작동 중단 시간을 최소화하려면 설치 프로그램을 실행하기 전에 .NET Framework 4.0을 설치하는 것이 좋습니다.  
  
-   Visual Studio 구성 요소를 올바르게 설치할 수 있도록 되도록 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 업데이트를 설치 해야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램에서 이 업데이트가 있는지 여부를 확인한 다음 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치를 계속하기 전에 업데이트를 다운로드하여 설치해야 합니다. 하는 동안 중단을 방지 하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 다운로드 하 고 실행 하기 전에 업데이트를 설치할 수 있습니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 아래 설명 된 대로 설치 (또는 Windows Update에서 사용 가능한.NET 3.5 SP1에 대 한 모든 업데이트를 설치 합니다.):  
  
     설치 하는 경우 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Widows Server 2008 SP2 운영 체제가 설치 된 컴퓨터에서 필요한 업데이트를 가져올 수 있습니다 [여기](http://go.microsoft.com/fwlink/?LinkId=198093)  
  
     [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] SP1 또는 [!INCLUDE[win7](../../../includes/win7-md.md)] SP1 운영 체제가 설치된 컴퓨터에 [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]를 설치하는 경우 이 업데이트가 포함되어 있습니다.  
  
-   .NET Framework 3.5 SP1은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램으로 더 이상 설치되지 않지만 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)]를 설치할 경우 필요할 수 있습니다. 자세한 내용은 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)][릴리스 정보](http://go.microsoft.com/fwlink/?LinkId=296445)를 참조하십시오.  
  
-   로컬로 설치하는 경우 관리자로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 실행해야 합니다. 원격 공유에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 설치하는 경우 원격 공유에 대한 읽기 권한이 있는 도메인 계정을 사용해야 합니다.  
  
-   인스턴스를 업그레이드 하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 장애 조치 클러스터를 업그레이드 중인 인스턴스에 장애 조치 클러스터 여야 합니다.  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 독립 실행형 인스턴스를 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 장애 조치(Failover) 클러스터로 이동하려면 새 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 장애 조치(Failover) 클러스터를 설치한 다음 데이터베이스 복사 마법사를 사용하여 독립 실행형 인스턴스의 사용자 데이터베이스를 마이그레이션합니다. 자세한 내용은 [Use the Copy Database Wizard](../../../relational-databases/databases/use-the-copy-database-wizard.md)을 참조하세요.  
  
## <a name="rolling-upgrades"></a>롤링 업그레이드  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터를 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]로 업그레이드하려면 패시브 노드부터 시작하여 장애 조치(Failover) 클러스터 노드 각각에서 한 번에 하나씩 업그레이드 동작으로 설치 프로그램을 실행해야 합니다. 업그레이드된 각 노드는 장애 조치 클러스터의 가능한 소유자 노드에서 제외됩니다. 예기치 않은 장애 조치(Failover)의 경우 업그레이드된 노드는 클러스터 리소스 그룹 소유권이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램에 의해 업그레이드된 노드로 이동하기 전까지는 장애 조치(Failover)에 참여하지 않습니다.  
  
 기본적으로 업그레이드된 노드로 장애 조치(Failover)를 수행할 시기가 설치 프로그램에서 자동으로 결정됩니다. 이 시기는 장애 조치 클러스터 인스턴스의 총 노드 수 및 이미 업그레이드된 노드 수에 따라 다릅니다. 절반 이상의 노드가 이미 업그레이드된 경우, 다음 노드에서 업그레이드를 수행하면 설치 프로그램은 업그레이드된 노드로의 장애 조치(Failover)를 발생시킵니다. 업그레이드된 노드로 장애 조치가 수행되면 곧바로 클러스터 그룹이 업그레이드된 노드로 이동합니다. 업그레이드된 모든 노드가 가능한 소유자 목록에 배치되고 업그레이드되지 않은 모든 노드는 가능한 소유자 목록에서 제거됩니다. 남아 있는 각 노드를 업그레이드하면 이러한 노드는 장애 조치 클러스터의 가능한 소유자 노드에 추가됩니다.  
  
 이 프로세스로 인해 전체 장애 조치(Failover) 클러스터 업그레이드 중의 작동 중단은 장애 조치(Failover) 시간 및 데이터베이스 업그레이드 스크립트 실행 시간으로만 제한됩니다.  
  
 업그레이드 프로세스 중에 클러스터 노드의 장애 조치(Failover) 동작을 제어하려면 명령 프롬프트에서 업그레이드 작업을 실행하고 /FAILOVERCLUSTERROLLOWNERSHIP 매개 변수를 사용합니다. 자세한 내용은 [명령 프롬프트에서 SQL Server 2014 설치](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)를 참조하세요.  
  
 **참고** 단일 노드 장애 조치 클러스터의 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스 그룹을 오프 라인입니다.  
  
## <a name="considerations-when-upgrading-from-includessversion2005includesssversion2005-mdmd"></a>[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 업그레이드할 경우 고려해야 할 사항  
 클러스터 보안 정책에 대해 도메인 그룹을 지정한 경우 [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)]에서 서비스 SID를 지정할 수 없습니다. 서비스 SID를 사용하려면 병렬 업그레이드를 수행해야 합니다.  
  
 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]을 업그레이드하도록 선택하면 전체 텍스트 검색이 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에 설치되어 있는지 여부와 상관없이 이 기능이 설치에 포함됩니다.  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 전체 텍스트 검색을 사용한 경우 사용 가능한 옵션과 상관없이 설치 프로그램을 통해 전체 텍스트 검색 카탈로그가 다시 작성됩니다.  
  
## <a name="upgrading-to-a-includesssql14includessssql14-mdmd-multi-subnet-failover-cluster"></a>[!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 다중 서브넷 장애 조치(Failover) 클러스터로 업그레이드  
 다음과 같은 두 가지 업그레이드 시나리오가 있을 수 있습니다.  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치 클러스터가 현재 단일 서브넷에 구성 되어 있습니다.: 기존 클러스터를 먼저 업그레이드 해야 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 설치 프로그램을 시작 하 고 다음 업그레이드 프로세스에서 합니다. 기존 장애 조치(Failover) 클러스터의 업그레이드를 완료한 후에는 AddNode 기능을 사용해서 다른 서브넷에 있는 노드를 추가합니다. 클러스터 네트워크 구성 페이지에서 IP 주소 리소스 종속성을 OR로 변경하도록 확인하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다중 서브넷 장애 조치(Failover) 클러스터 구성이 완료됩니다.  
  
2.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치 클러스터가 현재 V-LAN 늘이기 기술을 사용 하는 여러 서브넷에 구성 된: 기존 클러스터를 먼저 업그레이드 해야 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]합니다. V-LAN 확장 기술은 단일 서브넷을 구성하기 때문에 네트워크 구성을 다중 서브넷으로 변경하고 Windows 장애 조치(Failover) 클러스터 관리 도구를 사용하여 IP 주소 리소스 종속성을 OR로 변경해야 합니다.  
  
###  <a name="BestPractices"></a> 업그레이드 수행 전 최선의 방법은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치 클러스터  
 다시 시작으로 인한 예기치 않은 작동 중단 시간을 없애려면 클러스터 노드에서 업그레이드를 실행하기 전에 모든 장애 조치(Failover) 클러스터 노드에 .NET Framework 4.0용 다시 부팅 불필요 패키지를 사전 설치합니다. 다음 단계를 수행하여 필수 구성 요소를 사전 설치하는 것이 좋습니다.  
  
-   .NET Framework 4.0용 다시 부팅 불필요 패키지를 설치하고 패시브 노드부터 시작하여 공유 구성 요소만 업그레이드합니다. 그러면 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 4.0, Windows Installer 4.5 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 지원 파일이 설치됩니다.  
  
-   필요한 경우 한 번 이상 다시 시작합니다.  
  
-   업그레이드된 노드로 장애 조치를 수행합니다.  
  
-   마지막으로 남은 노드에서 공유 구성 요소를 업그레이드합니다.  
  
 모든 공유 구성 요소를 업그레이드하고 필수 구성 요소를 설치한 후 장애 조치(Failover) 클러스터 업그레이드 프로세스를 시작합니다. 각 장애 조치(Failover) 클러스터 노드에서 업그레이드를 실행해야 합니다. 이때 먼저 패시브 노드부터 시작하여 클러스터 리소스 그룹 소유권을 가진 노드로 진행합니다.  
  
-   기존 장애 조치 클러스터에 기능을 추가할 수 없습니다.  
  
-   장애 조치(Failover) 클러스터의 버전 변경은 특정 시나리오로만 제한됩니다. 자세한 내용은 [지원되는 버전 및 에디션 업그레이드](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md)를 참조하세요.  
  
##  <a name="UpgradeSteps"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터를 업그레이드하려면  
  
#### <a name="to-upgrade-a-includessnoversionincludesssnoversion-mdmd-failover-cluster"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터를 업그레이드하려면  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 미디어를 넣고 루트 폴더에서 Setup.exe를 두 번 클릭합니다. 네트워크 공유에서 설치하려면 공유에서 루트 폴더로 이동한 다음 Setup.exe를 두 번 클릭합니다. 필수 구성 요소가 설치되어 있지 않은 경우 해당 구성 요소를 설치하라는 메시지가 나타날 수 있습니다.  
  
2.  > [!IMPORTANT]  
    >  3단계 및 4단계에 대한 자세한 내용은 [장애 조치(Failover) 클러스터 업그레이드 수행 전 최선의 방법](#BestPractices) 섹션을 참조하십시오.  
  
3.  필수 구성 요소를 설치하고 나면 설치 마법사를 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 센터가 시작됩니다. 기존 인스턴스를 업그레이드 하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], 클릭 **에서 업그레이드 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]합니다 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)], 또는 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]합니다.**  
  
4.  설치 지원 파일이 필요한 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램이 이를 설치합니다. 컴퓨터를 다시 시작하라는 메시지가 표시되면 컴퓨터를 다시 시작한 후 작업을 계속합니다.  
  
5.  시스템 구성 검사기가 컴퓨터에서 검색 작업을 실행합니다. 계속하려면 [!INCLUDE[clickOK](../../../includes/clickok-md.md)].  
  
6.  제품 키 페이지에서 기존 제품 버전에 맞는 새 버전의 PID 키를 입력합니다. 예를 들어 Enterprise 장애 조치(Failover) 클러스터를 업그레이드하려면 [!INCLUDE[ssEnterprise](../../../includes/ssenterprise-md.md)]용 PID 키를 입력해야 합니다. 계속하려면 **다음** 을 클릭합니다. 장애 조치(Failover) 클러스터 업그레이드에 사용하는 PID 키는 동일 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 내의 모든 장애 조치(Failover) 클러스터 노드에서 동일해야 합니다. 자세한 내용은 [버전 및 SQL Server 2014 구성 요소](../../editions-and-components-of-sql-server-2016.md) 하 고 [Supported Version and Edition Upgrades](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md)합니다.  
  
7.  사용 조건 페이지에서 사용권 계약을 읽은 다음 사용 조건과 계약 조건에 동의하면 해당 확인란을 선택합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 개선을 돕기 위해 기능 사용 옵션을 사용하도록 설정하여 [!INCLUDE[msCoName](../../../includes/msconame-md.md)]로 보고서를 보낼 수도 있습니다. 계속하려면**다음**을 클릭합니다. 설치를 끝내려면 **취소**를 클릭합니다.  
  
8.  인스턴스 선택 페이지에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로 업그레이드할 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]인스턴스를 지정합니다. 계속하려면**다음**을 클릭합니다.  
  
9. 기능 선택 페이지에는 업그레이드할 기능이 미리 선택되어 있습니다. 기능 이름을 선택하면 오른쪽 창에 각 구성 요소 그룹에 대한 설명이 나타납니다. 업그레이드할 기능은 변경할 수 없으며, 업그레이드 작업 중에 기능을 추가할 수도 없습니다. 업그레이드 된 인스턴스에 기능을 추가할 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 업그레이드 작업이 완료 되 면 참조 [는 인스턴스에 SQL Server 2014의 기능 추가 &#40;설치&#41;](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-setup.md)합니다.  
  
     선택한 기능의 필수 구성 요소가 오른쪽 창에 표시됩니다. 설치되어 있지 않은 필수 구성 요소가 있는 경우 SQL Server 설치 프로그램은 이 절차의 뒷부분에 설명된 설치 단계에서 이를 설치합니다.  
  
10. 인스턴스 구성 페이지의 필드가 기존 인스턴스 정보로 자동으로 채워집니다. 필요에 따라 새 InstanceID 값을 지정할 수 있습니다.  
  
     **인스턴스 ID** - 기본적으로 인스턴스 이름이 인스턴스 ID로 사용됩니다. 인스턴스 ID는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스의 설치 디렉터리 및 레지스트리 키를 식별하는 데 사용됩니다. 이는 기본 인스턴스와 명명된 인스턴스에 모두 해당됩니다. 기본 인스턴스의 경우 인스턴스 이름 및 인스턴스 ID는 MSSQLSERVER입니다. 기본이 아닌 인스턴스 ID를 사용하려면 **인스턴스 ID** 확인란을 선택하고 값을 입력합니다. 기본값을 재정의하는 경우, 모든 장애 조치 클러스터 노드에서 업그레이드할 인스턴스에 대해 동일한 인스턴스 ID를 지정해야 합니다. 업그레이드된 인스턴스에 대한 인스턴스 ID는 다수의 노드에서 일치해야 합니다.  
  
     **감지 된 인스턴스 및 기능** -인스턴스의 표 형식으로 표시 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 중인 설치 프로그램을 실행 중인 컴퓨터에 있는 합니다. 계속하려면**다음**을 클릭합니다.  
  
11. 디스크 공간 요구 사항 페이지에서는 사용자가 지정한 기능에 필요한 디스크 공간을 계산한 후 설치 프로그램을 실행 중인 컴퓨터에서 사용 가능한 디스크 공간과 실제로 필요한 디스크 공간의 크기를 비교하여 보여 줍니다.  
  
12. 전체 텍스트 검색 업그레이드 페이지에서 업그레이드하려는 데이터베이스의 업그레이드 옵션을 지정합니다. 자세한 내용은 [전체 텍스트 검색 업그레이드 옵션](../../install/full-text-search-upgrade-options.md)을 참조하세요.  
  
13. **오류 보고** 페이지에서 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 개선에 도움이 되도록 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 보낼 정보를 지정할 수 있습니다. 오류 보고 옵션은 기본적으로 사용됩니다.  
  
14. 시스템 구성 검사기는 업그레이드 작업이 시작되기 전에 사용자가 지정한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기능에 따라 사용자 컴퓨터 구성이 유효한지 검사하기 위한 하나 이상의 규칙 집합을 실행합니다.  
  
15. 클러스터 업그레이드 보고서 페이지에 장애 조치 클러스터 인스턴스의 노드 목록 및 각 노드에 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 요소 관련 인스턴스 버전 정보가 표시됩니다. 여기에는 데이터베이스 스크립트 상태 및 복제 스크립트 상태가 나타나며, **다음**을 클릭하면 어떤 동작이 발생하는지에 대한 정보 메시지도 표시됩니다. 이미 업그레이드된 장애 조치 클러스터 노드 수 및 총 노드 수에 따라 **다음**을 클릭하면 나타나는 장애 조치 동작이 설치 프로그램에서 표시됩니다. 또한, 필수 구성 요소를 설치하지 않은 경우에는 불필요한 작동 중단 발생 가능성에 대해서도 경고합니다.  
  
16. 업그레이드 준비 페이지에는 설치 중에 지정된 설치 옵션이 트리 뷰로 표시됩니다. 계속하려면 **업그레이드**를 클릭합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램은 선택한 기능에 대한 필수 구성 요소를 먼저 설치하고 그 다음에 기능을 설치합니다.  
  
17. 업그레이드 중에 진행률 페이지에서 제공하는 상태 정보를 통해 현재 노드에서의 업그레이드 진행률을 모니터링할 수 있습니다.  
  
18. 현재 노드의 업그레이드가 완료되면 클러스터 업그레이드 보고서 페이지에 모든 장애 조치 클러스터 노드, 각 장애 조치 클러스터 노드상의 기능, 해당 버전 정보 등이 표시됩니다. 표시된 버전 정보를 확인하고 계속해서 나머지 노드의 업그레이드를 진행합니다. 업그레이드된 노드로 장애 조치가 수행된 경우 이 정보도 상태 페이지에 나타납니다. Windows 클러스터 관리 도구에서 검토하여 확인할 수도 있습니다.  
  
19. 업그레이드가 끝나면 설치 및 기타 중요한 참고 사항에 대한 요약 로그 파일을 볼 수 있는 링크가 완료 페이지에 제공됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 과정을 완료하려면 **닫기**를 클릭합니다.  
  
20. 컴퓨터를 다시 시작합니다. 설치가 끝나면 설치 마법사에 표시되는 메시지를 읽어야 합니다. 설치 로그 파일에 대한 자세한 내용은 [SQL Server 설치 로그 파일 보기 및 읽기](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)를 참조하세요.  
  
21. 업그레이드 프로세스를 완료하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에 있는 다른 모든 노드에서 1-21단계를 반복합니다.  
  
## <a name="to-upgrade-a-includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다중 서브넷 장애 조치(Failover) 클러스터를 업그레이드하려면  
  
#### <a name="to-upgrade-to-a-includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster-existing-includessnoversionincludesssnoversion-mdmd-cluster-is-a-non-multi-subnet-cluster"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다중 서브넷 장애 조치(Failover) 클러스터로 업그레이드하려면(기존 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클러스터가 다중 서브넷 클러스터가 아닌 경우)  
  
1.  에 설명 된 1-24 단계를 수행 합니다 [SQL Server 장애 조치 클러스터로 업그레이드](#UpgradeSteps) 클러스터를 업그레이드 하려면 위의 섹션 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]합니다.  
  
2.  AddNode 설치 동작을 사용하여 다른 서브넷에 있는 노드를 추가하고 **클러스터 네트워크 구성** 페이지에서 IP 주소 리소스 종속성을 OR로 설정합니다. 자세한 내용은 [SQL Server 장애 조치(failover) 클러스터에서 노드 추가 또는 제거&#40;설치 프로그램&#41;](../install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)을 참조하세요.  
  
#### <a name="to-upgrade-a-multi-subnet-cluster-currently-using-stretch-v-lan"></a>현재 V-LAN 확장을 사용하는 다중 서브넷 클러스터를 업그레이드하려면  
  
1.  에 설명 된 1-24 단계를 수행 합니다 [SQL Server 장애 조치 클러스터로 업그레이드](#UpgradeSteps) 클러스터를 업그레이드 하려면 위의 섹션 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]합니다.  
  
2.  네트워크 설정을 변경하여 원격 노드를 다른 서브넷으로 이동합니다.  
  
3.  Windows 장애 조치(Failover) 클러스터 관리 도구를 사용하여 새 서브넷에 대한 새 IP 주소를 추가하고 IP 주소 리소스 종속성을 OR로 설정합니다.  
  
## <a name="next-steps"></a>다음 단계  
 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]로 업그레이드한 후 다음 태스크를 완료하십시오.  
  
-   서버 등록  
  
     업그레이드를 수행하면 이전 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대한 레지스트리 설정이 제거됩니다. 업그레이드한 후 서버를 다시 등록해야 합니다.  
  
-   통계 업데이트  
  
     쿼리 성능을 최적화할 수 있도록 업그레이드 후에 모든 데이터베이스에 대한 통계를 업데이트하는 것이 좋습니다. **sp_updatestats** 저장 프로시저를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 있는 사용자 정의 테이블의 통계를 업데이트할 수 있습니다.  
  
-   새 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 구성  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 공격받을 수 있는 시스템의 노출 영역을 줄이기 위해 핵심 서비스와 기능을 선별적으로 설치하고 활성화합니다. 노출 영역 구성 도구에 대한 자세한 내용은 이 릴리스의 추가 정보 파일을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [명령 프롬프트에서 SQL Server 2014 설치](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
 [SQL Server 설치 로그 파일 보기 및 읽기](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
