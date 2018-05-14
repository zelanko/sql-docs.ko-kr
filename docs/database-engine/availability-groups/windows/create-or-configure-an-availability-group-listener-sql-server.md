---
title: 가용성 그룹 수신기 만들기 또는 구성(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroup.newaglistener.general.f1
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- Availability Groups [SQL Server], client connectivity
ms.assetid: 2bc294f6-2312-4b6b-9478-2fb8a656e645
caps.latest.revision: 52
author: MikeRayMSFT
ms.author: mikeray
manager: erikre
ms.openlocfilehash: 1b1106913af5e7b6c2e9cd4a2e8b329efa0d596a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="create-or-configure-an-availability-group-listener-sql-server"></a>가용성 그룹 수신기 만들기 또는 구성(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 *,* 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]의 PowerShell을 사용하여 Always On 가용성 그룹에 대한 단일 [!INCLUDE[tsql](../../../includes/tsql-md.md)]가용성 그룹 수신기 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]를 만들거나 구성하는 방법에 대해 설명합니다.  
  
> [!IMPORTANT]  
>  가용성 그룹에 대한 첫 번째 가용성 그룹 수신기를 만들려면 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell을 사용하는 것이 좋습니다. 추가 수신기를 만들려는 경우처럼 필요한 경우를 제외하고 WSFC 클러스터에서 수신기를 직접 만들지 마세요.  
  
