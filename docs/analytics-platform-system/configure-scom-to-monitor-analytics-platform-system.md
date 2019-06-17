---
title: Analytics Platform System을 모니터링 하도록 SCOM 구성 | Microsoft Docs
description: Analytics Platform System에 대 한 System Center Operations Manager (SCOM) 관리 팩을 구성 하려면 다음이 단계를 따릅니다. 관리 팩은 SCOM에서 Analytics Platform System을 모니터링 해야 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2dae92263d7be76490a51ea7027f79ab5fcd6118
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62509799"
---
# <a name="configure-system-center-operations-manager-scom-to-monitor-analytics-platform-system"></a>System Center Operations Manager (SCOM) 분석 플랫폼 시스템 모니터링 구성
Analytics Platform System에 대 한 System Center Operations Manager (SCOM) 관리 팩을 구성 하려면 다음이 단계를 따릅니다. 관리 팩은 SCOM에서 Analytics Platform System을 모니터링 해야 합니다.  
  
## <a name="BeforeBegin"></a>시작하기 전 주의 사항  
**필수 구성 요소**  
  
System Center Operations Manager 2007 R2는 설치 하 고 실행 해야 합니다.  
  
관리 팩을 설치 하 고 구성 해야 합니다. 참조 [SCOM 관리 팩을 설치 &#40;Analytics Platform System&#41; ](install-the-scom-management-packs.md) 하 고 [PDW 용 SCOM 관리 팩 가져오기 &#40;분석 플랫폼 시스템&#41;](import-the-scom-management-pack-for-pdw.md).  
  
## <a name="ConfigureRunAsProfile"></a>System Center에서 실행 프로필 구성  
System Center를 구성 하려면 다음 단계를 수행 해야 합니다.  
  
-   에 대 한 실행 계정 만들기를 **AP Watcher** 도메인 사용자 매핑합니다는 **Microsoft APS Watcher 계정.**  
  
-   에 대 한 실행 계정 만들기를 **monitoring_user** AP 사용자 매핑합니다 합니다 **Microsoft APS 작업 계정**합니다.  
  
작업을 수행 하는 방법에 대 한 자세한 지침은 다음과 같습니다.  
  
1.  만들기는 **AP Watcher** 실행 계정을 사용 하 여 **Windows** 계정에 대 한 유형 합니다 **AP Watcher** 도메인 사용자입니다.  
  
    1.  로 이동 합니다 **관리** 창에서 마우스 오른쪽 단추로 클릭 **실행 구성** -> **계정** 선택 하 고 **실행 계정 만들기...**  
  
        ![ConfigureScomCreateRunAsAccount](./media/configure-scom-to-monitor-analytics-platform-system/ConfigureScomCreateRunAsAccount.png "ConfigureScomCreateRunAsAccount")  
  
    2.  합니다 **실행 계정 만들기 마법사** 대화 상자가 열립니다. 에 **소개** 페이지에서 클릭 **다음**합니다.  
  
    3.  에 **일반 속성** 페이지에서 **Windows** 에서 **실행 계정 유형** "AP Watcher"으로 지정 합니다 **표시 이름**합니다.  
  
        ![CreateRunAsAccountWizardGeneralProperties](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties.png "CreateRunAsAccountWizardGeneralProperties")  
  
    4.  에 **자격 증명** 페이지에서 ![CreateRunAsAccountWizardCredentials](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials.png "CreateRunAsAccountWizardCredentials")  
  
    5.  에 **배포 보안** 페이지에서 **떨어집니다** 클릭 합니다 **만들기** 완료 단추.  
  
        ![CreateRunAsAccountWizardDistributionSecurity](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardDistributionSecurity.png "CreateRunAsAccountWizardDistributionSecurity")  
  
        1.  사용 하려는 경우는 **보다 안전한** 수동으로 자격 증명을 배포할 컴퓨터를 지정 해야 하는 옵션입니다. 이렇게 하려면 실행 계정을 만든 후,를 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다.  
  
        2.  로 이동 합니다 **배포** 탭 및 **추가** 필요한 컴퓨터입니다.  
  
            ![RunAsAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/RunAsAccountProperties.png "RunAsAccountProperties")  
  
2.  설정 합니다 **Microsoft APS Watcher 계정** 프로필을 사용 하 여 **AP Watcher** 실행 계정.  
  
    1.  이동할 **관리** -> **구성으로 실행** -> **프로필**합니다.  
  
        ![AdministrationRunAsConfigurationProfiles](./media/configure-scom-to-monitor-analytics-platform-system/AdministrationRunAsConfigurationProfiles.png "AdministrationRunAsConfigurationProfiles")  
  
    2.  마우스 오른쪽 단추로 클릭 **Microsoft APS Watcher 계정** 목록에서 선택 **속성**합니다.  
  
        ![MicrosoftApsWatcherAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/MicrosoftApsWatcherAccountProperties.png "MicrosoftApsWatcherAccountProperties")  
  
    3.  합니다 **실행 프로필 마법사** 대화 상자가 열립니다. 건너뛰기는 **소개** 를 클릭 하 여 페이지 **다음**합니다.  
  
    4.  에 **일반 속성** 페이지에서 클릭 **다음**합니다.  
  
    5.  에 **실행 계정** 페이지에서 클릭을 **추가...**  단추 및 이전에 만든 선택 **AP Watcher** 실행 계정.  
  
        ![RunAsProfileWizardAdd](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd.png "RunAsProfileWizardAdd")  
  
    6.  클릭 **저장할** 프로필 할당을 완료 합니다.  
  
3.  APS 어플라이언스 검색 완료 될 때까지 기다립니다.  
  
    1.  로 이동 합니다 **모니터링** 연 창 합니다 **SQL Server 어플라이언스** -> **Microsoft Analytics Platform System**  ->   **어플라이언스** 상태 보기입니다.  
  
        ![SqlServerApplianceMicrosoftApsAppliances](./media/configure-scom-to-monitor-analytics-platform-system/SqlServerApplianceMicrosoftApsAppliances.png "SqlServerApplianceMicrosoftApsAppliances")  
  
    2.  어플라이언스 목록에 나타날 때까지 기다립니다. 어플라이언스의 이름을 레지스트리에 지정 된와 동일 해야 합니다. 검색이 완료 되 면 나열 되지만 모니터링 되지 않는 모든 어플라이언스에 표시 됩니다. 모니터링을 사용 하려면 다음 단계를 수행 합니다.  
  
    > [!NOTE]  
    > 초기 어플라이언스 검색 완료를 대기 하는 동안 동시에 다음 단계를 완료할 수 있습니다.  
  
4.  다른 새 실행 계정을 AP 상태 데이터 검색에 대 한 쿼리를 만듭니다.  
  
    1.  1 단계에서 설명한 대로 새 실행 계정 만들기를 시작 합니다.  
  
    2.  에 **일반 속성** 페이지에서 **기본 인증** 계정 유형입니다.  
  
        ![CreateRunAsAccountWizardGeneralProperties2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties2.png "CreateRunAsAccountWizardGeneralProperties2")  
  
    3.  에 **자격 증명** 페이지, AP 상태 Dmv에 액세스 하려면 유효한 자격 증명을 제공 합니다.  
  
        ![CreateRunAsAccountWizardCredentials2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials2.png "CreateRunAsAccountWizardCredentials2")  
  
5.  구성 된 **Microsoft APS 작업 계정** AP 인스턴스에 대 한 새로 만든된 실행 계정을 사용 하는 프로필입니다.  
  
    1.  로 이동 합니다 **Microsoft APS 작업 계정** 2 단계에 설명 된 대로 속성입니다.  
  
    2.  에 **실행 계정** 페이지에서 **추가...**  및 
    3.  새로 만든된 실행 계정을 선택 합니다.  
  
        ![RunAsProfileWizardAdd2](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd2.png "RunAsProfileWizardAdd2")  
  
## <a name="next-step"></a>다음 단계  
관리 팩을 구성 했으므로 어플라이언스 모니터링을 시작할 준비가 되었습니다. 자세한 내용은 [System Center Operations Manager를 사용 하 여 어플라이언스 모니터링 &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)합니다.  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
