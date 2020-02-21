---
title: 장애 조치(Failover) 클러스터링을 설치하기 전에 | Microsoft 문서
ms.custom: ''
ms.date: 08/24/2016
ms.reviewer: ''
ms.prod: sql
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- clusters [SQL Server], preinstallation checklist
- installing failover clusters
- failover clustering [SQL Server], preinstallation checklist
ms.assetid: a655225d-8c54-4b30-95fd-31f588167899
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5d2fe2d80b0f9d54e877d6bc1be9a05c8c34c584
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "72517935"
---
# <a name="before-installing-failover-clustering"></a>장애 조치(Failover) 클러스터링을 설치하기 전에
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQL Server 장애 조치(Failover) 클러스터를 설치하기 전에 SQL Server에서 실행할 하드웨어와 운영 체제를 선택해야 합니다. 또한 WSFC(Windows Server 장애 조치(Failover) 클러스터링)를 구성하고 네트워크, 보안 및 기타 장애 조치(Failover) 클러스터에서 실행할 소프트웨어에 대한 고려 사항을 검토해야 합니다.  
  
 Windows 클러스터에 로컬 디스크 드라이브가 있고, 하나 이상의 클러스터 노드에서 같은 드라이브 문자가 공유 드라이브로 사용된 경우 해당 드라이브에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 을 설치할 수 없습니다. 이 제한은 SQL Server 장애 조치(failover) 클러스터 인스턴스와 Windows 장애 조치 클러스터 인스턴스의 일부인 서버에 있는 독립 실행형 인스턴스에 모두 적용됩니다.
  
 그리고 다음 항목들을 검토하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터링 개념과 기능 및 태스크를 보다 자세히 배울 수 있습니다.  
  
