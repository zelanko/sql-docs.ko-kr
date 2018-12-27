---
title: 로컬 관리에 대해 기본 모드 보고서 서버 구성(SSRS) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- UAC
- installing Reporting Services
- Windows Vista
- Localhost
- windows server 2008
- Vista
ms.assetid: 312c6bb8-b3f7-4142-a55f-c69ee15bbf52
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e997b12f84189ac738c5a93b513d19696beb6c10
ms.sourcegitcommit: c7febcaff4a51a899bc775a86e764ac60aab22eb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/30/2018
ms.locfileid: "52710794"
---
# <a name="configure-a-native-mode-report-server-for-local-administration-ssrs"></a>로컬 관리에 대해 기본 모드 보고서 서버 구성(SSRS)
  보고서 서버 인스턴스를 로컬로 관리하려는 경우 다음 운영 체제 중 하나에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버를 배포하려면 추가 구성 단계가 필요합니다. 이 항목에서는 로컬 관리를 위한 보고서 서버를 구성하는 방법을 설명합니다. 보고서 서버를 설치 또는 구성하지 않은 경우 [설치 마법사에서 SQL Server 설치&#40;설치 프로그램&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md) 및 [Reporting Services 기본 모드 보고서 서버 관리](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)를 참조하세요.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드|  
  
-   [!INCLUDE[winblue_server_2](../../includes/winblue-server-2-md.md)]  
  
-   [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]  
  
-   [!INCLUDE[win8](../../includes/win8-md.md)]  
  
-   [!INCLUDE[win8srv](../../includes/win8srv-md.md)]  
  
-   [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]  
  
-   [!INCLUDE[win7](../../includes/win7-md.md)]  
  
-   [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]  
  
 위에 나와 있는 운영 체제는 권한을 제한하므로 로컬 Administrators 그룹의 멤버는 대부분의 애플리케이션을 표준 사용자 계정을 사용할 때처럼 실행하게 됩니다.  
  
 이를 통해 전반적인 시스템 보안이 개선되지만 Reporting Services에서 로컬 관리자용으로 만드는 미리 정의된 기본 제공 역할 할당은 사용할 수 없습니다.  
  
-   [구성 변경 개요](#bkmk_configuraiton_overview)  
  
-   [로컬 보고서 서버 및 보고서 관리자 관리를 구성하려면](#bkmk_configure_local_server)  
  
-   [로컬 보고서 서버 관리에 대해 SSMS(SQL Server Management Studio)를 구성하려면](#bkmk_configure_ssms)  
  
-   [로컬 보고서 서버에 게시하도록 SSDT(SQL Server Data Tools)를 구성하려면](#bkmk_configure_ssdt)  
  
-   [추가 정보](#bkmk_addiitonal_informaiton)  
  
##  <a name="bkmk_configuraiton_overview"></a> 구성 변경 개요  
 다음 구성 변경은 표준 사용자 권한을 사용하여 보고서 서버 내용 및 작업을 관리할 수 있도록 서버를 구성합니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL을 신뢰할 수 있는 사이트에 추가합니다. 기본적으로 위에 나와 있는 운영 체제에서 실행되는 Internet Explorer는 **보호 모드**로 실행됩니다. 이 모드는 같은 컴퓨터에서 실행되는 높은 수준의 프로세스에 브라우저 요청이 도달하지 못하도록 차단하는 기능입니다. 이 URL을 신뢰할 수 있는 사이트에 추가하면 보고서 서버 애플리케이션에 대한 보호 모드를 해제할 수 있습니다.  
  
-   Internet Explorer에서 **관리자 권한으로 실행** 기능을 사용하지 않고도 보고서 서버 관리자에게 내용 및 작업을 관리하는 권한을 부여하는 역할 할당을 만듭니다. Windows 사용자 계정에 대한 역할 할당을 만들면 Reporting Services에서 만드는 미리 정의된 기본 제공 역할 할당을 대체하는 명시적인 역할 할당을 통해 내용 관리자 및 시스템 관리자 권한으로 보고서 서버에 액세스할 수 있습니다.  
  
##  <a name="bkmk_configure_local_server"></a> 로컬 보고서 서버 및 보고서 관리자 관리를 구성하려면  
 로컬 보고서 서버로 이동하는 동안 다음과 유사한 오류가 나타나면 이 섹션의 구성 단계를 완료합니다.  
  
-   사용자 `'Domain\[user name]`'에게 필요한 권한이 없습니다. 충분한 권한이 부여되고 Windows UAC(사용자 계정 컨트롤) 제한이 해결되었는지 확인하세요.  
  
###  <a name="bkmk_site_settings"></a> 브라우저의 신뢰할 수 있는 사이트 설정  
  
1.  관리자 권한으로 실행 권한을 사용하여 브라우저 창을 엽니다. **시작** 메뉴에서 **모든 프로그램**을 클릭하고 **Internet Explorer**를 마우스 오른쪽 단추로 클릭한 다음 **관리자 권한으로 실행**을 선택합니다.  
  
2.  **허용** 을 클릭하여 계속합니다.  
  
3.  URL 주소에 보고서 관리자 URL을 입력합니다. 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 [보고서 관리자&#40;SSRS 기본 모드&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)를 참조하세요.  
  
4.  **도구**를 클릭합니다.  
  
5.  **인터넷 옵션**을 클릭합니다.  
  
6.  **보안**을 클릭합니다.  
  
7.  **신뢰할 수 있는 사이트**를 클릭합니다.  
  
8.  **사이트**를 클릭합니다.  
  
9. `https://<your-server-name>`를 추가합니다.  
  
10. 기본 사이트에 HTTPS를 사용하지 않으면 **이 영역이 있는 모든 사이트에 대해 서버 확인(https:) 필요** 확인란의 선택을 취소합니다.  
  
11. **추가**를 클릭합니다.  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
###  <a name="bkmk_configure_folder_settings"></a> 보고서 관리자 폴더 설정  
  
1.  보고서 관리자의 홈 페이지에서 **폴더 설정**을 클릭합니다.  
  
2.  폴더 설정 페이지에서 **보안**을 클릭합니다.  
  
3.  **새 역할 할당**을 클릭합니다.  
  
4.  **그룹 또는 사용자 이름** 필드에 `<domain>\<user>`형식으로 Windows 사용자 계정을 입력합니다.  
  
5.  **내용 관리자**를 선택합니다.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
###  <a name="bkmk_configure_site_settings"></a> 보고서 관리자 사이트 설정  
  
1.  관리자 권한을 가진 브라우저를 열고 보고서 관리자 `https://<server name>/reports`로 이동합니다.  
  
2.  홈 페이지의 위쪽 모퉁이에 있는 **사이트 설정** 을 클릭합니다.  
  
    > [!TIP]  
    >  **참고:** **사이트 설정** 옵션이 표시되지 않으면 브라우저를 닫았다가 다시 열고 관리자 권한으로 보고서 관리자로 이동합니다.  
  
3.  **보안**을 클릭합니다.  
  
4.  **새 역할 할당**을 클릭합니다.  
  
5.  **그룹 또는 사용자 이름** 필드에 `<domain>\<user>`형식으로 Windows 사용자 계정을 입력합니다.  
  
6.  **시스템 관리자**를 선택합니다.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  보고서 관리자를 닫습니다.  
  
9. **관리자 권한으로 실행**을 사용하지 않고 Internet Explorer에서 보고서 관리자를 다시 엽니다.  
  
##  <a name="bkmk_configure_ssms"></a> 로컬 보고서 서버 관리에 대해 SSMS(SQL Server Management Studio)를 구성하려면  
 기본적으로 관리자 권한으로 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 시작해야 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에서 사용할 수 있는 모든 보고서 서버 속성에 액세스할 수 있습니다.  
  
 **매번 승격된 권한으로 SSDT를 시작할 필요가 없도록 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]** 를 시작할 필요가 없도록 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 역할 속성 및 역할 할당을 구성하려면  
  
-   **시작** 메뉴에서 **모든 프로그램**, **SQL Server 2014**를 차례로 클릭하고 **[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]** 를 마우스 오른쪽 단추로 클릭한 다음 **관리자 권한으로 실행**을 클릭합니다.  
  
-   로컬 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서버에 연결합니다.  
  
-   **보안** 노드에서 **시스템 역할**을 클릭합니다.  
  
-   **시스템 관리자** 를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
-   **시스템 역할 속성** 페이지에서 **보고서 서버 속성 보기**를 선택합니다. 시스템 관리자 역할의 멤버와 연결할 다른 속성을 모두 선택합니다.  
  
-   **확인**을 클릭합니다.  
  
-   닫기 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]  
  
-   사용자를 "시스템 관리자" 시스템 역할에 추가하려면 이 항목의 앞부분에 나오는 [보고서 관리자 사이트 설정](#bkmk_configure_site_settings) 섹션을 참조하세요.  
  
 이제 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 열 때 **관리자 권한으로 실행** 을 명시적으로 선택하지 않아도 보고서 서버 속성에 액세스할 수 있습니다.  
  
##  <a name="bkmk_configure_ssdt"></a> 로컬 보고서 서버에 게시하도록 SSDT(SQL Server Data Tools)를 구성하려면  
 이 항목의 첫 번째 섹션에 나와 있는 운영 체제 중 하나에 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 를 설치했고 SSDT가 로컬 기본 모드 보고서 서버와 상호 작용하도록 하려는 경우 승격된 권한으로 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 를 열지 않거나 Reporting Services 역할을 구성하지 않으면 권한 오류가 발생합니다. 예를 들어 충분한 권한이 없으면 다음과 유사한 문제가 발생합니다.  
  
-   보고서 항목을 로컬 보고서 서버에 배포하려고 하면 **오류 목록** 창에 다음과 유사한 오류 메시지가 표시됩니다.  
  
    -   ‘Domain\\<user name\>’ 사용자에게 부여된 권한으로는 이 작업을 수행할 수 없습니다.  
  
 **SSDT를 열 때마다 승격된 권한으로 실행하려면**  
  
1.  시작 화면에서 **sql server** 를 입력한 다음 **SQL Server Data Tools**를 마우스 오른쪽 단추로 클릭합니다.  **관리자 권한으로 실행**을 클릭합니다.  
  
2.  **계속**을 클릭합니다.  
  
3.  **프로그램 실행**을 클릭합니다.  
  
 이제 로컬 보고서 서버에 보고서 및 기타 항목을 배포할 수 있습니다.  
  
 **매번 승격된 권한으로 SSDT를 시작할 필요가 없도록 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 역할 할당을 구성하려면**  
  
-   이 항목의 앞부분에 있는 [보고서 관리자 폴더 설정](#bkmk_configure_folder_settings) 및 [보고서 관리자 사이트 설정](#bkmk_configure_site_settings) 섹션을 참조하세요.  
  
##  <a name="bkmk_addiitonal_informaiton"></a> 추가 정보  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 관리와 관련된 일반적인 추가 구성 단계는 보고서 서버 컴퓨터에 대한 액세스를 허용하도록 Windows 방화벽에서 포트 80을 여는 것입니다. 자세한 내용은 [Configure a Firewall for Report Server Access](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services 기본 모드 보고서 서버 관리](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  
  
  
