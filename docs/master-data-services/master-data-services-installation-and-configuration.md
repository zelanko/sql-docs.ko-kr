---
title: 설치 및 구성
description: Windows Server 2012 R2 컴퓨터에 MDS(Master Data Services)를 설치 하 고, MDS 데이터베이스 및 웹 사이트를 구성 하 고, 샘플 모델 및 데이터를 배포 하는 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: quickstart
ms.assetid: f6cd850f-b01b-491f-972c-f966b9fe4190
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: f9a0a43bb913437e4818c46fc81c0794019639c7
ms.sourcegitcommit: 7d6eb09588ff3477cf39a8fd507d537a603bc60d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/16/2020
ms.locfileid: "84796284"
---
# <a name="master-data-services-installation-and-configuration"></a>Master Data Services 설치 및 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  이 문서에서는 Windows Server 2012 R2 컴퓨터에 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 를 설치하고, MDS 데이터베이스 및 웹 사이트를 설정하고, 샘플 모델 및 데이터를 배포하는 방법을 설명합니다. MDS([!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] )를 사용하면 조직에서 신뢰할 수 있는 버전의 데이터를 관리할 수 있습니다.   
  
> [!NOTE] 
> 이제 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]를 지원하는 디벨로퍼 버전을 사용할 때 Windows 10 컴퓨터에 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]를 설치할 수 있습니다. 
>>다양한 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] 버전에 대한 운영 체제 지원에 대한 자세한 내용은 [SQL Server 2016 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)을 참조하세요. 

