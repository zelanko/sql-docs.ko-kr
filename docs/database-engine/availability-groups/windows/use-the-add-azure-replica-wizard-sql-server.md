---
title: 가용성 그룹에서 Azure VM을 보조 복제본으로 구성
description: Azure 복제본 추가 마법사를 사용하여 하이브리드 IT에서 새 Azure VM을 만들고 새로운 또는 기존 Always On 가용성 그룹에 대한 보조 복제본으로 구성할 수 있습니다.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.addreplicawizard.azurereplica.f1
ms.assetid: b89cc41b-07b4-49f3-82cc-bc42b2e793ae
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2eb45257f2641b1e4e9f94865784f8910ebf27fd
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "74822665"
---
# <a name="configure-azure-vm-as-a-secondary-replica-in-an-availability-group"></a>가용성 그룹에서 Azure VM을 보조 복제본으로 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Azure 복제본 추가 마법사를 사용하여 하이브리드 IT에서 새 Azure VM을 만들고 새로운 또는 기존 Always On 가용성 그룹에 대한 보조 복제본으로 구성할 수 있습니다.  
  

##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
 가용성 그룹에 가용성 복제본을 추가한 적이 없는 경우 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)의 "서버 인스턴스" 섹션과 "가용성 그룹 및 복제본" 섹션을 참조하세요.  
  
##  <a name="prerequisites"></a><a name="Prerequisites"></a> 필수 조건  
  
-   현재 주 복제본을 호스팅하는 서버 인스턴스에 연결되어 있어야 합니다.  
  
-   온-프레미스 서브넷에 Azure를 사용하는 사이트 간 VPN을 갖춘 하이브리드 IT 환경이 있어야 합니다. 자세한 내용은 [관리 포털에서 사이트 간 VPN 구성](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create)을 참조하세요.  
  
-   가용성 그룹은 온-프레미스 가용성 복제본을 포함해야 합니다.  
  
-   가용성 그룹 수신기의 클라이언트는 가용성 그룹이 Azure 복제본으로 장애 조치될 때 수신기와 연결을 유지하려는 경우 인터넷에 연결해야 합니다.  
  
-   **전체 초기 데이터 동기화를 사용하기 위한 사전 요구 사항** 마법사에서 백업을 만들고 액세스하려면 네트워크 공유를 지정해야 합니다. 주 복제본의 경우 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 을 시작하는 데 사용되는 계정은 네트워크 공유에 대한 읽기 및 쓰기 파일 시스템 권한이 있어야 합니다. 보조 복제본에 대한 계정은 네트워크 공유에 대한 읽기 권한이 있어야 합니다.  
  
     마법사를 사용하여 전체 초기 데이터 동기화를 수행할 수 없는 경우에는 보조 데이터베이스를 수동으로 준비해야 합니다. 마법사를 실행하기 전이나 후에 이 작업을 수행할 수 있습니다. 자세한 내용은 [가용성 그룹에 대한 보조 데이터베이스 수동 준비&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)또는 PowerShell을 사용하여 Always On 가용성 그룹에 보조 데이터베이스를 조인하는 방법에 대해 설명합니다.  
  
##  <a name="permissions"></a><a name="Permissions"></a> 권한  
 가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다.  
  
 가용성 그룹에 복제본 추가 마법사에서 데이터베이스 미러링 엔드포인트를 관리할 수 있도록 하려면 CONTROL ON ENDPOINT 권한도 필요합니다.  
  
##  <a name="using-the-add-azure-replica-wizard-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Azure 복제본 추가 마법사 사용(SQL Server Management Studio)  
 [복제본 페이지 지정](../../../database-engine/availability-groups/windows/specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md)에서 Azure 복제본 추가 마법사를 시작할 수 있습니다. 다음 두 가지 방법으로 이 페이지에 도달할 수 있습니다.  
  
-   [가용성 그룹 마법사 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [가용성 그룹에 복제본 추가 마법사 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
 Azure 복제본 추가 마법사를 시작한 후 아래 단계를 따릅니다.  
  
1.  먼저 Azure 구독의 관리 인증서를 다운로드합니다. **다운로드** 를 클릭하여 로그인 페이지를 엽니다.  
  
2.  Microsoft 계정 또는 조직 계정으로 Microsoft Azure에 로그인합니다. Microsoft 또는 조직 계정은 "mailto:patc@contoso.com" patc@contoso.com 하이퍼링크와 같은 이메일 주소 형식입니다. Azure 자격 증명에 대한 자세한 내용은 [Microsoft 조직 계정 FAQ](https://technet.microsoft.com/jj592903) 및 [조직 계정을 사용하는 로그인의 문제 해결](https://support.microsoft.com/kb/2756852)을 참조하세요.  
  
3.  다음에는 **연결**을 클릭하여 구독에 연결합니다. 연결되면 드롭다운 목록에 **가상 네트워크** 및 **가상 네트워크 서브넷**과 같은 Azure 매개 변수가 채워집니다.  
  
4.  새 보조 복제본을 호스트할 Azure VM에 대한 설정을 지정합니다.  
  
     이미지  
     Azure VM에 사용할 SQL Server 이미지의 이름  
  
     VM 크기  
     Azure VM의 크기  
  
     VM 이름  
     Azure VM의 DNS 이름  
  
     VM 사용자 이름  
     Azure VM 기본 관리자의 사용자 이름  
  
     VM 관리자 암호(및 암호 확인)  
     Azure VM 기본 관리자의 암호  
  
     Virtual Network  
     Azure VM을 배치할 가상 네트워크  
  
     가상 네트워크 서브넷  
     Azure VM을 배치할 가상 네트워크 서브넷  
  
     도메인  
     Azure VM을 조인할 Active Directory(AD) 도메인  
  
     도메인 사용자 이름  
     Azure VM을 도메인에 조인하는 데 사용되는 AD 사용자 이름  
  
     암호  
     Azure VM을 도메인에 조인하는 데 사용되는 암호  
  
5.  **확인** 을 클릭하여 설정을 커밋하고 Azure 복제본 추가 마법사를 끝냅니다.  
  
6.  새 복제본에 대해 수행하는 것과 같은 방법으로 [복제본 지정 페이지](../../../database-engine/availability-groups/windows/specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md) 의 나머지 구성 단계를 계속합니다.  
  
     가용성 그룹 마법사 또는 가용성 그룹에 복제본 추가 마법사를 마치면 구성 프로세스를 통해 Azure에서 새 VM 만들기, AD 도메인에 VM 조인, Windows 클러스터에 VM 추가, Always On 고가용성 사용 설정, 가용성 그룹에 새 복제본 추가 등의 모든 작업이 수행됩니다.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 관련 작업  
  
-   [가용성 그룹에 보조 복제본 추가&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [가용성 그룹에 보조 복제본 추가&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
  
