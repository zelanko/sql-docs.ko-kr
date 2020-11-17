---
title: '가용성 그룹: 필수 조건, 제한 사항 및 권장 사항'
description: SQL Server에 Always On 가용성 그룹을 배포하기 위한 필수 조건, 제한 사항 및 권장 사항에 대한 설명입니다.
ms.custom: seo-lt-2019
ms.date: 07/22/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
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
author: cawrites
ms.author: chadam
ms.openlocfilehash: 56a36ef2372e1b8171bf957f2d2c2d7dc2eaa356
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584088"
---
# <a name="prerequisites-restrictions-and-recommendations-for-always-on-availability-groups"></a>Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  이 문서에서는 호스트 컴퓨터, WSFC(Windows Server 장애 조치 클러스터), 서버 인스턴스 및 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항을 포함하여 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 배포할 때 고려해야 할 사항에 대해 설명합니다. 이러한 각 구성 요소에 대한 보안 고려 사항과 필요한 권한이 있는 경우 알려줍니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 배포하기 전에 이 항목의 모든 섹션을 읽어 보십시오.  
    
##  <a name="net-hotfixes-that-support-availability-groups"></a><a name="DotNetHotfixes"></a> 가용성 그룹을 지원하는 .NET 핫픽스  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]과 함께 사용할 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 구성 요소 및 기능에 따라 다음 테이블에 표시되어 있는 추가 .NET 핫픽스를 설치해야 할 수 있습니다. 이러한 핫픽스는 순서에 관계없이 설치할 수 있습니다.  
  
