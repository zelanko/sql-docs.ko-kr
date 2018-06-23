---
title: 필수 구성 요소, 제한 사항 및 AlwaysOn 가용성 그룹 (SQL Server)에 대 한 권장 사항 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], WSFC clusters
- Availability Groups [SQL Server], about
- Availability Groups [SQL Server], prerequisites and restrictions
- Availability Groups [SQL Server], Failover Cluster Instances
- Availability Groups [SQL Server], databases
- Availability Groups [SQL Server]
ms.assetid: edbab896-42bb-4d17-8d75-e92ca11f7abb
caps.latest.revision: 146
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: 299d93dbafce40b4e610258c6238d3b72b953f9c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36186839"
---
# <a name="prerequisites-restrictions-and-recommendations-for-alwayson-availability-groups-sql-server"></a>온라인 설명서의 AlwaysOn 가용성 그룹(SQL Server)에 대한 필수 구성 요소, 제한 사항 및 권장 사항
  이 항목에서는 호스트 컴퓨터, WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터, 서버 인스턴스 및 가용성 그룹에 대한 필수 구성 요소, 제한 사항 및 권장 사항을 비롯하여 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 배포할 때 고려해야 할 사항에 대해 설명합니다. 이러한 각 구성 요소에 대한 보안 고려 사항과 필요한 권한이 있는 경우 알려줍니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 배포하기 전에 이 항목의 모든 섹션을 읽어 보십시오.  
  
 
  
##  <a name="DotNetHotfixes"></a> AlwaysOn 가용성 그룹을 지 원하는.Net 핫픽스  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 에 사용할 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]구성 요소 및 기능에 따라 다음 표에서 확인할 수 있는 추가 .Net 핫픽스를 설치해야 할 수 있습니다. 이러한 핫픽스는 순서에 관계없이 설치할 수 있습니다.  
  
