---
title: Reporting Services 설치 마이그레이션(SharePoint 모드) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 61290949-690a-4e19-b078-57c99b6b30fa
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0c2d28900e8e0c75123e48704de56ff69d720d17
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108744"
---
# <a name="migrate-a-reporting-services-installation-sharepoint-mode"></a>Reporting Services 설치 마이그레이션(SharePoint 모드)
  이 항목은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드 배포를 한 SharePoint 환경에서 다른 SharePoint 환경으로 마이그레이션하는 데 필요한 단계에 대한 개요입니다. 마이그레이션하려는 원본 버전에 따라 특정 단계는 달라질 수 있습니다. SharePoint 모드에 대한 업그레이드 및 마이그레이션 시나리오에 대한 자세한 내용은 [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)을 참조하십시오. 한 서버에서 다른 서버로 보고서 항목을 복사하기만 하려면 [보고서 서버 간 콘텐츠 마이그레이션을 위한 예제 Reporting Services rs.exe](../tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)를 참조하세요.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드 배포를 마이그레이션하는 방법은 [Reporting Services 설치 마이그레이션&#40;기본 모드&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)을 참조하세요.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010 및 SharePoint 2013|  
  
 일반적으로 SharePoint 2010 배포를 SharePoint 2013으로 업그레이드하려는 경우 마이그레이션을 완료합니다. SharePoint 2013은 SharePoint 2010에서의 전체 업그레이드를 지원하지 않으므로 **데이터베이스 연결 업그레이드** 또는 콘텐츠 전용 마이그레이션 절차를 완료해야 합니다.  
  
 SharePoint 2013 업그레이드에 대한 자세한 내용은 다음을 참조하십시오.  
  
-   [SharePoint 2013으로 업그레이드 프로세스의 개요](https://go.microsoft.com/fwlink/p/?LinkId=256688).  
  
-   [SharePoint 2010에서 SharePoint 2013으로 데이터베이스 업그레이드](https://go.microsoft.com/fwlink/p/?LinkId=256690).  
  
-   [SharePoint 2013에서 콘텐츠 데이터베이스 이동](https://technet.microsoft.com/library/cc262792.aspx).  
  
 
  
##  <a name="bkmk_prior_versions"></a> SQL Server 2012 이전의 Reporting Services SharePoint 모드 버전에서 마이그레이션  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서 서비스 응용 프로그램 데이터베이스 스키마를 비롯한 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]SharePoint 모드 아키텍처가 변경되었습니다. [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 이전 버전에서 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]SharePoint 모드로 마이그레이션하려면 먼저 SharePoint 및 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드를 설치하여 새 SharePoint 환경을 만듭니다. 자세한 내용은 [Reporting Services SharePoint 모드 설치 &#40;SharePoint 2010 및 SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)합니다.  
  
 새 SharePoint 환경이 실행 중이면 콘텐츠 데이터베이스가 포함된 데이터베이스 수준에서 콘텐츠 전용 마이그레이션 또는 전체 마이그레이션을 선택할 수 있습니다.  
  
###  <a name="bkmk_content_only_migration"></a> 콘텐츠 전용 마이그레이션  
 **Reporting Services 콘텐츠 전용 마이그레이션:** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 콘텐츠를 새 팜으로 복사하려는 경우 **rs.exe**와 같은 도구를 사용하여 콘텐츠를 새 SharePoint 설치에 복사해야 합니다. 콘텐츠 전용 마이그레이션에 대한 자세한 내용은 다음을 참조하십시오.  
  
-   **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] RSS 스크립트:** 스크립트는 콘텐츠 및 기본 모드와 SharePoint 모드 보고서 서버 간에 리소스를 마이그레이션할 수 있습니다. 자세한 내용은 [Sample Reporting Services rs.exe 스크립트 마이그레이션 콘텐츠 between Report Servers](../tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md) 고 [다른에하나의보고서서버에서콘텐츠를마이그레이션하는ReportingServicesRS.exe스크립트](http://azuresql.codeplex.com/releases/view/115207).  
  
-   **Reporting Services 마이그레이션 도구:** 도구는 SharePoint 모드 서버로 기본 모드 서버에서 보고서 항목을 복사할 수 있습니다. 자세한 내용은 [Reporting Services 마이그레이션 도구](https://www.microsoft.com/download/details.aspx?id=29560)(영문)를 참조하세요.  
  
###  <a name="bkmk_full_migration"></a> 전체 마이그레이션  
 **전체 마이그레이션:** 와 함께 SharePoint 콘텐츠 데이터베이스를 마이그레이션하려는 경우는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 카탈로그 데이터베이스를 새 팜으로 있는 일련의이 항목에서는 백업 및 복원 옵션을 수행할 수 있습니다. 백업 단계에서 사용한 도구와 다른 도구를 복원 단계에 사용해야 하는 경우도 있습니다. 예를 들어 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 이전 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서 암호화 키를 백업할 수 있지만 암호화 키를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드 설치로 복원할 때는 SharePoint 중앙 관리 또는 PowerShell을 사용해야 합니다.  
  
####  <a name="bkmk_databases"></a> 완료된 마이그레이션에 나타나는 데이터베이스  
 다음 표에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 설치를 성공적으로 마이그레이션한 후의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 와 관련된 SQL Server에 대해 설명합니다.  
  
|데이터베이스|이름 예||  
|--------------|------------------|-|  
|카탈로그 데이터베이스|ReportingService_[service application GUID] **(\*)**|사용자가 마이그레이션합니다.|  
|임시 데이터베이스|ReportingService_[service application GUID]TempDB **(\*)**|사용자가 마이그레이션합니다.|  
|경고 데이터베이스|ReportingService_[service application GUID]_Alerting|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램을 만들 때 만들어집니다.|  
  
 **(\*)** 위의 표에 예로 나와 있는 이름은 새 SSRS 서비스 응용 프로그램을 만들 때 SSRS에서 사용하는 명명 규칙을 따릅니다. 다른 서버에서 마이그레이션하는 경우 카탈로그와 tempDB의 이름은 원래 설치에서와 같습니다.  
  
####  <a name="bkmk_backup_operations"></a> 백업 작업  
 이 섹션에서는 마이그레이션해야 하는 정보 유형과 백업을 완료하는 데 사용하는 도구나 프로세스에 대해 설명합니다.  
  
 ![SSRS SharePoint 마이그레이션의 기본 다이어그램](../../../2014/sql-server/install/media/rs-sharepoint-migration.gif "SSRS SharePoint 마이그레이션의 기본 다이어그램")  
  
||개체|메서드|참고|  
|-|-------------|------------|-----------|  
|**1**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 암호화 키|**Rskeymgmt.exe** 또는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자. [Reporting Services 암호화 키 백업 및 복원](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)을 참조하세요.|표에 나와 있는 도구는 백업 작업에는 사용할 수 있지만 복원 작업 작업에는 사용할 수 없습니다. 복원 작업에는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 관리 페이지 또는 PowerShell을 사용합니다.|  
|**2**|SharePoint 콘텐츠 데이터베이스||데이터베이스를 백업하고 분리합니다.<br /><br /> [업그레이드 방법 결정(SharePoint Server 2010)(https://technet.microsoft.com/library/cc263447.aspx)](https://technet.microsoft.com/library/cc263447.aspx)의 "데이터베이스 연결 업그레이드" 섹션을 참조하세요.|  
|**3**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]카탈로그 데이터베이스인 SQL Server 데이터베이스|SQL Server 데이터베이스 백업 및 복원<br /><br /> 로 구분하거나 여러<br /><br /> SQL Server 데이터베이스 분리 및 연결||  
|**4**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 파일|단순한 파일 복사|파일을 사용자 지정한 경우에만 rsreportserver.config를 복사해야 합니다. 파일 기본 위치의 예: C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting<br /><br /> Rsreportserver.config<br /><br /> Rssvrpolicy.config<br /><br /> 보고서 서버 ASP.NET 애플리케이션용 Web.config<br /><br /> ASP.NET용 Machine.config|  
  
####  <a name="bkmk_restore_operations"></a> 복원 작업  
 이 섹션에서는 마이그레이션해야 하는 정보 유형과 복원을 완료하는 데 사용하는 도구나 프로세스에 대해 설명합니다. 복원하는 데 사용하는 도구는 백업하는 데 사용한 도구와 다를 수 있습니다.  
  
 복원 단계를 완료하기 전에 SharePoint 팜 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드를 설치하고 구성해야 합니다. 기본 설치에 대 한 자세한 내용은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드의 경우 참조 [Reporting Services SharePoint 모드 설치 &#40;SharePoint 2010 및 SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)합니다.  
  
||개체|메서드|참고|  
|-|-------------|------------|-----------|  
|**1**|SharePoint 콘텐츠 데이터베이스를 새 팜에 복원|SharePoint "데이터베이스 연결 업그레이드" 방법|기본 단계:<br /><br /> 1) 새 서버에서 데이터베이스를 복원합니다.<br /><br /> 2) URL을 지정하여 콘텐츠 데이터베이스를 웹 애플리케이션에 연결합니다.<br /><br /> 3) Get-SPWebapplication이 모든 웹 애플리케이션과 URL을 나열합니다.<br /><br /> [업그레이드 방법 결정(SharePoint Server 2010)(https://technet.microsoft.com/library/cc263447.aspx)](https://technet.microsoft.com/library/cc263447.aspx) 및 [데이터베이스 연결 및 SharePoint Server 2010으로 업그레이드(https://technet.microsoft.com/library/cc263299.aspx)](https://technet.microsoft.com/library/cc263299.aspx)의 "데이터베이스 연결 업그레이드" 섹션을 참조하세요.|  
|**2**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 카탈로그 데이터베이스인 SQL 데이터베이스(ReportServer) 복원|SQL 데이터베이스 백업 및 복원<br /><br /> **또는**<br /><br /> SQL Server 데이터베이스 연결 및 분리|데이터베이스를 처음 사용하는 경우 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 환경에서 사용할 수 있도록 필요에 따라 데이터베이스 스키마를 업데이트합니다.|  
|**3**|새 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션 만들기|SharePoint 중앙 관리|새 서비스 애플리케이션을 만들 때 복사한 보고서 서버 데이터베이스를 사용하도록 구성합니다.<br /><br /> SharePoint 중앙 관리 사용에 대한 자세한 정보는 "3단계: Reporting Services 서비스 응용 프로그램 만들기"섹션에서 [Reporting Services SharePoint 모드 설치 SharePoint 2013 용](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md)합니다.<br /><br /> PowerShell 사용 예제가 필요한 경우 [Reporting Services SharePoint Service and Service Applications](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md)(영문)의 "PowerShell을 사용하여 Reporting Services 서비스 애플리케이션을 만드는 방법" 섹션을 참조하세요.|  
|**4**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 파일 복원|단순한 파일 복사|파일 기본 위치의 예: C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting.|  
|**5**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 암호화 키를 복원합니다.|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션 "SystemSettings" 페이지<br /><br /> **또는**<br /><br /> PowerShell을 사용하여 키 백업 파일 복원|[Reporting Services SharePoint 서비스 애플리케이션 관리](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md) 토픽의 "키 관리" 섹션을 참조하세요.|  
  
#####  <a name="bkmk_additional_configuration"></a> 기타 고려 사항  
 이전 SharePoint 환경의 구성 방법에 따라 다음 작업 중 하나 이상을 완료해야 할 수 있습니다.  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램에 대해 NTLM 인증을 구성합니다. 자세한 내용은 [Reporting Services 서비스 응용 프로그램에 대한 메일 구성&#40;SharePoint 2010 및 SharePoint 2013&#41;](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)을 참조하세요.  
  
##  <a name="bkmk_migrate_from_ctp"></a> SQL Server 2012 배포에서 마이그레이션  
 다중 서버 팜에서는 사용자가 콘텐츠 데이터베이스 및 카탈로그 데이터베이스를 다른 컴퓨터에 포함하고 있을 가능성이 많습니다. 이 경우에는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스가 설치되어 있는 새 서버를 SharePoint 팜에 추가한 다음 이전 서버를 제거하면 됩니다. 데이터베이스를 복사할 필요가 없습니다.  
  
### <a name="backup-operations"></a>백업 작업  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 암호화 키를 백업합니다.  
  
2.  SharePoint 중앙 관리 또는 PowerShell을 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션을 백업합니다. 그러면 SharePoint의 서비스 애플리케이션 데이터베이스도 백업됩니다. [Reporting Services SharePoint 서비스 응용 프로그램 백업 및 복원](../../../2014/reporting-services/backup-and-restore-reporting-services-sharepoint-service-applications.md)항목을 참조하세요.  
  
3.  UEA(무인 실행 계정) 및 Windows 인증이 있는 경우 복원 프로세스에 사용할 수 있도록 자격 증명을 기록해 두십시오.  
  
4.  자세한 내용은 [SharePoint 2013에서 서비스 애플리케이션 백업](https://technet.microsoft.com/library/ee428318.aspx)을 참조하십시오.  
  
### <a name="restore-operations"></a>복원 작업  
  
1.  SharePoint 중앙 관리를 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션을 복원합니다. 이때 PowerShell을 사용할 수도 있습니다.  
  
2.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 암호화 키를 복원합니다.  
  
     [Reporting Services SharePoint 서비스 애플리케이션 관리](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md) 토픽의 "키 관리" 섹션을 참조하세요.  
  
3.  서비스 애플리케이션에 대한 UEA 및 Windows 자격 증명을 구성합니다.  
  
4.  자세한 내용은 [SharePoint 2013에서 서비스 애플리케이션 복원](https://technet.microsoft.com/library/ee428305.aspx)을 참조하십시오.  
  
##  <a name="bkmk_additional_resources"></a> 추가 리소스  
  
-   [SharePoint 2013으로 업그레이드 시작(https://technet.microsoft.com/library/ee833948.aspx)](https://technet.microsoft.com/library/ee833948.aspx).  
  
-   [SharePoint 2013으로 업그레이드 프로세스의 개요(https://technet.microsoft.com/library/cc262483.aspx)](https://technet.microsoft.com/library/cc262483.aspx).  
  
## <a name="see-also"></a>관련 항목  
 [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
 [Reporting Services 설치 마이그레이션&#40;기본 모드&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)  
  
  
