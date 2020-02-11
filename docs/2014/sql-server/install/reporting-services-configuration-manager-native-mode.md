---
title: Reporting Services 구성 관리자(기본 모드) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Configuration tool
- configuration options [Reporting Services]
- report servers [Reporting Services], configuring
- components [Reporting Services], Reporting Services Configuration tool
ms.assetid: 379eab68-7f13-4997-8d64-38810240756e
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: e7b5e46b90702bf39bf2902eed3e5a6c609757e0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952489"
---
# <a name="reporting-services-configuration-manager-native-mode"></a>Reporting Services 구성 관리자(기본 모드)
  
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드 설치를 구성할 수 있습니다. 파일 전용 설치 옵션을 사용하여 보고서 서버를 설치한 경우, 이를 사용할 수 있으려면 먼저 구성 관리자를 사용해서 서버를 구성해야 합니다. 기본 구성 설치 옵션을 사용하여 보고서 서버를 설치한 경우에는 구성 관리자를 사용하여 설치 중에 지정된 설정을 확인하거나 수정할 수 있습니다. 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하면 로컬 또는 원격 보고서 서버 인스턴스를 구성할 수 있습니다.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드입니다.  
  
> [!NOTE]  
>  
  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 릴리스부터는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자가 SharePoint 모드 보고서 서버를 관리하도록 디자인되지 않았습니다. SharePoint 모드는 SharePoint 중앙 관리 및 PowerShell 스크립트를 사용하여 관리 및 구성됩니다. 자세한 내용은 sharepoint [모드 설치 &#40;sharepoint 2010 및 sharepoint 2013&#41;Reporting Services ](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)를 참조 하세요.  
  
 **이 섹션의 설명:**  
  
 [보고서 서버 서비스 계정 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)  
 서비스 계정 및 암호를 수정하는 방법에 대한 권장 사항과 단계를 제공합니다.  
  
 [보고서 서버 URL 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
 보고서 서버 웹 서비스 및 보고서 관리자에 액세스하는 데 사용되는 URL을 구성하는 방법을 설명합니다.  
  
 [보고서 서버 데이터베이스 만들기&#40;SSRS 구성 관리자&#41;](../../../2014/sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)  
 서버 메타데이터 및 개체를 저장하는 데 필요한 보고서 서버 데이터베이스를 만드는 방법을 설명합니다.  
  
 [보고서 서버 데이터베이스 연결 구성&#40;SSRS 구성 관리자&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
 보고서 서버에서 보고서 서버 데이터베이스에 연결하는 데 사용하는 연결 문자열을 수정하는 방법을 설명합니다.  
  
 [무인 실행 계정 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)  
 보고서를 무인 모드로 처리하는 데 필요한 사용자 계정을 구성하는 방법을 설명합니다.  
  
 [SSRS Configuration Manager &#40;전자 메일 배달에 대 한 보고서 서버 구성&#41;](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)  
 전자 메일 보고서 배포를 지원하도록 보고서 서버를 구성하는 방법을 설명합니다.  
  
 [기본 모드 보고서 서버 확장 배포 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)  
 공유 보고서 서버 데이터베이스를 사용하도록 여러 보고서 서버 인스턴스를 구성하는 방법을 설명합니다.  
  
 [암호화 키 구성 및 관리&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
 중요한 데이터 저장에 사용되는 암호화 키를 사용 및 관리하는 방법을 설명합니다.  
  
 [Reporting Services 기본 모드 보고서 서버 관리](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  
 일반 태스크에 대한 단계별 지침을 제공합니다.  
  
 [Reporting Services 구성 관리자 F1 도움말 항목 &#40;SSRS 기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구의 페이지에 대한 도움말 항목을 제공합니다.  
  
 **항목 내용**  
  
-   [Reporting Services 구성 관리자 사용할 시나리오](#bkmk_scenarios)  
  
-   [요구 사항](#bkmk_requirements)  
  
-   [Reporting Services 구성 관리자를 시작 하려면](#bkmk_start_configuration_manager)  
  
##  <a name="bkmk_scenarios"></a>Reporting Services 구성 관리자 사용할 시나리오  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 수행할 수 있는 태스크는 다음과 같습니다.  
  
-   보고서 서버 서비스 계정 구성. 이 계정은 설치 중에 처음 구성되지만 암호를 업데이트하거나 다른 계정을 사용하려는 경우 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 수정할 수 있습니다.  
  
-   URL 만들기 및 구성. 보고서 서버와 보고서 관리자는 URL을 통해 액세스되는 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 애플리케이션입니다. 보고서 서버 URL을 사용하면 보고서 서버의 SOAP 엔드포인트에 액세스할 수 있으며 보고서 관리자 URL을 사용하면 보고서 관리자를 열 수 있습니다. 각 애플리케이션에 대해 URL을 한 개 또는 여러 개 구성할 수 있습니다.  
  
-   보고서 서버 데이터베이스 만들기 및 구성. 보고서 서버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 내부 스토리지로 사용하는 상태 비저장 서버입니다. 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 보고서 서버 데이터베이스에 대한 연결을 만들고 구성할 수 있습니다. 사용하려는 내용이 이미 포함되어 있는 기존 보고서 서버 데이터베이스를 선택할 수도 있습니다.  
  
-   기본 모드 스케일 아웃 배포를 구성합니다. 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 여러 개의 보고서 서버 인스턴스가 한 개의 공유 보고서 서버 데이터베이스를 사용하도록 허용하는 배포 토폴로지를 지원합니다. 보고서 서버 스케일 아웃 배포를 구현하려면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 각 보고서 서버를 공유 보고서 서버 데이터베이스에 연결해야 합니다.  
  
-   저장된 연결 문자열과 자격 증명을 암호화하는 데 사용되는 대칭 키 백업, 복원 또는 교체. 서비스 계정을 변경하거나 보고서 서버 데이터베이스를 다른 컴퓨터로 이동하는 경우 대칭 키 백업이 있어야 합니다.  
  
-   무인 실행 계정을 구성합니다. 이 계정은 예약된 작업이 수행되는 동안이나 사용자 자격 증명을 사용할 수 없는 경우 원격 연결에 사용됩니다.  
  
-   보고서 서버 전자 메일 구성 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에는 SMTP(Simple Mail Transport Protocol)를 통해 보고서 또는 보고서 처리 알림을 전자 사서함에 배달하는 메일 배달 확장 프로그램이 포함되어 있습니다. 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 네트워크에서 전자 메일 배달에 사용할 SMTP 서버나 게이트웨이를 지정할 수 있습니다.  
  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 보고서 서버 내용을 관리하거나 추가 기능을 활성화하거나 서버에 대한 액세스 권한을 부여할 수는 없습니다. 전체 배포를 사용 하려면를 사용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 하 여 추가 기능을 활성화 하거나 기본값을 수정 하 고 보고서 관리자 서버에 대 한 사용자 액세스 권한을 부여 해야 합니다.  
  
##  <a name="bkmk_requirements"></a>사항이  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자는 버전별로 다릅니다. 이 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 와 함께 설치되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 이전 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 구성할 수 없습니다. 같은 컴퓨터에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 의 이전 버전과 최신 버전이 함께 실행되고 있는 경우 각 버전과 함께 제공되는 Reporting Services 구성 관리자를 사용하여 각 인스턴스를 구성해야 합니다.  
  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하려면 다음 사항을 충족해야 합니다.  
  
-   구성하려는 보고서 서버를 호스팅하는 컴퓨터에 대한 로컬 시스템 관리자 권한이 있어야 합니다. 원격 컴퓨터를 구성하는 경우에는 해당 컴퓨터에 대한 로컬 시스템 관리자 권한도 있어야 합니다.  
  
-   보고서 서버 데이터베이스를 호스팅하는 데 사용되는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 에 데이터베이스를 만들 수 있는 사용 권한이 있어야 합니다.  
  
-   구성하는 보고서 서버에 WMI(Windows Management Instrumentation) 서비스가 활성화되어 실행되고 있어야 합니다. 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자는 보고서 서버 WMI 공급자를 사용하여 로컬 및 원격 보고서 서버에 연결합니다. 원격 보고서 서버를 구성하는 경우에는 컴퓨터에서 원격 WMI 액세스를 허용해야 합니다. 자세한 내용은 [원격 관리를 위한 보고서 서버 구성](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)을 참조하세요.  
  
-   원격 보고서 서버 인스턴스에 연결하여 구성하기 전에 원격 WMI(Windows Management Instrumentation) 호출이 Windows 방화벽을 통과하도록 설정해야 합니다. 자세한 내용은 [온라인 설명서의](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md) 원격 관리를 위한 보고서 서버 구성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 참조하세요.  
  
 이 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
##  <a name="bkmk_start_configuration_manager"></a>Reporting Services 구성 관리자를 시작 하려면  
  
#### <a name="to-start-reporting-services-configuration"></a>Reporting Services 구성을 시작하려면  
  
1.  사용자의 Microsoft Windows 버전에 적합한 방식으로 다음 단계를 사용합니다.  
  
    -   Windows 시작 화면에서 **Reporting** 을 입력하고 검색 결과에서 **Reporting Services 구성 관리자** 를 선택합니다.  
  
    -   
  **시작**을 클릭하고 **모든 프로그램**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **구성 도구**를 차례로 가리킵니다.  
  
         
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이전 버전의 보고서 서버 인스턴스를 구성하려면 해당 버전의 프로그램 폴더를 엽니다. 예를 들어 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 대신 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] 을 가리켜서 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 서버 구성 요소에 대한 구성 도구를 엽니다.  
  
         
  **Reporting Services 구성 관리자**를 클릭합니다.  
  
2.  구성할 보고서 서버 인스턴스를 선택할 수 있도록 **Reporting Services 구성 연결** 대화 상자가 나타납니다. **연결**을 클릭합니다.  
  
3.  
  **서버 이름**에 보고서 서버 인스턴스가 설치된 컴퓨터의 이름을 지정합니다. 기본적으로 로컬 컴퓨터의 이름이 표시되지만 원격 컴퓨터에 설치된 보고서 서버에 연결하려는 경우 원격 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름을 입력할 수도 있습니다.  
  
4.  원격 컴퓨터를 지정하는 경우 **찾기** 를 클릭하여 연결을 설정합니다.  
  
5.  
  **Report Server stance**에서 구성할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스를 선택합니다. 목록에 이 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보고서 서버 인스턴스만 표시됩니다. 이전 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]는 구성할 수 없습니다.  
  
6.  **연결**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 관리자&#40;SSRS 기본 모드&#41;](../../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Reporting Services 도구](../../reporting-services/tools/reporting-services-tools.md)   
 [SSRS Configuration Manager &#40;보고서 서버 데이터베이스 연결 구성&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [SQL Server 구성 관리자](../../relational-databases/sql-server-configuration-manager.md)   
 [보고서 서버 구성 및 관리&#40;SSRS 기본 모드&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
  
  
