---
title: "Master Data Services 설치 및 구성 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: f6cd850f-b01b-491f-972c-f966b9fe4190
caps.latest.revision: 44
author: sabotta
ms.author: carlasab
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 25e5dc869efd2417c47b72c70ede7ba19ab54b46
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="master-data-services-installation-and-configuration"></a>Master Data Services 설치 및 구성
  이 문서에서는 Windows Server 2012 R2 컴퓨터에 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 를 설치하고, MDS 데이터베이스 및 웹 사이트를 설정하고, 샘플 모델 및 데이터를 배포하는 방법을 설명합니다. MDS([!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] )를 사용하면 조직에서 신뢰할 수 있는 버전의 데이터를 관리할 수 있습니다.   
  
> [!NOTE] 
> 설치할 수 있습니다 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 이제 Developer edition을 사용 하는 경우 컴퓨터에서 지 원하는 Windows 10에서 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]합니다. 
>>에 대 한 지원 운영 체제에 대 한 자세한 내용은 다른 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] 버전에서는 참조 [Hardware and Software Requirements for Installing SQL Server 2016](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)합니다. 

[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]에서 데이터를 구성하는 방법에 대한 개요는 [MDS(Master Data Services) 개요](../master-data-services/master-data-services-overview-mds.md)를 참조하세요.     
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]의 새로운 기능에 대한 자세한 내용은 [MDS&#40;Master Data Services&#41;의 새로운 기능](../master-data-services/what-s-new-in-master-data-services-mds.md)을 참조하세요.  
 
[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]를 알아보는 데 유용한 동영상 및 기타 학습 리소스의 링크는 [Master Data Services에 대해 알아보기](../master-data-services/learn-sql-server-master-data-services.md)를 참조하세요. 
  
> **다운로드**  
>-   [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]를 다운로드하려면  **[평가 센터](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2017-ctp/)**로 이동하세요.  
>-   Azure 계정이 있으세요?  이동 하 여  **[여기](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)**  에 이미 설치 된 SQL Server 가상 컴퓨터를 실행 합니다.  
 
> **MDS 웹 사이트를 만들 수 없는 경우**
>>이 Microsoft 지원 문서에서 이 문제를 해결하는 방법에 대한 지침을 확인하세요.
[SQL Server 2016에서 낮은 권한 계정을 통해 MDS 웹 사이트를 만들 수 없는 경우](https://aka.ms/mdssupport) 

## <a name="internet-explorer-and-silverlight"></a>Silverlight 및 Internet Explorer
- 설치 하는 경우 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] Windows Server 2012 컴퓨터 Internet Explorer 보안 강화 웹 응용 프로그램 사이트에 대 한 스크립팅을 허용 하도록 구성 해야 할 수 있습니다. 그렇지 않으면 서버 컴퓨터에 사이트를 찾아 실패 합니다.
- 웹 응용 프로그램에서 작동 하려면 클라이언트 컴퓨터에 Silverlight 5는 설치 합니다. 필요한 버전의 Silverlight가에서 필요로 하는 웹 응용 프로그램의 영역으로 이동 하는 경우 설치 하 라는 메시지가 표시 됩니다. Silverlight 5를 설치할 수  **[여기](https://www.microsoft.com/silverlight/)**합니다.

## <a name="includessmdsshortmdincludesssmdsshort-mdmd-on-an-azure-virtual-machine"></a>[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]Azure 가상 컴퓨터
기본적으로 된 Azure 가상 컴퓨터를 회전 하면 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] 이미 설치 되어 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 도 설치 됩니다. 

다음 단계 인터넷 정보 서비스 (IIS)를 설치 하는 것입니다. 참조는 [IIS 구성 및 설치](#InstallIIS) 섹션. 

설치를 변경 하는 데 관심이 있는지 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], 기본 위치에 setup.exe 파일을 찾을 수 `<drive>`: \SQLServer_13.0_Full 합니다.
  
## <a name="InstallMDS"></a>Master Data Services 설치  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치 프로그램의 설치 마법사 또는 명령 프롬프트를 사용하여 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]를 설치합니다.  
  
 **[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치 프로그램을 사용하여 Windows Server 2012 R2 컴퓨터에 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]를 설치하려면**  
  
1.  Setup.exe를 두 번 클릭하고 설치 마법사의 단계를 따릅니다.  
  
2.  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 기능 선택 **페이지의** 공유 기능 **에서**를 선택합니다.  
  
     [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], 어셈블리, Windows PowerShell 스냅인, 웹 응용 프로그램과 서비스의 폴더 및 파일이 설치됩니다.  
  
     ![mds_SQLServer2016Setup_FeatureSelection](../master-data-services/media/mds-sqlserver2016setup-featureselection.png "mds_SQLServer2016Setup_FeatureSelection")  
  
3.  설치 마법사를 완료합니다.  

## <a name="InstallIIS"></a>IIS 설치 및 구성
  
1.  [!INCLUDE[winblue_server_2](../includes/winblue-server-2-md.md)]에서 **데스크톱** 의 작업 표시줄에 있는 **서버 관리자**아이콘을 클릭합니다.  
  
     ![서버 관리자에 대 한 Windows Server 2012 작업 표시줄에서 아이콘](../master-data-services/media/mds-windowsservertaskbar-servermanagericon.png "서버 관리자에 대 한 Windows Server 2012 작업 표시줄에서 아이콘")  
  
5.  **서버 관리자**에서 **관리** 메뉴에 있는 **역할 및 기능 추가** 를 클릭합니다.  
   
     ![관리 서버, 역할 및 추가 기능 메뉴 명령에서](../master-data-services/media/mds-servermanagerdashboard-addrolesfeaturesmenu.png "서버에서 관리, 역할 및 추가 기능 메뉴 명령")  
  
6.  **역할 및 기능 추가 마법사** 의 **설치 유형**페이지에서 기본값(**역할 기반 또는 기능 기반 설치**)을 적용하고 **다음**을 클릭합니다.  
  
7.  **서버 풀에서 서버 선택**을 클릭한 다음 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]를 설치한 서버를 클릭합니다.  
  
     ![mds_AddRolesFeaturesWizard_ServerSelectionPage](../master-data-services/media/mds-addrolesfeatureswizard-serverselectionpage.png) 
  
