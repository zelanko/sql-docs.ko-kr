---
title: Azure 복제본 추가 마법사 사용(SQL Server) | Microsoft Docs
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
- sql13.swb.addreplicawizard.azurereplica.f1
ms.assetid: b89cc41b-07b4-49f3-82cc-bc42b2e793ae
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c82e0f71a717732289f03ecee84717667c892c13
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="use-the-add-azure-replica-wizard-sql-server"></a>Azure 복제본 추가 마법사 사용(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Azure 복제본 추가 마법사를 사용하여 하이브리드 IT에서 새 Microsoft Azure VM을 만들고 새로운 또는 기존 Always On 가용성 그룹에 대한 보조 복제본으로 구성할 수 있습니다.  
  
-   **시작하기 전 주의 사항:**  
  
     [필수 구성 요소](#Prerequisites)  
  
     [보안](#Security)  
  
-   **복제본을 추가하려면:**  [Azure 복제본 추가 마법사(SQL Server Management Studio)](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
 가용성 그룹에 가용성 복제본을 추가한 적이 없는 경우 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)의 "서버 인스턴스" 섹션과 "가용성 그룹 및 복제본" 섹션을 참조하세요.  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
  
-   현재 주 복제본을 호스팅하는 서버 인스턴스에 연결되어 있어야 합니다.  
  
-   온-프레미스 서브넷에 Windows Azure를 사용하는 사이트 간 VPN을 갖춘 하이브리드 IT 환경이 있어야 합니다. 자세한 내용은 [관리 포털에서 사이트 간 VPN 구성](https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-site-to-site-create)을 참조하세요.  
  
-   가용성 그룹은 온-프레미스 가용성 복제본을 포함해야 합니다.  
  
-   가용성 그룹 수신기의 클라이언트는 가용성 그룹이 Windows Azure 복제본으로 장애 조치될 때 수신기와 연결을 유지하려는 경우 인터넷에 연결해야 합니다.  
  
-   **전체 초기 데이터 동기화를 사용하기 위한 사전 요구 사항** 마법사에서 백업을 만들고 액세스하려면 네트워크 공유를 지정해야 합니다. 주 복제본의 경우 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 을 시작하는 데 사용되는 계정은 네트워크 공유에 대한 읽기 및 쓰기 파일 시스템 권한이 있어야 합니다. 보조 복제본에 대한 계정은 네트워크 공유에 대한 읽기 권한이 있어야 합니다.  
  
     마법사를 사용하여 전체 초기 데이터 동기화를 수행할 수 없는 경우에는 보조 데이터베이스를 수동으로 준비해야 합니다. 마법사를 실행하기 전이나 후에 이 작업을 수행할 수 있습니다. 자세한 내용은 [가용성 그룹에 대한 보조 데이터베이스 수동 준비&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)에서 AlwaysOn 가용성 그룹을 만들고 구성하는 방법을 설명합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 [Security](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md#Security)를 참조하세요.  
  
##  <a name="SSMSProcedure"></a> Azure 복제본 추가 마법사 사용(SQL Server Management Studio)  
 [복제본 페이지 지정](../../../database-engine/availability-groups/windows/specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md)에서 Azure 복제본 추가 마법사를 시작할 수 있습니다. 다음 두 가지 방법으로 이 페이지에 도달할 수 있습니다.  
  
-   [가용성 그룹 마법사 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [가용성 그룹에 복제본 추가 마법사 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
 Azure 복제본 추가 마법사를 시작한 후 아래 단계를 따릅니다.  
  
1.  먼저 Windows Azure 구독을 위한 관리 인증서를 다운로드합니다. **다운로드** 를 클릭하여 로그인 페이지를 엽니다.  
  
2.  Microsoft 계정 또는 조직 계정으로 Microsoft Azure에 로그인합니다. Microsoft 또는 조직 계정은 "mailto:patc@contoso.com" patc@contoso.com 하이퍼링크와 같은 이메일 주소 형식입니다. Azure 자격 증명에 대한 자세한 내용은 [Microsoft 조직 계정 FAQ](http://technet.microsoft.com/jj592903) 및 [조직 계정을 사용하는 로그인의 문제 해결](https://support.microsoft.com/kb/2756852)을 참조하세요.  
  
3.  다음에는 **연결**을 클릭하여 구독에 연결합니다. 연결되면 드롭다운 목록에 **가상 네트워크** 및 **가상 네트워크 서브넷**과 같은 Microsoft Azure 매개 변수가 채워집니다.  
  
4.  새 보조 복제본을 호스팅할 Windows Azure VM에 대한 설정을 지정합니다.  
  
     이미지  
     Windows Azure VM에 사용할 SQL Server 이미지의 이름  
  
     VM 크기  
     Windows Azure VM의 크기입니다.  
  
     VM 이름  
     Windows Azure VM의 DNS 이름입니다.  
  
     VM 사용자 이름  
     Windows Azure VM 기본 관리자의 사용자 이름  
  
     VM 관리자 암호(및 암호 확인)  
     Windows Azure VM 기본 관리자의 암호  
  
     가상 네트워크  
     Windows Azure VM을 배치할 가상 네트워크  
  
     가상 네트워크 서브넷  
     Windows Azure VM을 배치할 가상 네트워크 서브넷  
  
     도메인  
     Windows Azure VM에 조인할 Active Directory(AD) 도메인  
  
     도메인 사용자 이름  
     Windows Azure VM을 도메인에 조인하는 데 사용되는 AD 사용자 이름  
  
     암호  
     Windows Azure VM을 도메인에 조인하는 데 사용되는 암호  
  
5.  **확인** 을 클릭하여 설정을 커밋하고 Azure 복제본 추가 마법사를 끝냅니다.  
  
6.  새 복제본에 대해 수행하는 것과 같은 방법으로 [복제본 지정 페이지](../../../database-engine/availability-groups/windows/specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md) 의 나머지 구성 단계를 계속합니다.  
  
     가용성 그룹 마법사 또는 가용성 그룹에 복제본 추가 마법사를 마치면 구성 프로세스를 통해 Microsoft Azure에서 새 VM 만들기, AD 도메인에 VM 조인, Windows 클러스터에 VM 추가, Always On 고가용성 활성화, 가용성 그룹에 새 복제본 추가 등의 모든 작업이 수행됩니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [가용성 그룹에 보조 복제본 추가&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [가용성 그룹에 보조 복제본 추가&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
  
