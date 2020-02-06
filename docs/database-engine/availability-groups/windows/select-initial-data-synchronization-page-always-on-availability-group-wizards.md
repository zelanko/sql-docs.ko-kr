---
title: 초기 데이터 동기화 페이지 선택(가용성 그룹 마법사)
description: SSMS(SQL Server Management Studio)의 Always On 가용성 그룹 마법사에 있는 ‘초기 데이터 동기화 선택 페이지’에 대해 설명합니다.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.adddatabasewizard.selectinitialdatasync.f1
- sql13.swb.newagwizard.selectinitialdatasync.f1
- sql13.swb.addreplicawizard.selectinitialdatasync.f1
ms.assetid: 457b1140-4819-4def-8f7c-54a406e6db12
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e8a6a14a6efc6a9d5f96144364f1532c14b0c1c0
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75235338"
---
# <a name="select-initial-data-synchronization-page-always-on-availability-group-wizards"></a>초기 데이터 동기화 페이지 선택(Always On 가용성 그룹 마법사)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Always On **초기 데이터 동기화 선택** 페이지를 사용하여 새 보조 데이터베이스의 초기 데이터 동기화에 대한 기본 설정을 표시합니다. 이 페이지는 세 가지 마법사([!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)], [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)]및 [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)])에서 공유됩니다.  
  
 가능한 선택에는 **자동 시드**, **전체 데이터베이스 및 로그 백업**, **조인만** 또는 **초기 데이터 동기화 건너뛰기**가 있습니다. **자동 시드**, **전체** 또는 **조인만**을 선택하기 전에 환경이 필수 조건을 충족하는지 확인합니다.  
    
##  <a name="Recommendations"></a> 권장 사항  
  
-   초기 데이터 동기화 동안 주 데이터베이스에 대한 로그 백업 태스크를 일시 중지합니다.  
  