||종속 기능|핫픽스|링크|  
|------|-----------------------|------------|----------|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]|.Net 3.5 SP1 핫픽스는 읽기 전용 및 multisubnetFailover의 AlwaysOn 기능을 위한 SQL 클라이언트에 대한 지원을 추가합니다. 각 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 보고서 서버에 핫픽스를 설치해야 합니다.|KB 2654347: [AlwaysOn 기능 지원을 추가하기 위한 .Net 3.5 SP1 핫픽스](http://go.microsoft.com/fwlink/?LinkId=242896)|  
  
##  <a name="SystemReqsForAOAG"></a> Windows 시스템 요구 사항 및 권장 사항  
  
  
###  <a name="SystemRequirements"></a> 검사 목록: 요구 사항(Windows 시스템)  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 기능을 지원하려면 하나 이상의 가용성 그룹에 참여할 모든 컴퓨터가 다음 기본 요구 사항을 충족해야 합니다.  
  
||요구 사항|링크|  
|------|-----------------|----------|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|시스템이 도메인 컨트롤러가 아닌지 확인하세요.|가용성 그룹은 도메인 컨트롤러에서 지원되지 않습니다.|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|각 컴퓨터에서 x86(비 WOW64) 또는 x64 Windows Server 2008 이상 버전이 실행되고 있어야 합니다.|WOW64(Windows 32-bit on Windows 64-bit)에서는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 지원하지 않습니다.|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|각 컴퓨터가 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터의 노드여야 합니다.|[SQL Server의 WSFC&#40;Windows Server 장애 조치(failover) 클러스터링&#41;](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|WSFC 클러스터에 가용성 그룹 구성을 지원하기에 충분한 노드가 포함되어 있어야 합니다.|WSFC 노드는 특정 가용성 그룹에 대한 하나의 가용성 복제본만 호스팅할 수 있습니다. 특정 WSFC 노드에서는 하나 이상의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 여러 가용성 그룹의 가용성 복제본을 호스팅할 수 있습니다.<br /><br /> 계획된 가용성 그룹의 가용성 복제본을 지원하는 데 필요한 WSFC 노드 수를 해당 데이터베이스 관리자에게 문의하세요.<br /><br /> [AlwaysOn 가용성 그룹 개요&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|적용 가능한 모든 Windows 핫픽스가 WSFC 클러스터의 모든 노드에 설치되어 있는지 확인합니다.|**\*\* 중요 한 \* \***  는 많은 수의 핫픽스가 필요 하거나 클러스터는 WSFC 노드에 대 한 권장 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 배포 되 고 있습니다. 자세한 내용은 이 섹션의 뒷부분에 나오는 [AlwaysOn 가용성 그룹을 지원하는 Windows 핫픽스(Windows 시스템)](#WinHotfixes)을 참조하십시오.|  
  
> [!IMPORTANT]  
>  또한 시스템이 가용성 그룹에 연결되도록 올바르게 구성되었는지 확인합니다. 자세한 내용은 참조 [AlwaysOn 클라이언트 연결 (SQL Server)](always-on-client-connectivity-sql-server.md)합니다.  
  
####  <a name="WinHotfixes"></a> AlwaysOn 가용성 그룹 (Windows 시스템)을 지 원하는 Windows 핫픽스  
 클러스터 토폴로지에 따라 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 지원하기 위해 몇 가지 Windows Server 2008 SP2(서비스 팩 2) 또는 Windows Server 2008 R2 핫픽스를 추가로 적용할 수도 있습니다. 다음 표에서는 이러한 핫픽스에 대해 설명합니다. 이러한 핫픽스는 순서에 관계없이 설치할 수 있습니다.  
  
||Windows 2008 SP2에 적용|Windows 2008 R2 SP1에 적용|Windows 2012에 포함됨|지원 대상|핫픽스|링크|  
|------|---------------------------------|------------------------------------|------------------------------|-----------------|------------|----------|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|√|√|예|**최적의 WSFC 쿼럼 구성**|각 WSFC 노드에 기술 자료 문서 2494036에 설명되어 있는 핫픽스가 설치되어 있는지 확인합니다.<br /><br /> 이 핫픽스는 자동이 아닌 장애 조치(Failover) 대상에 대한 최적의 쿼럼 구성을 지원합니다. 이 기능을 사용하면 투표할 노드를 선택할 수 있으므로 다중 사이트 클러스터가 향상됩니다.|KB 2494036:  [Windows Server 2008 및 Windows Server 2008 R2에서 쿼럼 투표가 없는 클러스터 노드를 구성하는 데 사용할 수 있는 핫픽스](http://support.microsoft.com/kb/2494036)<br /><br /> 쿼럼 투표에 대한 자세한 내용은 [WSFC 쿼럼 모드 및 투표 구성&#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)을 참조하세요.|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|√|√|예|**보다 효율적인 네트워크 대역폭 사용**|각 WSFC 노드에 기술 자료 문서 2616514에 설명되어 있는 핫픽스가 설치되어 있는지 확인합니다.<br /><br /> 이 핫픽스가 없으면 클러스터 서비스가 클러스터 노드 간에 불필요한 레지스트리 알림을 보냅니다. 이 동작은 네트워크 대역폭을 제한하며 [!INCLUDE[ssHADRc](../../../includes/sshadrc-md.md)]에 심각한 문제가 됩니다.|KB 2616514:  [Windows Server 2008 또는 Windows Server 2008 R2에서 클러스터 서비스가 클러스터 노드 간에 불필요한 레지스트리 키 변경 알림을 보낸다](http://support.microsoft.com/kb/2616514)|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")||√|해당 사항 없음|**일부 WSFC 노드에서 사용할 수 없는 디스크에 대 한 테스트 한 VPD 저장소**|WSFC 노드에서 Windows Server 2008 R2 SP1(서비스 팩 1)을 실행 중일 때 WSFC 클러스터의 모든 노드에 사용할 수 없는 온라인 상태의 디스크에서 이 서비스 팩을 잘못 실행한 후 SCSI 장치 VPD(Vital Product Data) 유효성 검사 저장소 테스트가 실패할 경우 기술 자료 문서 2531907에 설명되어 있는 핫픽스를 설치해야 합니다.<br /><br /> 이 핫픽스를 사용하면 디스크가 온라인 상태일 때 유효성 검사 보고서에 잘못된 경고나 오류가 나타나지 않습니다.|KB 2531907:  [Windows Server 2008 R2 SP1을 설치한 후 SCSI 장치 VPD(Vital Product Data) 테스트 유효성 확인](http://support.microsoft.com/kb/2531907)|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")||√|예|**로컬 복제본으로 보다 빠르게 장애 조치할**|WSFC 노드에서 Windows Server 2008 R2 SP1(서비스 팩 1)을 실행하는 경우 기술 자료 문서 KB 2687741에 설명되어 있는 핫픽스가 설치되어 있는지 확인합니다.<br /><br /> 이 핫픽스를 사용하면 로컬 복제본으로의 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 장애 조치(Failover) 성능이 향상됩니다.|KB 2687741:  [SQL Server 2012에 포함된 "AlwaysOn 가용성 그룹" 기능의 성능을 향상시키는 핫픽스를 Windows Server 2008 R2에 사용할 수 있음](http://support.microsoft.com/KB/2687741)|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|√|√|예|**비대칭 저장소-장애 조치 클러스터 인스턴스 (Fci)에 대 한**|FCI(장애 조치(Failover) 클러스터 인스턴스)가 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에 대해 설정되어 있는 경우 Windows Server 2008 핫픽스 976097을 설치합니다.<br /><br /> 이 핫픽스는 장애 조치(Failover) 클러스터 MMC(Microsoft Management Console) 스냅인을 사용하여 비대칭 저장소(일부 WSFC 노드에서만 사용할 수 있는 공유 디스크)를 지원합니다.|KB 976097:  [Windows Server 2008 또는 Windows Server 2008 R2를 실행 중인 장애 조치(failover) 클러스터를 위한 장애 조치(Failover) 클러스터 MMC 스냅인에 비대칭 저장소에 대한 지원을 추가하는 핫픽스](http://support.microsoft.com/kb/976097)<br /><br /> [AlwaysOn 아키텍처 가이드: 장애 조치 클러스터 인스턴스 및 가용성 그룹을 사용 하 여 고가용성 및 재해 복구 솔루션 구축](http://technet.microsoft.com/library/jj215886.aspx)|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|√|√|해당 사항 없음|**인터넷 프로토콜 보안 (IPsec)**|IPsec 연결을 사용하는 환경에서는 클라이언트 컴퓨터에서 가상 네트워크 이름(이 컨텍스트의 경우 가용성 그룹 수신기)에 대한 IPSec 연결을 다시 설정할 때 시간이 많이 지연(약 2-3분)될 수 있습니다. IPsec 연결을 사용하는 경우 기술 자료 문서(KB 980915)에 설명된 특정 시나리오를 검토하는 것이 좋습니다.|KB 980915:  [Windows Server 2003, Windows Vista, Windows Server 2008, Windows 7 또는 Windows Server 2008 R2를 실행 중인 컴퓨터에서 IPSec를 다시 연결할 때 긴 시간 지연 발생](http://support.microsoft.com/kb/980915)|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|√|√|예|**I p v 6**|IPv6을 사용하는 경우 Windows Server 운영 체제에 따라 기술 자료 문서 2578103 또는 2578113에 설명된 특정 시나리오를 검토하는 것이 좋습니다.<br /><br /> Windows Server 토폴로지에서 IP 버전 6(IPv6)을 사용하는 경우 WSFC 클러스터 서비스가 IPv6 IP 주소를 장애 조치(Failover)하는 데 30초 정도 걸립니다. 따라서 클라이언트에서 IPv6 IP 주소에 다시 연결하려면 약 30초 동안 기다려야 합니다.|KB 2578103(Windows Server 2008):  [클러스터 서비스가 Windows Server 2008에서 IPv6 IP 주소를 장애 조치하는 데 30초 정도 걸림](http://support.microsoft.com/kb/2578103)<br /><br /> KB 2578113(Windows Server 2008 R2):  **Windows Server 2008 R2:** [클러스터 서비스가 Windows Server 2008 R2에서 IPv6 IP 주소를 장애 조치하는 데 30초 정도 걸림](http://support.microsoft.com/kb/2578113)|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|√|√|예|**서버 간에 라우터가 없음 클러스터 및 응용 프로그램**|장애 조치(Failover) 클러스터와 응용 프로그램 서버 사이에 라우터가 없는 경우 클러스터 서비스가 네트워크 관련 리소스를 느리게 장애 조치(Failover)합니다. 이에 따라 가용성 그룹이 장애 조치된 후 클라이언트 재연결이 지연됩니다. 라우터가 없으면 해당 환경에 적용 가능한 경우 기술 자료 문서 2582281에 설명된 특정 시나리오를 검토하는 것이 좋습니다.|KB 2582281:  [클러스터와 응용 프로그램 서버 사이에 라우터가 없는 경우 장애 조치(Failover) 작업이 느려진다](http://support.microsoft.com/kb/2582281)|  
  
###  <a name="ComputerRecommendations"></a> 가용성 복제본을 호스팅하는 컴퓨터에 대한 권장 사항(Windows 시스템)  
  
-   **동등한 시스템:**  특정 가용성 그룹의 모든 가용성 복제본은 동일한 작업을 처리할 수 있는 동등한 시스템에서 실행해야 합니다.  
  
-   **전용 네트워크 어댑터:**  최상의 성능을 위해 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]전용 네트워크 어댑터(네트워크 인터페이스 카드)를 사용하세요.  
  
-   **충분한 디스크 공간:**  가용성 복제본을 호스팅하는 서버 인스턴스가 있는 모든 컴퓨터에는 가용성 그룹의 모든 데이터베이스를 저장하기에 충분한 디스크 공간이 있어야 합니다. 주 데이터베이스의 크기가 늘어나면 해당하는 보조 데이터베이스도 같은 크기만큼 늘어난다는 것에 유의해야 합니다.  
  
###  <a name="PermissionsWindows"></a> 사용 권한(Windows 시스템)  
 WSFC 클러스터를 관리하려면 사용자가 모든 클러스터 노드에서 시스템 관리자여야 합니다.  
  
 클러스터 관리를 위한 계정에 대한 자세한 내용은 [부록 A: 장애 조치(failover) 클러스터 요구 사항](http://technet.microsoft.com/library/dd197454\(WS.10\).aspx)을 참조하세요.  
  
###  <a name="RelatedTasksWindows"></a> 관련 태스크(Windows 시스템)  
  
|태스크|링크|  
|----------|----------|  
|HostRecordTTL 값을 설정합니다.|[HostRecordTTL 변경(Windows PowerShell 사용)](#ChangeHostRecordTTLps)|  
  
####  <a name="ChangeHostRecordTTLps"></a> HostRecordTTL 변경(Windows PowerShell 사용)  
  
1.  **관리자 권한으로 실행**을 통해 PowerShell 창을 엽니다.  
  
2.  FailoverClusters 모듈을 가져옵니다.  
  
3.  사용 하 여는 `Get-ClusterResource` cmdlet을 사용 하 여 네트워크 이름 리소스를 찾은 `Set-ClusterParameter` 설정 하는 cmdlet는 `HostRecordTTL` 값을 다음과 같이 합니다.  
  
     Get-ClusterResource “*\<NetworkResourceName>*” | Set-ClusterParameter HostRecordTTL *\<TimeInSeconds>*  
  
     다음 PowerShell 예에서는 "`SQL Network Name (SQL35)`"이라는 네트워크 이름 리스스에 대해 HostRecordTTL을 300초로 설정합니다.  
  
    ```  
    Import-Module FailoverClusters  
  
    $nameResource = "SQL Network Name (SQL35)"  
    Get-ClusterResource $nameResource | Set-ClusterParameter ClusterParameter HostRecordTTL 300  
    ```  
  
    > [!TIP]  
    >  새 PowerShell 창을 열 때마다 가져와야 할는 `FailoverClusters` 모듈입니다.  
  
##### <a name="related-content-powershell"></a>관련 내용(PowerShell)  
  
-   [클러스터링 및 고가용성](http://blogs.msdn.com/b/clustering/archive/2009/05/23/9636665.aspx) (장애 조치(failover) 클러스터링 및 네트워크 부하 분산 팀 블로그)  
  
-   [장애 조치(Failover) 클러스터에서 Windows PowerShell 시작](http://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [클러스터 리소스 명령 및 해당 Windows PowerShell Cmdlet](http://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
###  <a name="RelatedContentWS"></a> 관련 콘텐츠(Windows 시스템)  
  
-   [다중 사이트 장애 조치(Failover) 클러스터에서 DNS 설정 구성](http://technet.microsoft.com/library/dd197562\(WS.10\).aspx)  
  
-   [네트워크 이름 리소스에 DNS 등록](http://blogs.msdn.com/b/clustering/archive/2009/07/17/9836756.aspx)  
  
-   [Windows 2008 R2 장애 조치 멀티 사이트 클러스터링](http://www.microsoft.com/windowsserver2008/en/us/failover-clustering-multisite.aspx)  
  
##  <a name="ServerInstance"></a> SQL Server 인스턴스 필수 구성 요소 및 제한 사항  
 각 가용성 그룹에는 *인스턴스에서 호스팅되는*가용성 복제본 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]이라는 일련의 장애 조치(Failover) 파트너가 필요합니다. 특정 서버 인스턴스는 *독립 실행형 인스턴스* 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]*장애 조치(failover) 클러스터 인스턴스* 일 수 있습니다.  
  
 
  
###  <a name="PrerequisitesSI"></a> 검사 목록: 필수 구성 요소(서버 인스턴스)  
  
||사전 요구 사항|링크|  
|-|------------------|-----------|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|호스트 컴퓨터는 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 노드여야 합니다. 지정된 가용성 그룹의 가용성 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스는 단일 WSFC 클러스터의 개별 노드에 있어야 합니다. 유일한 예외는 다른 WSFC 클러스터로 마이그레이션되는 동안 가용성 그룹이 일시적으로 두 클러스터에 걸쳐 있는 경우입니다.|[SQL Server의 WSFC&#40;Windows Server 장애 조치(failover) 클러스터링&#41;](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)<br /><br /> [장애 조치 클러스터링 및 AlwaysOn 가용성 그룹 &#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|가용성 그룹이 Kerberos로 작동하도록 하려는 경우:<br /><br /> 가용성 그룹에 대한 가용성 복제본을 호스팅하는 모든 서버 인스턴스는 동일한 SQL Server 서비스 계정을 사용해야 합니다.<br /><br /> 도메인 관리자는 가용성 그룹 수신기의 VNN(가상 네트워크 이름)에 대해 SQL Server 서비스 계정에서 Active Directory에 SPN(서비스 사용자 이름)을 수동으로 등록해야 합니다. SQL Server 서비스 계정이 아닌 다른 계정에 SPN이 등록된 경우 인증이 실패합니다.<br /><br /> **\*\* 중요 \*\*** SQL Server 서비스 계정을 변경하면 도메인 관리자가 SPN을 수동으로 다시 등록해야 합니다.|[Kerberos 연결의 서비스 사용자 이름 등록](../../configure-windows/register-a-service-principal-name-for-kerberos-connections.md)<br /><br /> **간략한 설명:**<br /><br /> Kerberos 및 SPN은 상호 인증을 강제 적용합니다. SPN은 SQL Server 서비스를 시작하는 Windows 계정에 매핑됩니다. SPN이 올바르게 등록되지 않았거나 실패하면, Windows 보안 계층이 SPN과 연결된 계정을 확인할 수 없으며, Kerberos 인증을 사용할 수 없습니다.<br /><br /> 참고: NTLM에는 이러한 요구 사항이 없습니다.|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI(장애 조치(Failover) 클러스터 인스턴스)를 사용하여 가용성 복제본을 호스팅하려는 경우 FCI 제한 사항을 이해하고 FCI 요구 사항을 충족해야 합니다.|[SQL Server FCI(장애 조치(failover) 클러스터 인스턴스)를 사용하여 가용성 복제본을 호스트하기 위한 필수 구성 요소 및 요구 사항](#FciArLimitations) (이 항목 뒷부분)|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|각 서버 인스턴스는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]Enterprise Edition을 실행해야 합니다.|[SQL Server 2014 버전에서 지원하는 기능](../../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|가용성 그룹의 가용성 복제본을 호스팅하는 모든 서버 인스턴스는 동일한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 정렬을 사용해야 합니다.|[서버 데이터 정렬 설정 또는 변경](../../../relational-databases/collations/set-or-change-the-server-collation.md)|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|가용성 그룹의 가용성 복제본을 호스팅할 각 서버 인스턴스에서 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 기능을 사용하도록 설정합니다. 특정 컴퓨터에서 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 설치에서 지원하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서버 인스턴스를 개수에 관계없이 사용하도록 설정할 수 있습니다.|[AlwaysOn 가용성 그룹 활성화 및 비활성화&#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)<br /><br /> **\*\* 중요 \*\*** WSFC 클러스터를 삭제한 다음 다시 만들려는 경우 원본 WSFC 클러스터에서 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 에 사용할 수 있도록 설정한 각 서버 인스턴스에서 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 기능을 사용하지 않도록 설정한 후 다시 사용하도록 설정해야 합니다.|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|각 서버 인스턴스에는 데이터베이스 미러링 끝점이 있어야 합니다. 이 끝점은 서버 인스턴스의 미러링 모니터 서버 및 데이터베이스 미러링 파트너와 모든 가용성 복제본에서 공유합니다.<br /><br /> 가용성 복제본을 호스트하도록 선택한 서버 인스턴스가 도메인 사용자 계정으로 실행되고 있고 아직 데이터베이스 미러링 끝점을 가지고 있지 않는 경우, [새 가용성 그룹 마법사](use-the-availability-group-wizard-sql-server-management-studio.md) (또는 [가용성 그룹에 복제본 추가 마법사](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)) 가 끝점을 만들고 서버 인스턴스 서비스 계정에 CONNECT 권한을 부여할 수 있습니다. 그러나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스가 로컬 시스템, 로컬 서비스 또는 네트워크 서비스와 같은 기본 제공 계정이나 비도메인 계정으로 실행 중인 경우에는 사용자가 끝점 인증을 위한 인증서를 사용해야 하며 마법사를 통해 서버 인스턴스에 대한 데이터베이스 미러링 끝점을 만들 수는 없습니다. 이 경우 마법사를 시작하기 전에 데이터 미러링 끝점을 수동으로 만드는 것이 좋습니다.<br /><br /> **\*\* 보안 정보 \*\*** [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 에 대한 전송 보안은 데이터베이스 미러링의 경우와 동일합니다.|[데이터베이스 미러링 끝점&#40;SQL Server&#41;](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)<br /><br /> [데이터베이스 미러링 및 AlwaysOn 가용성 그룹에 대 한 전송 보안 &#40;SQL Server&#41;](../../database-mirroring/transport-security-database-mirroring-always-on-availability.md)|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|FILESTREAM을 사용하는 데이터베이스를 가용성 그룹에 추가하려는 경우 가용성 그룹의 가용성 복제본을 호스팅할 모든 서버 인스턴스에 FILESTREAM이 설정되었는지 확인합니다.|[Enable and Configure FILESTREAM](../../../relational-databases/blob/enable-and-configure-filestream.md)|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|포함 된 데이터베이스는 가용성 그룹에 추가 될 경우 되도록는 `contained database authentication` 서버 옵션을 설정 `1` 가용성 그룹에 대 한 가용성 복제본을 호스팅할 모든 서버 인스턴스에서 합니다.|[contained database authentication 서버 구성 옵션](../../configure-windows/contained-database-authentication-server-configuration-option.md)<br /><br /> [서버 구성 옵션&#40;SQL Server&#41;](../../configure-windows/server-configuration-options-sql-server.md)|  
  
###  <a name="ThreadUsage"></a> 가용성 그룹의 스레드 사용량  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 은 작업자 스레드에 대해 다음 요구 사항을 충족해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 유휴 인스턴스에서 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 은 0개의 스레드를 사용합니다.  
  
-   가용성 그룹에서 사용되는 최대 스레드 수는 최대 서버 스레드 수('`max worker threads`')에서 40을 빼고 구성된 설정입니다.  
  
-   지정된 서버 인스턴스에서 호스팅되는 가용성 복제본은 단일 스레드 풀을 공유합니다.  
  
     스레드는 다음과 같이 요청 시 공유됩니다.  
  
    -   일반적으로 3-10개의 공유 스레드가 있지만 이 수는 주 복제본 작업에 따라 증가할 수 있습니다.  
  
    -   지정된 스레드가 얼마 동안 유휴 상태인 경우 일반 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 스레드 풀로 반환됩니다. 일반적으로 비활성 스레드는 아무 작업이 없는 상태가 지속된 지 15초 이내에 해제됩니다. 그러나 마지막 활동에 따라 유휴 스레드가 더 길게 유지될 수 있습니다.  
  
-   또한 가용성 그룹은 다음과 같이 비공유 스레드를 사용합니다.  
  
    -   각각의 주 복제본은 각 주 데이터베이스에 대해 1개의 로그 캡처 스레드를 사용합니다. 또한 각 보조 데이터베이스에 대해 1개의 로그 전송 스레드를 사용합니다. 로그 전송 스레드는 아무 작업이 없는 상태가 지속된 지 15초 이내에 해제됩니다.  
  
    -   각 보조 복제본은 각 보조 데이터베이스에 대해 1개의 다시 실행 스레드를 사용합니다. 다시 실행 스레드는 아무 작업이 없는 상태가 지속된 지 15초 이내에 해제됩니다.  
  
    -   보조 복제본의 백업은 백업 작업 시간 동안 주 스레드를 복제본에 보관합니다.  
  
 자세한 내용은 [AlwaysON - HADRON Learning Series: Worker Pool Usage for HADRON Enabled Databases](http://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)(AlwaysON - HADRON 학습 시리즈: HADRON 지원 데이터베이스에 대한 작업자 풀 사용)(CSS [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 엔지니어 블로그)을 참조하세요.  
  
###  <a name="PermissionsSI"></a> 사용 권한(서버 인스턴스)  
  
|태스크|필요한 권한|  
|----------|--------------------------|  
|데이터베이스 미러링 끝점 만들기|CREATE ENDPOINT 권한 또는 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  CONTROL ON ENDPOINT 권한도 필요합니다. 자세한 내용은 [GRANT 끝점 사용 권한&#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-endpoint-permissions-transact-sql)을 참조하세요.|  
|다음 사용 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]|로컬 컴퓨터 **관리자** 그룹의 멤버 자격과 WSFC 클러스터에 대한 모든 권한이 필요합니다.|  
  
###  <a name="RelatedTasksSI"></a> 관련 태스크(서버 인스턴스)  
  
|태스크|항목|  
|----------|-----------|  
|데이터베이스 미러링 끝점이 있는지 여부 확인|[sys.database_mirroring_endpoints&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)|  
|데이터베이스 미러링 끝점 만들기(없는 경우)|[Windows 인증에 대한 데이터베이스 미러링 끝점 만들기&#40;Transact-SQL&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)<br /><br /> [데이터베이스 미러링 끝점에 대한 인증서 사용&#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)<br /><br /> [데이터베이스를 AlwaysOn 가용성 그룹에 대 한 미러링 끝점 만들기 &#40;SQL Server PowerShell&#41;](database-mirroring-always-on-availability-groups-powershell.md)|  
|AlwaysOn 가용성 그룹 사용|[AlwaysOn 가용성 그룹 활성화 및 비활성화&#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)|  
  
###  <a name="RelatedContentSI"></a> 관련 내용(서버 인스턴스)  
  
-   [AlwaysON-HADRON 학습 시리즈: HADRON에 대 한 작업자 풀 사용 사용 데이터베이스](http://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
##  <a name="NetworkConnect"></a> 네트워크 연결 권장 사항  
 WSFC 클러스터 멤버 간의 통신 및 가용성 복제본 간의 통신에는 동일한 네트워크 링크를 사용하는 것이 좋습니다.  개별 네트워크 링크를 사용하면 가끔씩이라도 일부 링크에 문제가 발생할 경우 예기치 않은 동작이 발생할 수 있습니다.  
  
 예를 들어, 가용성 그룹으로 자동 장애 조치(Failover)를 지원하기 위해서는 자동 장애 조치(Failover) 파트너인 두 번째 복제본이 SYNCHRONIZED 상태여야 합니다. 이 보조 복제본에 대한 네트워크 링크가 가끔씩이라도 실패할 경우 복제본이 UNSYNCHRONIZED 상태가 되고 링크가 복원될 때까지 다시 동기화를 시작할 수 없습니다. 보조 복제본이 동기화되지 않은 상태에서 WSFC 클러스터가 자동 장애 조치(Failover)를 요청할 경우 자동 장애 조치(Failover)가 수행되지 않습니다.  
  
##  <a name="ClientConnSupport"></a> 클라이언트 연결 지원  
 에 대 한 내용은 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 클라이언트 연결에 대 한 지원, 참조 [AlwaysOn 클라이언트 연결 (SQL Server)](always-on-client-connectivity-sql-server.md)합니다.  
  
##  <a name="FciArLimitations"></a> SQL Server FCI(장애 조치(Failover) 클러스터 인스턴스)를 사용하여 가용성 복제본을 호스팅하기 위한 필수 구성 요소 및 제한 사항  
 
  
###  <a name="RestrictionsFCI"></a> 제한 사항(FCI)  
  
> [!NOTE]  
>  [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]부터 AlwaysOn 장애 조치(failover) 클러스터 인스턴스는 [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] 및 [!INCLUDE[win8srv](../../../includes/win8srv-md.md)] 모두에서 CSV(클러스터 공유 볼륨)를 지원합니다. CSV에 대한 자세한 내용은 [장애 조치(Failover) 클러스터에서 클러스터 공유 볼륨 이해](http://technet.microsoft.com/library/dd759255.aspx)를 참조하십시오.  
  
-   **FCI의 클러스터 노드는 특정 가용성 그룹에 대한 하나의 복제본만 호스팅할 수 있습니다.**  FCI에 가용성 복제본을 추가하는 경우 잠재적인 FCI 소유자인 WSFC 클러스터 노드는 동일한 가용성 그룹에 대해 다른 복제본을 호스팅할 수 없습니다.  
  
     또한 다른 모든 복제본은 동일한 WSFC 클러스터의 다른 WSFC 노드에 있는 SQL Server 2012 인스턴스에서 호스팅해야 합니다. 유일한 예외는 다른 WSFC 클러스터로 마이그레이션되는 동안 가용성 그룹이 일시적으로 두 클러스터에 걸쳐 있는 경우입니다.  
  
-   **FCI가 가용성 그룹별 자동 장애 조치(Failover)를 지원하지 않음:**  FCI는 가용성 그룹별 자동 장애 조치(Failover)를 지원하지 않으므로 FCI에서 호스팅하는 모든 가용성 복제본은 수동 장애 조치(Failover)에 대해서만 구성될 수 있습니다.  
  
-   **FCI 네트워크 이름 변경:**  가용성 복제본을 호스트하는 FCI의 네트워크 이름을 변경해야 하는 경우 복제본을 해당 가용성 그룹에서 제거한 다음 다시 가용성 그룹에 추가해야 합니다. 주 복제본은 제거할 수 없으므로 주 복제본을 호스팅하는 FCI의 이름을 바꾸려는 경우 보조 복제본으로 장애 조치한 다음 이전 주 복제본을 제거하고 다시 추가해야 합니다. FCI 이름을 바꾸면 해당 데이터베이스 미러링 끝점의 URL이 변경될 수 있습니다. 복제본을 추가할 때 현재 끝점 URL을 지정해야 합니다.  
  
###  <a name="PrerequisitesFCI"></a> 검사 목록: 필수 구성 요소(FCI)  
  
||사전 요구 사항|링크|  
|-|------------------|----------|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|FCI를 사용하여 가용성 복제본을 호스팅하기 전에 시스템 관리자가 기술 자료 문서 KB 976097에 설명된 Windows Server 2008 핫픽스를 설치했는지 확인합니다. 이 핫픽스는 장애 조치(Failover) 클러스터 MMC(Microsoft Management Console) 스냅인을 사용하여 비대칭 저장소(일부 WSFC 노드에서만 사용할 수 있는 공유 디스크)를 지원합니다.|KB 976097:  [Windows Server 2008 또는 Windows Server 2008 R2를 실행 중인 장애 조치(failover) 클러스터를 위한 장애 조치(Failover) 클러스터 MMC 스냅인에 비대칭 저장소에 대한 지원을 추가하는 핫픽스](http://support.microsoft.com/kb/976097)|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|각 SQL Server FCI(장애 조치(Failover) 클러스터 인스턴스)에 SQL Server FCI(장애 조치(Failover) 클러스터 인스턴스 설치별로 필요한 공유 저장소가 있는지 확인합니다.||  
  
###  <a name="RelatedTasksFCIs"></a> 관련 태스크(FCI)  
  
|태스크|항목|  
|----------|-----------|  
|SQL Server 장애 조치(Failover) 클러스터 설치|[새 SQL Server 장애 조치(failover) 클러스터 만들기&#40;설치 프로그램&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)|  
|SQL Server 장애 조치(Failover) 클러스터의 전체 업그레이드|[SQL Server 장애 조치(failover) 클러스터 인스턴스 업그레이드&#40;설치 프로그램&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)|  
|기존 SQL Server 장애 조치(Failover) 클러스터 유지 관리|[SQL Server 장애 조치(failover) 클러스터에서 노드 추가 또는 제거&#40;설치 프로그램&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)|  
  
###  <a name="RelatedContentFCIs"></a> 관련 내용(FCI)  
  
-   [장애 조치 클러스터링 및 AlwaysOn 가용성 그룹 &#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)  
  
-   [AlwaysOn 아키텍처 가이드: 장애 조치 클러스터 인스턴스 및 가용성 그룹을 사용 하 여 고가용성 및 재해 복구 솔루션 구축](http://technet.microsoft.com/library/jj215886.aspx)  
  
##  <a name="PrerequisitesForAGs"></a> 가용성 그룹 필수 구성 요소 및 제한 사항  

  
###  <a name="RestrictionsAG"></a> 제한 사항(가용성 그룹)  
  
-   **한 WSFC 클러스터의 다른 노드에서 가용성 복제본을 호스팅해야 함:**  특정 가용성 그룹의 가용성 복제본은 동일한 WSFC 클러스터의 다른 노드에서 실행되는 서버 인스턴스에서 호스팅해야 합니다. 유일한 예외는 다른 WSFC 클러스터로 마이그레이션되는 동안 가용성 그룹이 일시적으로 두 클러스터에 걸쳐 있는 경우입니다.  
  
    > [!NOTE]  
    >  동일한 실제 컴퓨터에 가상 머신이 있는 경우에는 각 가상 머신이 개별 컴퓨터 역할을 하므로 가상 머신별로 동일한 가용성 그룹의 가용성 복제본을 하나씩 호스팅할 수 있습니다.  
  
-   **고유 가용성 그룹 이름:**  각 가용성 그룹 이름은 WSFC 클러스터에서 고유해야 합니다. 가용성 그룹 이름의 최대 길이는 128자입니다.  
  
-   **가용성 복제본:**  각 가용성 그룹은 하나의 주 복제본과 최대 8개의 보조 복제본을 지원합니다. 모든 복제본은 비동기 커밋 모드에서 실행하거나 최대 3개의 복제본은 동기 커밋 동기 모드에서 실행할 수 있습니다(하나의 주 복제본과 2개의 동기 보조 복제본).  
  
-   **가용성 그룹 및 컴퓨터당 가용성 데이터베이스의 최대 수:** 컴퓨터(가상 컴퓨터 또는 물리적 컴퓨터)에 만들 수 있는 데이터베이스와 가용성 그룹의 실제 수는 하드웨어 및 작업에 따라 다르며 정해진 제한은 없습니다. Microsoft는 물리적 컴퓨터당 10AG 및 100DB로 광범위하게 테스트되었습니다. 오버로드된 시스템 징후에는 작업자 스레드 소진, AlwaysOn 시스템 뷰와 DMV에 대한 느린 응답 시간 및/또는 대기된 디스패처 시스템 덤프 및 기타 징후가 포함될 수 있습니다. 해당 응용 프로그램 SLA 내에서 최대 작업량을 처리할 수 있도록 하기 위해 프로덕션 환경과 유사한 작업으로 환경을 철저히 테스트하십시오. SLA를 고려할 경우 예상 응답 시간뿐 아니라 오류 상태에서의 로드를 검토해야 합니다.  
  
-   **장애 조치(Failover) 클러스터 관리자를 사용하여 가용성 그룹을 조작하지 마세요.**  
  
     예를 들어:  
  
    -   가능한 소유자와 같은 가용성 그룹 속성을 변경하지 마세요.  
  
    -   장애 조치(Failover) 클러스터 관리자를 사용하여 가용성 그룹을 장애 조치하지 마세요. [!INCLUDE[tsql](../../../includes/tsql-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]를 사용해야 합니다.  
  
###  <a name="RequirementsAG"></a> 필수 구성 요소(가용성 그룹)  
 가용성 그룹 구성을 구성하거나 다시 구성할 때 다음 요구 사항을 따라야 합니다.  
  
||사전 요구 사항|Description|  
|-|------------------|-----------------|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI(장애 조치(Failover) 클러스터 인스턴스)를 사용하여 가용성 복제본을 호스팅하려는 경우 FCI 제한 사항을 이해하고 FCI 요구 사항을 충족해야 합니다.|[SQL Server FCI(장애 조치(failover) 클러스터 인스턴스)를 사용하여 가용성 복제본을 호스트하기 위한 필수 구성 요소 및 제한 사항](#FciArLimitations) (이 항목 앞부분)|  
  
###  <a name="SecurityAG"></a> 보안(가용성 그룹)  
  
-   보안은 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터에서 상속됩니다. WSFC는 전체 WSFC 클러스터 API에서 세부적으로 두 가지 수준의 사용자 보안을 제공합니다.  
  
    -   읽기 전용 액세스  
  
    -   모든 권한  
  
         [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 에 모든 권한이 필요하며 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 인스턴스에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 을 사용하도록 설정하면 서비스 SID를 통해 WSFC 클러스터의 모든 권한이 제공됩니다.  
  
         WSFC 장애 조치(Failover) 클러스터 관리자에서 서버 인스턴스에 대한 보안을 직접 추가하거나 제거할 수는 없습니다. WSFC 보안 세션을 관리하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 동등한 WMI 항목을 사용합니다.  
  
-   각 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에는 레지스트리, 클러스터 등에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 가용성 복제본을 호스팅하는 서버 인스턴스 간의 연결에는 암호화를 사용하는 것이 좋습니다.  
  
#### <a name="permissions-availability-groups"></a>사용 권한(가용성 그룹)  
  
|태스크|필요한 권한|  
|----------|--------------------------|  
|가용성 그룹 만들기|CREATE AVAILABILITY GROUP 서버 권한, ALTER ANY AVAILABILITY GROUP 권한, CONTROL SERVER 권한 중 하나와 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.|  
|가용성 그룹 변경|가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다.<br /><br /> 또한 데이터베이스를 가용성 그룹에 조인하려면 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.|  
|가용성 그룹 삭제|가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다. 로컬 복제본 위치에서 호스팅되지 않는 가용성 그룹을 삭제하려면 해당 가용성 그룹에 대한 CONTROL SERVER 권한이나 CONTROL 권한이 필요합니다.|  
  
###  <a name="RelatedTasksAGs"></a> 관련 태스크(가용성 그룹)  
  
|태스크|항목|  
|----------|-----------|  
|가용성 그룹 만들기|[가용성 그룹 사용(새 가용성 그룹 마법사)](use-the-availability-group-wizard-sql-server-management-studio.md)<br /><br /> [가용성 그룹 만들기(Transact-SQL)](create-an-availability-group-transact-sql.md)<br /><br /> [가용성 그룹 만들기(SQL Server PowerShell)](../../../powershell/sql-server-powershell.md)<br /><br /> [가용성 복제본 추가 또는 수정 시 끝점 URL 지정&#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)|  
|가용성 복제본 개수 수정|[가용성 그룹에 보조 복제본 추가&#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> [가용성 그룹에 보조 복제본 조인&#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> [가용성 그룹에서 보조 복제본 제거&#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)|  
|가용성 그룹 수신기 만들기|[가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)|  
|가용성 그룹 삭제|[가용성 그룹 제거&#40;SQL Server&#41;](remove-an-availability-group-sql-server.md)|  
  
##  <a name="PrerequisitesForDbs"></a> 가용성 데이터베이스 필수 구성 요소 및 제한 사항  
 가용성 그룹에 추가하기에 적합한 데이터베이스는 다음 필수 구성 요소 및 제한 사항을 충족해야 합니다.  
  
 
  
###  <a name="RequirementsDb"></a> 검사 목록: 요구 사항(가용성 데이터베이스)  
 가용성 그룹에 추가하기에 적합한 데이터베이스는 다음 조건을 충족해야 합니다.  
  
||요구 사항|링크|  
|-|------------------|----------|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|사용자 데이터베이스여야 합니다. 시스템 데이터베이스는 가용성 그룹에 포함될 수 없습니다.||  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|가용성 그룹을 만들려고 하며 서버 인스턴스에서 액세스할 수 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 있어야 합니다.||  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|읽기/쓰기 데이터베이스여야 합니다. 읽기 전용 데이터베이스는 가용성 그룹에 추가할 수 없습니다.|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**is_read_only** = 0)|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|다중 사용자 데이터베이스여야 합니다.|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**user_access** = 0)|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|AUTO_CLOSE를 사용하면 안 됩니다.|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**is_auto_close_on** = 0)|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|전체 복구 모델(전체 복구 모드라고도 함)을 사용합니다.|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**recovery_model** = 1)|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|전체 데이터베이스 백업을 하나 이상 소유해야 합니다.<br /><br /> 참고: 데이터베이스를 전체 복구 모드로 설정한 후 전체 복구 로그 체인을 시작하려면 전체 백업이 필요합니다.|[전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|기존 가용성 그룹에 속하지 않아야 합니다.|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**group_database_id** = NULL)|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|데이터베이스 미러링용으로 구성되지 않아야 합니다.|[sys.database_mirroring](/sql/relational-databases/system-catalog-views/sys-database-mirroring-transact-sql) (데이터베이스가 미러링에 참가하지 않으면 접두사가 "mirroring_"인 모든 열이 NULL입니다.)|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|FILESTREAM을 사용하는 데이터베이스를 가용성 그룹에 추가하려면 먼저 가용성 그룹의 가용성 복제본을 호스팅하거나 호스팅할 모든 서버 인스턴스에서 FILESTREAM을 사용하도록 설정되어 있는지 확인합니다.|[FILESTREAM 사용 및 구성](../../../relational-databases/blob/enable-and-configure-filestream.md)|  
|![확인란](../../media/checkboxemptycenterxtraspacetopandright.gif "확인란")|포함된 된 데이터베이스를 가용성 그룹에 추가 하기 전에 확인 하는 `contained database authentication` 서버 옵션을 설정 `1` 모든 서버에서 호스팅하는 인스턴스 또는 가용성 그룹에 대 한 가용성 복제본을 호스팅할 합니다.|[contained database authentication 서버 구성 옵션](../../configure-windows/contained-database-authentication-server-configuration-option.md)<br /><br /> [서버 구성 옵션&#40;SQL Server&#41;](../../configure-windows/server-configuration-options-sql-server.md)|  
  
> [!NOTE]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]은 지원되는 모든 데이터베이스 호환성 수준에서 작동합니다.  
  
###  <a name="RestrictionsDb"></a> 제한 사항(가용성 데이터베이스)  
  
-   보조 데이터베이스의 파일 경로(드라이브 문자 포함)와 해당하는 주 데이터베이스의 경로가 다를 경우 다음 제한 사항이 적용됩니다.  
  
    -   **[!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)]/[!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)]:** **초기 데이터 동기화 선택** 페이지에서[전체](select-initial-data-synchronization-page-always-on-availability-group-wizards.md) 옵션이 지원되지 않습니다.  
  
    -   **RESTORE WITH MOVE:**  보조 데이터베이스를 만들려면 보조 복제본을 호스팅하는 각 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에서 데이터베이스 파일에 대해 RESTORED WITH MOVE를 실행해야 합니다.  
  
    -   **파일 추가 작업에 미치는 영향:**  보조 데이터베이스에서 보조 복제본에 대한 이후 파일 추가 작업은 실패할 수 있습니다. 이 오류로 인해 보조 데이터베이스가 일시 중지될 수 있습니다. 이로 인해 보조 복제본이 NOT SYNCHRONIZING 상태가 됩니다.  
  
        > [!NOTE]  
        >  실패한 파일 추가 작업을 해결하는 방법은 [실패한 파일 추가 작업 문제 해결&#40;AlwaysOn 가용성 그룹&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)을 참조하세요.  
  
-   현재 가용성 그룹에 속한 데이터베이스는 삭제할 수 없습니다.  
  
###  <a name="TDEdbs"></a> TDE 데이터베이스 보호를 위한 후속 작업  
 TDE(투명한 데이터 암호화)를 사용하는 경우 다른 키를 만들고 해독하기 위한 인증서 또는 비대칭 키가 가용성 그룹의 가용성 복제본을 호스팅하는 모든 서버 인스턴스에서 동일해야 합니다. 자세한 내용은 [다른 SQL Server로 TDE 보호 데이터베이스 이동](../../../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md)을 참조하세요.  
  
###  <a name="PermissionsDbs"></a> 사용 권한(가용성 데이터베이스)  
 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
###  <a name="RelatedTasksADb"></a> 관련 태스크(가용성 데이터베이스)  
  
|태스크|항목|  
|----------|-----------|  
|보조 데이터베이스 준비(수동)|[가용성 그룹에 대한 보조 데이터베이스 준비&#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)|  
|가용성 그룹에 보조 데이터베이스 조인(수동)|[가용성 그룹에 보조 데이터베이스 조인&#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)|  
|가용성 데이터베이스 개수 수정|[가용성 그룹에 데이터베이스 추가&#40;SQL Server&#41;](availability-group-add-a-database.md)<br /><br /> [가용성 그룹에서 보조 데이터베이스 제거&#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md)<br /><br /> [가용성 그룹에서 주 데이터베이스 제거&#40;SQL Server&#41;](remove-a-primary-database-from-an-availability-group-sql-server.md)|  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   [고가용성 및 재해 복구를 위한 Microsoft SQL Server AlwaysOn 솔루션 가이드](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [SQL Server AlwaysOn 팀 블로그: 공식 SQL Server AlwaysOn 팀 블로그](http://blogs.msdn.com/b/sqlalwayson/)  
  
-   [AlwaysON-HADRON 학습 시리즈: HADRON에 대 한 작업자 풀 사용 사용 데이터베이스](http://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
## <a name="see-also"></a>관련 항목  
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [장애 조치 클러스터링 및 AlwaysOn 가용성 그룹 &#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 클라이언트 연결 (SQL Server)](always-on-client-connectivity-sql-server.md)  
  
  
