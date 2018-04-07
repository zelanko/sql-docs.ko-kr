---
title: 분석 플랫폼 시스템을 모니터링 하는 SCOM 구성
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4dba9b50-1447-45fc-b219-b9fc99d47d8d
caps.latest.revision: 10
ms.openlocfilehash: 53fc0bce73f2fd30553e2a834122e86cdb0a65fc
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="configure-scom-to-monitor-analytics-platform-system"></a>분석 플랫폼 시스템을 모니터링 하는 SCOM 구성
분석 플랫폼 시스템에 대 한 System Center Operations Manager (SCOM) 관리 팩을 구성 하려면 다음이 단계를 수행 합니다. 관리 팩은 SCOM에서 분석 플랫폼 시스템을 모니터링 해야 합니다.  
  
## <a name="BeforeBegin"></a>시작하기 전 주의 사항  
**필수 구성 요소**  
  
System Center Operations Manager 2007 r 2는 설치 되어 실행 중 이어야 합니다.  
  
관리 팩을 설치 하 고 구성 해야 합니다. 참조 [SCOM 관리 팩을 설치 &#40;분석 플랫폼 시스템&#41; ](install-the-scom-management-packs.md) 및 [PDW에 대 한 SCOM 관리 팩을 가져올 &#40;분석 플랫폼 시스템&#41;](import-the-scom-management-pack-for-pdw.md)합니다.  
  
## <a name="ConfigureRunAsProfile"></a>시스템 센터에서 실행 프로필을 구성 합니다.  
System Center 구성 하려면 다음 단계를 수행 해야 합니다.  
  
-   에 대 한 실행 계정 만들기는 **APS 감시자** 도메인 사용자 매핑합니다는 **Microsoft APS 감시자 계정.**  
  
-   에 대 한 실행 계정 만들기는 **monitoring_user** APS 사용자 매핑합니다는 **Microsoft APS 작업 계정**합니다.  
  
이 수행할 수 있는 방법에 대 한 자세한 지침은 다음과 같습니다.  
  
1.  만들기는 **APS 감시자** 인 실행 계정을 **Windows** 계정에 대 한 유형은 **APS 감시자** 도메인 사용자입니다.  
  
    1.  로 이동는 **관리** 창에서 마우스 오른쪽 단추로 클릭 **실행 구성** -> **계정** 선택 **실행 계정을 만드는 중...**  
  
        ![ConfigureScomCreateRunAsAccount](./media/configure-scom-to-monitor-analytics-platform-system/ConfigureScomCreateRunAsAccount.png "ConfigureScomCreateRunAsAccount")  
  
    2.  **실행 계정 만들기 마법사** 대화 상자가 열립니다. 에 **소개** 페이지 **다음**합니다.  
  
    3.  에 **일반 속성** 페이지 선택 **Windows** 에서 **실행 계정 유형** "APS 감시자"으로 지정 된 **표시 이름**합니다.  
  
        ![CreateRunAsAccountWizardGeneralProperties](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties.png "CreateRunAsAccountWizardGeneralProperties")  
  
    4.  에 **자격 증명** 페이지 "APS 감시자" 도메인 사용자 자격 증명을 제공 합니다.  
  
        ![CreateRunAsAccountWizardCredentials](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials.png "CreateRunAsAccountWizardCredentials")  
  
    5.  에 **배포 보안** 페이지 선택 **덜 안전한** 클릭는 **만들기** 끝나기를 단추입니다.  
  
        ![CreateRunAsAccountWizardDistributionSecurity](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardDistributionSecurity.png "CreateRunAsAccountWizardDistributionSecurity")  
  
        1.  사용 하려는 경우는 **더 안전한** 배포 되는 자격 증명에 컴퓨터를 수동으로 지정 해야 하는 옵션입니다. 실행 계정을 만든 후이 작업을 수행 하려면에서 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다.  
  
        2.  로 이동 된 **배포** 탭 및 **추가** 필요한 컴퓨터입니다.  
  
            ![RunAsAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/RunAsAccountProperties.png "RunAsAccountProperties")  
  
2.  설정의 **Microsoft APS 감시자 계정** 사용할 프로필을 **APS 감시자** 계정으로 실행 합니다.  
  
    1.  로 이동 **관리** -> **실행 구성** -> **프로필**합니다.  
  
        ![AdministrationRunAsConfigurationProfiles](./media/configure-scom-to-monitor-analytics-platform-system/AdministrationRunAsConfigurationProfiles.png "AdministrationRunAsConfigurationProfiles")  
  
    2.  마우스 오른쪽 단추로 클릭 **Microsoft APS 감시자 계정** 선택 목록에서 **속성**합니다.  
  
        ![MicrosoftApsWatcherAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/MicrosoftApsWatcherAccountProperties.png "MicrosoftApsWatcherAccountProperties")  
  
    3.  **실행 프로필 마법사** 대화 상자가 열립니다. 건너뛰기는 **소개** 페이지를 클릭 하 여 **다음**합니다.  
  
    4.  에 **일반 속성** 페이지 **다음**합니다.  
  
    5.  에 **실행 계정** 페이지는 **추가 중...** 단추 및 이전에 만든 선택 **APS 감시자** 계정으로 실행 합니다.  
  
        ![RunAsProfileWizardAdd](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd.png "RunAsProfileWizardAdd")  
  
    6.  클릭 **저장** 프로필 할당을 완료 합니다.  
  
3.  APS 어플라이언스 검색 완료 될 때까지 대기 합니다.  
  
    1.  로 이동는 **모니터링** 창 및 open의 **SQL Server 어플라이언스** -> **Microsoft 분석 플랫폼 시스템**  ->   **어플라이언스** 상태 보기입니다.  
  
        ![SqlServerApplianceMicrosoftApsAppliances](./media/configure-scom-to-monitor-analytics-platform-system/SqlServerApplianceMicrosoftApsAppliances.png "SqlServerApplianceMicrosoftApsAppliances")  
  
    2.  어플라이언스에 목록에 표시 될 때까지 기다립니다. 장치 이름을 레지스트리에 지정 된 1과 같은 해야 합니다.  
  
    검색을 완료 한 후 나열 되어 있지만 모니터링 되지 않는 모든 기기 표시 되어야 합니다. 작업을 모니터링 하기 위한 다음 단계를 수행 합니다.  
  
    > [!NOTE]  
    > 초기 어플라이언스 검색을 완료 하를 대기 하는 동안 동시에 다음 단계를 완료할 수 있습니다.  
  
4.  새 계정으로 실행 하려면 다른 계정을 APS 상태 데이터 검색에 대 한 쿼리를 만듭니다.  
  
    1.  1 단계에 설명 된 대로 새 계정으로 실행 계정 만들기를 시작 합니다.  
  
    2.  에 **일반 속성** 페이지 선택 **기본 인증** 계정 유형입니다.  
  
        ![CreateRunAsAccountWizardGeneralProperties2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties2.png "CreateRunAsAccountWizardGeneralProperties2")  
  
    3.  에 **자격 증명** 공급 APS 상태 Dmv를 액세스 하려면 유효한 자격 증명 페이지입니다.  
  
        ![CreateRunAsAccountWizardCredentials2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials2.png "CreateRunAsAccountWizardCredentials2")  
  
5.  구성에서 **Microsoft APS 작업 계정** APS 인스턴스에 대 한 새로 만든된 실행 계정을 사용 하도록 합니다.  
  
    1.  로 이동 된 **Microsoft APS 작업 계정** 2 단계에서 설명한 대로 속성입니다.  
  
    2.  에 **실행 계정** 페이지 **추가 중...** 새로 만든된 계정으로 실행 계정을 선택 합니다.  
  
        ![RunAsProfileWizardAdd2](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd2.png "RunAsProfileWizardAdd2")  
  
## <a name="next-step"></a>다음 단계  
관리 팩을 구성 했으므로 어플라이언스에 모니터링을 시작할 준비가 된 것입니다. 자세한 내용은 참조 [System Center Operations Manager를 사용 하 여 어플라이언스에 모니터링 &#40;분석 플랫폼 시스템&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)합니다.  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