-   큰 데이터베이스에 대한 전체 백업 및 복원 작업에는 많은 시간과 자원이 소모될 수 있습니다. 이러한 경우 보조 데이터베이스를 직접 준비하는 것이 좋습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [수동으로 보조 데이터베이스를 준비하려면](#PrepareSecondaryDbs)을 참조하세요.  
  
-   전체 초기 데이터 동기화를 수행하려면 네트워크 공유를 지정해야 합니다. 마법사를 사용하여 전체 초기 데이터 동기화를 수행하기 전에 네트워크 공유 폴더의 액세스 권한에 대해 보안 계획을 구현하는 것이 좋습니다. 폴더에 대해 READ 권한이 있는 사람이 백업 파일의 중요한 데이터에 액세스할 수 있으므로 이 예방 조치가 중요합니다. 또한 백업 및 복원 작업을 보호하려면 가용성 복제본을 호스팅하는 모든 서버 인스턴스와 네트워크 공유 폴더 사이의 네트워크 채널에 대해 보안을 유지하는 것이 좋습니다.  
  
     백업 및 복원 작업에 대해 엄격히 보안을 유지해야 하는 경우 **조인만** 또는 **초기 데이터 동기화 건너뛰기** 옵션을 선택하는 것이 좋습니다.  
  
## <a name="Auto"></a> 자동 시드
 
 SQL Server는 자동으로 그룹의 모든 데이터베이스에 대한 보조 복제본을 만듭니다. 자동 시드를 사용하려면 데이터 및 로그 파일 경로가 그룹에 참여하는 모든 SQL Server 인스턴스에서 동일해야 합니다. [!INCLUDE[sssql15-md.md](../../../includes/sssql15-md.md)] 이상에서 사용할 수 있습니다. [Always On 가용성 그룹 자동 초기화](automatically-initialize-always-on-availability-group.md)를 참조하세요.

##  <a name="Full"></a> 전체 데이터베이스 및 로그 백업 
 각각의 주 데이터베이스에 대해 **전체 데이터베이스 및 로그 백업** 옵션은 하나의 워크플로에서 여러 작업을 수행합니다. 즉, 주 데이터베이스의 전체 및 로그 백업을 만들고, 보조 복제본을 호스팅하는 모든 서버 인스턴스에서 이러한 백업을 복원하여 해당 보조 데이터베이스를 만들고, 가용성 그룹에 각 보조 데이터베이스를 조인합니다.  
  
 현재 환경이 전체 초기 데이터 동기화를 사용하기 위한 다음 사전 요구 사항을 충족하고 마법사를 사용하여 데이터 동기화를 자동으로 시작하려는 경우에만 이 옵션을 선택합니다.  
  
 **전체 데이터베이스 및 로그 백업 초기 데이터 동기화를 사용하기 필수 조건**  
  
-   모든 데이터베이스 파일 경로는 가용성 그룹에 대한 복제본을 호스팅하는 모든 서버 인스턴스에서 동일해야 합니다.  
  
    > [!NOTE]  
    >  마법사를 실행하는 서버 인스턴스와 보조 복제본을 호스팅할 서버 인스턴스 간에 백업 및 복원 파일 경로가 다른 경우, WITH MOVE 옵션을 사용하여 수동으로 백업 및 복원 작업을 수행해야 합니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [수동으로 보조 데이터베이스를 준비하려면](#PrepareSecondaryDbs)을 참조하세요.  
  
-   보조 복제본을 호스팅하는 서버 인스턴스에 주 데이터베이스 이름이 없을 수 있습니다. 즉, 새 보조 데이터베이스가 아직 없을 수 있습니다.  
  
-   마법사에서 백업을 만들고 액세스하려면 네트워크 공유를 지정해야 합니다. 주 복제본의 경우 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 을 시작하는 데 사용되는 계정은 네트워크 공유에 대한 읽기 및 쓰기 파일 시스템 권한이 있어야 합니다. 보조 복제본에 대한 계정은 네트워크 공유에 대한 읽기 권한이 있어야 합니다.  
  
    > [!IMPORTANT]  
    >  로그 백업이 로그 백업 체인의 일부입니다. 로그 백업 파일을 적절히 저장합니다.  
  
 **사전 요구 사항이 충족되지 않는 경우**  
  
 마법사에서 이 가용성 그룹에 대한 보조 데이터베이스를 만들 수 없습니다. 보조 데이터를 준비하는 방법에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 [수동으로 보조 데이터베이스를 준비하려면](#PrepareSecondaryDbs)을 참조하세요.  
  
 **사전 요구 사항이 충족되는 경우**  
  
 이러한 필수 조건이 모두 충족되고 마법사에서 전체 초기 데이터 동기화를 수행하도록 하려면 **전체 데이터베이스 및 로그 백업** 옵션을 선택하고 네트워크 공유를 지정합니다. 그러면 마법사가 선택한 모든 데이터베이스에 대해 전체 데이터베이스 및 로그 백업를 만들고 지정한 네트워크 공유에 이러한 백업을 배치합니다. 그런 다음 새로운 보조 복제본 중 하나를 호스팅하는 모든 서버 인스턴스에서 마법사는 RESTORE WITH NORECOVERY를 사용하여 백업을 복원하는 방법으로 보조 데이터베이스를 만듭니다. 각 보조 데이터베이스를 만든 후 마법사는 새 보조 데이터베이스를 가용성 그룹에 조인합니다. 보조 데이터베이스가 조인되는 즉시 해당 데이터베이스에서 데이터 동기화가 시작됩니다.  
  
 **모든 복제본에서 액세스할 수 있는 공유 네트워크 위치 지정**  
 백업을 만들고 복원하려면 마법사에서 네트워크 공유를 지정해야 합니다. 가용성 복제본을 호스팅하는 각 서버 인스턴스에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 을 시작하는 데 사용하는 계정은 네트워크 공유에 대한 읽기 및 쓰기 파일 시스템 권한이 있어야 합니다.  
  
> [!IMPORTANT]  
>  로그 백업이 로그 백업 체인의 일부입니다. 백업 파일을 적절히 저장합니다.  
  
##  <a name="Joinonly"></a> 조인만  
 가용성 그룹의 보조 복제본을 호스팅하는 각 서버 인스턴스에 새 보조 데이터베이스가 이미 있는 경우에만 이 옵션을 선택합니다. 보조 데이터베이스 준비에 대한 자세한 내용은 이 섹션의 뒷부분에 나오는 [수동으로 보조 데이터베이스를 준비하려면](#PrepareSecondaryDbs)을 참조하세요.  
  
 **조인만**을 선택하면 마법사는 각 기존 보조 데이터베이스를 가용성 그룹에 조인하려고 시도합니다.  
  
## <a name="Skip"></a> 초기 데이터 동기화 건너뛰기  
 모든 주 데이터베이스의 데이터베이스 및 로그 백업을 직접 수행하고 보조 복제본을 호스팅하는 모든 서버 인스턴스로 복원하려는 경우에만 이 옵션을 선택합니다. 마법사를 종료한 후 모든 보조 복제본에서 모든 보조 데이터베이스를 조인해야 합니다.  
  
> [!NOTE]  
>  자세한 내용은 [Always On 보조 데이터베이스에서 데이터 이동 시작&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)를 참조하세요.  
  
##  <a name="PrepareSecondaryDbs"></a> 수동으로 보조 데이터베이스를 준비하려면  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 마법사와 독립적으로 보조 데이터베이스를 준비하려면 다음 방법 중 하나를 사용합니다.  
  
-   RESTORE WITH NORECOVERY를 사용하여 주 데이터베이스의 최신 데이터베이스 백업을 수동으로 복원한 다음 RESTORE WITH NORECOVERY를 사용하여 각 후속 로그 백업을 복원합니다. 주 데이터베이스와 보조 데이터베이스의 파일 경로가 다른 경우에는 WITH MOVE 옵션을 사용해야 합니다. 가용성 그룹의 보조 복제본을 호스팅하는 모든 서버 인스턴스에서 이 복원 시퀀스를 수행합니다.  [!INCLUDE[tsql](../../../includes/tsql-md.md)] 및 PowerShell을 사용하여 이러한 백업 및 복원 작업을 수행할 수 있습니다.  
  
     **자세한 내용은 다음을 참조하세요.**  
  
     [가용성 그룹에 대한 보조 데이터베이스 준비&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   하나 이상의 로그 전달 주 데이터베이스를 가용성 그룹에 추가하는 경우 로그 전달에서 하나 이상의 해당 보조 데이터베이스를 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]로 마이그레이션할 수 있습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [로그 전달에서 Always On 가용성 그룹으로 마이그레이션하기 위한 필수 조건&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-migrating-log-shipping-to-always-on-availability-groups.md))에서 공유합니다.  
  
    > [!NOTE]  
    >  가용성 그룹에 대해 모든 보조 데이터베이스를 만든 후에는 보조 복제본에서 백업을 수행할 경우 가용성 그룹의 자동화된 백업 기본 설정을 다시 구성해야 합니다.  
  
     **자세한 내용은 다음을 참조하세요.**  
  
     [로그 전달에서 Always On 가용성 그룹으로 마이그레이션하기 위한 필수 조건&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-migrating-log-shipping-to-always-on-availability-groups.md)  
  
     [가용성 복제본에 백업 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
 보조 데이터베이스를 만든 후 모든 현재 로그 백업을 새 보조 데이터베이스에 적용합니다.  
  
 필요에 따라 마법사를 실행하기 전에 모든 보조 데이터베이스를 준비할 수 있습니다. 그런 다음 마법사의 **초기 데이터 동기화 지정** 페이지에서 **조인만** 을 선택하여 새 보조 데이터베이스를 가용성 그룹에 자동으로 조인합니다.  
  
##  <a name="LaunchWiz"></a> 관련 작업  
  
-   [새 가용성 그룹 대화 상자 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [가용성 그룹에 복제본 추가 마법사 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [가용성 그룹에 데이터베이스 추가 마법사 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
-   [가용성 그룹 장애 조치(Failover) 마법사 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-fail-over-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Always On 보조 데이터베이스에서 데이터 이동 시작&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)  
  
-   [가용성 그룹에 보조 데이터베이스 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [새 가용성 그룹 대화 상자 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
