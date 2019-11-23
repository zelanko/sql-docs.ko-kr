---
title: '복제본 지정 페이지(새 가용성 그룹 마법사: 복제본 추가 마법사) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.newagwizard.listeners.f1
- sql12.swb.newagwizard.specifyreplicas.f1
- sql12.swb.addreplicawizard.specifyreplicas.f1
ms.assetid: 2d90fc12-a67b-4bd0-b0ab-899b73017196
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5ab74dc982416e3c18f2a0ad649e52de23770c5a
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176051"
---
# <a name="specify-replicas-page-new-availability-group-wizard-add-replica-wizard"></a>복제본 페이지 지정(새 가용성 그룹 마법사: 복제본 추가 마법사)
  이 항목에서는 **복제본 선택** 페이지의 옵션에 대해 설명합니다. 이 페이지는 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] 의 [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)] 및 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]에 적용됩니다. **복제본 선택** 페이지에서 하나 이상의 가용성을 지정하고 구성하여 가용성 그룹을 추가합니다. 이 페이지에 포함된 4개의 탭은 다음 표에 설명되어 있습니다. 표에서 탭 이름을 클릭하면 이 항목 뒷부분의 해당 섹션으로 이동할 수 있습니다.  
  
|탭|간단한 설명|  
|---------|-----------------------|  
|[복제본](#ReplicasTab)|보조 복제본을 호스팅할 예정이거나 현재 호스팅하고 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 각 인스턴스를 지정하려면 이 탭을 사용합니다. 현재 연결된 서버 인스턴스가 주 복제본을 호스팅해야 합니다.<br /><br /> 팁: 다른 탭을 시작하기 전에 **복제본** 탭에서 모든 복제본의 지정을 마칩니다.|  
|[엔드포인트](#EndpointsTab)|기존 데이터베이스 미러링 엔드포인트를 확인하고, 서비스 계정에서 Windows 인증을 사용하는 서버 인스턴스에 이 엔드포인트가 없는 경우 엔드포인트를 자동으로 만들려면 이 탭을 사용합니다.|  
|[백업 기본 설정](#BackupPreferencesTab)|가용성 그룹 전체에 대한 백업 기본 설정과 개별 가용성 복제본에 대한 백업 우선 순위를 지정하려면 이 탭을 사용합니다.|  
|[수신기](#Listener)|가능한 경우 가용성 그룹 수신기를 만들려면 이 탭을 사용합니다. 기본적으로 수신기는 만들어지지 않습니다.<br /><br /> 참고: 이 탭은 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)]를 실행하는 경우에만 사용할 수 있습니다.|  
  
##  <a name="ReplicasTab"></a> 복제본 탭  
 **서버 인스턴스**  
 가용성 복제본을 호스팅할 서버 인스턴스의 이름을 표시합니다.  
  
 보조 복제본을 호스팅하는 데 사용하는 서버 인스턴스가 **가용성 복제본** 표에 나열되지 않는 경우 **복제본 추가** 단추를 클릭합니다. 하이브리드 IT 환경에서 가용성 그룹을 구성하는 경우( [Azure Virtual Machines에서 SQL Server에 대한 고가용성 및 재해 복구](https://msdn.microsoft.com/library/windowsazure/jj870962.aspx) 참조) **Azure 복제본 추가** 단추를 클릭하여 Azure에서 보조 복제본을 사용하는 가상 머신을 만들 수 있습니다.  
  
 **초기 역할**  
 새 복제본이 처음에 수행할 역할( **주** 또는 **보조**)을 나타냅니다.  
  
 **자동 장애 조치 (Failover) (최대 2 개)**  
 이 가용성 복제본을 자동 장애 조치(failover) 파트너로 사용하려는 경우에만 이 확인란을 선택합니다. 자동 장애(failover) 조치를 구성하려면 초기 주 복제본 및 보조 복제본 하나에 대해 이 옵션을 선택해야 합니다. 이러한 복제본은 모두 동기-커밋 가용성 모드를 사용합니다. 두 개의 복제본만 자동 장애 조치(failover)를 지원할 수 있습니다.  
  
 동기-커밋 가용성 모드에 대 한 자세한 내용은 [가용성 모드 (AlwaysOn 가용성 그룹)](availability-modes-always-on-availability-groups.md)를 참조 하세요. 자동 장애 조치(failover)에 대한 자세한 내용은 [장애 조치(Failover) 및 장애 조치(Failover) 모드&#40;AlwaysOn 가용성 그룹&#41;](failover-and-failover-modes-always-on-availability-groups.md)를 참조하세요.  
  
 **동기 커밋(최대 3개)**  
 복제본에 대해 **자동 장애 조치(Failover)(최대 2개)** 를 선택한 경우 **동기 커밋(최대 3개)** 도 선택됩니다. 확인란이 비어 있으면 이 복제본에서 계획 수동 장애 조치와 함께 동기-커밋을 사용하려는 경우에만 이 확인란을 선택합니다. 3개의 복제본만 동기-커밋 모드를 사용할 수 있습니다.  
  
 이 복제본에서 비동기-커밋 가용성 모드를 사용하려는 경우 이 확인란을 비워 둡니다. 복제본은 강제 수동 장애 조치(데이터 손실 가능)만 지원합니다. 비동기-커밋 가용성 모드에 대 한 자세한 내용은 [가용성 모드 (AlwaysOn 가용성 그룹)](availability-modes-always-on-availability-groups.md)를 참조 하세요. 계획 수동 장애 조치(failover) 및 강제 수동 장애 조치(failover)에 대한 자세한 내용은 [장애 조치(Failover) 및 장애 조치(Failover) 모드&#40;AlwaysOn 가용성 그룹&#41;](failover-and-failover-modes-always-on-availability-groups.md)를 참조하세요.  
  
 **읽기 가능 보조 역할**  
 다음과 같이 **읽기용 보조** 드롭 목록에서 값을 선택합니다.  
  
 **아니오**  
 이 복제본의 보조 데이터베이스에 대한 직접 연결이 허용되지 않습니다. 즉, 읽기 액세스가 가능하지 않습니다. 이 값은 기본 설정입니다.  
  
 **읽기 전용만**  
 이 복제본의 보조 데이터베이스에 대한 직접 읽기 전용 연결만 허용됩니다. 즉, 모든 보조 데이터베이스에 대한 읽기 액세스가 가능합니다.  
  
 **예**  
 이 복제본의 보조 데이터베이스에 대한 모든 연결이 허용되지만 읽기 액세스만 가능합니다. 즉, 모든 보조 데이터베이스에 대한 읽기 액세스가 가능합니다.  
  
 **복제본 추가**  
 가용성 그룹에 보조 복제본을 추가하려면 클릭합니다.  
  
 **Azure 복제본 추가**  
 가용성 그룹에서 보조 복제본을 실행하는 Azure 가상 머신을 만들려면 클릭합니다. 이 옵션은 하이브리드 IT에서 온-프레미스 복제본이 포함된 가용성 그룹에만 적용할 수 있습니다. 자세한 내용은 [Azure Virtual Machines에서 SQL Server에 대한 고가용성 및 재해 복구](https://msdn.microsoft.com/library/windowsazure/jj870962.aspx)를 참조하세요.  
  
 **복제본 제거**  
 선택한 보조 복제본을 가용성 그룹에서 제거하려면 클릭합니다.  
  
##  <a name="EndpointsTab"></a> 엔드포인트 탭  
 **엔드포인트** 탭에는 가용성 복제본을 호스팅할 각 서버 인스턴스에 대한 기존 데이터베이스 미러링 엔드포인트의 실제 값(있는 경우)이나 Windows 인증을 사용할 잠재적인 새 엔드포인트의 제안된 값이 표시됩니다. 엔드포인트 값 표에는 기존 엔드포인트와 잠재적인 엔드포인트 모두에 대한 다음 정보가 표시됩니다.  
  
 **서버 이름**  
 가용성 복제본을 호스팅할 서버 인스턴스의 이름을 표시합니다.  
  
 **엔드포인트 URL**  
 데이터베이스 미러링 엔드포인트의 실제 또는 제안된 URL을 표시합니다. 제안된 새 엔드포인트의 경우 이 값을 변경할 수 있습니다. 이러한 URL 형식에 대한 자세한 내용은 [가용성 복제본 추가 또는 수정 시 엔드포인트 URL 지정&amp;#40;SQL Server&amp;#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)을 참조하세요.  
  
 **포트 번호**  
 엔드포인트의 실제 또는 제안된 포트 번호를 표시합니다. 제안된 새 엔드포인트의 경우 이 값을 변경할 수 있습니다.  
  
 **엔드포인트 이름**  
 엔드포인트의 실제 또는 제안된 이름을 표시합니다. 제안된 새 엔드포인트의 경우 이 값을 변경할 수 있습니다.  
  
 **데이터 암호화**  
 이 엔드포인트를 통해 보내는 데이터가 암호화되는지 여부를 나타냅니다. 제안된 새 엔드포인트의 경우 이 설정을 변경할 수 있습니다.  
  
 **SQL Server 서비스 계정**  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정의 사용자 이름입니다.  
  
 서버 인스턴스에서 Windows 인증을 사용하는 엔드포인트를 사용하려면 해당 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정은 도메인 계정이어야 합니다.  
  
 이 요구 사항에 따라 다음과 같이 이후 구성 단계가 결정됩니다.  
  
-   모든 서버 인스턴스가 도메인 서비스 계정으로 실행 중인 경우, 즉 **SQL Server 서비스 계정** 열에 각 서버 인스턴스의 도메인 서비스 계정이 표시되는 경우 **다음**을 클릭합니다.  
  
-   서버 인스턴스가 도메인 서비스 계정이 아닌 계정으로 실행 중인 경우 마법사를 계속하려면 먼저 서버 인스턴스를 수동으로 변경해야 합니다. 이 경우 **다음** 을 클릭 하면 경고 대화 상자가 나타납니다. **아니요**를 클릭 하 여**끝점** 탭으로 돌아갑니다. **복제본 지정** 페이지에서 마법사를 종료 하는 동안 **SQL Server 서비스 계정** 열에 비도메인 서비스 계정이 표시 되는 각 서버 인스턴스에 대해 다음 변경 중 하나를 수행 합니다.  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정을 도메인 계정으로 변경합니다. 자세한 내용은 [SQL Server의 서비스 시작 계정 변경&#40;SQL Server 구성 관리자&#41;](../../configure-windows/scm-services-change-the-service-startup-account.md)을 참조하세요.  
  
    -   인증서를 사용하는 데이터베이스 미러링 엔드포인트를 수동으로 만들려면 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 또는 PowerShell을 사용합니다. 자세한 내용은 [CREATE ENDPOINT&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql) 또는 [AlwaysOn 가용성 그룹에 대한 데이터베이스 미러링 엔드포인트 만들기&#40;SQL Server PowerShell&#41;](database-mirroring-always-on-availability-groups-powershell.md)를 참조하세요.  
  
     엔드포인트를 구성하는 동안 **가용성 복제본 지정** 페이지를 열어 둔 경우 **엔드포인트** 탭으로 돌아와서 **새로 고침** 을 클릭하여 **엔드포인트 값** 표를 업데이트합니다.  
  
##  <a name="BackupPreferencesTab"></a> 백업 기본 설정 탭  
 백업이 수행되는 위치를 지정하려면 다음 옵션 중 하나를 선택합니다.  
  
 **보조 사용**  
 백업이 보조 복제본에서 수행되도록 지정합니다. 주 복제본이 유일한 온라인 복제본인 경우는 예외로, 이 경우에는 백업이 주 복제본에서 수행되어야 합니다. 이 옵션이 기본 옵션입니다.  
  
 **보조만**  
 백업이 주 복제본에서 수행되지 않도록 지정합니다. 주 복제본이 유일한 온라인 복제본인 경우에는 백업이 수행되지 않아야 합니다.  
  
 **주**  
 백업이 항상 주 복제본에서 수행되도록 지정합니다. 이 옵션은 백업이 보조 복제본에서 실행될 때 지원되지 않는 차등 백업 만들기와 같은 백업 기능이 필요한 경우에 유용합니다.  
  
 **임의의 복제본**  
 백업을 수행할 복제본을 선택할 때 백업 작업에서 가용성 복제본의 역할을 무시하도록 지정합니다. 백업 작업에서는 각 가용성 복제본의 작동 상태 및 연결 상태와 함께 백업 우선 순위 등의 기타 요인을 평가할 수 있습니다.  
  
> [!IMPORTANT]  
>  백업 기본 설정은 적용되지 않습니다. 이 기본 설정의 해석은 지정된 가용성 그룹의 데이터베이스에 대한 백업 작업으로 스크립팅하는 논리(있는 경우)에 따라 달라집니다. 자세한 내용은 [활성 보조: 보조 복제본에 백업 (AlwaysOn 가용성 그룹)](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)을 참조 하세요.  
  
### <a name="replica-backup-priorities-grid"></a>복제본 백업 우선 순위 표  
 가용성 그룹의 각 복제본에 대한 백업 우선 순위를 지정하려면 **복제 백업 우선 순위** 표를 사용합니다. 이 표에는 다음 열이 있습니다.  
  
 **서버 인스턴스**  
 가용성 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름을 표시합니다.  
  
 **백업 우선 순위(최저 = 1, 최고 = 100)**  
 동일한 가용성 그룹의 다른 복제본과 관련하여 이 복제본에서 수행할 백업의 우선 순위를 할당합니다. 기본값은 50입니다. 0 ~ 100의 범위에서 다른 정수를 선택할 수 있습니다. 1은 가장 낮은 우선 순위를 나타내고 100은 가장 높은 우선 순위를 나타냅니다. **백업 우선 순위** 를 1로 설정하면 현재 사용 가능한 더 높은 우선 순위의 가용성 복제본이 없는 경우에만 해당 가용성 복제본이 백업 수행을 위해 선택됩니다.  
  
 **복제본 제외**  
 백업 수행을 위해 이 가용성 복제를 선택할 수 없도록 합니다. 이 값은 예를 들어 백업을 장애 조치할 대상으로 사용하지 않을 원격 가용성 복제본의 경우에 유용합니다.  
  
##  <a name="Listener"></a> 수신기 탭  
 클라이언트 연결 지점을 제공하는[가용성 그룹 수신기](../../listeners-client-connectivity-application-failover.md)에 대한 기본 설정을 지정합니다.  
  
 **가용성 그룹 수신기를 지금 만들지 않습니다.**  
 이 단계를 건너뛰려면 선택합니다. 나중에 수신기를 만들 수 있습니다. 자세한 내용은 [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)에 적용됩니다.  
  
 **가용성 그룹 수신기를 만듭니다.**  
 다음과 같이 이 가용성 그룹에 대한 수신기 기본 설정을 지정합니다.  
  
 **수신기 DNS 이름**  
 수신기의 네트워크 이름을 지정합니다. 이 이름은 도메인에서 고유해야 하며 영숫자, 대시( **-** ) 및 하이픈( **_** )만 임의의 순서로 포함할 수 있습니다. **수신기** 탭을 사용하여 지정한 경우 DNS 이름은 15자까지 가능합니다.  
  
> [!IMPORTANT]  
>  **수신기** 탭에 잘못된 DNS 수신기 이름(또는 포트 번호)을 입력하면 **복제본 지정** 페이지에서 **다음** 단추를 사용할 수 없습니다.  
  
 **포트**  
 이 수신기에서 사용되는 TPC 포트를 지정합니다.  
  
> [!NOTE]  
>  **수신기** 탭에 잘못된 포트 번호(또는 DNS 수신기 이름)를 입력하면 **복제본 지정** 페이지에서 **다음** 단추를 사용할 수 없습니다.  
  
 **네트워크 모드**  
 드롭 목록을 사용하여 이 수신기에 사용할 네트워크 모드를 선택합니다.  
  
 **고정 IP**  
 수신기가 두 개 이상의 서브넷에서 수신하도록 하려는 경우에 선택합니다. 고정 IP 네트워크 모드를 사용하려면 가용성 그룹 수신기가 가용성 그룹의 가용성 복제본을 호스팅하는 모든 서브넷에서 수신해야 합니다. 각 서브넷에 대해 **추가** 를 클릭하여 서브넷 주소를 선택하고 IP 주소를 지정합니다.  
  
 **고정 IP** 를 네트워크 모드(기본 선택 사항)로 선택하면 표에는 **서브넷** 및 **IP 주소** 열이 표시되고 관련된 **추가** 및 **제거** 단추가 표시됩니다. 첫 번째 서브넷을 추가할 때까지 표는 비어 있습니다.  
  
 **서브넷** 열  
 수신기에 추가한 각 서비스에 대해 선택한 서브넷 주소를 표시합니다.  
  
 **IP 주소** 열  
 지정한 서브넷에 대해 지정한 IPv4 또는 IPv6 주소를 표시합니다.  
  
 **추가**  
 서브넷을 이 수신기에 추가하려면 클릭합니다. 그러면 **IP 주소 추가** 대화 상자가 열립니다. 자세한 내용은 [IP 주소 추가 대화 상자&#40;SQL Server Management Studio&#41;](add-ip-address-dialog-box-sql-server-management-studio.md) 도움말 항목을 참조하세요.  
  
 **제거**  
 표에서 현재 선택되어 있는 서브넷을 제거하려면 클릭합니다.  
  
 **DHCP**  
 수신기가 단일 서브넷에서 수신하고 DHCP(동적 호스트 구성 프로토콜)를 실행하는 서버에서 할당되는 동적 IPv4 주소를 사용하도록 하려는 경우에 선택합니다. DHCP는 가용성 그룹의 가용성 복제본을 호스팅하는 모든 서버 인스턴스에 공통되는 단일 서브넷으로 제한됩니다.  
  
> [!IMPORTANT]  
>  프로덕션 환경에서는 DHCP를 사용하지 않는 것이 좋습니다. 중단 시간이 있고 DHCP IP 임대가 만료되는 경우 수신기 DNS 이름과 연결되고 클라이언트 연결에 영향을 주는 새 DHCP 네트워크 IP 주소를 등록하기 위해 추가 시간이 필요합니다. 그러나 가용성 그룹의 기본 기능을 확인하고 애플리케이션과 통합하기 위해 DHCP를 개발 및 테스트 환경에 설정하는 것은 좋습니다.  
  
 **DHCP** 를 선택하면 **서브넷** 필드가 표시됩니다.  
  
 **서브넷**  
 **DHCP** 를 네트워크 모드로 선택한 경우 **서브넷** 드롭 목록을 사용하여 가용성 그룹의 가용성 복제본을 호스팅하는 서브넷에 대한 주소를 선택합니다.  
  
> [!IMPORTANT]
>  가용성 그룹 수신기를 정의한 후에는 다음을 수행하는 것이 좋습니다.  
> 
>  -   네트워크 관리자에게 요청하여 수신기의 IP 주소를 배타적으로 사용할 수 있도록 예약합니다. 이 가용성 그룹에 대한 클라이언트 연결을 요청할 때 연결 문자열에 사용할 수신기의 DNS 호스트 이름을 애플리케이션 개발자에게 제공합니다.  
> -   이 가용성 그룹에 대한 클라이언트 연결을 요청할 때 연결 문자열에 사용할 수신기의 DNS 호스트 이름을 애플리케이션 개발자에게 제공합니다.  
  
##  <a name="RelatedTasks"></a> 관련 작업  
  
-   [가용성 그룹 마법사 사용&#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [가용성 그룹에 복제본 추가 마법사 사용&#40;SQL Server Management Studio&#41;](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [데이터베이스 미러링 엔드포인트에 대한 인증서 사용 &#40;Transact-SQL &#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   [CREATE ENDPOINT&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)  
  
-   [AlwaysOn 가용성 그룹 &#40;SQL Server PowerShell에 대 한 데이터베이스 미러링 끝점 만들기&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
## <a name="see-also"></a>참고 항목  
 [AlwaysOn 가용성 그룹 &#40;SQL Server&#41; 개요](overview-of-always-on-availability-groups-sql-server.md)   
 [CREATE AVAILABILITY GROUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-availability-group-transact-sql)   
 [AlwaysOn 가용성 그룹 &#40;에 대 한 사전 요구 사항, 제한 사항 및 권장 사항 SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
  
  
