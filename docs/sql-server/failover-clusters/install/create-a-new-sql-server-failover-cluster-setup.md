---
title: 새 SQL Server 장애 조치(Failover) 클러스터 만들기(설치) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- adding nodes
- failover clustering [SQL Server], creating clusters
- nodes [Faillover Clustering], removing
- nodes [Faillover Clustering], adding
- clusters [SQL Server], creating
- removing nodes
ms.assetid: 30e06a7d-75e9-44e2-bca3-b3b0c4a33f61
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c93844267fd91f248c073b00b12c4a07d16d7da5
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52525288"
---
# <a name="create-a-new-sql-server-failover-cluster-setup"></a>새 SQL Server 장애 조치(Failover) 클러스터 만들기(설치)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터를 설치하거나 업그레이드하려면 장애 조치 클러스터의 각 노드에서 설치 프로그램을 실행해야 합니다. 기존의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에 노드를 추가하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스에 추가할 노드에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 실행해야 합니다. 다른 노드를 관리하려고 액티브 노드에서 설치 프로그램을 실행하지 않도록 주의해야 합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터는 노드가 클러스터되는 방식에 따라 다음과 같은 방법으로 구성됩니다.  
  
-   같은 서브넷 또는 같은 서브넷 집합의 노드 - 이러한 유형의 구성에 대해 IP 주소 리소스 종속성을 AND로 설정합니다.  
  