[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]에서 데이터를 구성하는 방법에 대한 개요는 [MDS(Master Data Services) 개요](../master-data-services/master-data-services-overview-mds.md)를 참조하세요.     
  
 의 새로운 기능에 대 한 자세한 내용은 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [MDS(MASTER DATA SERVICES) &#40;MDS&#41;의 새로운 ](../master-data-services/what-s-new-in-master-data-services-mds.md)기능을 참조 하세요.  
 
[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]를 알아보는 데 유용한 동영상 및 기타 학습 리소스의 링크는 [Master Data Services에 대해 알아보기](../master-data-services/learn-sql-server-master-data-services.md)를 참조하세요. 
  
> **다운로드**  
> -   [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]를 다운로드하려면  **[평가 센터](https://www.microsoft.com/evalcenter/evaluate-sql-server-2017-ctp/)** 로 이동하세요.  
> -   Azure 계정이 있으세요?  계정이 있는 경우 **[여기](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)** 로 이동하여 SQL Server가 이미 설치된 가상 머신을 실행해 보세요.  
> 
> **MDS 웹 사이트를 만들 수 없는 경우**
> >이 Microsoft 지원 문서에서 이 문제를 해결하는 방법에 대한 지침을 확인하세요.
> [SQL Server 2016에서 낮은 권한 계정을 통해 MDS 웹 사이트를 만들 수 없는 경우](https://aka.ms/mdssupport) 

## <a name="internet-explorer-and-silverlight"></a>Internet Explorer 및 Silverlight
- Windows Server 2012 컴퓨터에 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]를 설치하는 경우 웹 애플리케이션 사이트에 대한 스크립팅을 허용하도록 Internet Explorer 보안 강화를 구성해야 할 수 있습니다. 그렇게 하지 않으면 서버 컴퓨터에서 해당 사이트로의 이동에 실패합니다.
- 웹 애플리케이션에서 작업하려면 클라이언트 컴퓨터에 Silverlight 5가 설치되어 있어야 합니다. 필요한 Silverlight 버전이 설치되어 있지 않으면 Silverlight이 필요한 웹 애플리케이션 영역으로 이동할 때 Silverlight를 설치하라는 메시지가 표시됩니다. Silverlight 5는 **[여기](https://www.microsoft.com/silverlight/)** 에서 설치할 수 있습니다.

## <a name="ssmdsshort_md-on-an-azure-virtual-machine"></a>Azure 가상 머신의 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]
기본적으로,가 이미 설치 된 Azure 가상 컴퓨터를 실행 하면 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 도 설치 됩니다. 

다음 단계는 IIS(인터넷 정보 서비스)를 설치하는 것입니다. [IIS 설치 및 구성](#InstallIIS) 섹션을 참조하세요. 

[!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] 설치를 변경하는 데 관심이 있는 경우 기본 위치인 `<drive>`:\SQLServer_13.0_Full에서 setup.exe 파일은 찾을 수 있습니다.
  
## <a name="installing-master-data-services"></a><a name="InstallMDS"></a> Master Data Services 설치  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치 프로그램의 설치 마법사 또는 명령 프롬프트를 사용하여 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]를 설치합니다.  
  
 **[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치 프로그램을 사용하여 Windows Server 2012 R2 컴퓨터에 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]를 설치하려면**  
  
1.  Setup.exe를 두 번 클릭하고 설치 마법사의 단계를 따릅니다.  
  
2.  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 기능 선택 **페이지의** 공유 기능 **에서**를 선택합니다.  
  
     [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], 어셈블리, Windows PowerShell 스냅인, 웹 애플리케이션과 서비스의 폴더 및 파일이 설치됩니다.  
  
     ![mds_SQLServer2016Setup_FeatureSelection](../master-data-services/media/mds-sqlserver2016setup-featureselection.png "mds_SQLServer2016Setup_FeatureSelection")  
  
3.  설치 마법사를 완료합니다.  

## <a name="installing-and-configuring-iis"></a><a name="InstallIIS"></a> IIS 설치 및 구성
  
1.  [!INCLUDE[winblue_server_2](../includes/winblue-server-2-md.md)]에서 **데스크톱** 의 작업 표시줄에 있는 **서버 관리자**아이콘을 클릭합니다.  
  
     ![Windows Server 2012 작업 표시줄의 서버 관리자 아이콘](../master-data-services/media/mds-windowsservertaskbar-servermanagericon.png "Windows Server 2012 작업 표시줄의 서버 관리자 아이콘")  
  
5.  **서버 관리자**에서 **관리** 메뉴에 있는 **역할 및 기능 추가** 를 클릭합니다.  
   
     ![서버 관리의 역할 및 기능 추가 메뉴 명령](../master-data-services/media/mds-servermanagerdashboard-addrolesfeaturesmenu.png "서버 관리의 역할 및 기능 추가 메뉴 명령")  
  
6.  **역할 및 기능 추가 마법사** 의 **설치 유형**페이지에서 기본값(**역할 기반 또는 기능 기반 설치**)을 적용하고 **다음**을 클릭합니다.  
  
7.  **서버 풀에서 서버 선택**을 클릭한 다음 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]를 설치한 서버를 클릭합니다.  
  
     ![mds_AddRolesFeaturesWizard_ServerSelectionPage](../master-data-services/media/mds-addrolesfeatureswizard-serverselectionpage.png) 
  
8. **서버 역할** 페이지에서 **웹 서버**를 클릭한 후 **다음**을 클릭합니다. 

   ![mds_AddRolesFeaturesWizard_ServerRolesPage](../master-data-services/media/mds-addrolesfeatureswizard-serverrolespage.png)
   
9. **기능** 페이지에서 다음 기능이 선택되었는지 확인한 후 **다음**을 클릭합니다. 이러한 기능은 [!INCLUDE[winblue_server_2_md](../includes/winblue-server-2-md.md)]의 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]에 필요합니다.
  
    |기능|기능|  
    |--------------|--------------|  
    |![mds_AddRolesFeaturesWizard_FeaturesPage](../master-data-services/media/mds-addrolesfeatureswizard-featurespage.png)|![mds_AddRolesFeaturesWizard_FeaturesPage_WindowsProcActive](../master-data-services/media/mds-addrolesfeatureswizard-featurespage-windowsprocactive.png)|  

10. 왼쪽 창에서 **웹 서버 역할(IIS)** 을 클릭한 후 **역할 서비스**를 클릭합니다.
11. **역할 서비스** 페이지에서 다음 서비스가 선택되었는지 확인한 후 **다음**을 클릭합니다. 이러한 서비스는 [!INCLUDE[winblue_server_2](../includes/winblue-server-2-md.md)]의 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에 필요합니다.

    > [!WARNING]  
    >  WebDAV 게시 역할 서비스를 설치하지 마세요. WebDAV 게시는 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]와 호환되지 않습니다.  
  
     |역할 서비스|역할 서비스|  
    |-----------------------------|-----------------------------|  
    |![mds_AddRolesFeaturesWizard_RoleServicesPage](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage.png)|![mds_AddRolesFeaturesWizard_RoleServicesPage_PerformSecurity](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage-performsecurity.png)|  
    |![mds_AddRolesFeaturesWizard_RoleServicesPage_AppDevsection](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage-appdevsection.png)|![mds_AddRolesFeaturesWizard_RoleServicesPage_ManageToolssection](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage-managetoolssection.png)|  
    |||  
  
     다른 운영 체제에서 필요한 기능 및 역할 서비스 목록은 [웹 애플리케이션 요구 사항&#40;Master Data Services&#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md)을 참조하세요.   
  
 설치 프로그램을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 설치하는 방법에 대한 자세한 내용은 [설치 마법사에서 SQL Server 2016 설치&#40;설치 프로그램&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)를 참조하세요.  
  
 명령 프롬프트를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 를 설치하는 방법에 대한 자세한 내용은 [명령 프롬프트에서 SQL Server 2016 설치](../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)를 참조하세요. 명령 프롬프트를 사용하는 경우 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 는 기능 매개 변수로 사용할 수 있습니다.  
  
 사전 설치 작업에 대한 추가 정보 링크가 있는 간단한 설명은 [Master Data Services 설치](../master-data-services/install-windows/install-master-data-services.md)를 참조하세요.  
  
##  <a name="setting-up-the-database-and-website"></a><a name="SetUpWeb"></a> 데이터베이스 및 웹 사이트 설정  
 **을 사용 하 여 데이터베이스 및 웹 사이트를 설정 하려면[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]**  

 
> [!WARNING]
>  [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] Configuration Manager를 실행하기 전에 [IIS를 설치](#InstallIIS)해야 합니다. 그렇지 않으면 Configuration Manager에 인터넷 정보 서비스 오류가 표시되고 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 웹 애플리케이션을 만들 수 없게 됩니다.  
> 
> **브라우저 요구 사항**
> >[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 웹 애플리케이션은 IE(Internet Explorer) 9 이상에서만 작동합니다. IE 8 이하 버전, Microsoft Edge 및 Chrome은 지원되지 않습니다.    
  
1.  [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]를 시작하고 왼쪽 창에서 **데이터베이스 구성** 을 클릭합니다.  
  
2.  **데이터베이스 만들기**를 클릭한 다음 **데이터베이스 만들기 마법사** 에서 **다음**을 클릭합니다.  
  
3.  **데이터베이스 서버** 페이지에서 SQL Server 인스턴스를 지정 합니다. 

    >  [!INCLUDE[sqlv15](../includes/sssqlv15-md.md)]Managed Instance SQL Server에 대 한 지원을 추가 합니다. **SQL Server 인스턴스** 값을 Azure SQL Database 관리 되는 인스턴스의 호스트로 설정 합니다. 예들 들어 `xxxxxx.xxxxxx.database.windows.net`입니다.

4. **인증 유형을** 선택한 다음 **연결 테스트** 를 클릭 하 여 선택한 인증 유형에 대 한 자격 증명을 사용 하 여 데이터베이스에 연결할 수 있는지 확인 합니다. **다음**을 클릭합니다.

    >의 경우 [!INCLUDE[sqlv15](../includes/sssqlv15-md.md)] 관리 되는 인스턴스에 Azure SQL Database 연결 하려면 다음 인증 유형 중 하나를 사용 합니다.
    >
    >- Azure Active Directory 통합 인증: **현재 사용자 – Active Directory 통합**
    >- SQL Server 인증: **SQL Server 계정**.
    >
    >Azure SQL Database 관리 되는 인스턴스에서 사용자는 고정 서버 역할의 멤버 여야 합니다 `sysadmin` .

    > [!NOTE]  
    >  인증 유형으로 **현재 사용자 통합 보안** 을 선택 하는 경우 **사용자 이름** 상자는 읽기 전용 이며 컴퓨터에 로그온 한 Windows 사용자 계정의 이름을 표시 합니다. Azure Virtual Machine(VM)에서 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)](을)를 실행하는 경우 **사용자 이름** 상자에 VM 이름과 VM의 로컬 관리자 계정에 대한 사용자 이름이 표시됩니다. 

    ![mds_2016ConfigManager_CreateDatabaseWizard_ServerPage](../master-data-services/media/mds-2016configmanager-createdatabasewizard-serverpage.png)  
  
4.  **데이터베이스 이름** 필드에 이름을 입력합니다. 필요에 따라 Windows 데이터 정렬을 선택하려면 **SQL Server 기본 데이터 정렬** 확인란의 선택을 취소하고 **대/소문자 구분**과 같은 사용 가능한 옵션 중 하나 이상을 클릭합니다. **다음**을 클릭합니다.

    ![mds_2016ConfigManager_CreateDatabaseWizard_DatabasePage](../master-data-services/media/mds-2016configmanager-createdatabasewizard-databasepage.png)  
  
     Windows 데이터 정렬에 대한 자세한 내용은 [Windows 데이터 정렬 이름(Transact-SQL)](../t-sql/statements/windows-collation-name-transact-sql.md)을 참조하세요.  
  
5.  **사용자 이름** 필드에서 Master Data Services의 기본 슈퍼 사용자로 설정할 사용자의 Windows 계정을 지정합니다. 슈퍼 사용자는 모든 기능 영역에 액세스할 수 있으며 모든 모델을 추가, 삭제 및 업데이트할 수 있습니다.  

    ![mds_2016ConfigManager_CreateDatabaseWizard_AdminPage](../master-data-services/media/mds-2016configmanager-createdatabasewizard-adminpage.png)  
  
6.  **다음** 을 클릭하여 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에 대한 설정 요약을 본 후에 다시 **다음** 을 클릭하여 데이터베이스를 만듭니다. **진행 후 마침** 페이지가 표시됩니다.

7. 데이터베이스가 생성되고 구성되면 **마침**을 클릭합니다.  
  
     **데이터베이스 만들기 마법사**의 설정에 대한 자세한 내용은 [데이터베이스 만들기 마법사&#40;Master Data Services 구성 관리자&#41;](../master-data-services/create-database-wizard-master-data-services-configuration-manager.md)를 참조하세요.  
  
7.  [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]의 **데이터베이스 구성** 페이지에서 **데이터베이스 선택**을 클릭합니다.  
  
8.  **연결**을 클릭하고 7단계에서 만든 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스를 선택한 후 **확인**을 클릭합니다. 

    ![mds_2016ConfigManager_SelectDatabaseButton_ConnectToDatabaseDialog](../master-data-services/media/mds-2016configmanager-selectdatabasebutton-connecttodatabasedialog.png)  
  
     데이터베이스 설정을 마쳤습니다. 이제 **데이터베이스 구성** 페이지에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에 대해 연결된 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]인스턴스, 만든 데이터베이스 및 현재 데이터베이스 버전이 표시됩니다.  

    ![mds_2016ConfigManager_DatabaseConfig_Completed](../master-data-services/media/mds-2016configmanager-databaseconfig-completed.png)   
  
9. [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]의 왼쪽 창에서 **웹 구성** 을 클릭합니다.  
  
10. **웹 사이트** 목록 상자에서 **기본 웹 사이트**를 클릭한 다음 **만들기** 를 클릭하여 웹 애플리케이션을 만듭니다.  
  
    > [!NOTE]  
    >  **기본 웹 사이트**를 선택할 경우 웹 애플리케이션을 만들어야 합니다. 목록 상자에서 **새 웹 사이트 만들기** 를 선택하면 애플리케이션이 자동으로 만들어집니다.  

     ![mds_2016ConfigManager_WebConfig](../master-data-services/media/mds-2016configmanager-webconfig.png)  
  
11. **애플리케이션 풀** 섹션에서 다음 중 하나를 수행합니다.  
  
    -   데이터베이스 **관리자 계정**에 대해 5단계에서 입력한 것과 동일한 사용자 이름을 입력하고 암호를 입력한 다음 **확인**을 클릭합니다.  
  
         **디스크나**  
  
    -   다른 사용자 이름을 입력하고 암호를 입력한 다음 확인을 클릭합니다.  
  
         데이터베이스와 웹 애플리케이션을 만들 때 동일한 계정을 사용해야 하는 것은 아닙니다.  

        ![mds_2016ConfigManager_WebConfig_CreateWebApplication](../master-data-services/media/mds-2016configmanager-webconfig-createwebapplication.png)   
  
     **웹 애플리케이션 만들기** 대화 상자에 대한 자세한 내용은 [웹 애플리케이션 만들기 대화 상자&#40;Master Data Services 구성 관리자&#41;](../master-data-services/create-web-application-dialog-box-master-data-services-configuration-manager.md)를 참조하세요.  
  
12. **웹 구성** 페이지의 **웹 애플리케이션** 상자에서 만든 애플리케이션을 클릭한 다음 **데이터베이스에 애플리케이션 연결** 섹션에서 **선택**을 클릭합니다.  
  
13. **연결**을 클릭하고 웹 애플리케이션에 연결할 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스를 선택한 다음 **확인**을 클릭합니다.  
  
     웹 사이트 설정을 마쳤습니다. 이제 **웹 구성** 페이지에 선택한 웹 사이트, 만든 웹 애플리케이션, 애플리케이션과 연결된 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스가 표시됩니다.  

     ![mds_2016ConfigManager_WebConfig_Completed](../master-data-services/media/mds-2016configmanager-webconfig-completed.png)  
 
     
15. **적용**을 클릭합니다. **구성 완료** 메시지 상자가 표시됩니다. 메시지 상자에서 **확인**을 클릭하고 웹 애플리케이션을 시작합니다. 웹 사이트 주소는 https://*server name* / *웹 응용 프로그램*/입니다. 


![mds_2016ConfigurationComplete_MessageBox](../master-data-services/media/mds-2016configurationcomplete-messagebox.png) 
  
     For more information about the settings on the Web Configuration page, see [Web Configuration Page &#40;Master Data Services Configuration Manager&#41;](../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)  
  
 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 를 사용하여 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스와 연결된 웹 애플리케이션 및 서비스에 대한 다른 설정을 지정할 수도 있습니다. 예를 들어 데이터를 로드하는 빈도나 유효성 검사 메일을 전송하는 빈도를 지정할 수 있습니다. 자세한 내용은 [시스템 설정&#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md)을 참조하세요.  
  
##  <a name="deploying-sample-models-and-data"></a><a name="deploySample"></a> 샘플 모델 및 데이터 배포  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에는 다음 세 가지 샘플 모델 패키지가 포함되어 있습니다.   이러한 샘플 모델은 데이터를 포함합니다. **샘플 모델 패키지의 기본 위치는 %programfiles%\Microsoft SQL Server\140\Master Data Services\Samples\Packages입니다.**
  
-   chartofaccounts_en.pkg  
  
-   customer_en.pkg  
  
-   product_en.pkg  
  
 MDSModelDeploy 도구를 사용하여 패키지를 배포합니다. MDSModelDeploy 도구의 기본 위치는 *드라이브*\Program Files\Microsoft SQL Server\ 140\Master Data Services\Configuration입니다.  
  
 이 도구를 실행하기 위한 필수 조건에 대한 자세한 내용은 [MDSModelDeploy를 사용하여 모델 배포 패키지 배포](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)를 참조하세요.  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]의 새로운 기능을 지원하기 위한 데이터 업데이트에 대한 자세한 내용은 [SQL Server 샘플: 모델 배포 패키지(MDS)](../master-data-services/sql-server-samples-model-deployment-packages-mds.md)를 참조하세요.  
  
 **샘플 모델을 배포하려면**  
  
1.  샘플 모델 패키지를 *드라이브*\Program Files\Microsoft SQL Server\140\Master Data Services\Configuration에 복사합니다.  
  
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
    > 샘플 모델의 메타데이터 정보에 대해 자세히 알아보려면 "c:\Program Files\Microsoft SQL Server\140\Master Data Services\Configuration"에서 추가 정보 파일을 참조하십시오.
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
  
     ![제품 샘플 모델을 배포 하기 위한 명령줄](../master-data-services/media/mds-commandprompt-deployingsamplemodel-product.png "제품 샘플 모델을 배포 하기 위한 명령줄")  
  
4.  샘플 모델을 보려면 다음을 수행합니다.  
  
    1.  설정한 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 웹 사이트로 이동합니다. [데이터베이스 및 웹 사이트 설정](#SetUpWeb) 섹션을 참조하세요.  
  
         웹 사이트 주소는 https://*server name* / *웹 응용 프로그램*/입니다.  
  
    2.  **모델** 목록 상자에서 모델을 선택하고 **탐색기**를 클릭합니다.  
  
         ![MDS 웹 사이트, 홈 페이지.](../master-data-services/media/mds-mdswebsite-homepage-selectsamplemodel.png "MDS 웹 사이트, 홈 페이지.")  
  
## <a name="next-step"></a>다음 단계  
 데이터에 대한 새 모델 및 엔터티를 만듭니다. [모델 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md) 및 [엔터티 만들기&#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)를 참조하세요.  
  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 모델 및 엔터티를 사용하여 데이터 구조를 작성하는 방법에 대한 개요는 [Master Data Services 개요&#40;MDS&#41;](../master-data-services/master-data-services-overview-mds.md)를 참조하세요.  
    
## <a name="see-also"></a>참고 항목  
 [MDS(Master Data Services) 데이터베이스](../master-data-services/master-data-services-database.md)   
 [웹 응용 프로그램 마스터 데이터 관리자](../master-data-services/master-data-manager-web-application.md)   
 [데이터베이스 구성 페이지 &#40;Master Data Services 구성 관리자&#41;](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
 [MDS&#40;Master Data Services&#41;의 새로운 기능](../master-data-services/what-s-new-in-master-data-services-mds.md)  
  
  