|종속 기능|핫픽스|링크|  
|-----------------------|------------|----------|  
|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]|.NET 3.5 SP1 핫픽스는 읽기 전용 및 multisubnetfailover Always On 기능을 위한 지원을 SQL 클라이언트에 추가합니다. 각 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 보고서 서버에 핫픽스를 설치해야 합니다.|KB 2654347: [Always On 기능을 위한 지원을 추가하는 .NET 3.5 SP1 핫픽스](https://go.microsoft.com/fwlink/?LinkId=242896)|  
  

###  <a name="checklist-requirements-windows-system"></a><a name="SystemRequirements"></a> 검사 목록: 요구 사항(Windows 시스템)  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 기능을 지원하려면 하나 이상의 가용성 그룹에 참여할 모든 컴퓨터가 다음 기본 요구 사항을 충족해야 합니다.  
  
|요구 사항|링크|  
|-----------------|----------|  
|시스템이 도메인 컨트롤러가 아닌지 확인하세요.|가용성 그룹은 도메인 컨트롤러에서 지원되지 않습니다.|  
|각 컴퓨터에서 Windows Server 2012 이상 버전이 실행되고 있어야 합니다.|[SQL Server 2016 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)|  
|각 컴퓨터가 WSFC의 노드인지 확인합니다.|[SQL Server의 WSFC&#40;Windows Server 장애 조치(failover) 클러스터링&#41;](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)|  
|WSFC에 가용성 그룹 구성을 지원할 수 있는 노드가 충분한지 확인합니다.|클러스터 노드는 가용성 그룹에 복제본 1개를 호스트할 수 있습니다. 동일한 노드는 동일한 가용성 그룹에서 복제본 2개를 호스트할 수 없습니다. 클러스터 노드는 각 그룹의 복제본 1개를 사용하여 여러 가용성 그룹에 참여할 수 있습니다. <br /><br /> 계획된 가용성 그룹의 가용성 복제본을 지원하는 데 필요한 클러스터 노드 수를 데이터베이스 관리자에게 문의하세요.<br /><br /> [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)을 참조하세요.|  

  
> [!IMPORTANT]  
>  또한 시스템이 가용성 그룹에 연결되도록 올바르게 구성되었는지 확인합니다. 자세한 내용은 [Always On 클라이언트 연결&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)을 참조하세요.  
  
##  <a name="recommendations-for-computers-that-host-availability-replicas-windows-system"></a><a name="ComputerRecommendations"></a> 가용성 복제본을 호스팅하는 컴퓨터에 대한 권장 사항(Windows 시스템)  
  
-   **동등한 시스템:**  지정된 가용성 그룹의 경우 모든 가용성 복제본은 동일한 작업을 처리할 수 있는 동등한 시스템에서 실행해야 합니다.  
  
-   **전용 네트워크 어댑터:**  성능을 최대화하려면 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 전용 네트워크 어댑터(네트워크 인터페이스 카드)를 사용합니다.  
  
-   **충분한 디스크 공간:**  가용성 복제본을 호스팅하는 서버 인스턴스가 있는 모든 컴퓨터에는 가용성 그룹의 모든 데이터베이스를 저장하기에 충분한 디스크 공간이 있어야 합니다. 주 데이터베이스의 크기가 늘어나면 해당하는 보조 데이터베이스도 같은 크기만큼 늘어난다는 것에 유의해야 합니다.  
  
###  <a name="permissions-windows-system"></a><a name="PermissionsWindows"></a> 사용 권한(Windows 시스템)  
 WSFC를 관리하려면 사용자가 모든 클러스터 노드의 시스템 관리자여야 합니다.  
  
 클러스터 관리를 위한 계정에 대한 자세한 내용은 [부록 A: 장애 조치(failover) 클러스터 요구 사항](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd197454(v=ws.10))을 참조하세요.  
  
###  <a name="related-tasks-windows-system"></a><a name="RelatedTasksWindows"></a> 관련 태스크(Windows 시스템)  
  
|Task|링크|  
|----------|----------|  
|HostRecordTTL 값을 설정합니다.|[HostRecordTTL 변경(Windows PowerShell 사용)](#ChangeHostRecordTTLps)|  
  
####  <a name="change-the-hostrecordttl-using-windows-powershell"></a><a name="ChangeHostRecordTTLps"></a> HostRecordTTL 변경(Windows PowerShell 사용)  
  
1.  **관리자 권한으로 실행** 을 통해 PowerShell 창을 엽니다.  
  
2.  FailoverClusters 모듈을 가져옵니다.  
  
3.  **Get-ClusterResource** cmdlet을 사용하여 네트워크 이름 리소스를 찾은 다음에 아래와 같이 **Set-ClusterParameter** cmdlet을 사용하여 **HostRecordTTL** 값을 설정합니다.  
  
     Get-ClusterResource " *\<NetworkResourceName>* " | Set-ClusterParameter HostRecordTTL *\<TimeInSeconds>*  
  
     다음 PowerShell 예제에서는 `SQL Network Name (SQL35)`라는 네트워크 이름 리소스에 대해 HostRecordTTL을 300초로 설정합니다.  
  
    ```powershell
    Import-Module FailoverClusters  
  
    $nameResource = "SQL Network Name (SQL35)"  
    Get-ClusterResource $nameResource | Set-ClusterParameter ClusterParameter HostRecordTTL 300  
    ```  
  
    > [!TIP]  
    >  새 PowerShell 창을 열 때마다 **FailoverClusters** 모듈을 가져와야 합니다.  
  
##### <a name="related-content-powershell"></a>관련 내용(PowerShell)  
  
-   [클러스터링 및 고가용성](https://techcommunity.microsoft.com/t5/failover-clustering/bg-p/FailoverClustering) (장애 조치(failover) 클러스터링 및 네트워크 부하 분산 팀 블로그)  
  
-   [장애 조치(Failover) 클러스터에서 Windows PowerShell 시작](https://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [클러스터 리소스 명령 및 해당 Windows PowerShell Cmdlet](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee619744(v=ws.10)#BKMK_resource)  
  
###  <a name="related-content-windows-system"></a><a name="RelatedContentWS"></a> 관련 콘텐츠(Windows 시스템)  
  
-   [다중 사이트 장애 조치(Failover) 클러스터에서 DNS 설정 구성](https://technet.microsoft.com/library/dd197562\(WS.10\).aspx)  
  
-   [네트워크 이름 리소스에 DNS 등록](https://techcommunity.microsoft.com/t5/failover-clustering/dns-registration-with-the-network-name-resource/ba-p/371482)  
  

##  <a name="sql-server-instance-prerequisites-and-restrictions"></a><a name="ServerInstance"></a> SQL Server 인스턴스 필수 구성 요소 및 제한 사항  
 각 가용성 그룹에는 *인스턴스에서 호스팅되는* 가용성 복제본 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]이라는 일련의 장애 조치(Failover) 파트너가 필요합니다. 특정 서버 인스턴스는 *독립 실행형 인스턴스* 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]*장애 조치(failover) 클러스터 인스턴스* 일 수 있습니다.  
  
 **섹션 내용**  
  
-   [검사 목록: 필수 구성 요소](#PrerequisitesSI)  
  
-   [가용성 그룹의 스레드 사용량](#ThreadUsage)  
  
-   [권한](#PermissionsSI)  
  
-   [관련 작업](#RelatedTasksSI)  
  
-   [관련 내용](#RelatedContentSI)  
  
###  <a name="checklist-prerequisites-server-instance"></a><a name="PrerequisitesSI"></a> 검사 목록: 필수 구성 요소(서버 인스턴스)  
  
|필수 요소|링크|  
|------------------|-----------|  
|호스트 컴퓨터는 WSFC 노드여야 합니다. 지정된 가용성 그룹의 가용성 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스는 클러스터의 개별 노드에 있습니다. 다른 클러스터로 마이그레이션되는 동안 가용성 그룹이 일시적으로 두 클러스터에 걸쳐 있을 수 있습니다. SQL Server 2016에서는 분산된 가용성 그룹을 소개합니다. 분산 가용성 그룹에서는 두 가용성 그룹이 서로 다른 클러스터에 있습니다.|[SQL Server의 WSFC&#40;Windows Server 장애 조치(failover) 클러스터링&#41;](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)<br /><br /> [장애 조치(failover) 클러스터링 및 Always On 가용성 그룹&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)<br/> <br/> [분산된 가용성 그룹(Always On 가용성 그룹)](./distributed-availability-groups.md)|  
|가용성 그룹이 Kerberos로 작동하도록 하려는 경우:<br /><br /> 가용성 그룹에 대한 가용성 복제본을 호스팅하는 모든 서버 인스턴스는 동일한 SQL Server 서비스 계정을 사용해야 합니다.<br /><br /> 도메인 관리자는 가용성 그룹 수신기의 VNN(가상 네트워크 이름)에 대해 SQL Server 서비스 계정에서 Active Directory에 SPN(서비스 사용자 이름)을 수동으로 등록해야 합니다. SQL Server 서비스 계정이 아닌 다른 계정에 SPN이 등록된 경우 인증이 실패합니다.<br /><br /> <br /><br /> <b>\*\* 중요 \*\*</b> SQL Server 서비스 계정을 변경하면 도메인 관리자가 SPN을 수동으로 다시 등록해야 합니다.|[Kerberos 연결의 서비스 사용자 이름 등록](../../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)<br /><br /> **간략한 설명:**<br /><br /> Kerberos 및 SPN은 상호 인증을 강제 적용합니다. SPN은 SQL Server 서비스를 시작하는 Windows 계정에 매핑됩니다. SPN이 올바르게 등록되지 않았거나 실패하면, Windows 보안 계층이 SPN과 연결된 계정을 확인할 수 없으며, Kerberos 인증을 사용할 수 없습니다.<br /><br /> <br /><br /> 참고: NTLM에는 이러한 요구 사항이 없습니다.|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI(장애 조치(Failover) 클러스터 인스턴스)를 사용하여 가용성 복제본을 호스팅하려는 경우 FCI 제한 사항을 이해하고 FCI 요구 사항을 충족해야 합니다.|[SQL Server FCI(장애 조치(failover) 클러스터 인스턴스)를 사용하여 가용성 복제본을 호스트하기 위한 필수 구성 요소 및 요구 사항](#FciArLimitations)(이 문서 뒷부분)|  
|각 서버 인스턴스는 Always On 가용성 그룹에 참여하기 위해 동일한 버전의 SQL Server를 실행해야 합니다.|[SQL 2014](/previous-versions/sql/2014/getting-started/features-supported-by-the-editions-of-sql-server-2014?view=sql-server-2014&preserve-view=true), [SQL 2016](../../../sql-server/editions-and-components-of-sql-server-2016.md?view=sql-server-2016&preserve-view=true), [SQL 2017](../../../sql-server/editions-and-components-of-sql-server-2017.md?view=sql-server-2017&preserve-view=true)의 버전 및 지원되는 기능|  
|가용성 그룹의 가용성 복제본을 호스팅하는 모든 서버 인스턴스는 동일한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 정렬을 사용해야 합니다.|[서버 데이터 정렬 설정 또는 변경](../../../relational-databases/collations/set-or-change-the-server-collation.md)|  
|가용성 그룹의 가용성 복제본을 호스팅할 각 서버 인스턴스에서 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 기능을 사용하도록 설정합니다. 특정 컴퓨터에서 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 설치에서 지원하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서버 인스턴스를 개수에 관계없이 사용하도록 설정할 수 있습니다.|[Always On 가용성 그룹 활성화 및 비활성화&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)<br /><br /> <br /><br /> <b>\*\* 중요 \*\*</b> WSFC를 삭제하고 다시 만드는 경우 원본 클러스터에서 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에 대해 사용하도록 설정한 각 서버 인스턴스에서 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 기능을 해제한 다음 다시 사용하도록 설정해야 합니다.|  
|각 서버 인스턴스에는 데이터베이스 미러링 엔드포인트가 있어야 합니다. 이 엔드포인트는 서버 인스턴스의 미러링 모니터 서버 및 데이터베이스 미러링 파트너와 모든 가용성 복제본에서 공유합니다.<br /><br /> 가용성 복제본을 호스팅하도록 선택한 서버 인스턴스가 도메인 사용자 계정으로 실행되고 있고 아직 데이터베이스 미러링 엔드포인트를 가지고 있지 않는 경우, [새 가용성 그룹 마법사](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md) (또는 [가용성 그룹에 복제본 추가 마법사](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)) 가 엔드포인트를 만들고 서버 인스턴스 서비스 계정에 CONNECT 권한을 부여할 수 있습니다. 그러나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스가 로컬 시스템, 로컬 서비스 또는 네트워크 서비스와 같은 기본 제공 계정이나 비도메인 계정으로 실행 중인 경우에는 사용자가 엔드포인트 인증을 위한 인증서를 사용해야 하며 마법사를 통해 서버 인스턴스에 대한 데이터베이스 미러링 엔드포인트를 만들 수는 없습니다. 이 경우 마법사를 시작하기 전에 데이터 미러링 엔드포인트를 수동으로 만드는 것이 좋습니다.<br /><br /> <br /><br /> <b>\*\* 보안 정보 \*\*</b>[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 에 대한 전송 보안은 데이터베이스 미러링의 경우와 동일합니다.|[데이터베이스 미러링 엔드포인트&#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)<br /><br /> [데이터베이스 미러링 및 Always On 가용성 그룹에 대한 전송 보안&#40;SQL Server&#41;](../../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)|  
|FILESTREAM을 사용하는 데이터베이스를 가용성 그룹에 추가하려는 경우 가용성 그룹의 가용성 복제본을 호스팅할 모든 서버 인스턴스에 FILESTREAM이 설정되었는지 확인합니다.|[Enable and Configure FILESTREAM](../../../relational-databases/blob/enable-and-configure-filestream.md)|  
|포함된 데이터베이스를 가용성 그룹에 추가하려는 경우 가용성 그룹의 가용성 복제본을 호스팅할 모든 서버 인스턴스에서 **contained database authentication** 서버 옵션이 **1** 로 설정되어 있는지 확인합니다.|[contained database authentication 서버 구성 옵션](../../../database-engine/configure-windows/contained-database-authentication-server-configuration-option.md)<br /><br /> [서버 구성 옵션&#40;SQL Server&#41;](../../../database-engine/configure-windows/server-configuration-options-sql-server.md)|  
  
###  <a name="thread-usage-by-availability-groups"></a><a name="ThreadUsage"></a> 가용성 그룹의 스레드 사용량  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 은 작업자 스레드에 대해 다음 요구 사항을 충족해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 유휴 인스턴스에서 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 은 0개의 스레드를 사용합니다.  
  
-   가용성 그룹에서 사용되는 최대 스레드 수는 최대 서버 스레드 수('**max worker threads**')에서 40을 빼고 구성된 설정입니다.  
  
-   지정된 서버 인스턴스에서 호스팅되는 가용성 복제본은 단일 스레드 풀을 공유합니다.  
  
     스레드는 다음과 같이 요청 시 공유됩니다.  
  
    -   일반적으로 3-10개의 공유 스레드가 있지만 이 수는 주 복제본 워크로드에 따라 증가할 수 있습니다.  
  
    -   지정된 스레드가 얼마 동안 유휴 상태인 경우 일반 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 스레드 풀로 반환됩니다. 일반적으로 비활성 스레드는 아무 작업이 없는 상태가 지속된 지 15초 이내에 해제됩니다. 그러나 마지막 활동에 따라 유휴 스레드가 더 길게 유지될 수 있습니다.  

    -   SQL Server 인스턴스에서는 보조 복제본에 대한 병렬 다시 실행을 위해 최대 100개의 스레드를 사용합니다. 각 데이터베이스는 최대 총 CPU 코어 수의 절반을 사용하지만 데이터베이스당 스레드는 16개까지 사용됩니다. 단일 인스턴스에 필요한 총 스레드 수가 100개를 넘으면 SQL Server에서는 나머지 모든 데이터베이스에 대해 단일 다시 실행 스레드를 사용합니다. 직렬 다시 실행 스레드는 아무 작업이 없는 상태가 지속된 지 15초 이내에 해제됩니다. 
     
-   또한 가용성 그룹은 다음과 같이 비공유 스레드를 사용합니다.  
  
    -   각각의 주 복제본은 각 주 데이터베이스에 대해 1개의 로그 캡처 스레드를 사용합니다. 또한 각 보조 데이터베이스에 대해 1개의 로그 전송 스레드를 사용합니다. 로그 전송 스레드는 아무 작업이 없는 상태가 지속된 지 15초 이내에 해제됩니다.    
  
    -   보조 복제본의 백업은 백업 작업 시간 동안 주 스레드를 복제본에 보관합니다. 

-  SQL Server 2019에서는 메모리 최적화 가용성 그룹 데이터베이스를 위한 병렬 다시 실행이 도입되었습니다. SQL Server 2016 및 2017에서는 가용성 그룹의 데이터베이스가 메모리 최적화된 경우에도 디스크 기반 테이블에서 병렬 다시 실행을 사용하지 않습니다. 
  
 자세한 내용은 [Always On - HADRON 학습 시리즈: HADRON 사용 데이터베이스의 작업자 풀 사용](/archive/blogs/psssql/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases)(CSS [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 엔지니어 블로그)을 참조하세요.  
  
###  <a name="permissions-server-instance"></a><a name="PermissionsSI"></a> 사용 권한(서버 인스턴스)  
  
|Task|필요한 권한|  
|----------|--------------------------|  
|데이터베이스 미러링 엔드포인트 만들기|CREATE ENDPOINT 권한 또는 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  CONTROL ON ENDPOINT 권한도 필요합니다. 자세한 내용은 [GRANT 엔드포인트 사용 권한&#40;Transact-SQL&#41;](../../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)을 참조하세요.|  
|다음 사용 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]|로컬 컴퓨터의 **관리자** 그룹 멤버 자격과 WSFC에 대한 모든 권한이 필요합니다.|  
  
###  <a name="related-tasks-server-instance"></a><a name="RelatedTasksSI"></a> 관련 태스크(서버 인스턴스)  
  
|Task|아티클|  
|----------|-----------|  
|데이터베이스 미러링 엔드포인트가 있는지 여부 확인|[sys.database_mirroring_endpoints&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)|  
|데이터베이스 미러링 엔드포인트 만들기(없는 경우)|[Windows 인증에 대한 데이터베이스 미러링 엔드포인트 만들기&#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)<br /><br /> [데이터베이스 미러링 엔드포인트에 대한 인증서 사용&#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)<br /><br /> [Always On 가용성 그룹에 대한 데이터베이스 미러링 엔드포인트 만들기&#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md)|  
|가용성 그룹 활성화|[Always On 가용성 그룹 활성화 및 비활성화&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)|  
  
###  <a name="related-content-server-instance"></a><a name="RelatedContentSI"></a> 관련 내용(서버 인스턴스)  
  
-   [Always On - HADRON 학습 시리즈: HADRON 사용 데이터베이스의 작업자 풀 사용](/archive/blogs/psssql/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases)  
  
##  <a name="network-connectivity-recommendations"></a><a name="NetworkConnect"></a> 네트워크 연결 권장 사항  
 WSFC 노드 간의 통신 및 가용성 복제본 간의 통신에는 동일한 네트워크 링크를 사용하는 것이 좋습니다.  개별 네트워크 링크를 사용하면 가끔씩이라도 일부 링크에 문제가 발생할 경우 예기치 않은 동작이 발생할 수 있습니다.  
  
 예를 들어, 가용성 그룹으로 자동 장애 조치(Failover)를 지원하기 위해서는 자동 장애 조치(Failover) 파트너인 두 번째 복제본이 SYNCHRONIZED 상태여야 합니다. 이 보조 복제본에 대한 네트워크 링크가 가끔씩이라도 실패할 경우 복제본이 UNSYNCHRONIZED 상태가 되고 링크가 복원될 때까지 다시 동기화를 시작할 수 없습니다. 보조 복제본이 동기화되지 않은 상태에서 WSFC가 자동 장애 조치를 요청하는 경우 자동 장애 조치가 수행되지 않습니다.  
  
##  <a name="client-connectivity-support"></a><a name="ClientConnSupport"></a> 클라이언트 연결 지원  
 클라이언트 연결의 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 지원에 대한 자세한 내용은 [Always On 클라이언트 연결&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)을 참조하세요.  
  
##  <a name="prerequisites-and-restrictions-for-using-a-sql-server-failover-cluster-instance-fci-to-host-an-availability-replica"></a><a name="FciArLimitations"></a> SQL Server FCI(장애 조치(Failover) 클러스터 인스턴스)를 사용하여 가용성 복제본을 호스팅하기 위한 필수 구성 요소 및 제한 사항  
 **섹션 내용**  
  
-   [제한 사항](#RestrictionsFCI)  
  
-   [검사 목록: 필수 구성 요소](#PrerequisitesFCI)  
  
-   [관련 작업](#RelatedTasksFCIs)  
  
-   [관련 내용](#RelatedContentFCIs)  
  
###  <a name="restrictions-fcis"></a><a name="RestrictionsFCI"></a> 제한 사항(FCI)  
  
> [!NOTE]  
> 장애 조치(failover) 클러스터 인스턴스는 CSV(클러스터 공유 볼륨)를 지원합니다. CSV에 대한 자세한 내용은 [장애 조치(Failover) 클러스터에서 클러스터 공유 볼륨 이해](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd759255(v=ws.11))를 참조하세요.  
  
-   **FCI의 클러스터 노드는 특정 가용성 그룹에 대한 하나의 복제본만 호스팅할 수 있습니다.**  FCI에 가용성 복제본을 추가하는 경우 잠재적인 FCI 소유자인 WSFC 노드는 동일한 가용성 그룹에 대해 다른 복제본을 호스팅할 수 없습니다.  가능한 충돌을 방지하려면 장애 조치(Failover) 클러스터 인스턴스의 가능한 소유자를 구성하는 것이 좋습니다. 그러면 단일 WSFC에서 동일한 가용성 그룹의 두 가용성 복제본을 호스트하려고 시도하지 않게 됩니다.
  
     또한 다른 모든 복제본은 동일한 Windows Server 장애 조치(Failover) 클러스터의 다른 클러스터 노드에 있는 SQL Server 2016 인스턴스에서 호스트해야 합니다. 유일한 예외는 다른 클러스터로 마이그레이션되는 동안 가용성 그룹이 일시적으로 두 클러스터에 걸쳐 있을 수 있는 경우입니다. 

  >[!WARNING]
  > 장애 조치(Failover) 클러스터 관리자를 사용하여 가용성 그룹을 호스트하는 *장애 조치(Failover) 클러스터 인스턴스* 를 동일한 가용성 그룹의 복제본을 *이미* 호스트하는 노드로 이동하면 가용성 그룹의 복제본이 손실되어 대상 노드에서 온라인 상태가 될 수 없습니다. 장애 조치(Failover) 클러스터의 단일 노드는 동일한 가용성 그룹의 복제본 2개 이상을 호스트할 수 없습니다. 이러한 결과가 나타나는 방식 및 복구 방법에 대한 자세한 내용은 블로그 [Replica unexpectedly dropped in availability group](/archive/blogs/alwaysonpro/issue-replica-unexpectedly-dropped-in-availability-group)(복제본이 가용성 그룹에서 예기치 않게 손실되는 경우)를 참조하세요. 

  
-   **FCI는 가용성 그룹별 자동 장애 조치(failover)를 지원하지 않습니다.**  FCI는 가용성 그룹에 의한 자동 장애 조치(failover)를 지원하지 않으므로 FCI에서 호스트하는 모든 가용성 복제본은 수동 장애 조치(failover)에 대해서만 구성될 수 있습니다.  
  
-   **FCI 네트워크 이름 변경:**  가용성 복제본을 호스트하는 FCI의 네트워크 이름을 변경해야 하는 경우 복제본을 해당 가용성 그룹에서 제거한 다음, 다시 가용성 그룹에 추가해야 합니다. 주 복제본은 제거할 수 없으므로 주 복제본을 호스팅하는 FCI의 이름을 바꾸려는 경우 보조 복제본으로 장애 조치한 다음 이전 주 복제본을 제거하고 다시 추가해야 합니다. FCI 이름을 바꾸면 해당 데이터베이스 미러링 엔드포인트의 URL이 변경될 수 있습니다. 복제본을 추가할 때 현재 엔드포인트 URL을 지정해야 합니다.  
  
###  <a name="checklist-prerequisites-fcis"></a><a name="PrerequisitesFCI"></a> 검사 목록: 필수 구성 요소(FCI)  
  
|필수 요소|링크|  
|------------------|----------|  
|각 SQL Server FCI(장애 조치(Failover) 클러스터 인스턴스)에 SQL Server FCI(장애 조치(Failover) 클러스터 인스턴스 설치별로 필요한 공유 스토리지가 있는지 확인합니다.||  
  
###  <a name="related-tasks-fcis"></a><a name="RelatedTasksFCIs"></a> 관련 태스크(FCI)  
  
|Task|아티클|  
|----------|-----------|  
|SQL Server 장애 조치(Failover) 클러스터 설치|[새 SQL Server 장애 조치(failover) 클러스터 만들기&#40;설치 프로그램&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)|  
|SQL Server 장애 조치(Failover) 클러스터의 전체 업그레이드|[SQL Server 장애 조치(failover) 클러스터 인스턴스 업그레이드&#40;설치 프로그램&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)|  
|기존 SQL Server 장애 조치(Failover) 클러스터 유지 관리|[SQL Server 장애 조치(Failover) 클러스터에서 노드 추가 또는 제거&#40;설치&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)|  
  
###  <a name="related-content-fcis"></a><a name="RelatedContentFCIs"></a> 관련 내용(FCI)  
  
-   [장애 조치(failover) 클러스터링 및 가용성 그룹&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)  
  
-   [Always On 아키텍처 가이드: 장애 조치(failover) 클러스터 인스턴스 및 가용성 그룹을 사용하여 고가용성 및 재해 복구 솔루션 빌드](/previous-versions/sql/sql-server-2012/jj215886(v=msdn.10))  
  
##  <a name="availability-group-prerequisites-and-restrictions"></a><a name="PrerequisitesForAGs"></a> 가용성 그룹 필수 구성 요소 및 제한 사항  
 **섹션 내용**  
  
-   [제한 사항](#RestrictionsAG)  
  
-   [요구 사항](#RequirementsAG)  
  
-   [보안](#SecurityAG)  
  
-   [관련 작업](#RelatedTasksAGs)  
  
###  <a name="restrictions-availability-groups"></a><a name="RestrictionsAG"></a> 제한 사항(가용성 그룹)  
  
-   **가용성 복제본은 하나의 WSFC의 다른 노드에서 호스팅해야 합니다.**  지정된 가용성 그룹의 경우 가용성 복제본은 동일한 WSFC의 다른 노드에서 실행되는 서버 인스턴스에서 호스팅해야 합니다. 유일한 예외는 다른 클러스터로 마이그레이션되는 동안 가용성 그룹이 일시적으로 두 클러스터에 걸쳐 있을 수 있는 경우입니다.  
  
    > [!NOTE]  
    >  동일한 실제 컴퓨터에 가상 머신이 있는 경우에는 각 가상 머신이 개별 컴퓨터 역할을 하므로 가상 머신별로 동일한 가용성 그룹의 가용성 복제본을 하나씩 호스팅할 수 있습니다.  
  
-   **고유한 가용성 그룹 이름:**  각 가용성 그룹 이름은 WSFC에서 고유해야 합니다. 가용성 그룹 이름의 최대 길이는 128자입니다.  
  
-   **가용성 복제본:**  각 가용성 그룹은 하나의 주 복제본과 최대 8개의 보조 복제본을 지원합니다. 모든 복제본은 비동기 커밋 모드에서 실행하거나 최대 3개의 복제본은 동기 커밋 동기 모드에서 실행할 수 있습니다(하나의 주 복제본과 2개의 동기 보조 복제본).  
  
-   **가용성 그룹 및 컴퓨터당 가용성 데이터베이스의 최대 수:** 컴퓨터(가상 머신 또는 물리적 컴퓨터)에 만들 수 있는 데이터베이스와 가용성 그룹의 실제 수는 하드웨어 및 작업에 따라 다르며 정해진 제한은 없습니다. Microsoft는 물리적 컴퓨터당 최대 10개의 AG와 100개의 DB를 테스트했으며, 하지만 이것이 바인딩 제한은 아닙니다. 서버의 하드웨어 사양 및 워크로드에 따라 더 많은 수의 데이터베이스와 가용성 그룹을 SQL Server 인스턴스에 배치할 수 있습니다. 오버로드된 시스템 징후에는 작업자 스레드 소진, 가용성 그룹 시스템 뷰와 DMV에 대한 느린 응답 시간 및/또는 대기된 디스패처 시스템 덤프 및 기타 징후가 포함될 수 있습니다. 해당 애플리케이션 SLA 내에서 최대 작업량을 처리할 수 있도록 하기 위해 프로덕션 환경과 유사한 작업으로 환경을 철저히 테스트하세요. SLA를 고려할 경우 예상 응답 시간뿐 아니라 오류 상태에서의 로드를 검토해야 합니다.  
  
-   **장애 조치(Failover) 클러스터 관리자를 사용하여 가용성 그룹을 조작하지 마세요**. SQL Server 장애 조치(Failover) 클러스터 인스턴스(FCI)의 상태는 SQL Server와 WSFC(Windows 장애 조치(failover) 클러스터) 간에 공유되며, SQL Server 클러스터에 관해 클러스터에 보다 더 자세한 상태 정보를 유지합니다. 관리 모델은 SQL Server가 트랜잭션을 구동해야 하며, 상태에 대한 클러스터의 보기를 SQL Server의 상태 뷰와 동기화 상태로 유지할 책임을 집니다. 클러스터의 상태가 SQL Server 외부에서 변경되는 경우 WSFC와 SQL Server 간에 상태가 동기화되지 않을 수 있으며 이로 인해 예기치 않은 동작이 발생할 수 있습니다.
  
     예를 들면 다음과 같습니다.  
  
    -   가능한 소유자와 같은 가용성 그룹 속성을 변경하지 마세요.  
  
    -   장애 조치(Failover) 클러스터 관리자를 사용하여 가용성 그룹을 장애 조치하지 마세요. [!INCLUDE[tsql](../../../includes/tsql-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]를 사용해야 합니다.  
  
###  <a name="prerequisites-availability-groups"></a><a name="RequirementsAG"></a> 필수 구성 요소(가용성 그룹)  
 가용성 그룹 구성을 구성하거나 다시 구성할 때 다음 요구 사항을 따라야 합니다.  
  
|필수 요소|Description|  
|------------------|-----------------|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI(장애 조치(Failover) 클러스터 인스턴스)를 사용하여 가용성 복제본을 호스팅하려는 경우 FCI 제한 사항을 이해하고 FCI 요구 사항을 충족해야 합니다.|[SQL Server FCI(장애 조치(Failover) 클러스터 인스턴스)를 사용하여 가용성 복제본을 호스트하기 위한 필수 구성 요소 및 제한 사항](#FciArLimitations)(이 문서 앞부분)|  
  
###  <a name="security-availability-groups"></a><a name="SecurityAG"></a> 보안(가용성 그룹)  
  
-   보안은 WSFC에서 상속됩니다. Windows Server 장애 조치 클러스터링은 전체 클러스터의 세분성에서 두 가지 수준의 사용자 보안을 제공합니다.  
  
    -   읽기 전용 액세스  
  
    -   모든 권한  
  
         [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에는 모든 권한이 필요하며, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에서 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 사용하도록 설정하면 서비스 SID를 통해 클러스터에 대한 모든 권한이 제공됩니다.  
  
         클러스터 관리자에서 서버 인스턴스에 대한 보안을 직접 추가하거나 제거할 수 없습니다. 클러스터 보안 세션을 관리하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자 또는 이와 동등한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 WMI를 사용합니다.  
  
-   각 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에는 레지스트리, 클러스터 등에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 가용성 복제본을 호스팅하는 서버 인스턴스 간의 연결에는 암호화를 사용하는 것이 좋습니다.  
  
#### <a name="permissions-availability-groups"></a>사용 권한(가용성 그룹)  
  
|Task|필요한 권한|  
|----------|--------------------------|  
|가용성 그룹 만들기|CREATE AVAILABILITY GROUP 서버 권한, ALTER ANY AVAILABILITY GROUP 권한, CONTROL SERVER 권한 중 하나와 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.|  
|가용성 그룹 변경|가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다.<br /><br /> 또한 데이터베이스를 가용성 그룹에 조인하려면 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.|  
|가용성 그룹 삭제|가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다. 로컬 복제본 위치에서 호스팅되지 않는 가용성 그룹을 삭제하려면 해당 가용성 그룹에 대한 CONTROL SERVER 권한이나 CONTROL 권한이 필요합니다.|  
  
###  <a name="related-tasks-availability-groups"></a><a name="RelatedTasksAGs"></a> 관련 태스크(가용성 그룹)  
  
|Task|아티클|  
|----------|-----------|  
|가용성 그룹 만들기|[가용성 그룹 사용(새 가용성 그룹 마법사)](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)<br /><br /> [가용성 그룹 만들기(Transact-SQL)](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)<br /><br /> [가용성 그룹 만들기(SQL Server PowerShell)](../../../database-engine/availability-groups/windows/create-an-availability-group-sql-server-powershell.md)<br /><br /> [가용성 복제본 추가 또는 수정 시 엔드포인트 URL 지정&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)|  
|가용성 복제본 개수 수정|[가용성 그룹에 보조 복제본 추가&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> [가용성 그룹에 보조 복제본 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> [가용성 그룹에서 보조 복제본 제거&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server.md)|  
|가용성 그룹 수신기 만들기|[가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)|  
|가용성 그룹 삭제|[가용성 그룹 제거&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)|  
  
##  <a name="availability-database-prerequisites-and-restrictions"></a><a name="PrerequisitesForDbs"></a> 가용성 데이터베이스 필수 구성 요소 및 제한 사항  
 가용성 그룹에 추가하기에 적합한 데이터베이스는 다음 필수 구성 요소 및 제한 사항을 충족해야 합니다.  
  
 **섹션 내용**  
  
-   [요구 사항](#RequirementsDb)  
  
-   [제한 사항](#RestrictionsDb)  
  
-   [가용성 복제본을 호스팅하는 컴퓨터에 대한 권장 사항(Windows 시스템)](#TDEdbs)  
  
-   [권한](#PermissionsDbs)  
  
-   [관련 작업](#RelatedTasksADb)  
  
###  <a name="checklist-requirements-availability-databases"></a><a name="RequirementsDb"></a> 검사 목록: 요구 사항(가용성 데이터베이스)  
 가용성 그룹에 추가하기에 적합한 데이터베이스는 다음 조건을 충족해야 합니다.  
  
|요구 사항|링크|  
|------------------|----------|  
|사용자 데이터베이스여야 합니다. 시스템 데이터베이스는 가용성 그룹에 포함될 수 없습니다.||  
|가용성 그룹을 만들려고 하며 서버 인스턴스에서 액세스할 수 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 있어야 합니다.||  
|읽기/쓰기 데이터베이스여야 합니다. 읽기 전용 데이터베이스는 가용성 그룹에 추가할 수 없습니다.|[sys.databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) (**is_read_only** = 0)|  
|다중 사용자 데이터베이스여야 합니다.|[sys.databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) (**user_access** = 0)|  
|AUTO_CLOSE를 사용하면 안 됩니다.|[sys.databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) (**is_auto_close_on** = 0)|  
|전체 복구 모델(전체 복구 모드라고도 함)을 사용합니다.|[sys.databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) (**recovery_model** = 1)|  
|전체 데이터베이스 백업을 하나 이상 소유해야 합니다.<br /><br /> 참고: 데이터베이스를 전체 복구 모드로 설정한 후 전체 복구 로그 체인을 시작하려면 전체 백업이 필요합니다.|[전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)|  
|기존 가용성 그룹에 속하지 않아야 합니다.|[sys.databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) (**group_database_id** = NULL)|  
|데이터베이스 미러링용으로 구성되지 않아야 합니다.|[sys.database_mirroring](../../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md) (데이터베이스가 미러링에 참가하지 않으면 접두사가 "mirroring_"인 모든 열이 NULL입니다.)|  
|FILESTREAM을 사용하는 데이터베이스를 가용성 그룹에 추가하려면 먼저 가용성 그룹의 가용성 복제본을 호스팅하거나 호스팅할 모든 서버 인스턴스에서 FILESTREAM을 사용하도록 설정되어 있는지 확인합니다.|[Enable and Configure FILESTREAM](../../../relational-databases/blob/enable-and-configure-filestream.md)|  
|포함된 데이터베이스를 가용성 그룹에 추가하기 전에 가용성 그룹의 가용성 복제본을 호스팅하거나 호스팅할 모든 서버 인스턴스에서 **contained database authentication** 서버 옵션이 **1** 로 설정되어 있는지 확인합니다.|[contained database authentication 서버 구성 옵션](../../../database-engine/configure-windows/contained-database-authentication-server-configuration-option.md)<br /><br /> [서버 구성 옵션&#40;SQL Server&#41;](../../../database-engine/configure-windows/server-configuration-options-sql-server.md)|  
  
> [!NOTE]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]은 지원되는 모든 데이터베이스 호환성 수준에서 작동합니다.  
  
###  <a name="restrictions-availability-databases"></a><a name="RestrictionsDb"></a> 제한 사항(가용성 데이터베이스)  
  
-   보조 데이터베이스의 파일 경로(드라이브 문자 포함)와 해당하는 주 데이터베이스의 경로가 다를 경우 다음 제한 사항이 적용됩니다.  
  
    -   **[!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)]/[!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)]:**  [초기 데이터 동기화 선택](../../../database-engine/availability-groups/windows/select-initial-data-synchronization-page-always-on-availability-group-wizards.md) 페이지에서 **전체** 옵션이 지원되지 않습니다.  
  
    -   **RESTORE WITH MOVE:**  보조 데이터베이스를 만들려면 보조 복제본을 호스팅하는 각 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에서 데이터베이스 파일에 대해 RESTORED WITH MOVE를 실행해야 합니다.  
  
    -   **파일 추가 작업에 미치는 영향:**  보조 데이터베이스에서 보조 복제본에 대한 이후 파일 추가 작업은 실패할 수 있습니다. 이 오류로 인해 보조 데이터베이스가 일시 중지될 수 있습니다. 이로 인해 보조 복제본이 NOT SYNCHRONIZING 상태가 됩니다.  
  
        > [!NOTE]  
        >  실패한 파일 추가 작업을 해결하는 방법은 [실패한 파일 추가 작업 문제 해결&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)을 참조하세요.  
  
-   현재 가용성 그룹에 속한 데이터베이스는 삭제할 수 없습니다.  
  
###  <a name="follow-up-for-tde-protected-databases"></a><a name="TDEdbs"></a> TDE 데이터베이스 보호를 위한 후속 작업  
 TDE(투명한 데이터 암호화)를 사용하는 경우 다른 키를 만들고 해독하기 위한 인증서 또는 비대칭 키가 가용성 그룹의 가용성 복제본을 호스팅하는 모든 서버 인스턴스에서 동일해야 합니다. 자세한 내용은 [다른 SQL Server로 TDE 보호 데이터베이스 이동](../../../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md)을 참조하세요.  
  
###  <a name="permissions-availability-databases"></a><a name="PermissionsDbs"></a> 사용 권한(가용성 데이터베이스)  
 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
###  <a name="related-tasks-availability-databases"></a><a name="RelatedTasksADb"></a> 관련 태스크(가용성 데이터베이스)  
  
|Task|아티클|  
|----------|-----------|  
|보조 데이터베이스 준비(수동)|[가용성 그룹에 대한 보조 데이터베이스 준비&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)|  
|가용성 그룹에 보조 데이터베이스 조인(수동)|[가용성 그룹에 보조 데이터베이스 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)|  
|가용성 데이터베이스 개수 수정|[가용성 그룹에 데이터베이스 추가&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/availability-group-add-a-database.md)<br /><br /> [가용성 그룹에서 보조 데이터베이스 제거&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md)<br /><br /> [가용성 그룹에서 주 데이터베이스 제거&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md)|  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> 관련 내용  
  
-   [고가용성 및 재해 복구를 위한 Microsoft SQL Server Always On 솔루션 가이드](/previous-versions/sql/sql-server-2012/hh781257(v=msdn.10))  
  
-   [SQL Server Always On 팀 블로그: 공식 SQL Server Always On 팀 블로그](/archive/blogs/sqlalwayson/)  
  
-   [Always On - HADRON 학습 시리즈: HADRON 사용 데이터베이스의 작업자 풀 사용](/archive/blogs/psssql/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [장애 조치(failover) 클러스터링 및 Always On 가용성 그룹&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Always On 클라이언트 연결&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)  
  
    
  
--------------------------------------------------