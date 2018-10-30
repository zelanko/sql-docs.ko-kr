---
title: 보고서 작성기 설치 | Microsoft Docs
ms.date: 09/22/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.assetid: 6b2291bb-1d20-4d08-81cb-a16dd8e01faf
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ebcef28bd5b785bb72059986e39aae34d8af7921
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50021327"
---
# <a name="install-report-builder"></a>Install Report Builder
  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]는 사용자나 관리자가 컴퓨터에 설치하는 독립 실행형 앱입니다. 이 응용 프로그램은 Microsoft 다운로드 센터, [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 보고서 서버 또는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]와 통합된 SharePoint 사이트에서 설치할 수 있습니다.  
  
 일반적으로 관리자는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 설치 및 구성하고 웹 포털에서 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]를 다운로드할 권한을 부여하며 보고서 서버에 저장된 보고서, 보고서 파트 및 공유 데이터 집합에 대한 폴더와 사용 권한을 관리합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 관리에 대한 자세한 내용은 [Reporting Services 보고서 서버&#40;기본 모드&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)를 참조하세요.  
  
## <a name="install-includessrbnoversionincludesssrbnoversionmd-from--a--web-portal-or-sharepoint-library"></a>웹 포털 또는 SharePoint 라이브러리에서 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 설치 
  
 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 웹 포털 또는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 와 통합된 SharePoint 사이트에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 시작할 수 있습니다. 자세한 내용은 [보고서 작성기 시작](../../reporting-services/report-builder/start-report-builder.md)을 참조하세요.  
  
### <a name="sharepoint-site-integrated-with-includessrsnoversionincludesssrsnoversion-mdmd"></a>다음과 통합된 SharePoint 사이트 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]와 통합된 SharePoint 사이트에서 **새 문서** 메뉴에 **보고서 작성기 보고서**, **보고서 작성기 모델**및 **보고서 데이터 원본**옵션이 나열되지 않은 경우 해당 내용 유형을 SharePoint 라이브러리에 추가해야 합니다. 자세한 내용은 [SharePoint 라이브러리에 Reporting Services 콘텐츠 형식 추가](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)를 참조하세요.  
 
## <a name="install-includessrbnoversionincludesssrbnoversionmd-with-system-center-configuration-manager"></a>System Center Configuration Manager를 사용하여 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 설치 
  
 관리자는 System Center Configuration Manager와 같은 소프트웨어를 사용하여 프로그램을 컴퓨터에 배포할 수도 있습니다. 특정 소프트웨어를 사용하여 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]를 설치하는 방법을 확인하려면 해당 소프트웨어의 설명서를 참조하십시오. 자세한 내용은 [System Center Configuration Manager 사이트](https://www.microsoft.com/en-us/cloud-platform/system-center-configuration-manager)를 참조하세요.  
  
> [!IMPORTANT]  
>  Windows Vista 및 Windows 7의 경우 보안 기능으로 인해 명령줄 작업을 실행하려면 높은 권한이 필요합니다. 따라서 명령줄을 실행할 경우 사용 권한을 요청하는 메시지가 표시되므로 자동 설치를 수행할 수 없습니다. 자동 설치를 수행하려면 관리자 권한으로 명령줄을 실행해야 합니다.  
  
## <a name="system-requirements"></a>시스템 요구 사항
  
 Microsoft 다운로드 센터에서 **보고서 작성기 다운로드 페이지** 의 [시스템 요구 사항](https://go.microsoft.com/fwlink/?LinkID=734968) 절을 참조하십시오.
  
##  <a name="download"></a> 다운로드 사이트에서 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 설치  
  
1.  [Microsoft 다운로드 센의 보고서 작성기 페이지](https://go.microsoft.com/fwlink/?LinkID=734968) 에서 **다운로드**를 클릭합니다.  
  
2.  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 에서 다운로드를 마치면  **실행**을 클릭합니다.  
  
     그러면 SQL Server [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 마법사가 실행됩니다.  
  
3.  사용권 계약에 동의한 후 **다음**을 클릭합니다.  
  
4.  **기본 대상 서버** 페이지에서 필요 시 대상 보고서 서버의 URL을 제공합니다(기본값과 다른 경우). **다음**을 클릭합니다.  
  
    > [!NOTE]  
    >  보고서 서버에 연결되었을 때 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 로 작업하려면 이 단계에서 서버 URL을 입력하는 것이 편리합니다. [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]의 **옵션** 대화 상자에서도 이 작업을 수행할 수 있습니다.  
  
5.  **설치**를 클릭하여 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]의 설치를 완료합니다.  
  
## <a name="to-install-includessrbnoversionincludesssrbnoversionmd-from-a-share"></a>공유에서 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]를 설치하려면  
  
1.  로컬 컴퓨터에 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]를 설치하기 위해 실행하는 ReportBuilder3.msi의 위치는 관리자에게 문의하세요.  
  
2.  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]의 Windows Installer 패키지(MSI)인 ReportBuilder3.msi를 찾아서 클릭합니다.  
  
     그러면 SQL Server [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 마법사가 실행됩니다.  
  
3.  [다운로드 사이트에서 보고서 작성기를 설치하려면](#download)의 나머지 단계를 완료합니다.  
  
## <a name="to-install-includessrbnoversionincludesssrbnoversionmd-from-the-command-line"></a>명령줄에서 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 설치 

 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 의 명령줄 설치를 수행하고 인수를 제공하여 설치를 사용자 지정할 수도 있습니다. 표준 MSI 내장 매개 변수 외에도 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]에서 제공하는 사용자 지정 매개 변수인 RBINSTALLDIR 및 REPORTSERVERURL을 사용할 수 있습니다. RBINSTALLDIR은 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]의 루트 설치 폴더를 지정합니다. REPORTSERVERURL은 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 에서 서버에 보고서를 저장하기 위해 사용하는 기본 보고서 서버를 지정합니다.  
  
 사용자 인터페이스의 상호 작용이 필요 없는 완전 자동 설치를 수행하려면 **/quiet** 옵션을 지정합니다. 기본적으로 quiet 옵션 플래그를 사용하면 설치 오류가 표시되지 않습니다. 따라서 quite 옵션을 사용할 때는 로깅을 지정하는 **/l** 옵션을 함께 사용하는 것이 좋습니다.   
  
1.  [Microsoft 다운로드 센의 보고서 작성기 페이지](https://go.microsoft.com/fwlink/?LinkID=734968)에서 **다운로드**를 클릭합니다.  
  
2.  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 에서 다운로드를 마치면  **저장**을 클릭합니다.  
  
3.  **시작** 메뉴에서 **실행**을 클릭합니다.  
  
4.  **열기** 상자에 **cmd.** 를 입력합니다.  
  
5.  명령 프롬프트 창에서 ReportBuilder3.msi를 저장한 폴더로 이동합니다.  
  
6.  다음 형식으로 명령을 입력합니다.  
  
     `msiexec/i ReportBuilder3.msi /option [value] [/option [value]]`  
  
     [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 설치 시에만 적용 가능한 두 가지 옵션은 BINSTALLDIR 및 REPORTSERVERURL입니다. 이러한 인수는 명령줄에 포함하지 않아도 됩니다. 기본 명령은 다음과 같습니다.  
  
     `msiexec /i ReportBuilder3_x86.msi /quiet`  
  
7.  명령을 실행하려면 Enter 키를 누릅니다.  
  
## <a name="set-includessrbnoversionincludesssrbnoversionmd-defaults"></a>[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 를 기본값으로 설정  
  
-   [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]를 설치한 다음 몇 가지 기본 옵션을 설정할 수 있습니다. **파일** > **옵션**을 클릭합니다.  
  
     기본 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 웹 포털 또는 SharePoint 사이트를 설정하는 것이 가장 유용합니다. 자세한 내용은 [Set default options for Report Builder](../../reporting-services/report-builder/set-default-options-for-report-builder.md)을 참조하세요.  
  
-   **보고서 작성기** 를 클릭합니다.  
  
     기존 서버 목록에 보고서 서버가 표시되지 않는 경우 **보고서 열기** 대화 상자를 닫은 다음 **하단에 있는** 연결 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 을 클릭하여 서버에 연결합니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 작성기 시작](../../reporting-services/report-builder/start-report-builder.md)   
 [보고서 작성기 제거](../../reporting-services/install-windows/uninstall-report-builder.md)  
  
  
