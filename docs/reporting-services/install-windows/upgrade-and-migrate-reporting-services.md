---
title: "Reporting Services 업그레이드 및 마이그레이션 | Microsoft Docs"
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SSRS, upgrading
- Reporting Services, upgrades
- SQL Server Reporting Services, upgrading
- upgrading Reporting Services
ms.assetid: 851a19a8-07ab-4d42-992f-1986c4c8df55
caps.latest.revision: 92
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 59c7e1cc3c31f77652acb21d375e1294bdc93397
ms.openlocfilehash: b5706abc4f362ee3bd4f042c1e081951dcd9ad1d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/27/2017

---

# <a name="upgrade-and-migrate-reporting-services"></a>Reporting Services 업그레이드 및 마이그레이션

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

  이 항목은 SQL Server Reporting Services에 대 한 업그레이드 및 마이그레이션 옵션의 개요. SQL Server Reporting Services 배포를 업그레이드 하는 데 두 가지 일반적인 방법이 있습니다.  
  
-   **업그레이드:** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소를 현재 설치되어 있는 서버 및 인스턴스에서 업그레이드합니다. 이를 일반적으로 "현재 위치" 업그레이드라고 부릅니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서버의 한 모드에서 다른 모드로의 전체 업그레이드는 지원되지 않습니다. 예를 들어 기본 모드 보고서 서버를 SharePoint 모드 보고서 서버로 업그레이드할 수 없습니다. 보고서 항목을 한 모드에서 다른 모드로 마이그레이션할 수 있습니다. 자세한 내용은 이 문서 뒷부분에 나오는 '기본 모드에서 SharePoint 모드로의 마이그레이션' 섹션을 참조하십시오.  
  
-   **마이그레이션**: 새 SharePoint 환경을 설치 및 구성하고, 보고서 항목 및 리소스를 새 환경에 복사하고, 기존 콘텐츠를 사용하도록 새 환경을 구성합니다. 낮은 수준 형식의 마이그레이션은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터베이스, 구성 파일 및 SharePoint 콘텐츠 데이터베이스(SharePoint 모드를 사용하는 경우)를 복사하는 것입니다.  
    
> **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드 &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드
  
##  <a name="bkmk_known_issues"></a> 알려진 업그레이드 문제 및 최선의 구현 방법  
 업그레이드할 수 있는 버전의 상세 목록은 [Supported Version and Edition Upgrades](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)를 참조하십시오.  
  
> [!TIP]  
>  최신 SQL Server와 함께 문제에 관한 정보를 보려면 다음을 참조 합니다.  
>   
>  -   [SQL Server 2016 릴리스 정보](http://go.microsoft.com/fwlink/?LinkID=398124).  
  
  
##  <a name="bkmk_side_by_side"></a> 함께 설치  
 SQL Server Reporting Services 기본 모드 설치--와 함께 수는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 또는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 기본 모드 배포 합니다.  
  
 SharePoint 모드에서 SQL Server Reporting Services의 병렬 하 여 배포에 지원 되지 않습니다 및 이전 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드 구성 요소입니다.  
  
  
##  <a name="bkmk_inplace_upgrade"></a> 내부 업그레이드  
 업그레이드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에 의해 완료됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 비롯한 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]구성 요소의 일부 또는 전체를 업그레이드할 수 있습니다. 설치 프로그램에서 기존 인스턴스를 감지하고 업그레이드할지 묻는 메시지를 표시합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 명령줄 인수로 지정하거나 설치 마법사에서 지정할 수 있는 업그레이드 옵션을 제공합니다.  
  
 실행 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설정 다음 버전 중 하나에서 업그레이드 하는 옵션을 선택할 수 있습니다 또는 SQL Server Reporting Services의 기존 설치에서 함께 실행 하는 새 인스턴스를 설치할 수 있습니다.  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 자세한 내용은 다음을 참조하세요.  