-   **시작하기 전 주의 사항:**  
  
     [이 가용성 그룹에 대한 수신기가 이미 존재합니까?](#DoesListenerExist)  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
     [필수 구성 요소](#Prerequisites)  
  
     [가용성 그룹 수신기의 DNS 이름에 대한 요구 사항](#DNSnameReqs)  
  
     [Windows 사용 권한](#WinPermissions)  
  
     [SQL Server 사용 권한](#SqlPermissions)  
  
-   **가용성 그룹을 만들거나 구성하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **문제 해결**  
  
     [Active Directory 할당량으로 인한 가용성 그룹 수신기 만들기의 오류](#ADQuotas)  
  
-   **후속 작업: 가용성 그룹 수신기를 만든 후**  
  
     [MultiSubnetFailover 키워드 및 관련 기능](#MultiSubnetFailover)  
  
     [RegisterAllProvidersIP 설정](#RegisterAllProvidersIP)  
  
     [HostRecordTTL 설정](#HostRecordTTL)  
  
     [RegisterAllProvidersIP를 비활성화하고 TTL을 줄이는 샘플 PowerShell 스크립트](#SampleScript)  
  
     [후속 권장 사항](#FollowUpRecommendations)  
  
     [가용성 그룹의 추가 수신기 만들기(선택 사항)](#CreateAdditionalListener)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="DoesListenerExist"></a> 이 가용성 그룹에 대한 수신기가 이미 존재합니까?  
 **가용성 그룹에 대한 수신기가 이미 존재하는지 확인하려면**  
  
-   [가용성 그룹 수신기 속성 보기&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)  
  
> [!NOTE]  
>  수신기가 이미 있는 상태에서 추가 수신기를 만들려면 이 항목의 뒷부분에 나오는 [가용성 그룹에 대한 추가 수신기를 만들려면(선택 사항)](#CreateAdditionalListener)을 참조하세요.  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 통해 가용성 그룹당 수신기를 하나만 만들 수 있습니다. 일반적으로 각 가용성 그룹에는 수신기가 하나만 필요합니다. 그러나 고객 시나리오에 따라 하나의 가용성 그룹에 여러 개의 수신기가 필요한 경우도 있습니다.   SQL Server를 통해 수신기를 만든 후 장애 조치(failover) 클러스터용 Windows PowerShell 또는 WSFC 장애 조치 클러스터 관리자를 사용하여 추가 수신기를 만들 수 있습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [가용성 그룹의 추가 수신기를 만들려면(선택 사항)](#CreateAdditionalListener)을 참조하세요.  
  
###  <a name="Recommendations"></a> 권장 사항  
 필수는 아니지만 여러 서브넷 구성에 대해 고정 IP 주소를 사용하는 것이 좋습니다.  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
  
-   주 복제본을 호스팅하는 서버 인스턴스에 연결되어 있어야 합니다.  
  
-   여러 서브넷에 대해 하나의 가용성 그룹 수신기를 설정하고 고정 IP 주소를 사용하려는 경우 수신기를 만들려는 가용성 그룹에 대해 가용성 복제본을 호스팅하는 모든 서브넷의 고정 IP 주소를 얻어야 합니다. 일반적으로 네트워크 관리자에게 고정 IP 주소를 문의해야 합니다.  
  
> [!IMPORTANT]  
>  첫 번째 수신기를 만들기 전에 [Always On 클라이언트 연결&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)을 읽어 보세요.  
  
###  <a name="DNSnameReqs"></a> 가용성 그룹 수신기의 DNS 이름에 대한 요구 사항  
 각 가용성 그룹 수신기에는 도메인과 NetBIOS에서 고유한 DNS 호스트 이름이 필요합니다. DNS 이름은 문자열 값입니다. 이 이름은 순서에 관계없이 영숫자 문자, 대시(-) 및 하이픈(_)만 포함할 수 있습니다. DNS 호스트 이름은 대/소문자를 구분하지 않습니다. 최대 길이는 63자이지만 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 지정할 수 있는 최대 길이는 15자입니다.  
  
 의미 있는 문자열을 지정하는 것이 좋습니다. 예를 들어, `AG1`이라는 가용성 그룹의 경우 `ag1-listener`와 같은 의미 있는 DNS 호스트 이름을 지정합니다.  
  
> [!IMPORTANT]  
>  NetBIOS는 dns_name에서 처음 15자만 인식합니다. 두 WSFC 클러스터가 동일한 Active Directory에 의해 제어될 때 15자 이상의 이름과 동일한 15자 접두사를 사용하여 두 클러스터 모두에서 가용성 그룹 수신기를 만들려고 하면Virtual Network 이름 리소스를 온라인으로 전환할 수 없다는 오류 메시지가 표시됩니다. DNS 이름의 접두사 명명 규칙에 대한 자세한 내용은 [도메인 이름 할당](http://technet.microsoft.com/library/cc731265\(WS.10\).aspx)을 참조하세요.  
  
###  <a name="WinPermissions"></a> Windows 사용 권한  
  
|사용 권한|링크|  
|-----------------|----------|  
|가용성 그룹을 호스팅하는 WSFC 클러스터의 CNO(클러스터 개체 이름)에는 **컴퓨터 개체 생성** 권한이 있어야 합니다.<br /><br /> Active Directory에서 기본적으로 CNO는 명시적으로 **컴퓨터 개체 생성** 권한이 없으며 10개의 VCO(가상 컴퓨터 개체)를 만들 수 있습니다. 10개의 VCO를 만든 후에는 VCO를 추가로 만들 수 없습니다. WSFC 클러스터의 CNO에 대한 권한을 명시적으로 부여하여 이 문제를 방지할 수 있습니다. 삭제한 가용성 그룹에 대한 VCO는 Active Directory에서 자동으로 삭제되지 않으며 수동으로 삭제하지 않는 한 10개의 VCO 기본 제한 개수에 대해 계산됩니다.<br /><br /> 참고: 일부 조직에서는 보안 정책에 따라 **컴퓨터 개체 생성** 권한을 개별 사용자 계정에 부여하는 작업이 금지됩니다.|*클러스터를 설치하는 사람의 계정을 구성하는 단계* - [장애 조치(Failover) 클러스터 단계별 가이드: Active Directory에서 계정 구성](http://technet.microsoft.com/library/cc731002\(WS.10\).aspx#BKMK_steps_installer)<br /><br /> *클러스터 이름 계정을 미리 준비하는 단계* - [장애 조치(Failover) 클러스터 단계별 가이드: Active Directory에서 계정 구성](http://technet.microsoft.com/library/cc731002\(WS.10\).aspx#BKMK_steps_precreating)|  
|조직에서 수신기 가상 네트워크 이름에 대한 컴퓨터 계정을 미리 준비해야 하는 경우 **계정 운영자** 그룹의 멤버 자격 또는 도메인 관리자의 지원이 필요합니다.|*클러스터형 서비스 또는 응용 프로그램에 대한 계정을 미리 준비하는 단계* - [장애 조치(Failover) 클러스터 단계별 가이드: Active Directory에서 계정 구성](http://technet.microsoft.com/library/cc731002\(WS.10\).aspx#BKMK_steps_precreating2)|  
  
> [!TIP]  
>  일반적으로 수신기 가상 네트워크 이름에 대한 컴퓨터 계정을 미리 준비하지 않는 것이 가장 간단합니다. 가능하면 WSFC 고가용성 마법사를 실행할 때 계정을 자동으로 만들고 구성하도록 합니다.  
  
###  <a name="SqlPermissions"></a> SQL Server 사용 권한  
  
|태스크|사용 권한|  
|----------|-----------------|  
|가용성 그룹 수신기를 만들려면|CREATE AVAILABILITY GROUP 서버 권한, ALTER ANY AVAILABILITY GROUP 권한, CONTROL SERVER 권한 중 하나와 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.|  
|기존 가용성 그룹 수신기를 수정하려면|가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다.|  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
> [!TIP]  
>  [새 가용성 그룹 마법사](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md) 는 새 가용성 그룹에 대한 수신기 만들기를 지원합니다.  
  
 **가용성 그룹 수신기를 만들거나 구성하려면**  
  
1.  개체 탐색기에서 가용성 그룹의 주 복제본을 호스팅하는 서버 인스턴스에 연결하고 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **Always On 고가용성** 노드 및 **가용성 그룹** 노드를 확장합니다.  
  
3.  수신기를 구성할 가용성 그룹을 클릭하고 다음 대체 방법 중 하나를 선택합니다.  
  
    -   수신기를 만들려면 **가용성 그룹 수신기** 노드를 마우스 오른쪽 단추로 클릭하고 **새 수신기** 명령을 선택합니다. 그러면 **새 가용성 그룹 수신기** 대화 상자가 열립니다. 자세한 내용은 이 항목의 뒷부분에 나와 있는 [가용성 그룹 수신기 추가(대화 상자)](#AddAgListenerDialog)를 참조하세요.  
  
    -   기존 수신기의 포트 수를 변경하려면 **가용성 그룹 수신기** 노드를 확장하고 수신기를 마우스 오른쪽 단추로 클릭한 다음 **속성** 명령을 선택합니다. **포트** 필드에 새 포트 번호를 입력하고 **확인**을 클릭합니다.  
  
###  <a name="AddAgListenerDialog"></a> 새 가용성 그룹 수신기(대화 상자)  
 **수신기 DNS 이름**  
 가용성 그룹 수신기의 DNS 호스트 이름을 지정합니다. DNS 이름은 문자열이며 도메인과 NetBIOS에서 고유해야 합니다. 이 이름은 순서에 관계없이 영숫자 문자, 대시(-) 및 하이픈(_)만 포함할 수 있습니다. DNS 호스트 이름은 대/소문자를 구분하지 않습니다. 최대 길이는 15자입니다.  
  
 자세한 내용은 이 항목의 앞부분에 나오는 [가용성 그룹 수신기의 DNS 이름에 대한 요구 사항](#DNSnameReqs)을 참조하세요.  
  
 **포트**  
 이 수신기에서 사용되는 TPC 포트입니다.  
  
 **네트워크 모드**  
 수신기에 사용되는 TCP 프로토콜을 나타내며 다음 중 하나입니다.  
  
 **DHCP**  
 수신기는 DHCP(동적 호스트 구성 프로토콜)를 실행하는 서버에서 할당되는 동적 IP 주소를 사용합니다. DHCP는 단일 서브넷으로 제한됩니다.  
  
> [!IMPORTANT]  
>  프로덕션 환경에서는 DHCP를 사용하지 않는 것이 좋습니다. 중단 시간이 있고 DHCP IP 임대가 만료되는 경우 수신기 DNS 이름과 연결되고 클라이언트 연결에 영향을 주는 새 DHCP 네트워크 IP 주소를 등록하기 위해 추가 시간이 필요합니다. 그러나 가용성 그룹의 기본 기능을 확인하고 응용 프로그램과 통합하기 위해 DHCP를 개발 및 테스트 환경에 설정하는 것은 좋습니다.  
  
 **고정 IP**  
 수신기는 하나 이상의 고정 IP 주소를 사용합니다. 추가 IP 주소는 선택적입니다. 여러 서브넷 간에 가용성 그룹 수신기를 만들려면 각 서브넷에 대해 수신기 구성에서 고정 IP 주소를 지정해야 합니다. 이러한 고정 IP 주소를 얻으려면 네트워크 관리자에게 문의하세요.  
  
 **고정 IP** 를 선택하면 **네트워크 모드** 필드 아래 서브넷 표가 나타납니다. 이 표에는 이 가용성 그룹 수신기가 액세스할 수 있는 각 서브넷에 대한 정보가 표시됩니다. **추가**를 클릭하여 고정 IP 주소를 추가할 때까지 이 표는 비어 있습니다.  
  
 열은 다음과 같습니다.  
  
 **서브넷**  
 가용성 그룹 수신기에 추가하는 각 서브넷의 식별자를 표시합니다.  
  
 **IP 주소**  
 지정된 서브넷의 IP 주소를 표시합니다.  지정된 서브넷에 대해 IP 주소는 IPv4 주소 또는 IPv6 주소입니다.  
  
 **추가**  
 선택한 서브넷 또는 이 수신기에 대한 다른 서브넷에 고정 IP 주소를 추가하려면 클릭합니다. 그러면 **IP 주소 추가** 대화 상자가 열립니다. 자세한 내용은 [IP 주소 추가 대화 상자&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/add-ip-address-dialog-box-sql-server-management-studio.md) 도움말 항목을 참조하세요.  
  
 **제거**  
 이 수신기에서 선택한 서브넷을 제거하려면 클릭합니다.  
  
 **확인**  
 지정한 가용성 그룹 수신기를 만들려면 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **가용성 그룹 수신기를 만들거나 구성하려면**  
  
1.  주 복제본을 호스팅하는 서버 인스턴스에 연결합니다.  
  
2.  [CREATE AVAILABILITY GROUP](../../../t-sql/statements/create-availability-group-transact-sql.md) 문의 LISTENER 옵션 또는 [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) 문의 ADD LISTENER 옵션을 사용합니다.  
  
     다음 예에서는 `MyAg2`라는 기존 가용성 그룹에 가용성 그룹 수신기를 추가합니다. 이 수신기에 대해 고유한 DNS 이름인 `MyAg2ListenerIvP6`이 지정됩니다. 두 복제본이 서로 다른 서브넷에 있으므로 수신기는 고정 IP 주소를 사용하는 것이 좋습니다. 두 가용성 복제본 각각에 대해 IPv6 형식을 사용하는 고정 IP 주소인 `2001:4898:f0:f00f::cf3c and 2001:4898:e0:f213::4ce2`를 WITH IP 절이 지정합니다. 또한 이 예제에서 PORT 인수(옵션)를 사용하여 포트 `60173` 을 수신기 포트로 지정합니다.  
  
    ```  
    ALTER AVAILABILITY GROUP MyAg2   
          ADD LISTENER ‘MyAg2ListenerIvP6’ ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173 );   
    GO  
  
    ```  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  
 **가용성 그룹 수신기를 만들거나 구성하려면**  
  
1.  주 복제본을 호스트하는 서버 인스턴스로 디렉터리(**cd**)를 변경합니다.  
  
2.  가용성 그룹 수신기를 만들거나 수정하려면 다음 cmdlet 중 하나를 사용합니다.  
  
     **New-SqlAvailabilityGroupListener**  
     새 가용성 그룹 수신기를 만들고 기존 가용성 그룹에 연결합니다.  
  
     예를 들어, 다음 **New-SqlAvailabilityGroupListener** 명령은 가용성 그룹 `MyListener` 에 대해 `MyAg`라는 가용성 그룹 수신기를 만듭니다. 이 수신기는 가상 IP 주소로 **-StaticIp** 매개 변수에 전달된 IPv4 주소를 사용합니다.  
  
    ```  
    New-SqlAvailabilityGroupListener -Name MyListener `   
    -StaticIp '192.168.3.1/255.255.252.0' `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg  
  
    ```  
  
     **Set-SqlAvailabilityGroupListener**  
     기존 가용성 수신기에서 포트 설정을 수정합니다.  
  
     예를 들어, 다음 **Set-SqlAvailabilityGroupListener** 명령은 `MyListener` 라는 가용성 그룹 수신기의 포트 번호를 `1535`로 설정합니다. 이 포트는 수신기에 대한 연결을 수신하는 데 사용됩니다.  
  
    ```  
    Set-SqlAvailabilityGroupListener -Port 1535 `   
    -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AGListeners\MyListener  
  
    ```  
  
     **Add-SqlAGListenerstaticIp**  
     기존 가용성 그룹 수신기 구성에 고정 IP 주소를 추가합니다. IP 주소는 서브넷이 있는 IPv4 주소이거나 IPv6 주소일 수 있습니다.  
  
     예를 들어, 다음 **Add-SqlAGListenerstaticIp** 명령은 가용성 그룹 `MyListener` 의 가용성 그룹 수신기 `MyAg`에 고정 IPv4 주소를 추가합니다. 이 IPv6 주소는 `255.255.252.0`서브넷에서 수신기의 가상 IP 주소로 사용됩니다. 가용성 그룹이 복수 서브넷에 있는 경우 각 서브넷에 대한 고정 IP 주소를 수신기에 추가해야 합니다.  
  
    ```  
    $path = "SQLSERVER:\SQL\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AGListeners\ MyListener" `   
    Add-SqlAGListenerstaticIp -Path $path `   
    -StaticIp "2001:0db8:85a3:0000:0000:8a2e:0370:7334"  
    ```  
  
    > [!NOTE]  
    >  cmdlet의 구문을 보려면 **PowerShell 환경에서**  Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cmdlet을 사용합니다. 자세한 내용은 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)을 참조하세요.  
  
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
## <a name="troubleshooting"></a>문제 해결  
  
###  <a name="ADQuotas"></a> Active Directory 할당량으로 인한 가용성 그룹 수신기 만들기의 오류  
 참여하는 클러스터 노드 컴퓨터 계정에 대한 Active Directory 할당량에 도달하여 새 가용성 그룹 수신기를 만들지 못할 수도 있습니다.  자세한 내용은 다음 문서를 참조하세요.  
  
-   [컴퓨터 개체 수정 시 클러스터 서비스 계정 문제를 해결하는 방법](http://support.microsoft.com/kb/307532)  
  
-   [Active Directory 할당량](http://technet.microsoft.com/library/cc904295\(WS.10\).aspx)  
  
##  <a name="FollowUp"></a> 후속 작업: 가용성 그룹 수신기를 만든 후  
  
###  <a name="MultiSubnetFailover"></a> MultiSubnetFailover 키워드 및 관련 기능  
 **MultiSubnetFailover** 는 SQL Server 2012에서 Always On 가용성 그룹과 Always On 장애 조치(Failover) 클러스터 인스턴스를 사용하여 보다 빠르게 장애 조치할 수 있도록 하는 데 사용되는 새로운 연결 문자열 키워드입니다. `MultiSubnetFailover=True` 가 연결 문자열에서 설정되면 다음 세 가지 하위 기능을 사용할 수 있습니다.  
  
-   Always On 가용성 그룹 또는 장애 조치(Failover) 클러스터 인스턴스에 대한 다중 서브넷 수신기로 보다 빠른 다중 서브넷 장애 조치  
  
-   Always On 가용성 그룹 또는 장애 조치(Failover) 클러스터 인스턴스에 대한 단일 서브넷 수신기로 보다 빠른 단일 서브넷 장애 조치  
  
    -   이 기능은 단일 서브넷의 단일 IP가 있는 수신기에 연결할 때 사용되며, 단일 서브넷 장애 조치(Failover) 속도를 높이기 위해 보다 적극적으로 TCP 연결을 다시 시도합니다.  
  
-   다중 서브넷 Always On 장애 조치(Failover) 클러스터 인스턴스로 명명된 인스턴스 확인  
  
    -   서브넷 끝점이 여러 개인 Always On 장애 조치(Failover) 클러스터 인스턴스에 대한 명명된 인스턴스 확인 지원을 추가합니다.  
  
 **MultiSubnetFailover=True가 .NET Framework 3.5 또는 OLEDB에서 지원되지 않음**  
  
 **문제:** 가용성 그룹 또는 장애 조치(Failover) 클러스터 인스턴스에 각기 다른 서브넷의 여러 IP 주소를 사용하는 수신기 이름(WSFC 클러스터 관리자에서는 네트워크 이름 또는 클라이언트 액세스 지점이라고도 함)이 있고 .NET Framework 3.5 SP1 또는 SQL Native Client 11.0 OLEDB가 있는 ADO.NET을 사용하는 경우 가용성 그룹 수신기에 대한 클라이언트 연결 요청 중 50%가 연결 제한 시간을 초과할 수 있습니다.  
  
 **해결 방법:** 다음 작업 중 하나를 수행하는 것이 좋습니다.  
  
-   클러스터 리소스를 조작할 권한이 없는 경우 연결 제한 시간을 30초로 변경합니다. 이 값은 20초 TCP 제한 시간 기간과 10초 버퍼를 더한 값입니다.  
  
     **장점**: 서브넷 간 장애 조치(Failover)가 발생하는 경우 클라이언트 복구 시간이 짧습니다.  
  
     **단점**: 클라이언트 연결 중 절반이 20초 이상 걸립니다.  
  
-   클러스터 리소스를 조작할 권한이 있는 경우 더 권장하는 방법은 가용성 그룹 수신기의 네트워크 이름을 `RegisterAllProvidersIP=0`으로 설정하는 것입니다. 자세한 내용은 이 항목의 뒷부분에 나오는 "RegisterAllProvidersIP 설정”을 참조하세요.  
  
     **장점** : 클라이언트 연결 제한 시간 값을 증가시키지 않아도 됩니다.  
  
     **단점:** 서브넷 간 장애 조치(Failover)가 발생하는 경우 클라이언트 복구 시간은 **HostRecordTTL** 설정 및 사이트 간 DNS/AD 복제 일정의 설정에 따라 15분 이상이 될 수 있습니다.  
  
###  <a name="RegisterAllProvidersIP"></a> RegisterAllProvidersIP 설정  
 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]또는 PowerShell을 사용하여 가용성 그룹 수신기를 만들면 WSFC에서 **RegisterAllProvidersIP** 속성이 1(true)로 설정된 클라이언트 액세스 지점이 만들어집니다. 이 속성 값의 효과는 클라이언트 연결 문자열에 따라 다음과 같이 달라집니다.  
  
-   **MultiSubnetFailover** 를 true로 설정하는 연결 문자열  
  
     [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 은 클라이언트 연결 문자열이 권장 사항에 따라  **를 지정하는 클라이언트에 대한 장애 조치(Failover) 후에 재연결 시간을 줄이기 위해** RegisterAllProvidersIP `MultiSubnetFailover = True`속성을 1로 설정합니다. 수신기의 다중 서브넷 기능을 사용하려면 클라이언트에 **MultiSubnetFailover** 키워드를 지원하는 데이터 공급자가 필요할 수 있습니다. 다중 서브넷 장애 조치(Failover)의 드라이버 지원에 대한 자세한 내용은 [Always On 클라이언트 연결&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)을 참조하세요.  
  
     다중 서브넷 클러스터링에 대한 자세한 내용은 [SQL Server 다중 서브넷 클러스터링&#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md)를 만들거나 구성하는 방법에 대해 설명합니다.  
  
    > [!TIP]  
    >  `RegisterAllProvidersIP = 1`일 때 WSFC 클러스터에서 WSFC 구성 유효성 검사 마법사를 실행하면 마법사가 다음과 같은 경고 메시지를 생성합니다.  
    >   
    >  “네트워크 이름 'Name:<network_name>'의 RegisterAllProviderIP 속성이 1로 설정되어 있습니다. 현재 클러스터 구성에서는 이 값을 0으로 설정해야 합니다.”  
    >   
    >  이 메시지는 무시하세요.  
  
-   **MultiSubnetFailover** 를 true로 설정하지 않는 연결 문자열  
  
     `RegisterAllProvidersIP = 1`일 때는 연결 문자열이 `MultiSubnetFailover = True`를 사용하지 않는 클라이언트에서 연결 대기 시간이 길어집니다. 이는 이러한 클라이언트가 모든 IP에 순차적으로 연결을 시도하기 때문에 발생합니다. 반면에 **RegisterAllProvidersIP** 를 0으로 변경하면 활성 IP 주소가 WSFC 클러스터의 클라이언트 액세스 지점에 등록되기 때문에 레거시 클라이언트에 대한 대기 시간이 줄어듭니다. 따라서 가용성 그룹 수신기에 연결할 필요가 없고 **MultiSubnetFailover** 속성을 사용할 수 없는 레거시 클라이언트가 있을 경우 **RegisterAllProvidersIP** 를 0으로 변경하는 것이 좋습니다.  
  
    > [!IMPORTANT]  
    >  WSFC 클러스터(장애 조치(Failover) 클러스터 관리자 GUI)를 통해 가용성 그룹 수신기를 만들면 기본적으로 **RegisterAllProvidersIP** 는 0(false)으로 설정됩니다.  
  
###  <a name="HostRecordTTL"></a> HostRecordTTL 설정  
 기본적으로 클라이언트는 클러스터 DNS 레코드를 20분 동안 캐시합니다.  캐시된 레코드에 대한 TTL(Time to Live)인 **HostRecordTTL**을 줄여 레거시 클라이언트가 더 빨리 다시 연결할 수 있습니다.  하지만 **HostRecordTTL** 설정을 줄이면 DN 서버의 트래픽이 증가할 수 있습니다.  
  
###  <a name="SampleScript"></a> RegisterAllProvidersIP를 비활성화하고 TTL을 줄이는 샘플 PowerShell 스크립트  
 다음 PowerShell 예에서는 수신기 리소스에 대한 **RegisterAllProvidersIP** 및 **HostRecordTTL** 클러스터 매개 변수를 구성하는 방법을 보여 줍니다.  DNS 레코드는 기본 20분이 아닌 5분 동안 캐시됩니다.  두 클러스터 매개 변수를 모두 수정하면 **MultiSubnetFailover** 매개 변수를 사용할 수 없는 레거시 클라이언트에 대한 장애 조치(Failover) 후 올바른 IP 주소에 연결하는 시간이 줄어들 수 있습니다.  `yourListenerName` 을 변경할 수신기의 이름으로 바꿉니다.  
  
```  
Import-Module FailoverClusters  
Get-ClusterResource yourListenerName | Set-ClusterParameter RegisterAllProvidersIP 0   
Get-ClusterResource yourListenerName|Set-ClusterParameter HostRecordTTL 300  
Stop-ClusterResource yourListenerName  
Start-ClusterResource yourListenerName  
```  
  
 장애 조치(Failover) 중 복구 시간에 대한 자세한 내용은 [Client Recovery Latency During Failover](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md#DNS)을 참조하세요.  
  
###  <a name="FollowUpRecommendations"></a> 후속 권장 사항  
 가용성 그룹 수신기를 만든 후:  
  
-   네트워크 관리자에게 요청하여 수신기의 IP 주소를 배타적으로 사용할 수 있도록 예약합니다.  
  
-   이 가용성 그룹에 대한 클라이언트 연결을 요청할 때 연결 문자열에 사용할 수신기의 DNS 호스트 이름을 응용 프로그램 개발자에게 제공합니다.  
  
-   가능한 경우 개발자가 클라이언트 연결 문자열을 업데이트하여 `MultiSubnetFailover = True`를 지정하도록 권장합니다. 다중 서브넷 장애 조치(Failover)의 드라이버 지원에 대한 자세한 내용은 [Always On 클라이언트 연결&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)을 참조하세요.  
  
###  <a name="CreateAdditionalListener"></a> 가용성 그룹의 추가 수신기 만들기(선택 사항)  
 SQL Server를 통해 수신기를 하나 만든 후 다음과 같이 추가 수신기를 추가할 수 있습니다.  
  
1.  다음 도구 중 하나를 사용하여 수신기를 만듭니다.  
  
    -   **WSFC 장애 조치(Failover) 클러스터 관리자 사용:**  
  
        1.  클라이언트 액세스 지점을 추가하고 IP 주소를 구성합니다.  
  
        2.  수신기를 온라인 상태로 전환합니다.  
  
        3.  WSFC 가용성 그룹 리소스에 종속성을 추가합니다.  
  
         장애 조치(Failover) 클러스터 관리자의 대화 상자와 탭에 대한 자세한 내용은 [사용자 인터페이스: 장애 조치(Failover) 클러스터 관리자 스냅인](http://technet.microsoft.com/library/cc772502.aspx)을 참조하세요.  
  
    -   **장애 조치(failover) 클러스터용 Windows PowerShell 사용:**  
  
        1.  [Add-ClusterResource](http://technet.microsoft.com/library/ee460983.aspx) 를 사용하여 네트워크 이름과 IP 주소 리소스를 만듭니다.  
  
        2.  [Start-ClusterResource](http://technet.microsoft.com/library/ee461056.aspx) 를 사용하여 네트워크 이름 리소스를 시작합니다.  
  
        3.  [Add-ClusterResourceDependency](http://technet.microsoft.com/library/ee461014.aspx) 를 사용하여 네트워크 이름과 기존 SQL Server 가용성 그룹 리소스 간의 종속성을 설정합니다.  
  
         장애 조치(failover) 클러스터용 Windows Powershell에 대한 자세한 내용은 [서버 관리자 명령 개요](http://technet.microsoft.com/library/cc732757.aspx#BKMK_wps)를 참조하세요.  
  
2.  새 수신기에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 수신 대기를 시작합니다. 추가 수신기를 만든 후 가용성 그룹의 주 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 인스턴스에 연결하고 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]또는 PowerShell을 사용하여 수신기 포트를 수정합니다.  
  
 자세한 내용은 [동일한 가용성 그룹에 대해 여러 수신기를 만드는 방법](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/03/how-to-create-multiple-listeners-for-same-availability-group-goden-yao/) (SQL Server Always On 팀 블로그)을 참조하세요.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [가용성 그룹 수신기 속성 보기&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)  
  
-   [가용성 그룹 수신기 제거&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-listener-sql-server.md)  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   [동일한 가용성 그룹에 대해 여러 수신기를 만드는 방법](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/03/how-to-create-multiple-listeners-for-same-availability-group-goden-yao/)  
  
-   [SQL Server Always On 팀 블로그: 공식 SQL Server Always On 팀 블로그](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 그룹 수신기, 클라이언트 연결 및 응용 프로그램 장애 조치(failover)&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)   
 [SQL Server 다중 서브넷 클러스터링&#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md)  
  
  