-   다른 서브넷의 노드 - IP 주소 리소스 종속성을 OR로 설정합니다. 이 구성을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다중 서브넷 장애 조치(Failover) 클러스터 구성이라고 합니다. 자세한 내용은 [SQL Server 다중 서브넷 클러스터링&#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md)을 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 설치에 사용할 수 있는 옵션은 다음과 같습니다.  
  
 **옵션 1: 통합 설치 - 노드 추가**  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 통합 장애 조치(Failover) 클러스터 설치는 다음 단계로 구성됩니다.  
  
-   단일 노드 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스를 만들고 구성합니다. 노드를 제대로 구성하면 완벽하게 작동하는 장애 조치(Failover) 클러스터 인스턴스가 만들어집니다. 이 시점에서는 장애 조치(Failover) 클러스터에 노드가 하나뿐이므로 고가용성은 지원되지 않습니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에 추가할 각 노드에서 노드 추가 기능으로 설치를 실행하여 해당 노드를 추가합니다.  
  
    -   추가하려는 노드에 추가 서브넷 또는 다른 서브넷이 있는 경우, 설치 프로그램에서 추가 IP 주소를 지정할 수 있습니다. 추가하려는 노드가 다른 서브넷에 있는 경우에는 OR에 대한 IP 주소 리소스 종속성 변경 사항도 확인해야 합니다. 노드 추가 작업 중 발생할 수 있는 다른 시나리오에 대한 자세한 내용은 [SQL Server 장애 조치(Failover) 클러스터에서 노드 추가 또는 제거&#40;설치 프로그램&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)를 참조하세요.  
  
 **옵션 2: 고급/엔터프라이즈 설치**  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 고급/엔터프라이즈 장애 조치(Failover) 클러스터 설치는 다음 단계로 구성됩니다.  
  
-   새 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터의 소유자가 될 수 있는 각 노드에서 [준비](#prepare)섹션에 나와 있는 설명에 따라 장애 조치(Failover) 클러스터 설치 준비 단계를 실행합니다. 한 노드에서 장애 조치(Failover) 클러스터 준비를 실행하고 나면 지정된 모든 설정의 목록을 포함하는 Configuration.ini 파일이 설치 프로그램을 통해 만들어집니다. 설치를 준비해야 할 다른 노드에서 같은 단계를 반복하는 대신 첫 노드에서 자동으로 생성된 Configuration.ini 파일을 설치 명령줄에 입력 매개 변수로 사용할 수 있습니다. 자세한 내용은 [구성 파일을 사용하여 SQL Server 2016 설치](../../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)를 참조하세요. 이 단계는 노드를 클러스터링할 수 있도록 준비하지만 이 시점에서는 작동하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 없습니다.  
  
-   노드를 클러스터링할 수 있도록 준비했으면 준비된 노드 중 하나에서 설치 프로그램을 실행합니다. 이 단계에서는 장애 조치(Failover) 클러스터 인스턴스를 구성하고 마칩니다. 이 단계를 마치고 나면 작동 가능한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스가 준비되고 해당 인스턴스에 대해 앞서 준비했던 모든 노드에서 새로 작성된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터를 소유할 수 있습니다.  
  
     여러 서브넷의 노드를 클러스터링하는 경우 설치 프로그램은 모든 노드에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스가 준비된 서브넷을 모두 감지합니다. 이러한 서브넷에 대해 여러 IP 주소를 지정할 수 있습니다. 준비된 각 노드는 IP 주소를 하나 이상 소유할 수 있어야 합니다.  
  
     서브넷에 대해 지정된 각 IP 주소가 준비된 모든 노드에서 지원되는 경우 종속성을 AND로 설정합니다.  
  
     서브넷에 대해 지정된 각 IP 주소가 준비된 일부 노드에서 지원되지 않는 경우 종속성을 OR로 설정합니다. 자세한 내용은 [SQL Server 다중 서브넷 클러스터링&#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md)을 참조하세요.  
  
    > [!NOTE]  
    >  장애 조치(Failover) 클러스터를 완료하는 데에는 기본 Windows 장애 조치(Failover) 클러스터가 필요합니다. Windows 장애 조치(Failover) 클러스터가 없으면 오류가 발생하고 설치가 종료됩니다.  
  
 기존 장애 조치(Failover) 클러스터 인스턴스에서 노드를 추가하거나 제거하는 방법은 [SQL Server 장애 조치(Failover) 클러스터에서 노드 추가 또는 제거&#40;설치 프로그램&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)를 참조하세요.  
  
 원격 설치에 대한 자세한 내용은 [지원되는 버전 및 에디션 업그레이드](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md)를 참조하세요.  
  
 Windows 장애 조치 클러스터에서 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 설치에 대한 자세한 내용은 [SQL Server Analysis Services 클러스터링 방법](https://go.microsoft.com/fwlink/p/?LinkId=396548)을 참조하십시오.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 시작하기 전에 다음 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 온라인 설명서 항목을 검토하십시오.  
  
-   [SQL Server 설치 계획](../../../sql-server/install/planning-a-sql-server-installation.md)  
  
-   [장애 조치(Failover) 클러스터링을 설치하기 전에](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)  
  
-   [SQL Server 설치에 대한 보안 고려 사항](../../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
-   [SQL Server 다중 서브넷 클러스터링&#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치를 실행하기 전에 클러스터 관리자의 공유 드라이브 위치를 메모해 두십시오. 새 장애 조치(Failover) 클러스터를 만드는 데 이 정보가 필요합니다.  
  
### <a name="to-install-a-new-includessnoversionincludesssnoversion-mdmd-failover-cluster-using-integrated-install-with-add-node"></a>통합 설치 - 노드 추가 방식으로 새 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터를 설치하려면  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 미디어를 넣고 루트 폴더에서 Setup.exe를 두 번 클릭합니다. 네트워크 공유 위치에서 설치하려면 공유 위치의 루트 폴더로 이동한 다음 Setup.exe를 두 번 클릭합니다. 필수 구성 요소를 설치하는 방법에 대한 자세한 내용은 [Before Installing Failover Clustering](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)를 참조하십시오.  
  
2.  설치 마법사가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 센터를 시작합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 클러스터를 새로 설치하려면 설치 페이지에서 **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 새로 설치**를 클릭합니다.  
  
3.  시스템 구성 검사기가 컴퓨터에서 검색 작업을 실행합니다. 계속하려면 [!INCLUDE[clickOK](../../../includes/clickok-md.md)]. **자세한 정보 표시**를 클릭하여 화면에 세부 정보를 표시하거나 **자세한 보고서 보기**를 클릭하여 HTML 보고서 형식으로 볼 수 있습니다.  
  
4.  계속하려면 **다음**을 클릭합니다.  
  
5.  설치 지원 파일 페이지에서 **설치** 를 클릭하여 설치 지원 파일을 설치합니다.  
  
6.  시스템 구성 검사기가 설치를 계속하기 전에 컴퓨터의 시스템 상태를 확인합니다. 검사가 완료되면 **다음** 을 클릭하여 작업을 계속 진행합니다. **자세한 정보 표시**를 클릭하여 화면에 세부 정보를 표시하거나 **자세한 보고서 보기**를 클릭하여 HTML 보고서 형식으로 볼 수 있습니다.  
  
7.  제품 키 페이지에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]무료 버전을 설치할지, 아니면 제품의 프로덕션 버전에 대한 PID 키가 있는지 표시합니다. 자세한 내용은 [SQL Server 2016 버전 및 구성 요소](../../../sql-server/editions-and-components-of-sql-server-2016.md)를 참조하세요.  
  
8.  사용 조건 페이지에서 사용권 계약을 읽은 다음 사용 조건과 계약 조건에 동의하면 해당 확인란을 선택합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 개선을 돕기 위해 기능 사용 옵션을 사용하도록 설정하여 [!INCLUDE[msCoName](../../../includes/msconame-md.md)]로 보고서를 보낼 수도 있습니다. 계속하려면 **다음** 을 클릭합니다. 설치를 끝내려면 **취소**를 클릭합니다.  
  
9. 기능 선택 페이지에서 설치할 구성 요소를 선택합니다. 기능 이름을 선택하면 오른쪽 창에 각 구성 요소 그룹에 대한 설명이 나타납니다. 확인란을 원하는 대로 선택할 수 있지만 장애 조치(Failover) 클러스터링을 지원하는 것은 테이블 형식 모드의 [!INCLUDE[ssDE](../../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 및 다차원 모드의 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 뿐입니다. 선택한 다른 구성 요소는 설치를 실행하고 있는 현재 노드에서 장애 조치(Failover) 기능 없이 독립 실행형 기능으로 실행됩니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 모드에 대한 자세한 내용은 [Analysis Services 인스턴스의 서버 모드 확인](../../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)을 참조하세요.  
  
     선택한 기능의 필수 구성 요소가 오른쪽 창에 표시됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램에서는 이미 설치되어 있지 않은 필수 구성 요소가 있는 경우 이 절차의 뒷부분에 설명된 설치 단계에서 이를 설치합니다.  
  
     이 페이지 아래 있는 필드를 사용하여 공유 구성 요소의 사용자 지정 디렉터리를 지정할 수 있습니다. 공유 구성 요소의 설치 경로를 변경하려면 대화 상자의 맨 아래에 있는 필드에서 경로를 업데이트하거나 줄임표 단추를 클릭하고 설치 디렉터리를 찾습니다. 기본 설치 경로는 C:\Program Files\\[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] \\입니다.  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 SMB(서버 메시지 블록) 파일 공유에서의 시스템 데이터베이스(Master, Model, MSDB 및 TempDB)와 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 사용자 데이터베이스의 설치도 지원합니다. 저장소로 SMB 파일 공유를 사용하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치에 대한 자세한 내용은 [SMB 파일 공유를 저장소 옵션으로 사용하여 SQL Server 설치](../../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md)를 참조하세요.  
  
     공유 구성 요소에 대해 절대 경로를 지정해야 합니다. 폴더는 압축하거나 암호화해서는 안 됩니다. 매핑된 드라이브는 지원되지 않습니다. 64비트 운영 체제에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 설치하는 경우 다음 옵션이 표시됩니다.  
  
    1.  공유 기능 디렉터리  
  
    2.  공유 기능 디렉터리(x86)  
  
     위의 각 옵션에 대해 다른 경로를 지정해야 합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 서비스 기능을 선택하면 복제 및 전체 텍스트 검색이 모두 자동으로 선택됩니다. [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 서비스 기능을 선택하면 DQS(Data Quality Services)도 선택됩니다. 이 하위 기능을 하나라도 선택 취소하면 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 서비스 기능도 선택 취소됩니다.  
  
10. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램은 구성의 유효성을 검사하기 위해 선택한 기능을 기반으로 하나 이상의 규칙 집합을 실행합니다.  
  
11. 인스턴스 구성 페이지에서 기본 인스턴스를 설치할지 명명된 인스턴스를 설치할지 지정합니다. 자세한 내용은 [Instance Configuration](../../install/instance-configuration.md)을 참조하세요.  
  
     **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 네트워크 이름** – 새 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에 대한 네트워크 이름을 지정합니다. 이 이름은 네트워크에서 장애 조치(Failover) 클러스터를 식별하는 데 사용되는 이름입니다.  
  
    > [!NOTE]  
    >  이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에서는 이를 가상 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이름이라고 했습니다.  
  
     **인스턴스 ID** - 기본적으로 인스턴스 이름이 인스턴스 ID로 사용됩니다. 인스턴스 ID는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스의 설치 디렉터리 및 레지스트리 키를 식별하는 데 사용됩니다. 이는 기본 인스턴스와 명명된 인스턴스에 모두 해당됩니다. 기본 인스턴스의 경우 인스턴스 이름 및 인스턴스 ID는 MSSQLSERVER입니다. 기본값이 아닌 인스턴스 ID를 사용하려면 **인스턴스 ID** 상자를 선택하고 값을 입력합니다.  
  
    > [!NOTE]  
    >  일반적인 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]독립 실행형 인스턴스의 경우 기본 인스턴스인지 명명된 인스턴스인지에 관계없이 **인스턴스 ID** 상자에 기본값을 사용합니다.  
  
     **인스턴스 루트 디렉터리** - 기본적으로 인스턴스 루트 디렉터리는 C:\Program Files\\[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]\\입니다. 기본이 아닌 루트 디렉터리를 지정하려면 제공된 필드를 사용하거나 줄임표 단추를 클릭하고 설치 폴더를 찾습니다.  
  
     **이 컴퓨터에서 발견된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 및 기능** - 설치 프로그램을 실행 중인 컴퓨터에 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 표 형식으로 표시됩니다. 컴퓨터에 기본 인스턴스가 이미 설치된 경우 명명된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 설치해야 합니다. 계속하려면 **다음** 을 클릭합니다.  
  
12. 클러스터 리소스 그룹 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가상 서버 리소스를 배치할 클러스터 리소스 그룹 이름을 지정합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클러스터 리소스 그룹 이름을 지정하는 데는 두 가지 방법이 있습니다.  
  
    -   드롭다운 상자에서 사용할 기존 그룹을 지정합니다.  
  
    -   새로 만들 그룹의 이름을 입력합니다. "Available storage"는 유효한 그룹 이름이 아닙니다.  
  
13. 클러스터 디스크 선택 페이지에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에 대한 공유 클러스터 디스크 리소스를 선택합니다. 클러스터 디스크에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터가 저장됩니다. 디스크를 여러 개 지정할 수 있습니다. 사용 가능한 공유 디스크 표에는 사용 가능한 디스크 목록, 각 디스크가 공유 디스크로 정규화되었는지 여부 및 각 디스크 리소스에 대한 설명이 표시됩니다. 계속하려면 **다음** 을 클릭합니다.  
  
    > [!NOTE]  
    >  모든 데이터베이스에 대해 첫 번째 드라이브가 기본 드라이브로 사용되지만 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 또는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 구성 페이지에서 이를 변경할 수 있습니다.  
    >   
    >  SMB 파일 공유를 데이터 폴더로 사용하려는 경우 클러스터 디스크 선택 페이지에서 공유 디스크 선택을 선택적으로 건너뛸 수 있습니다.  
  
14. 클러스터 네트워크 구성 페이지에서 장애 조치(Failover) 클러스터 인스턴스에 대한 네트워크 리소스를 지정합니다.  
  
    -   **네트워크 설정** – 장애 조치(Failover) 클러스터 인스턴스의 IP 유형과 IP 주소를 지정합니다.  
  
     계속하려면 **다음** 을 클릭합니다.  
  
15. 이 페이지를 사용하여 클러스터 보안 정책을 지정할 수 있습니다.  
  
    -   [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] 이상 버전의 경우 서비스 SID(서버 보안 ID)를 사용하는 것이 좋으며 이는 기본 설정이기도 합니다. 이를 보안 그룹으로 변경하는 옵션은 없습니다. [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)]의 서비스 SID 기능에 대한 자세한 내용은 [Windows 서비스 계정 및 권한 구성](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조하세요. 이 기능은 [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]의 독립 실행형 클러스터 설치에서 테스트되었습니다.  
  
    -   [!INCLUDE[winxpsvr](../../../includes/winxpsvr-md.md)]에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스에 대한 도메인 그룹을 지정합니다. 모든 리소스 사용 권한은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정을 그룹 멤버로 포함하는 도메인 수준 그룹을 통해 제어됩니다.  
  
     계속하려면 **다음** 을 클릭합니다.  
  
16. 이 항목의 나머지 부분에 대한 워크플로는 설치에 대해 지정한 기능에 따라 달라집니다. 선택 항목에 따라 일부 페이지가 표시되지 않을 수도 있습니다([!INCLUDE[ssDE](../../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]및 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]).  
  
17. 서버 구성 - 서비스 계정 페이지에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스에 대한 로그인 계정을 지정합니다. 이 페이지에 구성된 실제 서비스는 사용자가 설치하도록 선택한 기능에 따라 달라집니다.  
  
     모든 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스에 동일한 로그인 계정을 할당하거나 각 서비스 계정을 따로 구성할 수 있습니다. 전체 텍스트 검색 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트를 비롯한 모든 클러스터 인식 서비스에 대해서는 시작 유형이 "수동"으로 설정되며 설치 과정에서 이를 변경할 수 없습니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 에서는 서비스 계정을 개별적으로 구성하여 각 서비스에 대해 최소한의 권한만 제공할 것을 권장합니다. 이렇게 하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스에서 태스크를 완료하는 데 필요한 최소한의 권한만 부여할 수 있습니다. 자세한 내용은 [서버 구성 - 서비스 계정](https://msdn.microsoft.com/library/c283702d-ab20-4bfa-9272-f0c53c31cb9f) 및 [Windows 서비스 계정 및 권한 구성](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조하세요.  
  
     이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스의 모든 서비스 계정에 대해 동일한 로그온 계정을 지정하려면 페이지 맨 아래에 있는 필드에 자격 증명을 입력합니다.  
  
     **보안 정보** [!INCLUDE[ssNoteStrongPass](../../../includes/ssnotestrongpass-md.md)]  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스에 대한 로그인 정보 지정을 완료하면 **다음**을 클릭합니다.  
  
18. **서버 구성 - 데이터 정렬** 탭을 사용하여 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 및 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에 대해 기본이 아닌 데이터 정렬을 지정할 수 있습니다.  
  
19. [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 구성 - 계정 프로비전 페이지를 사용하여 다음을 지정합니다.  
  
    -   보안 모드 - [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에 대한 인증(Windows 인증 또는 혼합 모드 인증)을 선택합니다. 혼합 모드 인증을 선택할 경우 기본 제공 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 시스템 관리자 계정에 강력한 암호를 제공해야 합니다.  
  
         디바이스가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 성공적으로 연결되면 Windows 인증 및 혼합 모드에 모두 동일한 보안 메커니즘이 적용됩니다.  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 관리자 - [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에 대한 시스템 관리자를 한 명 이상 지정해야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 실행하는 계정을 추가하려면 **현재 사용자 추가**를 클릭합니다. 시스템 관리자 목록에 계정을 추가하거나 목록의 계정을 제거하려면 **추가** 또는 **제거**를 클릭한 다음 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에 대한 관리자 권한을 가질 사용자, 그룹 또는 컴퓨터 목록을 편집합니다.  
  
     목록 편집을 마쳤으면 [!INCLUDE[clickOK](../../../includes/clickok-md.md)]. 구성 대화 상자에서 관리자 목록을 확인합니다. 목록 구성을 완료했으면 **다음**을 클릭합니다.  
  
20. [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 구성 - 데이터 디렉터리 페이지를 사용하여 기본이 아닌 설치 디렉터리를 지정합니다. 기본 디렉터리에 설치하려면 **다음**을 클릭합니다.  
  
    > [!IMPORTANT]  
    >  기본이 아닌 설치 디렉터리를 지정하는 경우 해당 설치 폴더가 이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에만 사용되도록 해야 합니다. 이 대화 상자의 어떠한 디렉터리도 다른 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스의 디렉터리와 공유되지 않아야 합니다. 데이터 디렉터리는 장애 조치(Failover) 클러스터의 공유 클러스터 디스크에 배치해야 합니다.  
  
    > [!NOTE]  
    >  SMB(서버 메시지 블록) 파일 서버를 데이터 디렉터리로 지정하려면 **기본 데이터 루트 디렉터리** 를 \\\Servername\ShareName\\... 형식의 파일 공유로 설정합니다.  
   
21. [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 구성 - FILESTREAM 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에 FILESTREAM을 설정합니다. 계속하려면 **다음** 을 클릭합니다.  
  
22. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 구성 - 계정 프로비전 페이지를 사용하여 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에 대해 관리자 권한을 갖는 사용자 또는 계정을 지정합니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에 대한 시스템 관리자를 한 명 이상 지정해야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 실행하는 계정을 추가하려면 **현재 사용자 추가**를 클릭합니다. 시스템 관리자 목록에 계정을 추가하거나 목록의 계정을 제거하려면 **추가** 또는 **제거**를 클릭한 다음 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에 대한 관리자 권한을 가질 사용자, 그룹 또는 컴퓨터 목록을 편집합니다.
  
     목록 편집을 마쳤으면 [!INCLUDE[clickOK](../../../includes/clickok-md.md)]. 구성 대화 상자에서 관리자 목록을 확인합니다. 목록 구성을 완료했으면 **다음**을 클릭합니다.  
  
23. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 구성 - 데이터 디렉터리 페이지를 사용하여 기본이 아닌 설치 디렉터리를 지정합니다. 기본 디렉터리에 설치하려면 **다음**을 클릭합니다.  
  
    > [!IMPORTANT]  
    >  기본이 아닌 설치 디렉터리를 지정하는 경우 해당 설치 폴더가 이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에만 사용되도록 해야 합니다. 이 대화 상자의 어떠한 디렉터리도 다른 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스의 디렉터리와 공유되지 않아야 합니다. 데이터 디렉터리는 장애 조치(Failover) 클러스터의 공유 클러스터 디스크에 배치해야 합니다.  
   
24. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 구성 페이지를 사용하여 만들 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 설치 유형을 지정할 수 있습니다. 장애 조치(Failover) 클러스터 설치의 경우 이 옵션은 구성되지 않은 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 설치로 설정됩니다. 설치를 완료한 후에 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 서비스를 구성해야 합니다.  
  
 
25. 시스템 구성 검사기는 사용자가 지정한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기능에 따라 구성의 유효성을 검사하기 위해 하나 이상의 규칙 집합을 실행합니다.  
  
26. 설치 준비 완료 페이지에는 설치 중에 지정된 설치 옵션이 트리 뷰로 표시됩니다. 계속하려면 **설치**를 클릭합니다. 설치 프로그램은 선택한 기능에 대한 필수 구성 요소를 먼저 설치하고 그 다음에 기능을 설치합니다.  
  
27. 설치 중에 설치 진행률 페이지에서 제공하는 상태 정보를 통해 설치 진행률을 모니터링할 수 있습니다.  
  
28. 설치가 끝나면 설치 및 기타 중요한 참고 사항에 대한 요약 로그 파일을 볼 수 있는 링크가 **완료** 페이지에 제공됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 과정을 완료하려면 **닫기**를 클릭합니다.  
  
29. 컴퓨터를 다시 시작합니다. 설치가 끝나면 설치 마법사에 표시되는 메시지를 읽어야 합니다. 설치 로그 파일에 대한 자세한 내용은 [SQL Server 설치 로그 파일 보기 및 읽기](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)를 참조하세요.  
  
30. 방금 만든 단일 노드 장애 조치(Failover)에 노드를 추가하려면 추가할 각 노드에서 설치를 실행하고 AddNode 작업 단계를 따릅니다. 자세한 내용은 [SQL Server 장애 조치(failover) 클러스터에서 노드 추가 또는 제거&#40;설치 프로그램&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)을 참조하세요.  
  
    > [!NOTE]  
    >  노드를 여러 개 추가하는 경우 구성 파일을 사용하여 설치를 배포할 수 있습니다. 자세한 내용은 [구성 파일을 사용하여 SQL Server 2016 설치](../../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)를 참조하세요.  
    >   
    >  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터의 모든 노드에서 설치하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 버전이 동일해야 합니다. 기존 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에 새 노드를 추가할 때는 기존의 장애 조치(Failover) 클러스터 버전에 일치하는 버전을 지정해야 합니다.  
  
##  <a name="prepare"></a> 준비  
  
#### <a name="advancedenterprise-failover-cluster-install-step-1-prepare"></a>고급/엔터프라이즈 장애 조치(Failover) 클러스터 설치 1단계: 준비  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 미디어를 넣고 루트 폴더에서 Setup.exe를 두 번 클릭합니다. 네트워크 공유 위치에서 설치하려면 공유 위치의 루트 폴더로 이동한 다음 Setup.exe를 두 번 클릭합니다. 필수 구성 요소를 설치하는 방법에 대한 자세한 내용은 [Before Installing Failover Clustering](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)를 참조하십시오. 필수 구성 요소가 설치되어 있지 않은 경우 해당 구성 요소를 설치하라는 메시지가 나타날 수 있습니다.  
  
2.  Windows Installer 4.5가 필요하며 이는 설치 마법사에 의해 설치될 수 있습니다. 컴퓨터를 다시 시작하라는 메시지가 표시되면 컴퓨터를 다시 시작한 다음 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 다시 시작합니다.  
  
3.  필수 구성 요소를 설치하고 나면 설치 마법사를 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 센터가 시작됩니다. 클러스터링할 노드를 준비하려면 **고급** 페이지로 이동하여 **고급 클러스터 준비**를 클릭합니다.  
  
4.  시스템 구성 검사기가 컴퓨터에서 검색 작업을 실행합니다. 계속하려면 [!INCLUDE[clickOK](../../../includes/clickok-md.md)]. **자세한 정보 표시**를 클릭하여 화면에 세부 정보를 표시하거나 **자세한 보고서 보기**를 클릭하여 HTML 보고서 형식으로 볼 수 있습니다.  
  
5.  설치 지원 파일 페이지에서 **설치** 를 클릭하여 설치 지원 파일을 설치합니다.  
  
6.  시스템 구성 검사기가 설치를 계속하기 전에 컴퓨터의 시스템 상태를 확인합니다. 검사가 완료되면 **다음** 을 클릭하여 작업을 계속 진행합니다. **자세한 정보 표시**를 클릭하여 화면에 세부 정보를 표시하거나 **자세한 보고서 보기**를 클릭하여 HTML 보고서 형식으로 볼 수 있습니다.  
  
7.  지역화된 운영 체제에서 설치하고 있고 설치 미디어에 영어와 해당 운영 체제 언어에 대한 언어 팩이 둘 다 있는 경우 언어 선택 페이지에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 언어를 지정할 수 있습니다. 언어 간 호환성 지원 및 설치 고려 사항에 대한 자세한 내용은 [SQL Server의 로컬 언어 버전](../../../sql-server/install/local-language-versions-in-sql-server.md)을 참조하세요.  
  
     계속하려면 **다음**을 클릭합니다.  
  
8.  제품 키 페이지에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]무료 버전을 설치할지 아니면 제품의 프로덕션 버전에 대한 PID 키가 있는지 표시합니다. 자세한 내용은 [SQL Server 2016 버전 및 구성 요소](../../../sql-server/editions-and-components-of-sql-server-2016.md)를 참조하세요.  
  
    > [!NOTE]  
    >  동일한 장애 조치(Failover) 클러스터를 위해 준비하고 있는 모든 노드에서 동일한 제품 키를 지정해야 합니다.  
  
9. 사용 조건 페이지에서 사용권 계약을 읽은 다음 사용 조건과 계약 조건에 동의하면 해당 확인란을 선택합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 개선을 돕기 위해 기능 사용 옵션을 사용하도록 설정하여 [!INCLUDE[msCoName](../../../includes/msconame-md.md)]로 보고서를 보낼 수도 있습니다. 계속하려면 **다음** 을 클릭합니다. 설치를 끝내려면 **취소**를 클릭합니다.  
  
10. 기능 선택 페이지에서 설치할 구성 요소를 선택합니다. 기능 이름을 선택하면 오른쪽 창에 각 구성 요소 그룹에 대한 설명이 나타납니다. 확인란을 원하는 대로 선택할 수 있지만 장애 조치(Failover) 클러스터링을 지원하는 것은 테이블 형식 모드의 [!INCLUDE[ssDE](../../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 및 다차원 모드의 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 뿐입니다. 선택한 다른 구성 요소는 설치를 실행하고 있는 현재 노드에서 장애 조치(Failover) 기능 없이 독립 실행형 기능으로 실행됩니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 모드에 대한 자세한 내용은 [Analysis Services 인스턴스의 서버 모드 확인](../../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)을 참조하세요.  
  
     선택한 기능의 필수 구성 요소가 오른쪽 창에 표시됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램에서는 이미 설치되어 있지 않은 필수 구성 요소가 있는 경우 이 절차의 뒷부분에 설명된 설치 단계에서 이를 설치합니다.  
  
     이 페이지 아래 있는 필드를 사용하여 공유 구성 요소의 사용자 지정 디렉터리를 지정할 수 있습니다. 공유 구성 요소의 설치 경로를 변경하려면 대화 상자의 맨 아래에 있는 필드에서 경로를 업데이트하거나 줄임표 단추를 클릭하고 설치 디렉터리를 찾습니다. 기본 설치 경로는 C:\Program Files\\[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]\\입니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 서비스 기능을 선택하면 복제 및 전체 텍스트 검색이 모두 자동으로 선택됩니다. 이 하위 기능을 하나라도 선택 취소하면 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 서비스 기능도 선택 취소됩니다.  
  
11. 인스턴스 구성 페이지에서 기본 인스턴스를 설치할지 명명된 인스턴스를 설치할지 지정합니다.
  
     **인스턴스 ID** - 기본적으로 인스턴스 이름이 인스턴스 ID로 사용됩니다. 인스턴스 ID는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스의 설치 디렉터리 및 레지스트리 키를 식별하는 데 사용됩니다. 이는 기본 인스턴스와 명명된 인스턴스에 모두 해당됩니다. 기본 인스턴스의 경우 인스턴스 이름 및 인스턴스 ID는 MSSQLSERVER입니다. 기본값이 아닌 인스턴스 ID를 사용하려면 **인스턴스 ID** 입력란을 선택하고 값을 입력합니다.  
  
    > [!NOTE]  
    >  일반적인 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]독립 실행형 인스턴스의 경우 기본 인스턴스인지 명명된 인스턴스인지에 관계없이 **인스턴스 ID** 텍스트 상자에 기본값을 사용합니다.  
  
    > [!IMPORTANT]  
    >  장애 조치(Failover) 클러스터를 위해 준비한 모든 노드에 대해 동일한 인스턴스 ID를 사용합니다.  
  
     **인스턴스 루트 디렉터리** - 기본적으로 인스턴스 루트 디렉터리는 C:\Program Files\\[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]\\입니다. 기본이 아닌 루트 디렉터리를 지정하려면 제공된 필드를 사용하거나 줄임표 단추를 클릭하고 설치 폴더를 찾습니다.  
  
     **설치된 인스턴스** - 설치 프로그램을 실행 중인 컴퓨터에 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 표 형식으로 표시됩니다. 컴퓨터에 기본 인스턴스가 이미 설치된 경우 명명된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스를 설치해야 합니다. 계속하려면 **다음** 을 클릭합니다.  
  
12. 디스크 공간 요구 사항 페이지에서는 사용자가 지정한 기능에 필요한 디스크 공간을 계산한 후 설치 프로그램을 실행 중인 컴퓨터에서 사용 가능한 디스크 공간과 실제로 필요한 디스크 공간의 크기를 비교하여 보여 줍니다.  
  
13. 이 페이지를 사용하여 클러스터 보안 정책을 지정할 수 있습니다.  
  
    -   [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] 이상 버전의 경우 서비스 SID(서버 보안 ID)를 사용하는 것이 좋으며 이는 기본 설정이기도 합니다. 이를 보안 그룹으로 변경하는 옵션은 없습니다. [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)]의 서비스 SID 기능에 대한 자세한 내용은 [Windows 서비스 계정 및 권한 구성](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조하세요. 이 기능은 [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]의 독립 실행형 클러스터 설치에서 테스트되었습니다.  
  
    -   [!INCLUDE[winxpsvr](../../../includes/winxpsvr-md.md)]에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스에 대한 도메인 그룹을 지정합니다. 모든 리소스 사용 권한은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정을 그룹 멤버로 포함하는 도메인 수준 그룹을 통해 제어됩니다.  
  
     계속하려면 **다음** 을 클릭합니다.  
  
14. 이 항목의 나머지 부분에 대한 워크플로는 설치에 대해 지정한 기능에 따라 달라집니다. 선택 항목에 따라 일부 페이지가 표시되지 않을 수도 있습니다.  
  
15. 서버 구성 - 서비스 계정 페이지에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스에 대한 로그인 계정을 지정합니다. 이 페이지에 구성된 실제 서비스는 사용자가 설치하도록 선택한 기능에 따라 달라집니다.  
  
     모든 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스에 동일한 로그인 계정을 할당하거나 각 서비스 계정을 따로 구성할 수 있습니다. 전체 텍스트 검색 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트를 비롯한 모든 클러스터 인식 서비스에 대해서는 시작 유형이 "수동"으로 설정되며 설치 과정에서 이를 변경할 수 없습니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 에서는 서비스 계정을 개별적으로 구성하여 각 서비스에 대해 최소한의 권한만 제공할 것을 권장합니다. 이렇게 하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스에서 태스크를 완료하는 데 필요한 최소한의 권한만 부여할 수 있습니다. 자세한 내용은 [Windows 서비스 계정 및 권한 구성](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조하세요.  
  
     이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스의 모든 서비스 계정에 대해 동일한 로그온 계정을 지정하려면 페이지 맨 아래에 있는 필드에 자격 증명을 입력합니다.  
  
     **보안 정보** [!INCLUDE[ssNoteStrongPass](../../../includes/ssnotestrongpass-md.md)]  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스에 대한 로그인 정보 지정을 완료하면 **다음**을 클릭합니다.  
  
16. **서버 구성 - 데이터 정렬** 탭을 사용하여 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 및 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에 대해 기본이 아닌 데이터 정렬을 지정할 수 있습니다.  
  
17. **서버 구성 - Filestream** 을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에 FILESTREAM을 설정합니다.  계속하려면 **다음** 을 클릭합니다.  
  
18. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 구성 페이지를 사용하여 만들 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 설치 유형을 지정할 수 있습니다. 장애 조치(Failover) 클러스터 설치의 경우 이 옵션은 구성되지 않은 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 설치로 설정됩니다. 설치를 완료한 후에 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 서비스를 구성해야 합니다.  
   
19. 오류 보고 페이지에서 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 개선에 도움이 되도록 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 보낼 정보를 지정할 수 있습니다. 오류 보고 옵션은 기본적으로 사용됩니다.  
  
20. 시스템 구성 검사기는 사용자가 지정한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기능에 따라 구성의 유효성을 검사하기 위해 하나 이상의 규칙 집합을 실행합니다.  
  
21. 설치 준비 완료 페이지에는 설치 중에 지정된 설치 옵션이 트리 뷰로 표시됩니다. 계속하려면 **설치**를 클릭합니다. 설치 프로그램은 선택한 기능에 대한 필수 구성 요소를 먼저 설치하고 그 다음에 기능을 설치합니다.  
  
     설치 중에 설치 진행률 페이지에서 제공하는 상태 정보를 통해 설치 진행률을 모니터링할 수 있습니다. 설치가 끝나면 설치 및 기타 중요한 참고 사항에 대한 요약 로그 파일을 볼 수 있는 링크가 **완료** 페이지에 제공됩니다.  
  
22. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 과정을 완료하려면 **닫기**를 클릭합니다.  
  
23. 컴퓨터를 다시 시작합니다. 설치가 끝나면 설치 마법사에 표시되는 메시지를 읽어야 합니다. 설치 로그 파일에 대한 자세한 내용은 [SQL Server 설치 로그 파일 보기 및 읽기](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)를 참조하세요.  
  
24. 지금까지 설명한 단계를 반복하여 장애 조치(Failover) 클러스터의 다른 노드를 준비합니다. 자동 생성된 구성 파일을 사용하여 다른 노드를 준비할 수도 있습니다. 자세한 내용은 [구성 파일을 사용하여 SQL Server 2016 설치](../../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)를 참조하세요.  
  
## <a name="complete"></a>완료  
  
#### <a name="advancedenterprise-failover-cluster-install-step-2-complete"></a>고급/엔터프라이즈 장애 조치(Failover) 클러스터 설치 2단계: 완료  
  
1.  [준비 단계](#prepare)에서 설명하는 대로 모든 노드를 준비했으면 준비된 노드 중 하나에서 설치를 실행합니다. 대부분의 경우 공유 디스크를 소유한 노드에서 설치를 실행합니다. **설치 센터의** 고급 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 페이지에서 **고급 클러스터 완료**를 클릭합니다.  
  
2.  시스템 구성 검사기가 컴퓨터에서 검색 작업을 실행합니다. 계속하려면 [!INCLUDE[clickOK](../../../includes/clickok-md.md)]. **자세한 정보 표시**를 클릭하여 화면에 세부 정보를 표시하거나 **자세한 보고서 보기**를 클릭하여 HTML 보고서 형식으로 볼 수 있습니다.  
  
3.  설치 지원 파일 페이지에서 **설치** 를 클릭하여 설치 지원 파일을 설치합니다.  
  
4.  시스템 구성 검사기가 설치를 계속하기 전에 컴퓨터의 시스템 상태를 확인합니다. 검사가 완료되면 **다음** 을 클릭하여 작업을 계속 진행합니다. **자세한 정보 표시**를 클릭하여 화면에 세부 정보를 표시하거나 **자세한 보고서 보기**를 클릭하여 HTML 보고서 형식으로 볼 수 있습니다.  
  
5.  지역화된 운영 체제에서 설치하고 있고 설치 미디어에 영어와 해당 운영 체제 언어에 대한 언어 팩이 둘 다 있는 경우 언어 선택 페이지에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 언어를 지정할 수 있습니다. 언어 간 호환성 지원 및 설치 고려 사항에 대한 자세한 내용은 [SQL Server의 로컬 언어 버전](../../../sql-server/install/local-language-versions-in-sql-server.md)을 참조하세요.  
  
     계속하려면 **다음**을 클릭합니다.  
  
6.  클러스터 노드 구성 페이지를 사용하여 클러스터링을 위해 준비한 인스턴스 이름을 선택하고 새 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터의 네트워크 이름을 지정합니다. 이 이름은 네트워크에서 장애 조치(Failover) 클러스터를 식별하는 데 사용되는 이름입니다.  
  
    > [!NOTE]  
    >  이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에서는 이를 가상 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이름이라고 했습니다.  
  
7.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램은 구성의 유효성을 검사하기 위해 선택한 기능을 기반으로 하나 이상의 규칙 집합을 실행합니다.  
  
8.  클러스터 리소스 그룹 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가상 서버 리소스를 배치할 클러스터 리소스 그룹 이름을 지정합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클러스터 리소스 그룹 이름을 지정하는 방법에는 두 가지가 있습니다.  
  
    -   목록에서 사용할 기존 그룹을 지정합니다.  
  
    -   새로 만들 그룹의 이름을 입력합니다. "Available storage"는 유효한 그룹 이름이 아닙니다.  
  
9. 클러스터 디스크 선택 페이지에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에 대한 공유 클러스터 디스크 리소스를 선택합니다. 클러스터 디스크에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터가 저장됩니다. 디스크를 여러 개 지정할 수 있습니다. 사용 가능한 공유 디스크 표에는 사용 가능한 디스크 목록, 각 디스크가 공유 디스크로 정규화되었는지 여부 및 각 디스크 리소스에 대한 설명이 표시됩니다. 계속하려면 **다음** 을 클릭합니다.  
  
    > [!NOTE]  
    >  모든 데이터베이스에 대해 첫 번째 드라이브가 기본 드라이브로 사용되지만 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 또는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 구성 페이지에서 이를 변경할 수 있습니다.  
  
10. 클러스터 네트워크 구성 페이지에서 장애 조치(Failover) 클러스터 인스턴스에 대한 네트워크 리소스를 지정합니다.  
  
    -   **네트워크 설정** – 장애 조치(Failover) 클러스터 인스턴스의 모든 노드 및 서브넷에 대한 IP 유형과 IP 주소를 지정합니다. 다중 서브넷 장애 조치(Failover) 클러스터에 대해 여러 IP 주소를 지정할 수 있지만 IP 주소는 서브넷별로 하나씩만 지원됩니다. 모든 준비된 노드는 하나 이상의 IP 주소에 대한 소유자여야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에 여러 서브넷이 있는 경우 IP 주소 리소스 종속성을 OR로 설정하라는 메시지가 나타납니다.  
  
     계속하려면 **다음** 을 클릭합니다.  
  
11. 이 항목의 나머지 부분에 대한 워크플로는 설치에 대해 지정한 기능에 따라 달라집니다. 선택 항목에 따라 일부 페이지가 표시되지 않을 수도 있습니다.  
  
12. [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 구성 - 계정 프로비전 페이지를 사용하여 다음을 지정합니다.  
  
    -   보안 모드 - [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에 대한 인증(Windows 인증 또는 혼합 모드 인증)을 선택합니다. 혼합 모드 인증을 선택할 경우 기본 제공 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 시스템 관리자 계정에 강력한 암호를 제공해야 합니다.  
  
         디바이스가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 성공적으로 연결되면 Windows 인증 및 혼합 모드에 모두 동일한 보안 메커니즘이 적용됩니다.  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 관리자 - [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에 대한 시스템 관리자를 한 명 이상 지정해야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 실행하는 계정을 추가하려면 **현재 사용자 추가**를 클릭합니다. 시스템 관리자 목록에 계정을 추가하거나 목록의 계정을 제거하려면 **추가** 또는 **제거**를 클릭한 다음 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에 대한 관리자 권한을 가질 사용자, 그룹 또는 컴퓨터 목록을 편집합니다.  
  
     목록 편집을 마쳤으면 [!INCLUDE[clickOK](../../../includes/clickok-md.md)]. 구성 대화 상자에서 관리자 목록을 확인합니다. 목록 구성을 완료했으면 **다음**을 클릭합니다.  
  
13. [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 구성 - 데이터 디렉터리 페이지를 사용하여 기본이 아닌 설치 디렉터리를 지정합니다. 기본 디렉터리에 설치하려면 **다음**을 클릭합니다.  
  
    > [!IMPORTANT]  
    >  기본이 아닌 설치 디렉터리를 지정하는 경우 해당 설치 폴더가 이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에만 사용되도록 해야 합니다. 이 대화 상자의 어떠한 디렉터리도 다른 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스의 디렉터리와 공유되지 않아야 합니다. 데이터 디렉터리는 장애 조치(Failover) 클러스터의 공유 클러스터 디스크에 배치해야 합니다.  
  
  
14. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 구성 - 계정 프로비전 페이지를 사용하여 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에 대해 관리자 권한을 갖는 사용자 또는 계정을 지정합니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에 대한 시스템 관리자를 한 명 이상 지정해야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 실행하는 계정을 추가하려면 **현재 사용자 추가**를 클릭합니다. 시스템 관리자 목록에 계정을 추가하거나 목록의 계정을 제거하려면 **추가** 또는 **제거**를 클릭한 다음 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에 대한 관리자 권한을 가질 사용자, 그룹 또는 컴퓨터 목록을 편집합니다.  
  
     목록 편집을 마쳤으면 [!INCLUDE[clickOK](../../../includes/clickok-md.md)]. 구성 대화 상자에서 관리자 목록을 확인합니다. 목록 구성을 완료했으면 **다음**을 클릭합니다.  
  
15. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 구성 - 데이터 디렉터리 페이지를 사용하여 기본이 아닌 설치 디렉터리를 지정합니다. 기본 디렉터리에 설치하려면 **다음**을 클릭합니다.  
  
    > [!IMPORTANT]  
    >  기본이 아닌 설치 디렉터리를 지정하는 경우 해당 설치 폴더가 이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에만 사용되도록 해야 합니다. 이 대화 상자의 어떠한 디렉터리도 다른 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스의 디렉터리와 공유되지 않아야 합니다. 데이터 디렉터리는 장애 조치(Failover) 클러스터의 공유 클러스터 디스크에 배치해야 합니다.  
  
  
16. 시스템 구성 검사기는 사용자가 지정한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기능에 따라 구성의 유효성을 검사하기 위해 하나 이상의 규칙 집합을 실행합니다.  
  
17. 설치 준비 완료 페이지에는 설치 중에 지정된 설치 옵션이 트리 뷰로 표시됩니다. 계속하려면 **설치**를 클릭합니다. 설치 프로그램은 선택한 기능에 대한 필수 구성 요소를 먼저 설치하고 그 다음에 기능을 설치합니다.  
  
18. 설치 중에 설치 진행률 페이지에서 제공하는 상태 정보를 통해 설치 진행률을 모니터링할 수 있습니다.  
  
19. 설치가 끝나면 설치 및 기타 중요한 참고 사항에 대한 요약 로그 파일을 볼 수 있는 링크가 **완료** 페이지에 제공됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 과정을 완료하려면 **닫기**를 클릭합니다. 동일한 장애 조치(Failover) 클러스터를 위해 준비한 모든 노드가 이제 이 단계를 통해 최종 완료된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터의 일부가 됩니다.  
  
## <a name="next-steps"></a>Next Steps  
 **새 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 구성** - 공격받을 수 있는 시스템의 노출 영역을 줄이려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 핵심 서비스와 기능을 선별적으로 설치하고 활성화합니다. 자세한 내용은 [Surface Area Configuration](../../../relational-databases/security/surface-area-configuration.md)을 참조하세요.  
  
 로그 파일 위치에 대한 자세한 내용은 [SQL Server 설치 로그 파일 보기 및 읽기](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [명령 프롬프트에서 SQL Server 2016 설치](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  
  
  