* [SQL Server 2016으로 업그레이드](../../database-engine/install-windows/upgrade-sql-server.md)
* [설치 마법사를 사용하여 SQL Server 2016으로 업그레이드&#40;설치 프로그램&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)
* [명령 프롬프트에서 SQL Server 2016 설치](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)
  
  
##  <a name="bkmk_upgrade_checklist"></a> 업그레이드 전 검사 목록  
 SQL Server Reporting Services로 업그레이드 하기 전에 다음을 검토 합니다.  
  
-   사용 중인 하드웨어 및 소프트웨어가 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]를 지원하는지 확인하려면 요구 사항을 검토하십시오. 자세한 내용은 [SQL Server 2016 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)을 참조하세요.  
  
-   시스템 구성 검사기 (SCC)를 사용 하 여 SQL Server Reporting Services의 성공적인 설치를 방해할 수 있는 모든 조건에 대 한 보고서 서버 컴퓨터를 검색 합니다. 자세한 내용은 [Check Parameters for the System Configuration Checker](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)을 참조하세요.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 최상의 권장 보안 방법 및 지침을 검토하십시오. 자세한 내용은 [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)을 참조하세요.  
  
-   대칭 키를 백업합니다. 자세한 내용은 [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)을 참조하세요.  
  
-   보고서 서버 데이터베이스 및 구성 파일을 백업합니다. 자세한 내용은 [Backup and Restore Operations for Reporting Services](../../reporting-services/install-windows/backup-and-restore-operations-for-reporting-services.md)을 참조하세요.  
  
-   IIS의 기존 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 가상 디렉터리에 대한 모든 사용자 지정을 백업합니다.  
  
-   잘못된 SSL 인증서를 제거합니다.  여기에는 만료된 인증서 및 Reporting Services를 업그레이드하기 전에 업그레이드하지 않을 인증서가 포함됩니다.  잘못된 인증서가 있으면 업그레이드가 실패하고 Reporting Services 로그 파일에 **Microsoft.ReportingServices.WmiProvider.Exception: 웹 사이트에 SSL(Secure Sockets Layer) 인증서가 구성되어 있지 않습니다.**라는 오류 메시지가 기록됩니다.  
  
 프로덕션 환경을 업그레이드하기 전에 프로덕션 환경과 동일하게 구성된 사전 프로덕션 환경에서 항상 테스트 업그레이드를 실행하십시오.  
  
  
## <a name="overview-of-migration-scenarios"></a>마이그레이션 시나리오 개요  
 지원되는 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 업그레이드하는 경우 일반적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사를 실행하여 보고서 서버 프로그램 파일, 데이터베이스 및 모든 응용 프로그램 데이터를 업그레이드할 수 있습니다.  
  
 그러나 다음과 같은 조건에 해당하는 경우 보고서 서버 설치를 수동으로 **마이그레이션** 해야 합니다.  
  