8. 에 **서버 역할** 페이지 **웹 서버** 클릭 하 고 **다음**합니다. 

   ![mds_AddRolesFeaturesWizard_ServerRolesPage](../master-data-services/media/mds-addrolesfeatureswizard-serverrolespage.png)
   
9. 에 **기능** 페이지에서 다음과 같은 기능을 선택 하 고 클릭 한 다음 확인 **다음**합니다. 이러한 기능에 대 한 증명이 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 에 [!INCLUDE[winblue_server_2_md](../includes/winblue-server-2-md.md)]합니다.
  
    |기능|기능|  
    |--------------|--------------|  
    |![mds_AddRolesFeaturesWizard_FeaturesPage](../master-data-services/media/mds-addrolesfeatureswizard-featurespage.png)|![mds_AddRolesFeaturesWizard_FeaturesPage_WindowsProcActive](../master-data-services/media/mds-addrolesfeatureswizard-featurespage-windowsprocactive.png)|  

10. 왼쪽 창에서 클릭 **웹 서버 역할 (IIS)** 클릭 하 고 **역할 서비스**합니다.
11. 에 **역할 서비스** 페이지에서 다음 서비스를 선택 하 고 클릭 한 다음 확인 **다음**합니다. 이러한 서비스에 필요한는 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 에 [!INCLUDE[winblue_server_2](../includes/winblue-server-2-md.md)]합니다.

    > [!WARNING]  
    >  WebDAV 게시 역할 서비스를 설치하지 마세요. WebDAV 게시는 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]와 호환되지 않습니다.  
  
     |역할 서비스|역할 서비스|  
    |-----------------------------|-----------------------------|  
    |![mds_AddRolesFeaturesWizard_RoleServicesPage](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage.png)|![mds_AddRolesFeaturesWizard_RoleServicesPage_PerformSecurity](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage-performsecurity.png)|  
    |![mds_AddRolesFeaturesWizard_RoleServicesPage_AppDevsection](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage-appdevsection.png)|![mds_AddRolesFeaturesWizard_RoleServicesPage_ManageToolssection](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage-managetoolssection.png)|  
    |||  
  
     필요한 기능 및 다른 운영 체제에서 역할 서비스 목록에 대 한 참조 [웹 응용 프로그램 요구 사항 &#40; Master Data services&#41; ](../master-data-services/install-windows/web-application-requirements-master-data-services.md) .   
  
 설치 프로그램을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 설치하는 방법에 대한 자세한 내용은 [설치 마법사에서 SQL Server 2016 설치&#40;설치 프로그램&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)를 참조하세요.  
  
 명령 프롬프트를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 설치하는 방법에 대한 자세한 내용은 [명령 프롬프트에서 SQL Server 2016 설치](../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)를 참조하세요. 명령 프롬프트를 사용하는 경우 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 는 기능 매개 변수로 사용할 수 있습니다.  
  
 사전 설치 작업에 대한 추가 정보 링크가 있는 간단한 설명은 [Master Data Services 설치](../master-data-services/install-windows/install-master-data-services.md)를 참조하세요.  
  
##  <a name="SetUpWeb"></a> 데이터베이스 및 웹 사이트 설정  
 **[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]를 사용하여 데이터베이스 및 웹 사이트를 설정하려면**  

 
> [!WARNING]  
    >  수행 해야 [IIS 설치](#InstallIIS) 를 실행 하기 전에 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] Configuration Manager입니다. 그렇지 않으면 Configuration Manager에서 정보 서비스 오류를 표시 하 고 만들 수 있습니다는 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 웹 응용 프로그램입니다.  
    
> **브라우저 요구 사항**
>>[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 웹 응용 프로그램 작동만에서 Internet Explorer (IE) 9 이상. IE 8 및 이전 버전, Microsoft Edge 및 Chrome은 지원 되지 않습니다.    
  
1.  [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]를 시작하고 왼쪽 창에서 **데이터베이스 구성** 을 클릭합니다.  
  
2.  **데이터베이스 만들기**를 클릭한 다음 **데이터베이스 만들기 마법사** 에서 **다음**을 클릭합니다.  
  
3.  **데이터베이스 서버** 페이지에서 **인증 유형** 을 선택하고 **연결 테스트** 를 클릭하여 선택한 인증 유형에 대한 자격 증명으로 데이터베이스에 연결할 수 있는지 확인합니다. **다음**을 클릭합니다.
  
    > [!NOTE]  
    >  **현재 사용자 – 통합 보안** 을 인증 유형으로 선택할 경우 **사용자 이름** 상자는 읽기 전용이며 컴퓨터에 로그온된 Windows 사용자 계정의 이름이 표시됩니다. 실행 하는 경우 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 는 Azure 가상 컴퓨터 (VM)에서는 **사용자 이름** 상자 VM에 VM 이름 및 로컬 관리자 계정에 대 한 사용자 이름을 표시 합니다. 

    ![mds_2016ConfigManager_CreateDatabaseWizard_ServerPage](../master-data-services/media/mds-2016configmanager-createdatabasewizard-serverpage.png)  
  
4.  **데이터베이스 이름** 필드에 이름을 입력합니다. 필요에 따라 Windows 데이터 정렬을 선택 하려면 선택을 취소는 **SQL Server 기본 데이터 정렬** 확인란와 같은 사용 가능한 옵션 중 하나 이상을 클릭 하 고 **대/소문자 구분**합니다. **다음**을 클릭합니다.

    ![mds_2016ConfigManager_CreateDatabaseWizard_DatabasePage](../master-data-services/media/mds-2016configmanager-createdatabasewizard-databasepage.png)  
  
     Windows 데이터 정렬에 대한 자세한 내용은 [Windows 데이터 정렬 이름(Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx)을 참조하세요.  
  
5.  **사용자 이름** 필드에서 Master Data Services의 기본 슈퍼 사용자로 설정할 사용자의 Windows 계정을 지정합니다. 슈퍼 사용자는 모든 기능 영역에 액세스할 수 있으며 모든 모델을 추가, 삭제 및 업데이트할 수 있습니다.  

    ![mds_2016ConfigManager_CreateDatabaseWizard_AdminPage](../master-data-services/media/mds-2016configmanager-createdatabasewizard-adminpage.png)  
  
6.  **다음** 을 클릭하여 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에 대한 설정 요약을 본 후에 다시 **다음** 을 클릭하여 데이터베이스를 만듭니다. **진행 후 마침** 페이지가 나타납니다.

7. 데이터베이스를 만들고 구성 하는 경우 클릭 **마침**합니다.  
  
     **데이터베이스 만들기 마법사**의 설정에 대한 자세한 내용은 [데이터베이스 만들기 마법사&#40;Master Data Services 구성 관리자&#41;](../master-data-services/create-database-wizard-master-data-services-configuration-manager.md)를 참조하세요.  
  
7.  에 **데이터베이스 구성** 페이지에 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], 클릭 **데이터베이스 선택**합니다.  
  
8.  클릭 **연결**, 선택는 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 7 단계에서에서 만든을 클릭 한 다음 데이터베이스 **확인**합니다. 

    ![mds_2016ConfigManager_SelectDatabaseButton_ConnectToDatabaseDialog](../master-data-services/media/mds-2016configmanager-selectdatabasebutton-connecttodatabasedialog.png)  
  
     데이터베이스 설정을 마쳤습니다. 이제 **데이터베이스 구성** 페이지에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에 대해 연결된 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]인스턴스, 만든 데이터베이스 및 현재 데이터베이스 버전이 표시됩니다.  

    ![mds_2016ConfigManager_DatabaseConfig_Completed](../master-data-services/media/mds-2016configmanager-databaseconfig-completed.png)   
  
9. [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]의 왼쪽 창에서 **웹 구성** 을 클릭합니다.  
  
10. **웹 사이트** 목록 상자에서 **기본 웹 사이트**를 클릭한 다음 **만들기** 를 클릭하여 웹 응용 프로그램을 만듭니다.  
  
    > [!NOTE]  
    >  **기본 웹 사이트**를 선택할 경우 웹 응용 프로그램을 만들어야 합니다. 목록 상자에서 **새 웹 사이트 만들기** 를 선택하면 응용 프로그램이 자동으로 만들어집니다.  

     ![mds_2016ConfigManager_WebConfig](../master-data-services/media/mds-2016configmanager-webconfig.png)  
  
11. **응용 프로그램 풀** 섹션에서 다음 중 하나를 수행합니다.  
  
    -   데이터베이스 **관리자 계정**에 대해 5단계에서 입력한 것과 동일한 사용자 이름을 입력하고 암호를 입력한 다음 **확인**을 클릭합니다.  
  
         **또는**  
  
    -   다른 사용자 이름을 입력하고 암호를 입력한 다음 확인을 클릭합니다.  
  
         데이터베이스와 웹 응용 프로그램을 만들 때 동일한 계정을 사용해야 하는 것은 아닙니다.  

        ![mds_2016ConfigManager_WebConfig_CreateWebApplication](../master-data-services/media/mds-2016configmanager-webconfig-createwebapplication.png)   
  
     **웹 응용 프로그램 만들기** 대화 상자에 대한 자세한 내용은 [웹 응용 프로그램 만들기 대화 상자&#40;Master Data Services 구성 관리자&#41;](../master-data-services/create-web-application-dialog-box-master-data-services-configuration-manager.md)를 참조하세요.  
  
12. **웹 구성** 페이지의 **웹 응용 프로그램** 상자에서 만든 응용 프로그램을 클릭한 다음 **데이터베이스에 응용 프로그램 연결** 섹션에서 **선택**을 클릭합니다.  
  
13. **연결**을 클릭하고 웹 응용 프로그램에 연결할 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스를 선택한 다음 **확인**을 클릭합니다.  
  
     웹 사이트 설정을 마쳤습니다. 이제 **웹 구성** 페이지에 선택한 웹 사이트, 만든 웹 응용 프로그램, 응용 프로그램과 연결된 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스가 표시됩니다.  

     ![mds_2016ConfigManager_WebConfig_Completed](../master-data-services/media/mds-2016configmanager-webconfig-completed.png)  
 
     
15. **적용**을 클릭합니다. **구성 완료** 메시지 상자가 표시 됩니다. 클릭 **확인** 메시지 상자 웹 응용 프로그램을 시작 합니다. 웹 사이트 주소는 http://*서버 이름*/*웹 응용 프로그램*/입니다. 


![mds_2016ConfigurationComplete_MessageBox](../master-data-services/media/mds-2016configurationcomplete-messagebox.png) 
  
     For more information about the settings on the Web Configuration page, see [Web Configuration Page &#40;Master Data Services Configuration Manager&#41;](../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)  
  
 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 를 사용하여 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스와 연결된 웹 응용 프로그램 및 서비스에 대한 다른 설정을 지정할 수도 있습니다. 예를 들어 데이터를 로드하는 빈도나 유효성 검사 메일을 전송하는 빈도를 지정할 수 있습니다. 자세한 내용은 [시스템 설정&#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md)을 참조하세요.  
  
##  <a name="deploySample"></a> 샘플 모델 및 데이터 배포  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에는 다음 세 가지 샘플 모델 패키지가 포함되어 있습니다.   이러한 샘플 모델은 데이터를 포함합니다. **예제 모델 패키지에 대 한 기본 위치는 %programfiles%\Microsoft SQL Server\140\Master Data Services\Samples\Packages입니다.**
  
-   chartofaccounts_en.pkg  
  
-   customer_en.pkg  
  
-   product_en.pkg  
  
 MDSModelDeploy 도구를 사용하여 패키지를 배포합니다. MDSModelDeploy 도구에 대 한 기본 위치는 *드라이브*files\microsoft SQL Server\ 140\Master Data services\configuration에 있습니다.  
  
 이 도구를 실행하기 위한 필수 조건에 대한 자세한 내용은 [MDSModelDeploy를 사용하여 모델 배포 패키지 배포](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)를 참조하세요.  
  
 새로운 기능을 지원 하기 위해 데이터에 대 한 업데이트에 대 한 내용은 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], 참조 [SQL Server 샘플: 모델 배포 패키지 (MDS)](../master-data-services/sql-server-samples-model-deployment-packages-mds.md)합니다.  
  
 **샘플 모델을 배포하려면**  
  
1.  예제 모델 패키지를 복사 *드라이브*files\microsoft SQL Server\140\Master Data services\configuration에 있습니다.  
  
2.  관리자: 명령 프롬프트를 열고 다음 명령을 실행하여 MDSModelDeploy.exe로 이동합니다.  
  
    ```  
    cd c:\Program Files\Microsoft SQL Server\140\Master Data Services\Configuration  
    ```  
  
3.  다음 명령을 각각 실행하여 각 샘플 모델을 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 에 배포합니다.  
  
    > [!IMPORTANT]  
    >  아래 예제에서는 `MDS1` 서비스 값을 지정합니다. **웹 사이트를 설정할 때** 기본 웹 사이트 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 를 선택한 경우 이 값을 사용합니다.  [데이터베이스 및 웹 사이트 설정](#SetUpWeb) 섹션을 참조하세요.  
    >   
    >  새 웹 사이트를 만들거나 다른 기존 웹 사이트를 선택한 경우 먼저 다음 명령을 실행하여 올바른 서비스 값을 확인합니다.  
    >   
    >  `MDSModelDeploy listservices`  
    >   
    >  반환되는 값 목록의 첫 번째 서비스 값은 모델을 배포할 때 지정합니다.  
    >
    > [!NOTE]
    > 샘플 모델의 메타 데이터 정보에 대 한 자세한 내용을 보려면, 하기 위해이 위치 "c:\Program Files\Microsoft SQL Server\140\Master Data Services\Configuration"에 사용할 수 있는 추가 정보 파일을 참조 하십시오
    >
   
     **chartofaccounts_en.pkg 샘플 모델을 배포하려면**  
  
    ```  
    MDSModelDeploy deploynew -package chartofaccounts_en.pkg -model ChartofAccounts -service MDS1  
    ```  
  
     **customer_en.pkg 샘플 모델을 배포하려면**  
  
    ```  
    MDSModelDeploy deploynew -package customer_en.pkg -model Customer -service MDS1  
    ```  
  
     **product_en.pkg 샘플 모델을 배포하려면**  
  
    ```  
    MDSModelDeploy deploynew -package product_en.pkg -model Product -service MDS1  
  
    ```  
  
     모델이 성공적으로 배포되면 **MDSModelDeploy 작업이 완료되었습니다.** 라는 메시지가 표시됩니다.  
  
     다음 그림은 product_en.pkg 샘플 모델을 배포하기 위한 명령을 보여 줍니다.  
  
     ![제품 예제 모델을 배포 하기 위한 명령줄](../master-data-services/media/mds-commandprompt-deployingsamplemodel-product.png "제품 샘플 모델을 배포 하기 위한 명령줄")  
  
4.  샘플 모델을 보려면 다음을 수행합니다.  
  
    1.  설정한 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 웹 사이트로 이동합니다. [데이터베이스 및 웹 사이트 설정](#SetUpWeb) 섹션을 참조하세요.  
  
         웹 사이트 주소는 http://*서버 이름*/*웹 응용 프로그램*/입니다.  
  
    2.  **모델** 목록 상자에서 모델을 선택하고 **탐색기**를 클릭합니다.  
  
         ![MDS 웹 사이트, 홈 페이지입니다. ] (../master-data-services/media/mds-mdswebsite-homepage-selectsamplemodel.png "MDS 웹 사이트, 홈 페이지입니다.")  
  
## <a name="next-step"></a>다음 단계  
 데이터에 대한 새 모델 및 엔터티를 만듭니다. [모델 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md) 및 [엔터티 만들기&#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)를 참조하세요.  
  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 모델 및 엔터티를 사용하여 데이터 구조를 작성하는 방법에 대한 개요는 [Master Data Services 개요&#40;MDS&#41;](../master-data-services/master-data-services-overview-mds.md)를 참조하세요.  
  
## <a name="did-this-article-help-you-were-listening"></a>이 문서가 도움이 되었나요? 여러분의 의견을 환영합니다.  
 어떤 정보를 찾고 계세요? 정보를 찾으셨나요? 여러분의 의견은 문서의 내용을 개선하는 데 많은 도움이 됩니다. 의견이 있으면 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Get%20Started%20with%20Master%20Data%20Services)  
  
## <a name="see-also"></a>참고 항목  
 [Master Data Services 데이터베이스](../master-data-services/master-data-services-database.md)   
 [마스터 데이터 관리자 웹 응용 프로그램](../master-data-services/master-data-manager-web-application.md)   
 [데이터베이스 구성 페이지&#40;Master Data Services 구성 관리자&#41;](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
 [MDS&#40;Master Data Services&#41;의 새로운 기능](../master-data-services/what-s-new-in-master-data-services-mds.md)  
  
  