|항목 설명|항목|  
|-----------------------|-----------|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터링 개념에 대해 설명하고 연관된 콘텐츠 및 태스크에 대한 링크를 제공합니다.|[Always On 장애 조치(failover) 클러스터 인스턴스&#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 정책 개념에 대해 설명하고 조직 요구 사항에 맞는 장애 조치(Failover) 정책 구성과 관련된 링크를 제공합니다.|[Failover Policy for Failover Cluster Instances](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)|  
|기존 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터를 유지 관리하는 방법에 대해 설명합니다.|[장애 조치(failover) 클러스터 인스턴스 관리 및 유지 관리](../../../sql-server/failover-clusters/windows/failover-cluster-instance-administration-and-maintenance.md)|  
|WSFC(Windows Server Failover Cluster)에 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 를 설치하는 방법에 대해 설명합니다.|[SSAS(SQL Server Analysis Services) 클러스터링 방법](https://go.microsoft.com/fwlink/p/?LinkId=396548)|  
  
 
  
##  <a name="BestPractices"></a> 최선의 구현 방법  
  
-   [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [릴리스 정보](https://go.microsoft.com/fwlink/?LinkId=296445) 검토  
  
-   필수 구성 요소 소프트웨어를 설치합니다. 설치 프로그램을 실행하여 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]를 설치하거나 업그레이드하기 전에 다음과 같은 필수 구성 요소를 설치하여 설치 시간을 절약합니다. 각 장애 조치(Failover) 클러스터 노드에 필수 구성 요소 소프트웨어를 설치하고 노드를 한 번 다시 시작한 후 설치 프로그램을 실행해야 합니다.  
  
    -   Windows PowerShell은 더 이상 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램으로 설치되지 않습니다. [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)][!INCLUDE[ssDE](../../../includes/ssde-md.md)] 구성 요소 및 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]을 설치하려면 Windows PowerShell이 필요합니다. Windows PowerShell이 컴퓨터에 설치되어 있지 않은 경우 [Windows 관리 프레임워크](https://go.microsoft.com/fwlink/?LinkId=186214) 페이지에 나오는 지침에 따라 PowerShell을 사용하도록 설정할 수 있습니다.  
  
    -   .NET Framework 3.5 SP1은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램으로 더 이상 설치되지 않지만 이전 버전의 Windows 운영 체제에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 설치할 경우 필요할 수 있습니다. 자세한 내용은 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)][릴리스 정보](https://go.microsoft.com/fwlink/?LinkId=296445)를 참조하십시오.  
  
    -   **[!INCLUDE[msCoName](../../../includes/msconame-md.md)] 업데이트 패키지:** 설치 중 .NET Framework 4 설치로 인한 컴퓨터 다시 시작을 방지하려면 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 설치 전 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 업데이트가 컴퓨터에 설치되어 있어야 합니다.  [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 를 Windows 7 SP1 또는 [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] SP2에 설치하는 경우 이 업데이트가 포함됩니다. 이전 버전의 Windows 운영 체제에 설치하는 경우 [Windows Vista 및 Windows Server 2008의 .NET Framework 4.0용 Microsoft Update](https://go.microsoft.com/fwlink/?LinkId=198093)에서 다운로드하십시오.  
  
    -   .NET Framework 4: 설치 프로그램에서는 클러스터링된 운영 체제에 .NET Framework 4를 설치합니다. 설치 시간을 단축하려면 설치 프로그램을 실행하기 전에 .NET Framework 4를 설치하는 것이 좋습니다.  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 지원 파일. [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 설치 미디어에 있는 SqlSupport.msi를 실행하여 이러한 파일을 설치할 수 있습니다.  
  
-   바이러스 백신 소프트웨어가 WSFC 클러스터에 설치되지 않았는지 확인합니다. 자세한 내용은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 기술 자료 문서 [클러스터 서비스에서 백신 소프트웨어를 사용하면 문제가 발생할 수 있다(Antivirus software may cause problems with cluster services)](https://go.microsoft.com/fwlink/?LinkId=116986)를 참조하십시오.  
  
-   장애 조치(Failover) 클러스터 설치를 위한 클러스터 그룹의 이름을 지정할 경우 다음과 같은 문자를 클러스터 그룹 이름에 사용하면 안 됩니다.  
  
    -   보다 작음 연산자(\<)  
  
    -   보다 큼 연산자(>)  
  
    -   큰따옴표(")  
  
    -   작은따옴표(')  
  
    -   앰퍼샌드 (&)  
  
     또한 기존 클러스터 그룹 이름에 지원되지 않는 문자가 포함되지 않았는지 확인합니다.  
  
-   COM+, 디스크 드라이브 문자 및 관리자 그룹의 사용자 등을 포함하는 요소들을 모든 클러스터 노드에 동일하게 구성해야 합니다.  
  
-   모든 노드의 시스템 로그를 지우고 시스템 로그를 다시 확인합니다. 계속하기 전 로그에 오류 메시지가 없는지 확인합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터를 설치하거나 업그레이드하기 전에는 설치하는 동안 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 요소를 사용할 수 있는 모든 애플리케이션과 서비스를 비활성화해야 합니다. 이때 디스크 리소스는 온라인 상태로 둡니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클러스터 그룹과 장애 조치(Failover) 클러스터에 포함될 디스크 간의 종속성을 자동으로 설정합니다. 설치 전에 디스크에 종속성을 설정하지 마십시오.  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터를 설치하는 동안 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 네트워크 리소스 이름에 대한 컴퓨터 개체(Active Directory 컴퓨터 계정)가 생성됩니다. [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] 클러스터에서 클러스터 이름 계정(클러스터 자체의 컴퓨터 계정)에 컴퓨터 개체를 생성할 수 있는 권한이 있어야 합니다. 자세한 내용은 [장애 조치 클러스터 단계별 가이드: Active Directory에서 계정 구성](https://technet.microsoft.com/library/cc731002\(WS.10\).aspx)을 참조하십시오.  
  
    -   스토리지 옵션으로 SMB 파일 공유를 사용 중인 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 계정에는 파일 서버에 대한 SeSecurityPrivilege가 있어야 합니다. 이렇게 하려면 파일 서버의 로컬 보안 정책 콘솔을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 계정을 **감사 및 보안 로그 관리** 권한에 추가합니다.  
  
##  <a name="Hardware"></a> 하드웨어 솔루션 확인  
  
-   클러스터 솔루션에 지리적으로 분산된 클러스터 노드가 포함된 경우 네트워크 대기 시간 및 공유 디스크 지원과 같은 추가 항목을 확인해야 합니다.  
  
    -   [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] 및 [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]에 대한 자세한 내용은 [장애 조치(Failover) 클러스터에 대한 하드웨어 유효성 검사](https://go.microsoft.com/fwlink/?LinkId=196817) 및 [Windows 장애 조치(Failover) 클러스터에 대한 지원 정책](https://go.microsoft.com/fwlink/?LinkId=196818)을 참조하십시오.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 설치할 디스크가 압축되거나 암호화되지 않았는지 확인합니다. 압축된 드라이브 또는 암호화된 드라이브에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 설치하려고 시도하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램이 실패합니다.  
  
-   SAN 구성은 [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] 및 [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] Advanced Server 및 Datacenter Server 버전에서도 지원됩니다. Windows 카탈로그 및 하드웨어 호환성 목록 범주인 &quot;클러스터/다중 클러스터 디바이스&quot;에는 다중 WSFC 클러스터가 연결된 SAN 스토리지 디바이스로 지원되며 테스트를 마친 SAN 사용 가능 스토리지 디바이스 집합이 나열되어 있습니다. 인증된 구성 요소를 찾은 후 클러스터 유효성 검사를 실행하십시오.  
  
-   데이터 파일 설치에는 SMB 파일 공유도 지원됩니다. 자세한 내용은 [Storage Types for Data Files](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes)를 참조하세요.  
  
    > [!WARNING]  
    >  SMB 파일 공유 스토리지로 Windows 파일 서버를 사용 중인 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 계정에는 파일 서버에 대한 SeSecurityPrivilege가 있어야 합니다. 이렇게 하려면 파일 서버의 로컬 보안 정책 콘솔을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 계정을 **감사 및 보안 로그 관리** 권한에 추가합니다.  
    >   
    >  Windows 파일 서버 외의 SMB 파일 공유 스토리지를 사용 중인 경우 스토리지 공급업체에 파일 서버 쪽의 해당 설정에 대해 문의하십시오.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 탑재 지점을 지원합니다.  
  
     탑재된 볼륨 또는 탑재 지점을 사용하면 하나의 드라이브 문자를 사용하여 여러 디스크 또는 볼륨을 참조할 수 있습니다. 일반 디스크 또는 볼륨을 나타내는 드라이브 문자 D:가 있을 경우 고유의 드라이브 문자가 필요한 추가 디스크나 볼륨 없이 드라이브 문자 D:에서 추가 디스크나 볼륨을 디렉토리로 연결하거나 "마운팅"할 수 있습니다.  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터링을 위한 추가 탑재 지점 고려 사항:  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 실행하려면 탑재된 드라이브의 기본 드라이브에 연결된 드라이브 문자가 있어야 합니다. 장애 조치(Failover) 클러스터 설치를 위해서는 이 기본 드라이브가 클러스터형 드라이브여야 합니다. 이 릴리스에서는 볼륨 GUID가 지원되지 않습니다.  
  
    -   드라이브 문자가 있는 기본 드라이브는 장애 조치(Failover) 클러스터 인스턴스 간에 공유할 수 없습니다. 이는 장애 조치(Failover) 클러스터에 대한 일반적인 제한 사항이지만 독립 실행형 다중 인스턴스 서버에 대한 제한은 아닙니다.  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 클러스터형 설치는 사용 가능한 드라이브 문자의 수로 제한됩니다. 운영 체제에서 하나의 드라이브 문자만 사용하고 모든 다른 드라이브 문자를 일반 클러스터 드라이브 또는 클러스터 드라이브 호스팅 탑재 지점에 사용할 수 있다고 가정할 경우 장애 조치(Failover) 클러스터당 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 최대 25개로 제한됩니다.  
  
        > [!TIP]  
        >  25개의 인스턴스 제한은 SMB 파일 공유 옵션을 사용하여 확장할 수 있습니다. 스토리지 옵션으로 SMB 파일 공유를 사용할 경우 최대 50개까지 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스를 설치할 수 있습니다.  
  
    -   추가 드라이브를 마운트한 후에는 드라이브를 포맷할 수 없습니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 설치에서는 tempdb 파일 설치에 대해서만 로컬 디스크를 지원합니다. tempdb 데이터 및 로그 파일에 대해 지정된 경로가 모든 클러스터 노드에서 올바른지 확인하십시오. 장애 조치(failover) 중에 장애 조치 대상 노드에서 tempdb 디렉터리를 사용할 수 없으면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스가 온라인이 될 수 없습니다. 자세한 내용은 [Storage Types for Data Files](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes) 및 [Database Engine Configuration - Data Directories](https://msdn.microsoft.com/library/9b1fa0fc-623b-479a-afc3-4f13bd850487)를 참조하세요.  
  
-   iSCSI 기술 구성 요소에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터를 배포하는 경우 각별히 주의해야 합니다. 자세한 내용은 [iSCSI 기술 구성 요소의 SQL Server에 대한 지원](https://go.microsoft.com/fwlink/?LinkId=116960)을 참조하십시오.  
  
-   자세한 내용은 [Microsoft 클러스터링에 대한 SQL Server 지원 정책](https://go.microsoft.com/fwlink/?LinkId=116958)을 참조하십시오.  
  
-   적절한 쿼럼 드라이브 구성에 대한 자세한 내용은 [쿼럼 드라이브 구성 정보](https://go.microsoft.com/fwlink/?LinkId=196816)를 참조하십시오.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 원본 설치 파일과 클러스터가 서로 다른 도메인에 있을 때 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터를 설치하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에 사용할 수 있는 현재 도메인으로 설치 파일을 복사합니다.  
  
##  <a name="Security"></a> 보안 고려 사항 검토  
  
-   암호화를 사용하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터의 모든 노드에 WSFC 클러스터의 정규화된 DNS 이름을 가진 서버 인증서를 설치합니다. 예를 들어 "Test1.DomainName.com" 및 "Test2.DomainName.com"이라는 2개의 노드로 구성된 노드 클러스터와 "Virtsql"이라는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스가 있는 경우 "Virtsql.DomainName.com"에 대한 인증서를 구하여 test1 및 test2 노드에 인증서를 설치해야 합니다. 그런 다음 **구성 관리자의** 프로토콜 암호화 강제 사용 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 확인란을 선택하여 장애 조치(Failover) 클러스터에서 암호화를 사용하도록 구성할 수 있습니다.  
  
    > [!IMPORTANT]  
    >  장애 조치(failover) 클러스터 인스턴스의 모든 참여 노드에 인증서를 설치한 후에 **프로토콜 암호화 사용** 확인란을 선택합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치를 이전 버전과 함께 구성하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스는 전역 도메인 그룹에 있는 계정만 사용해야 합니다. 또한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스에서 사용하는 계정은 로컬 Administrators 그룹에 나타나지 않아야 합니다. 이 지침을 따르지 않으면 예기치 않은 보안 동작이 발생할 수 있습니다.  
  
-   장애 조치(Failover) 클러스터를 만들려면 서비스로 로그온할 수 있고 장애 조치(Failover) 클러스터 인스턴스의 모든 노드에서 운영 체제의 일부로 작동할 수 있는 권한을 가진 로컬 관리자여야 합니다.  
  
-   [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)]에서 서비스 SID는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 서비스에서 사용할 수 있도록 자동으로 생성됩니다. 이전 버전의 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 에서 업그레이드된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]장애 조치(Failover) 클러스터 인스턴스의 경우 기존 도메인 그룹 및 ACL 구성이 보존됩니다.  
  
-   도메인 그룹은 컴퓨터 계정과 같은 도메인 내에 있어야 합니다. 예를 들어 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 설치할 컴퓨터가 MYDOMAIN의 자식인 SQLSVR 도메인에 있는 경우 SQLSVR 도메인에 그룹을 지정해야 합니다. SQLSVR 도메인은 MYDOMAIN의 사용자 계정을 포함할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터링은 클러스터 노드가 도메인 컨트롤러인 경우 설치할 수 없습니다.  
  
-   [Security Considerations for a SQL Server Installation](../../../sql-server/install/security-considerations-for-a-sql-server-installation.md)의 내용을 검토합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 Kerberos 인증을 설정하려면 [기술 자료의](https://support.microsoft.com/kb/319723) SQL Server에서 Kerberos 인증을 사용하는 방법 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 을 참조하십시오.  

-   SQL Server FCI(장애 조치 클러스터 인스턴스)를 사용하려면 클러스터 노드가 도메인에 가입되어 있어야 합니다. 다음 구성은 **지원되지 않습니다**. 
    *   작업 그룹 클러스터에 대한 SQL FCI 
    *   다중 도메인 클러스터에 대한 SQL FCI   
    *   도메인 + 작업 그룹 클러스터에 대한 SQL FCI 

  
##  <a name="Network"></a> 네트워크, 포트 및 방화벽 고려 사항 검토  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 시작하기 전에 모든 프라이빗 네트워크 카드에서 NetBIOS를 해제했는지 확인합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 네트워크 이름과 IP 주소는 파일 공유와 같은 다른 목적을 위해 사용해서는 안 됩니다. 파일 공유 리소스를 만들려면 리소스에 다른 고유한 네트워크 이름과 IP 주소를 사용하십시오.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 동작과 성능에 영향을 줄 수 있으므로 데이터 드라이브에서의 파일 공유는 권장되지 않습니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 클러스터 안에서 TCP/IP를 통한 TCP/IP 소켓과 명명된 파이프를 모두 지원하더라도 클러스터형 구성에는 TCP/IP 소켓을 사용하는 것이 좋습니다.  
  
-   ISA 서버는 Windows 클러스터링에서 지원되지 않으므로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에서도 지원되지 않습니다.  
  
-   원격 레지스트리 서비스가 실행 중이어야 합니다.  
  
-   원격 관리를 설정해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 포트의 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 차단을 해제하려는 인스턴스의 TCP/IP 프로토콜에 대한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 네트워크 구성을 검사합니다. 설치 후 TCP를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 연결하려면 IPALL에 대한 TCP 포트를 설정해야 합니다. 기본적으로 SQL Browser는 UDP 포트 1434에서 수신합니다.  
  
-   장애 조치(Failover) 클러스터 설치 작업에는 네트워크 바인딩 순서를 검사하는 규칙이 포함됩니다. 바인딩 순서가 올바르게 보이더라도 시스템의 NIC 구성이 비활성화되었거나 "삭제"되었을 수 있습니다. "삭제된" NIC 구성은 바인딩 순서에 영향을 줄 수 있으며 바인딩 순서 규칙에서 경고가 발생하도록 할 수 있습니다. 이러한 상황을 방지하기 위해 다음 단계에 따라 비활성화된 네트워크 어댑터를 확인하고 제거합니다.  
  
    1.  명령 프롬프트에서 set devmgr_Show_Nonpersistent_Devices=1을 설정합니다.  
  
    2.  start Devmgmt.msc를 입력하고 실행합니다.  
  
    3.  네트워크 어댑터 목록을 확장합니다. 목록에는 실제 어댑터만 표시됩니다. 비활성화된 네트워크 어댑터가 있으면 설치 프로그램에서 네트워크 바인딩 순서 규칙 실패를 보고합니다. 제어판/네트워크 연결에서도 어댑터가 비활성화되었는지를 볼 수 있습니다. 제어판의 네트워크 설정에 표시되는 활성화된 실제 어댑터 목록이 devmgmt.msc에서 보여 주는 것과 동일한지 확인합니다.  
  
    4.  SQL Server 설치 프로그램을 실행하기 전에 비활성화된 네트워크 어댑터를 제거합니다.  
  
    5.  설치가 완료되면 제어판의 네트워크 연결로 돌아가서 현재 사용하고 있지 않은 모든 네트워크 어댑터를 비활성화합니다.  
  
##  <a name="OS_Support"></a> 운영 체제 확인  
 운영 체제가 올바르게 설치되었으며 장애 조치(Failover) 클러스터링을 지원하도록 디자인되었는지 확인합니다. 다음 표에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 버전과 각 버전을 지원하는 운영 체제의 목록이 나와 있습니다.  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 버전|[!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] Enterprise|[!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] Datacenter Server|[!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] Enterprise|[!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] Datacenter Server|  
|---------------------------------------|------------------------------------------------|-------------------------------------------------------|----------------------------------------------|-----------------------------------------------------|  
|[!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Enterprise(64비트) x64*|yes|yes|예**|예**|  
|[!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Enterprise(32비트)|yes|yes|||  
|[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] Developer(64비트)|yes|yes|예**|예**|  
|[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] Developer(32비트)|yes|yes|||  
|[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] Standard(64비트)|yes|yes|yes|yes|  
|[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] Standard(32비트)|yes|yes|||  
  
 *[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클러스터는 WOW 모드에서 지원되지 않습니다. 또한 WOW에 원래 설치했던 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에서 업그레이드하는 것도 지원되지 않습니다. 이 경우 업그레이드할 수 있는 유일한 방법은 새 버전을 추가로 설치한 후 마이그레이션하는 것 뿐입니다.  
  
 ** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다중 서브넷 장애 조치(failover) 클러스터링에 지원됩니다.  
  
##  <a name="MultiSubnet"></a> 다중 서브넷 구성을 위한 추가 고려 사항  
 아래 섹션에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다중 서브넷 장애 조치(Failover) 클러스터를 설치할 때 고려해야 하는 요구 사항에 대해 설명합니다. 다중 서브넷 구성에는 여러 서브넷 간의 클러스터링이 포함됩니다. 따라서 IP 주소가 여러 개 사용되고 IP 주소 리소스 종속성이 변경될 수 있습니다.  
  
### <a name="ssnoversion-edition-and-operating-system-considerations"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 버전 및 운영 체제 고려 사항  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다중 서브넷 장애 조치(failover) 클러스터를 지원하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 버전에 대한 자세한 내용은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다중 서브넷 장애 조치(Failover) 클러스터를 만들려면 먼저 여러 서브넷에서 [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] 다중 사이트 장애 조치(Failover) 클러스터를 만들어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터는 장애 조치(Failover) 시 IP 종속성 조건을 유지하기 위해 Windows Server 장애 조치(Failover) 클러스터에 종속됩니다.  
  
-   [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] 의 경우 모든 클러스터 서버가 동일한 Active Directory 도메인에 있어야 합니다. 따라서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다중 서브넷 장애 조치(Failover) 클러스터는 모든 클러스터 노드가 서브넷이 서로 다른 경우에도 동일한 Active Directory 도메인에 있어야 합니다.  
  
#### <a name="ip-address-and-ip-address-resource-dependencies"></a>IP 주소 및 IP 주소 리소스 종속성  
  
1.  IP 주소 리소스 종속성은 다중 서브넷 구성에서 OR로 설정됩니다. 자세한 내용은 [새 SQL Server 장애 조치(failover) 클러스터 만들기&#40;설치 프로그램&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)를 참조하세요.  
  
2.  Mixed AND-OR IP 주소 종속성은 지원되지 않습니다. 예: \<IP1> AND \<IP2> OR \<IP3>은 되지 않습니다.  
  
3.  서브넷당 둘 이상의 IP 주소는 지원되지 않습니다.  
  
     같은 서브넷에 대해 구성된 IP 주소를 두 개 이상 사용하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 시작하는 동안 클라이언트 연결 오류가 발생할 수 있습니다.  
  
#### <a name="related-content"></a>관련 내용  
 [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] 다중 사이트 장애 조치(failover)에 대한 자세한 내용은 [Windows Server 2008 R2 장애 조치(failover) 클러스터링 사이트](https://technet.microsoft.com/library/ff182338\(v=WS.10\).aspx) 및 [다중 사이트 장애 조치(failover) 클러스터에서 클러스터형 서비스 또는 애플리케이션 디자인](https://go.microsoft.com/fwlink/?LinkId=177873)을 참조하세요.  
  
##  <a name="WSFC"></a> Windows Server 장애 조치(Failover) 클러스터 구성  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Cluster Service(WSFC)는 하나 이상의 서버 클러스터 노드에 구성되어야 합니다. 또한 WSFC와 함께 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Enterprise, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Business Intelligence 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Standard를 실행해야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Enterprise는 최대 16개의 노드로 구성된 장애 조치(Failover) 클러스터를 지원합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Business Intelligence 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Standard는 2 노드 장애 조치(failover) 클러스터를 지원합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스에 대한 리소스 DLL은 WSFC 클러스터 관리자에서 사용되는 두 함수를 내보내 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스의 가용성을 검사합니다. 자세한 내용은 [장애 조치(failover) 클러스터 인스턴스용 장애 조치(failover) 정책](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)을 참조하세요.  
  
-   WSFC는 IsAlive 검사를 사용하여 장애 조치(Failover) 클러스터형 인스턴스가 실행 중인지 확인할 수 있어야 합니다. 이 작업을 수행하려면 트러스트된 연결을 사용하여 서버에 연결해야 합니다. 기본적으로 클러스터 서비스를 실행하는 계정은 클러스터의 노드에서 관리자로 구성되지 않으며 BUILTIN\Administrators 그룹은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 로그인 권한을 갖지 않습니다. 이러한 설정은 클러스터 노드에 대한 권한을 변경할 경우에만 변경됩니다.  
  
-   DNS(도메인 이름 서비스) 또는 WINS(Windows 인터넷 이름 서비스)를 구성합니다. DNS 서버 또는 WINS 서버는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터가 설치될 환경에서 실행되어야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 설치하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] IP 인터페이스 가상 참조의 동적 도메인 이름 서비스 등록이 필요합니다. DNS 서버 구성에서는 클러스터 노드가 네트워크 이름에 매핑된 온라인 IP 주소를 동적으로 등록할 수 있어야 합니다. 동적 등록을 완료할 수 없는 경우 설치 프로그램이 실패하고 설치가 롤백됩니다. 자세한 내용은 [기술 자료 문서](https://support.microsoft.com/kb/947048)를 참조하십시오.  
  
##  <a name="MSDTC"></a>[!INCLUDE[msCoName](../../../includes/msconame-md.md)] DTC(Distributed Transaction Coordinator) 설치  
 장애 조치(Failover) 클러스터에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 설치하기 전에 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] MSDTC(Distributed Transaction Coordinator) 클러스터 리소스를 만들어야 하는지 여부를 결정해야 합니다. [!INCLUDE[ssDE](../../../includes/ssde-md.md)]만 설치하는 경우 MSDTC 클러스터 리소스는 필요하지 않습니다. [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 과 SSIS 또는 워크스테이션 구성 요소를 설치하는 경우 또는 분산 트랜잭션을 사용하려는 경우에는 MSDTC를 설치해야 합니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]전용 인스턴스에는 MSDTC가 필요하지 않습니다.  
  
 [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] 및 [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]에서는 하나의 장애 조치(Failover) 클러스터에 여러 MSDTC 인스턴스를 설치할 수 있습니다. 설치된 MSDTC의 첫 번째 인스턴스는 MSDTC의 클러스터 기본 인스턴스가 됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 MSDTC 인스턴스를 자동으로 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로컬 클러스터 리소스 그룹에 설치된 MSDTC 인스턴스를 활용합니다. 그러나 개별 애플리케이션이 클러스터에 있는 임의의 MSDTC 인스턴스에 매핑될 수 있습니다.  
  
 다음 규칙은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 선택할 MSDTC 인스턴스에 적용됩니다.  
  
-   로컬 그룹에 설치된 MSDTC 사용  
  
-   MSDTC의 매핑된 인스턴스 사용  
  
-   MSDTC의 클러스터 기본 인스턴스 사용  
  
-   로컬 머신에 설치된 MSDTC 인스턴스 사용  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 로컬 클러스터 그룹에 설치된 MSDTC 인스턴스가 실패한 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 MSDTC의 기본 클러스터 인스턴스 또는 로컬 컴퓨터 인스턴스를 사용하려고 자동으로 시도하지 않습니다. 다른 MSDTC 인스턴스를 사용하려면 실패한 MSDTC 인스턴스를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 그룹에서 완전히 제거해야 합니다. 마찬가지로, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 대한 매핑을 만든 경우 매핑된 MSDTC 인스턴스가 실패하면 분산 트랜잭션도 실패합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서 다른 MSDTC 인스턴스를 사용하도록 하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 로컬 클러스터 그룹에 MSDTC 인스턴스를 추가하거나 매핑을 삭제해야 합니다.  
  
### <a name="configure-msconame-distributed-transaction-coordinator"></a>[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Distributed Transaction Coordinator 구성  
 운영 체제를 설치하고 클러스터를 구성한 다음에는 클러스터 관리자를 사용하여 MSDTC가 클러스터에서 작동하도록 구성해야 합니다. MSDTC 클러스터링에 실패해도 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치에는 문제가 없지만 MSDTC가 올바로 구성되지 않으면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 애플리케이션의 기능에 영향을 줄 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2016 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [시스템 구성 검사기의 검사 매개 변수](../../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)   
 [장애 조치(failover) 클러스터 인스턴스 관리 및 유지 관리](../../../sql-server/failover-clusters/windows/failover-cluster-instance-administration-and-maintenance.md)  
  
  