-   배포에 사용되는 보고서 서버의 유형을 변경하려고 합니다. 예를 들어 기본 모드 보고서 서버를 SharePoint 모드로 업그레이드하거나 변환할 수 없습니다. 자세한 내용은 참조 [기본 모드에서 SharePoint 모드로 마이그레이션 &#40; Ssrs&#41; ](../../reporting-services/install-windows/native-to-sharepoint-migration-ssrs.md).  
  
-   업그레이드 프로세스 중에 보고서 서버가 오프라인 상태가 되는 시간을 최소화해야 합니다. 기존 보고서 서버 설치의 상태를 변경하지 않으면서 콘텐츠 데이터를 새 보고서 서버 인스턴스로 복사하고 설치를 테스트하는 동안 현재 설치는 온라인 상태로 유지됩니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 의 SharePoint 2010 배포를 SharePoint 2013/2016으로 마이그레이션할 수 있습니다. SharePoint 2013/2016은 SharePoint 2010에서의 현재 위치 업그레이드를 지원하지 않습니다. 자세한 내용은 [Reporting Services 설치 마이그레이션&#40;SharePoint 모드&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md)을 참조하세요.  
  
  
##  <a name="bkmk_native_scenarios"></a> 기본 모드 업그레이드 및 마이그레이션 시나리오  
 **업그레이드:** 기본 모드의 현재 위치 업그레이드 프로세스는 이 항목의 앞부분에 나와 있는 지원되는 각 버전에 사용되는 프로세스와 동일합니다. SQL Server 설치 마법사 또는 명령줄 설치를 실행합니다. 설치하면 보고서 서버 데이터베이스가 새 보고서 서버 데이터베이스 스키마로 자동 업그레이드됩니다. 자세한 내용은 이 항목의 [현재 위치 업그레이드](#bkmk_inplace_upgrade) 섹션을 참조하세요.  
  
 업그레이드할 기존 보고서 서버 인스턴스를 선택하면 업그레이드 프로세스가 시작됩니다.  
  
1.  보고서 서버 데이터베이스가 원격 컴퓨터에 있어서 해당 데이터베이스를 업데이트할 수 있는 권한이 없는 경우 원격 보고서 서버 데이터베이스를 업데이트할 수 있는 자격 증명을 지정하라는 메시지가 나타납니다. 이때 **sysadmin** 또는 데이터베이스 업데이트 권한이 있는 자격 증명을 제공해야 합니다.  
  
2.  보고서 서버에 배포된 사용자 지정 확장 프로그램과 같이 업그레이드를 방해하는 조건이나 설정이 있는지 확인한 다음 구성 설정을 읽습니다. 업그레이드가 차단 된 경우 업그레이드가 더 이상 차단 하거나 마이그레이션 새 SQL Server Reporting Services 인스턴스를 설치 하거나 수정 해야 합니다. 자세한 내용은 업그레이드 관리자 설명서를 참조하십시오.  
  
3.  업그레이드를 진행할 수 있는 경우 업그레이드 프로세스를 계속할지 묻는 메시지가 표시됩니다.  
  
4.  설치 프로그램은 SQL Server Reporting Services 프로그램 파일용 새 폴더를 만듭니다. 프로그램 폴더는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치 포함 MSRS13.\< *인스턴스 이름을*> 합니다.  
  
5.  설치는 SQL Server Reporting Services 보고서 서버 프로그램 파일, 구성 도구 및 보고서 서버 기능의 일부인 명령줄 유틸리티에 추가 됩니다.  
  
    1.  이전 버전의 프로그램 파일이 제거됩니다.  
  
    2.  새 버전으로 업그레이드되는 보고서 서버 구성 도구 및 유틸리티에는 기본 모드 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구, 명령줄 유틸리티(예: RS.exe) 및 보고서 작성기가 포함됩니다.  
  
    3.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 와 같은 다른 클라이언트 도구는 별도로 다운로드되며 개별적으로 업그레이드해야 합니다. 자세한 내용은 [SSMS(SQL Server Management Studio) 다운로드](https://msdn.microsoft.com/library/mt238290.aspx)를 참조하세요.
  
    4.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 는 별도의 다운로드입니다. 자세한 내용은 [SQL Server Data Tools in Visual Studio 2015](https://msdn.microsoft.com/mt186501)(Visual Studio 2015의 SQL Server Data Tools)를 참조하세요.  
  
6.  설치 프로그램에는 SQL Server Reporting Services 보고서 서버 서비스에 대 한 서비스 제어 관리자에서 서비스 항목 다시 사용합니다. 이 서비스 항목에는 보고서 서버 Windows 서비스 계정이 포함됩니다.  
  
7.  설치 프로그램이 IIS의 기존 가상 디렉터리 설정에 따라 새 URL을 예약합니다. 설치 프로그램이 IIS의 가상 디렉터리를 제거하지 않을 수 있으므로 업그레이드가 끝나면 이 디렉터리를 수동으로 제거해야 합니다.  
  
8.  설치 프로그램이 구성 파일의 설정을 병합합니다. 현재 설치의 구성 파일을 기준으로 새 항목이 추가됩니다. 사용하지 않는 항목은 제거되지는 않지만 업그레이드가 끝난 후 보고서 서버에서 더 이상 읽어 들이지 않습니다. 업그레이드할 때 IIS에 있는 이전 로그 파일, 사용되지 않는 RSWebApplication.config 파일 또는 가상 설정이 삭제되지 않으며, 이전 버전의 보고서 디자이너, Management Studio 또는 기타 클라이언트 도구도 제거되지 않습니다. 따라서 이러한 파일과 도구가 더 이상 필요하지 않을 경우에는 업그레이드가 끝난 후 제거해야 합니다.  
  
 **마이그레이션:** 는이 항목의 앞부분에 나열 된 지원 되는 버전의 모든에 대해 동일한 단계에 SQL Server Reporting Services로 이전 버전의 기본 모드 설치 마이그레이션. 자세한 내용은 [Reporting Services 설치 마이그레이션&#40;기본 모드&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)을 참조하세요.  
  
  
##  <a name="bkmk_native_scaleout"></a> Reporting Services 기본 모드 확장 배포  
 다음은 둘 이상의 보고서 서버로 확장된 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드 배포를 업그레이드하는 방법을 요약한 내용입니다. 이 과정에는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 배포의 작동 중지 시간이 필요합니다.  
  
1.  보고서 서버 데이터베이스 및 암호화 키를 백업합니다. 자세한 내용은 참조 [Backup and Restore Operations for Reporting Services](../../reporting-services/install-windows/backup-and-restore-operations-for-reporting-services.md) 및 [추가 및 확장 배포 &#40;에 대 한 암호화 키 제거 SSRS 구성 관리자 &#41; ](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md).  
  
2.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여, 확장된 배포에서 모든 보고서 서버를 제거합니다. 자세한 내용은 [기본 모드 보고서 서버 확장 배포 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)을 참조하세요.  
  
3.  SQL Server Reporting services 보고서 서버 중 하나를 업그레이드 합니다.  
  
4.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 보고서 서버를 확장 배포에 다시 추가합니다. 자세한 내용은 [기본 모드 보고서 서버 확장 배포 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)을 참조하세요.  
  
     각 서버에 대해 업그레이드 및 확장 단계를 반복합니다.  
  
##  <a name="bkmk_sharePoint_scenarios"></a> SharePoint 모드 업그레이드 및 마이그레이션 시나리오  
 다음 섹션에서는 업그레이드 하거나 지정 된 버전의 마이그레이션하는 데 필요한 기본 단계 및 문제 설명 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SQL Server Reporting services SharePoint 모드 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드 배포를 업그레이드하는 두 가지 설치 구성 요소가 있습니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 공유 서비스.  
  
    > [!TIP]  
    >  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint cmdlet `Get-SPRSServiceApplicationServers` 를 사용하여, SharePoint 팜에서 현재 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 공유 서비스를 실행 중이어서 업그레이드가 필요한 서버를 확인합니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능(SharePoint 제품용). 자세한 내용은 [SharePoint용 Reporting Services 추가 기능 설치 또는 제거](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)를 참조하세요.  
  
 SharePoint 모드 설치를 마이그레이션하는 방법에 대 한 자세한 내용은 참조 하세요. [마이그레이션 Reporting Services 설치 &#40; SharePoint 모드 &#41; ](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md).  
  
> [!IMPORTANT]  
>  다음 시나리오 중 일부의 경우 업그레이드해야 하는 여러 기술 때문에 SharePoint 환경의 작동 중단이 필요합니다. 작동 중단이 허용되지 않는 상황에서는 내부 업그레이드 대신 마이그레이션을 완료해야 합니다.  
  
### <a name="includesssql14includessssql14-mdmd-to-sql-server-reporting-services"></a>[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]SQL server Reporting Services  
 **시작 환경:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 또는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP1, SharePoint 2010 또는 SharePoint 2013.  
  
 **종료 환경:** SQL Server Reporting Services, SharePoint 2013 또는 SharePoint 2016.   
  
-   **SharePoint 2013/2016:** SharePoint 2013/2016에서 SharePoint 2013으로 현재 위치 업그레이드를 수행할 수는 없습니다. 그러나 **데이터베이스 연결 업그레이드 절차는 지원**  됩니다.
  
     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치가 SharePoint 2010에 통합되어 있는 경우에는 SharePoint 서버를 전체 업그레이드할 수 없습니다. 그러나 SharePoint 2010 팜에서 콘텐츠 데이터베이스 및 서비스 응용 프로그램 데이터베이스를 SharePoint 2013/2016 팜으로 마이그레이션할 수 있습니다.  
  
### <a name="includesssql11includessssql11-mdmd-to-sql-server-reporting-services"></a>[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]SQL server Reporting Services  
 **시작 환경:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 또는 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)], SharePoint 2010  
  
 **종료 환경:** SQL Server Reporting Services, SharePoint 2013 또는 SharePoint 2016.   
  
-   **SharePoint 2013/2016:** SharePoint 2013/2016에서 SharePoint 2013으로 현재 위치 업그레이드를 수행할 수는 없습니다. 그러나 **데이터베이스 연결 업그레이드 절차는 지원**  됩니다.
  
     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치가 SharePoint 2010에 통합되어 있는 경우에는 SharePoint 서버를 전체 업그레이드할 수 없습니다. 그러나 SharePoint 2010 팜에서 콘텐츠 데이터베이스 및 서비스 응용 프로그램 데이터베이스를 SharePoint 2013/2016 팜으로 마이그레이션할 수 있습니다.  
  
### <a name="includesskilimanjaroincludessskilimanjaro-mdmd-to-sql-server-reporting-services"></a>[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]SQL server Reporting Services  
 **시작 환경:** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], SharePoint 2010  
  
 **종료 환경:** SQL Server Reporting Services, SharePoint 2013 또는 SharePoint 2016.  
 
-   **SharePoint 2013/2016:** SharePoint 2013/2016에서 SharePoint 2013으로 현재 위치 업그레이드를 수행할 수는 없습니다. 그러나 **데이터베이스 연결 업그레이드 절차는 지원**  됩니다.

    Reporting Services를 업그레이드하기 전에 먼저 SharePoint를 마이그레이션해야 합니다.
  
-   SQL Server Reporting Services 버전의 설치는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 용 추가 기능에 SharePoint 팜의 각 웹 프런트 엔드에서 합니다. SQL Server Reporting Services 설치 마법사를 사용 하 여 또는 추가 기능을 다운로드 하 여 추가 기능을 설치할 수 있습니다.  
  
-   각 '보고서 서버'에 대 한 SharePoint 모드를 업그레이드 하려면 SQL Server Reporting Services 설치를 실행 합니다. SQL Server 설치 마법사는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스를 설치하고 새 서비스 응용 프로그램을 만듭니다. 
  
  
##  <a name="bkmk_migration_considerations"></a> 마이그레이션 고려 사항  
 응용 프로그램 데이터를 이동할 때는 다음과 같은 고려 사항 및 제한 사항에 대해 알고 있어야 합니다.  
  
-   암호화 키 보호에는 컴퓨터 ID를 통합하는 해시가 포함됩니다.  
  
-   보고서 서버 데이터베이스 이름은 고정되어 있으며 새 컴퓨터에서 바꿀 수 없습니다.  
  
### <a name="encryption-key-considerations"></a>암호화 키 고려 사항  
 보고서 서버 데이터베이스를 새 컴퓨터로 이동하기 전에 항상 암호화 키를 백업합니다.  
  
 보고서 서버 설치를 다른 컴퓨터로 이동하면 보고서 서버 데이터베이스에 저장되어 있는 중요한 데이터의 보안을 강화하는 데 사용된 암호화 키를 보호하는 해시가 무효화됩니다. 데이터베이스를 사용하는 각 보고서 서버 인스턴스에는 암호화 키의 복사본이 포함되며 이 복사본은 현재 컴퓨터에서 정의될 때 서비스 계정의 ID로 암호화됩니다. 컴퓨터를 변경하는 경우 새 컴퓨터에서 동일한 계정 이름을 사용하더라도 서비스에서 더 이상 해당 키에 액세스할 수 없게 됩니다.  
  
 새 보고서 서버 컴퓨터에서 해독 가능한 암호화를 다시 설정하려면 이전에 백업한 키를 복원해야 합니다. 보고서 서버 데이터베이스에 저장되는 전체 키 집합은 대칭 키 값과 키를 저장한 보고서 인스턴스만 사용할 수 있도록 키에 대한 액세스를 제한하는 데 사용된 서비스 ID 정보로 구성됩니다. 키를 복원하는 동안 보고서 서버는 기존 키 복사본을 새 버전으로 바꿉니다. 새 버전에는 현재 컴퓨터에서 정의된 컴퓨터 및 서비스 ID 값이 포함됩니다. 자세한 내용은 다음 항목을 참조하세요.  
  
-   SharePoint 모드: 자세한 내용은 [Reporting Services SharePoint 서비스 응용 프로그램 관리](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)의 "키 관리" 섹션을 참조하세요.  
  
-   기본 모드: [Reporting Services 암호화 키 백업 및 복원](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)참조  
  
  
### <a name="fixed-database-name"></a>고정 데이터베이스 이름  
 보고서 서버 데이터베이스의 이름은 바꿀 수 없습니다. 데이터베이스 ID는 데이터베이스를 만들 때 보고서 서버 저장 프로시저에 기록됩니다. 보고서 서버 주 또는 임시 데이터베이스의 이름을 바꾸면 프로시저를 실행할 때 오류가 발생하고 보고서 서버 설치가 무효화됩니다.  
  
 기존 설치의 데이터베이스 이름이 새 설치에 적합하지 않은 경우 원하는 이름이 지정된 새 데이터베이스를 만든 다음 아래에 나열된 기술을 사용하여 기존 응용 프로그램 데이터를 로드해야 합니다.  
  
-   보고서 서버 웹 서비스 SOAP 메서드를 호출하여 데이터베이스 간에 데이터를 복사하는 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 스크립트를 작성합니다. RS.exe 유틸리티를 사용하여 이 스크립트를 실행할 수 있습니다. 이 접근 방법은 [Reporting Services를 사용한 스크립팅 및 PowerShell](../../reporting-services/tools/scripting-and-powershell-with-reporting-services.md)을 참조하세요.  
  
-   WMI 공급자를 호출하여 데이터베이스 간에 데이터를 복사하는 코드를 작성합니다. 이 접근 방법은 [Reporting Services WMI 공급자 액세스](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md)를 참조하세요.  
  
-   항목 수가 적은 경우 보고서, 보고서 모델 및 공유 데이터 원본을 보고서 디자이너, 모델 디자이너 및 보고서 작성기에서 새 보고서 서버로 다시 게시할 수 있습니다. 이 경우 역할 할당, 구독, 공유 일정, 보고서 스냅숏 일정, 보고서 또는 기타 항목에서 설정한 사용자 지정 속성, 모델 항목 보안 및 보고서 서버에서 설정한 속성을 다시 만들어야 합니다. 보고서 기록 및 보고서 실행 로그 데이터는 손실됩니다.  
  
  
##  <a name="bkmk_additional_resources"></a> 추가 리소스  
  
> [!NOTE]  
>  SharePoint 데이터베이스 연결 업그레이드에 대한 자세한 내용은 다음을 참조하십시오.  
  
-   [SharePoint 2016으로 업그레이드 프로세스의 개요](https://technet.microsoft.com/library/cc262483\(v=office.16\)).

-   [SharePoint 2013으로 업그레이드 프로세스의 개요](http://go.microsoft.com/fwlink/p/?LinkId=256688).
  
-   [SharePoint 2013으로 업그레이드하기 전에 정리 준비](http://go.microsoft.com/fwlink/p/?LinkId=256689).  
  
-   [SharePoint 2013에서 SharePoint 2016으로 데이터베이스 업그레이드](https://technet.microsoft.com/library/cc303436\(v=office.16\)).

-   [SharePoint 2010에서 SharePoint 2013으로 데이터베이스 업그레이드](http://go.microsoft.com/fwlink/p/?LinkId=256690).  

## <a name="next-steps"></a>다음 단계

[보고서 업그레이드](../../reporting-services/install-windows/upgrade-reports.md)   
[설치 마법사를 사용하여 SQL Server 2016으로 업그레이드&#40;설치 프로그램&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  

문의: [Reporting Services 포럼에서 질문](http://go.microsoft.com/fwlink/?LinkId=620231)
