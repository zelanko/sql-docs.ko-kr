---
title: Reporting Services 업그레이드 및 마이그레이션 | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- SSRS, upgrading
- Reporting Services, upgrades
- SQL Server Reporting Services, upgrading
- upgrading Reporting Services
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: 95bf8da81caa71b3f095e7143292cd60e807b585
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108630"
---
# <a name="upgrade-and-migrate-reporting-services"></a>Upgrade and Migrate Reporting Services

이 항목은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 업그레이드 및 마이그레이션 옵션에 대한 개요입니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 배포를 업그레이드하는 방법은 일반적으로 두 가지가 있습니다.  
  
-   **업그레이드:** 업그레이드는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소를 서버 및 현재 설치 된 인스턴스. 이를 일반적으로 "현재 위치" 업그레이드라고 합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서버의 한 모드에서 다른 모드로의 전체 업그레이드는 지원되지 않습니다. 예를 들어 기본 모드 보고서 서버를 SharePoint 모드 보고서 서버로 업그레이드할 수 없습니다. 보고서 항목을 한 모드에서 다른 모드로 마이그레이션할 수 있습니다. 자세한 내용은이 문서 및 관련된 항목 뒷부분에 나오는 '기본 모드에서 sharepoint 모드로 마이그레이션' 섹션을 참조 하세요 [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](../tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)합니다.  
  
-   **마이그레이션**: 설치 및 새 SharePoint 환경을 구성에 보고서 항목 및 리소스를 새 환경에 복사 하 기존 내용을 사용 하도록 새 환경을 구성 합니다. 낮은 수준 형식의 마이그레이션은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터베이스, 구성 파일 및 SharePoint 콘텐츠 데이터베이스(SharePoint 모드를 사용하는 경우)를 복사하는 것입니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드 &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드|  
  
##  <a name="bkmk_top"></a> 항목 내용  
  
-   [알려진된 업그레이드 문제 및 모범 사례](#bkmk_known_issues)  
  
-   [나란히 설치](#bkmk_side_by_side)  
  
-   [전체 업그레이드](#bkmk_inplace_upgrade)  
  
-   [업그레이드 전 검사 목록](#bkmk_upgrade_checklist)  
  
-   [기본 모드 업그레이드 및 마이그레이션 시나리오](#bkmk_native_scenarios)  
  
-   [Reporting Services 기본 모드 스케일 아웃 배포를 업그레이드 합니다.](#bkmk_native_scaleout)  
  
-   [SharePoint 모드 업그레이드 및 마이그레이션 시나리오](#bkmk_sharePoint_scenarios)  
  
-   [마이그레이션 고려 사항](#bkmk_migration_considerations)  
  
-   [추가 리소스](#bkmk_additional_resources)  
  
##  <a name="bkmk_known_issues"></a> 알려진 업그레이드 문제 및 최선의 구현 방법  
 업그레이드할 수 있는 버전의 상세 목록은 [Supported Version and Edition Upgrades](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)를 참조하십시오.  
  
> [!TIP]
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 문제에 대한 최신 정보는 다음을 참조하십시오.  
> 
>  -   [SQL Server 2014 릴리스 정보](https://go.microsoft.com/fwlink/?LinkID=296445)  
> -   [SQL Server 2014 Reporting Services 팁, 요령 및 문제 해결](https://go.microsoft.com/fwlink/?LinkID=391254)  
> -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업그레이드 관리자를 사용합니다. 자세한 내용은 [Reporting Services 업그레이드 문제 &#40;업그레이드 관리자&#41; ](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md) 하 고 [방법: 업그레이드 관리자 설치](../../../2014/sql-server/install/how-to-install-upgrade-advisor.md)합니다.  
  
 ![맨 위 링크와 함께 사용 되는 화살표 아이콘](../../2014-toc/media/uparrow16x16.gif "맨 위 링크와 함께 사용 되는 화살표 아이콘") [이 항목의 합니다.](#bkmk_top)  
  
##  <a name="bkmk_side_by_side"></a> 함께 설치  
 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 기본 모드를 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 기본 모드 배포와 함께 설치할 수 있습니다.  
  
 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] SharePoint 모드를 이전 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드 구성 요소와 함께 배포할 수는 없습니다.  
  
 ![맨 위 링크와 함께 사용 되는 화살표 아이콘](../../2014-toc/media/uparrow16x16.gif "맨 위 링크와 함께 사용 되는 화살표 아이콘") [이 항목의 합니다.](#bkmk_top)  
  
##  <a name="bkmk_inplace_upgrade"></a> 전체 업그레이드  
 업그레이드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에 의해 완료됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 비롯한 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]구성 요소의 일부 또는 전체를 업그레이드할 수 있습니다. 설치 프로그램에서 기존 인스턴스를 감지하고 업그레이드할지 묻는 메시지를 표시합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 명령줄 인수로 지정하거나 설치 마법사에서 지정할 수 있는 업그레이드 옵션을 제공합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 실행하면 다음 버전 중 하나에서 업그레이드하는 옵션을 선택하거나 기존 설치와 함께 실행되는 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 의 새 인스턴스를 설치할 수 있습니다.  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 자세한 내용은 다음을 참조하세요.  
  
||  
|-|  
|[SQL Server 2014로 업그레이드](../../database-engine/install-windows/upgrade-sql-server.md)|  
|[업그레이드 하려면 SQL Server 2014 설치 마법사를 사용 하 여 &#40;설치&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)|  
|[명령 프롬프트에서 SQL Server 2014 설치](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)|  
  
 ![맨 위 링크와 함께 사용 되는 화살표 아이콘](../../2014-toc/media/uparrow16x16.gif "맨 위 링크와 함께 사용 되는 화살표 아이콘") [이 항목의 합니다.](#bkmk_top)  
  
##  <a name="bkmk_upgrade_checklist"></a> 업그레이드 전 검사 목록  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]으로 업그레이드하기 전에 다음을 검토하십시오.  
  
-   사용 중인 하드웨어 및 소프트웨어가 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]를 지원하는지 확인하려면 요구 사항을 검토하십시오. 자세한 내용은 [Hardware and Software Requirements for Installing SQL Server 2014](../../../2014/sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)을 참조하세요.  
  
-   SCC(시스템 구성 검사기)를 사용하여 보고서 서버 컴퓨터에 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]을 설치하는 데 방해가 되는 조건이 있는지 검색합니다. 자세한 내용은 [Check Parameters for the System Configuration Checker](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)을 참조하세요.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 최상의 권장 보안 방법 및 지침을 검토하십시오. 자세한 내용은 [Security Considerations for a SQL Server Installation](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)을 참조하세요.  
  
-   보고서 서버 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업그레이드 관리자를 실행하여 업그레이드하는 데 방해가 되는 문제가 있는지 확인합니다. 자세한 내용은 [Use Upgrade Advisor to Prepare for Upgrades](../../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)을 참조하세요.  
  
-   대칭 키를 백업합니다. 자세한 내용은 [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)을 참조하세요.  
  
-   보고서 서버 데이터베이스 및 구성 파일을 백업합니다. 자세한 내용은 [Backup and Restore Operations for Reporting Services](../../reporting-services/install-windows/backup-and-restore-operations-for-reporting-services.md)을 참조하세요.  
  
-   IIS의 기존 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 가상 디렉터리에 대한 모든 사용자 지정을 백업합니다.  
  
-   잘못된 SSL 인증서를 제거합니다.  여기에는 만료된 인증서 및 Reporting Services를 업그레이드하기 전에 업그레이드하지 않을 인증서가 포함됩니다.  잘못 된 인증서가 있으면 업그레이드가 실패 하 고 Reporting Services 로그 파일에 다음과 비슷한 오류 메시지가 기록 됩니다. **Microsoft.ReportingServices.WmiProvider.WMIProviderException: Secure Sockets Layer (SSL) 인증서를 웹 사이트에서 구성 되지 않았습니다.** .  
  
 프로덕션 환경을 업그레이드하기 전에 프로덕션 환경과 동일하게 구성된 사전 프로덕션 환경에서 항상 테스트 업그레이드를 실행하십시오.  
  
 ![맨 위 링크와 함께 사용 되는 화살표 아이콘](../../2014-toc/media/uparrow16x16.gif "맨 위 링크와 함께 사용 되는 화살표 아이콘") [이 항목의 합니다.](#bkmk_top)  
  
## <a name="overview-of-migration-scenarios"></a>마이그레이션 시나리오 개요  
 지원되는 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 업그레이드하는 경우 일반적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사를 실행하여 보고서 서버 프로그램 파일, 데이터베이스 및 모든 애플리케이션 데이터를 업그레이드할 수 있습니다.  
  
 그러나 다음과 같은 조건에 해당하는 경우 보고서 서버 설치를 수동으로 **마이그레이션** 해야 합니다.  
  
-   업그레이드 관리자가 업그레이드 블로커를 하나 더 검색했습니다. 자세한 내용은 [Use Upgrade Advisor to Prepare for Upgrades](../../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)을 참조하세요.  
  
-   배포에 사용되는 보고서 서버의 유형을 변경하려고 합니다. 예를 들어 기본 모드 보고서 서버를 SharePoint 모드로 업그레이드하거나 변환할 수 없습니다. 자세한 내용은 [기본 모드에서 SharePoint 모드로의 마이그레이션&#40;SSRS&#41;](../../reporting-services/install-windows/native-to-sharepoint-migration-ssrs.md)을 참조하세요.  
  
-   업그레이드 프로세스 중에 보고서 서버가 오프라인 상태가 되는 시간을 최소화해야 합니다. 기존 보고서 서버 설치의 상태를 변경하지 않으면서 콘텐츠 데이터를 새 보고서 서버 인스턴스로 복사하고 설치를 테스트하는 동안 현재 설치는 온라인 상태로 유지됩니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 SharePoint 2010 배포를 SharePoint 2013으로 마이그레이션할 수 있습니다. SharePoint 2013은 SharePoint 2010에서의 전체 업그레이드를 지원하지 않습니다. 자세한 내용은 [Reporting Services 설치 마이그레이션&#40;SharePoint 모드&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md)을 참조하세요.  
  
 ![맨 위 링크와 함께 사용 되는 화살표 아이콘](../../2014-toc/media/uparrow16x16.gif "맨 위 링크와 함께 사용 되는 화살표 아이콘") [이 항목의 합니다.](#bkmk_top)  
  
##  <a name="bkmk_native_scenarios"></a> 기본 모드 업그레이드 및 마이그레이션 시나리오  
 **업그레이드:** 기본 모드에 대 한 전체 업그레이드는 지원 되는이 항목의 앞부분에 나열 된 버전 각각에 대 한 프로세스와 동일 합니다. SQL Server 설치 마법사 또는 명령줄 설치를 실행합니다. 설치하면 보고서 서버 데이터베이스가 새 보고서 서버 데이터베이스 스키마로 자동 업그레이드됩니다. 자세한 내용은 이 항목의 [In-place upgrade](#bkmk_inplace_upgrade) 섹션을 참조하세요.  
  
 업그레이드할 기존 보고서 서버 인스턴스를 선택하면 업그레이드 프로세스가 시작됩니다.  
  
1.  보고서 서버 데이터베이스가 원격 컴퓨터에 있어서 해당 데이터베이스를 업데이트할 수 있는 권한이 없는 경우 원격 보고서 서버 데이터베이스를 업데이트할 수 있는 자격 증명을 지정하라는 메시지가 나타납니다. 이때 `sysadmin` 또는 데이터베이스 업데이트 권한이 있는 자격 증명을 제공해야 합니다.  
  
2.  보고서 서버에 배포된 사용자 지정 확장 프로그램과 같이 업그레이드를 방해하는 조건이나 설정이 있는지 확인한 다음 구성 설정을 읽습니다. 업그레이드가 차단된 경우 업그레이드가 더 이상 차단되지 않도록 설치를 수정하거나 새 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스로 마이그레이션해야 합니다. 자세한 내용은 업그레이드 관리자 설명서를 참조하십시오.  
  
3.  업그레이드를 진행할 수 있는 경우 업그레이드 프로세스를 계속할지 묻는 메시지가 표시됩니다.  
  
4.  설치 프로그램이 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 프로그램 파일용 새 폴더를 만듭니다. 프로그램 폴더는 한 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] MSRS12 설치에 포함 되어 있습니다.\< *인스턴스 이름*>.  
  
5.  설치 프로그램이 보고서 서버 기능의 일부인 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 보고서 서버 프로그램 파일, 구성 도구 및 명령줄 유틸리티를 추가합니다.  
  
    1.  이전 버전의 프로그램 파일이 제거됩니다.  
  
    2.  새 버전으로 업그레이드되는 보고서 서버 구성 도구 및 유틸리티에는 기본 모드 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구, 명령줄 유틸리티(예: RS.exe) 및 보고서 작성기가 포함됩니다.  
  
    3.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 및 온라인 설명서와 같은 기타 클라이언트 도구는 업그레이드되지 않습니다. 이러한 도구의 새 버전을 얻으려면 설치 프로그램을 실행할 때 추가해야 합니다. 이전 버전은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전과 함께 존재합니다. 예제를 설치한 경우 이전 버전으로 계속 유지됩니다. 설치 프로그램은 SQL Server 예제에 대한 업그레이드를 지원하지 않습니다.  
  
    4.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 는 별도의 다운로드입니다. 자세한 내용은 [Microsoft SQL Server 2014 Data Tools - Microsoft Visual Studio 2012용 Business Intelligence](https://www.microsoft.com/download/details.aspx?id=36843)를 참조하십시오.  
  
6.  설치 프로그램은 서비스 제어 관리자에 있는 서비스 항목을 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 보고서 서버 서비스에 다시 사용합니다. 이 서비스 항목에는 보고서 서버 Windows 서비스 계정이 포함됩니다.  
  
7.  설치 프로그램이 IIS의 기존 가상 디렉터리 설정에 따라 새 URL을 예약합니다. 설치 프로그램이 IIS의 가상 디렉터리를 제거하지 않을 수 있으므로 업그레이드가 끝나면 이 디렉터리를 수동으로 제거해야 합니다.  
  
8.  설치 프로그램이 보고서 서버 데이터베이스를 새 스키마로 업그레이드하고 역할에 새 데이터베이스 소유자 권한을 추가하여 `RSExecRole`을 수정합니다. 이 단계는 SP1 이전의 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서 업그레이드하는 경우에만 수행됩니다.  
  
9. 설치 프로그램이 구성 파일의 설정을 병합합니다. 현재 설치의 구성 파일을 기준으로 새 항목이 추가됩니다. 사용하지 않는 항목은 제거되지는 않지만 업그레이드가 끝난 후 보고서 서버에서 더 이상 읽어 들이지 않습니다. 업그레이드할 때 IIS에 있는 이전 로그 파일, 사용되지 않는 RSWebApplication.config 파일 또는 가상 설정이 삭제되지 않으며, SQL Server 2005 보고서 디자이너, Management Studio 또는 기타 클라이언트 도구도 제거되지 않습니다. 따라서 이러한 파일과 도구가 더 이상 필요하지 않을 경우에는 업그레이드가 끝난 후 제거해야 합니다.  
  
 **마이그레이션:** 이전 버전의 기본 모드 설치를 마이그레이션하 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 는이 항목의 앞부분에 나와 있는 지원 버전 모두에 대 한 동일한 단계에 있습니다. 자세한 내용은 [Reporting Services 설치 마이그레이션&#40;기본 모드&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)을 참조하세요.  
  
 ![맨 위 링크와 함께 사용 되는 화살표 아이콘](../../2014-toc/media/uparrow16x16.gif "맨 위 링크와 함께 사용 되는 화살표 아이콘") [이 항목의 합니다.](#bkmk_top)  
  
##  <a name="bkmk_native_scaleout"></a> Reporting Services 기본 모드 확장 배포  
 다음은 둘 이상의 보고서 서버로 확장된 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드 배포를 업그레이드하는 방법을 요약한 내용입니다. 이 과정에는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 배포의 작동 중지 시간이 필요합니다.  
  
1.  보고서 서버 데이터베이스 및 암호화 키를 백업합니다. 자세한 내용은 [Reporting Services 백업 및 복원 작업](../../reporting-services/install-windows/backup-and-restore-operations-for-reporting-services.md) 및 [확장 배포의 암호화 키 추가 및 제거&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)를 참조하세요.  
  
2.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여, 확장된 배포에서 모든 보고서 서버를 제거합니다. 자세한 내용은 [기본 모드 보고서 서버 확장 배포 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)을 참조하세요.  
  
3.  보고서 서버 중 하나를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]으로 업그레이드합니다.  
  
4.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 보고서 서버를 스케일 아웃 배포에 다시 추가합니다. 자세한 내용은 [기본 모드 보고서 서버 확장 배포 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)을 참조하세요.  
  
     각 서버에 대해 업그레이드 및 확장 단계를 반복합니다.  
  
##  <a name="bkmk_sharePoint_scenarios"></a> SharePoint 모드 업그레이드 및 마이그레이션 시나리오  
 다음 섹션에서는 지정된 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드로 업그레이드하거나 마이그레이션하는 데 필요한 기본 단계 및 문제에 대해 설명합니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드 배포를 업그레이드하는 두 가지 설치 구성 요소가 있습니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 공유 서비스.  
  
    > [!TIP]  
    >  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint cmdlet `Get-SPRSServiceApplicationServers` 를 사용하여, SharePoint 팜에서 현재 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 공유 서비스를 실행 중이어서 업그레이드가 필요한 서버를 확인합니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능(SharePoint 제품용). 자세한 내용은 [설치 또는 SharePoint 용 Reporting Services 추가 기능에 제거 &#40;SharePoint 2010 및 SharePoint 2013&#41;](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)합니다.  
  
 SharePoint 모드 설치 마이그레이션에 대한 자세한 내용은 [Reporting Services 설치 마이그레이션&#40;SharePoint 모드&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  다음 시나리오 중 일부의 경우 업그레이드해야 하는 여러 기술 때문에 SharePoint 환경의 작동 중단이 필요합니다. 작동 중단이 허용되지 않는 상황에서는 내부 업그레이드 대신 마이그레이션을 완료해야 합니다.  
  
### <a name="includesssql11includessssql11-mdmd-to-includesssql14includessssql14-mdmd"></a>[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] - [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 **시작 환경:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 또는 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]., SharePoint 2010.  
  
 **종료 환경:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], SharePoint 2010 또는 SharePoint 2013  
  
-   **SharePoint  2010:** 전체 업그레이드의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 업그레이드 시나리오에는 SharePoint 환경의 작동 중단 시간이 필요 하지만 합니다.  
  
     종료 환경에서 SharePoint 2013을 실행하도록 하려면 SharePoint 2010에서 SharePoint 2013으로 데이터베이스 연결 업그레이드를 완료해야 합니다.  
  
-   **SharePoint 2013:** SharePoint 2013은 SharePoint 2010에서의 전체 업그레이드를 지원하지 않습니다. 그러나 **데이터베이스 연결 업그레이드 절차는 지원**됩니다. 동작은 전체 업그레이드 및 데이터베이스 연결 업그레이드의 두 가지 기본 업그레이드 방법 중 고객이 선택할 수 있는 SharePoint 2010으로 업그레이드와 다릅니다.  
  
     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치가 SharePoint 2010에 통합되어 있는 경우에는 SharePoint 서버를 전체 업그레이드할 수 없습니다. 그러나 SharePoint 2010 팜에서 콘텐츠 데이터베이스 및 서비스 애플리케이션 데이터베이스를 SharePoint 2013 팜으로 마이그레이션할 수 있습니다.  
  
### <a name="includesskilimanjaroincludessskilimanjaro-mdmd-to-includesssql14includessssql14-mdmd"></a>[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] - [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 **시작 환경:** SQL Server 2008 R2, SharePoint 2010.  
  
 **종료 환경:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], SharePoint 2010  
  
-   내부 업그레이드가 지원되며 SharePoint 환경에 대한 작동 중단 시간이 없습니다.  
  
-   팜의 각 웹 프런트 엔드에서 SharePoint용 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 추가 기능의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 버전을 설치합니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 마법사를 사용하거나 추가 기능을 다운로드하여 추가 기능을 설치할 수 있습니다.  
  
-   실행 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 각 '보고서 서버'에 대해 SharePoint 모드 업그레이드를 설치 합니다. SQL Server 설치 마법사가 설치 된 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 새 서비스 응용 프로그램을 만듭니다.  
  
     종료 환경에서 SharePoint 2013을 실행하도록 하려면 SharePoint 2010에서 SharePoint 2013으로 데이터베이스 연결 업그레이드를 완료해야 합니다.  
  
 ![맨 위 링크와 함께 사용 되는 화살표 아이콘](../../2014-toc/media/uparrow16x16.gif "맨 위 링크와 함께 사용 되는 화살표 아이콘") [이 항목의 합니다.](#bkmk_top)  
  
### <a name="includesskatmaiincludessskatmai-mdmd-sp2-to-includesssql14includessssql14-mdmd"></a>[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2 -&gt; [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 **시작 환경:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2, SharePoint 2007.  
  
 **종료 환경:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], SharePoint 2010  
  
-   이 내부 업그레이드 시나리오의 경우에는 SharePoint 및 SQL Server 기술 모두를 업그레이드해야 하므로 SharePoint 환경의 작동 중단 시간이 필요합니다. 따라서 내부 업그레이드 대신 마이그레이션을 완료할 것을 고려할 수 있습니다.  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에서 SP2(서비스 팩 2)로의 업그레이드가 완료되지 않은 경우 이를 먼저 수행합니다.  
  
-   SharePoint를 2010으로 업그레이드. SharePoint 2010 필수 구성 요소 설치 관리자를 실행하면 SharePoint 2010 제품용 Reporting Services 추가 기능도 업그레이드됩니다.  
  
-   모든 SharePoint 웹 프런트 엔드에서 SharePoint용 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 추가 기능의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 버전을 설치합니다. SharePoint 필수 구성 요소 설치 관리자가 SQL Server 2008 R2 버전의 추가 기능을 설치했지만 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 보고서 서버에서 사용할 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전이 필요합니다.  
  
-   > [!WARNING]  
    >  SharePoint 업그레이드를 수행하면 SQL Server가 업그레이드될 때까지 Reporting Services 환경이 작동하지 않는 상태에 있습니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]으로 업그레이드합니다. SQL Server 설치 마법사를 실행하면 "**SQL Server Reporting Services SharePoint 모드 인증**" 대화 상자가 나타납니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스가 설치되고 인증 페이지의 자격 증명이 새 SharePoint 응용 프로그램 풀을 만드는 데 사용됩니다.  
  
 ![맨 위 링크와 함께 사용 되는 화살표 아이콘](../../2014-toc/media/uparrow16x16.gif "맨 위 링크와 함께 사용 되는 화살표 아이콘") [이 항목의 합니다.](#bkmk_top)  
  
### <a name="sql-server-2005-sp2-to-includesssql14includessssql14-mdmd"></a>SQL Server 2005 SP2 -&gt; [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 **시작 환경:** SQL Server 2005 SP2, SharePoint 2007.  
  
 **종료 환경:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], SharePoint 2010  
  
-   이 내부 업그레이드 시나리오의 경우에는 SharePoint 및 SQL Server 기술 모두를 업그레이드해야 하므로 SharePoint 환경의 작동 중단 시간이 필요합니다. 따라서 내부 업그레이드 대신 마이그레이션을 완료할 것을 고려할 수 있습니다.  
  
-   SQL Server 2005의 SP2(서비스 팩 2)로의 업그레이드가 완료되지 않은 경우 이를 먼저 수행합니다.  
  
-   SharePoint를 SharePoint 2010으로 업그레이드. SharePoint 2010 필수 구성 요소 설치 관리자를 실행하면 SharePoint 2010 제품용 Reporting Services 추가 기능도 업그레이드됩니다.  
  
-   > [!WARNING]  
    >  SharePoint 업그레이드를 수행하면 SQL Server가 업그레이드될 때까지 Reporting Services 환경이 작동하지 않는 상태에 있습니다.  
  
-   모든 SharePoint 웹 프런트 엔드에서 SharePoint용 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 추가 기능의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 버전을 설치합니다. SharePoint 필수 구성 요소 설치 관리자가 SQL Server 2008 R2 버전의 추가 기능을 설치했지만 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 보고서 서버에서 사용할 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전이 필요합니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]으로 업그레이드합니다. SQL Server 설치 마법사를 실행하면 "SQL Server Reporting Services SharePoint 모드 인증" 대화 상자가 나타납니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스가 설치되고 인증 페이지의 자격 증명이 새 SharePoint 응용 프로그램 풀을 만드는 데 사용됩니다.  
  
 ![맨 위 링크와 함께 사용 되는 화살표 아이콘](../../2014-toc/media/uparrow16x16.gif "맨 위 링크와 함께 사용 되는 화살표 아이콘") [이 항목의 합니다.](#bkmk_top)  
  
##  <a name="bkmk_migration_considerations"></a> 마이그레이션 고려 사항  
 애플리케이션 데이터를 이동할 때는 다음과 같은 고려 사항 및 제한 사항에 대해 알고 있어야 합니다.  
  
-   암호화 키 보호에는 컴퓨터 ID를 통합하는 해시가 포함됩니다.  
  
-   보고서 서버 데이터베이스 이름은 고정되어 있으며 새 컴퓨터에서 바꿀 수 없습니다.  
  
### <a name="encryption-key-considerations"></a>암호화 키 고려 사항  
 보고서 서버 데이터베이스를 새 컴퓨터로 이동하기 전에 항상 암호화 키를 백업합니다.  
  
 보고서 서버 설치를 다른 컴퓨터로 이동하면 보고서 서버 데이터베이스에 저장되어 있는 중요한 데이터의 보안을 강화하는 데 사용된 암호화 키를 보호하는 해시가 무효화됩니다. 데이터베이스를 사용하는 각 보고서 서버 인스턴스에는 암호화 키의 복사본이 포함되며 이 복사본은 현재 컴퓨터에서 정의될 때 서비스 계정의 ID로 암호화됩니다. 컴퓨터를 변경하는 경우 새 컴퓨터에서 동일한 계정 이름을 사용하더라도 서비스에서 더 이상 해당 키에 액세스할 수 없게 됩니다.  
  
 새 보고서 서버 컴퓨터에서 해독 가능한 암호화를 다시 설정하려면 이전에 백업한 키를 복원해야 합니다. 보고서 서버 데이터베이스에 저장되는 전체 키 집합은 대칭 키 값과 키를 저장한 보고서 인스턴스만 사용할 수 있도록 키에 대한 액세스를 제한하는 데 사용된 서비스 ID 정보로 구성됩니다. 키를 복원하는 동안 보고서 서버는 기존 키 복사본을 새 버전으로 바꿉니다. 새 버전에는 현재 컴퓨터에서 정의된 컴퓨터 및 서비스 ID 값이 포함됩니다. 자세한 내용은 다음 항목을 참조하십시오.  
  
-   SharePoint 모드: "키 관리" 섹션을 참조 [Reporting Services SharePoint 서비스 응용 프로그램을 관리 합니다.](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)  
  
-   기본 모드: 참조 [백업 및 복원 Reporting Services 암호화 키](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)  
  
 ![맨 위 링크와 함께 사용 되는 화살표 아이콘](../../2014-toc/media/uparrow16x16.gif "맨 위 링크와 함께 사용 되는 화살표 아이콘") [이 항목의 합니다.](#bkmk_top)  
  
### <a name="fixed-database-name"></a>고정 데이터베이스 이름  
 보고서 서버 데이터베이스의 이름은 바꿀 수 없습니다. 데이터베이스 ID는 데이터베이스를 만들 때 보고서 서버 저장 프로시저에 기록됩니다. 보고서 서버 주 또는 임시 데이터베이스의 이름을 바꾸면 프로시저를 실행할 때 오류가 발생하고 보고서 서버 설치가 무효화됩니다.  
  
 기존 설치의 데이터베이스 이름이 새 설치에 적합하지 않은 경우 원하는 이름이 지정된 새 데이터베이스를 만든 다음 아래에 나열된 기술을 사용하여 기존 애플리케이션 데이터를 로드해야 합니다.  
  
-   보고서 서버 웹 서비스 SOAP 메서드를 호출하여 데이터베이스 간에 데이터를 복사하는 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 스크립트를 작성합니다. RS.exe 유틸리티를 사용하여 이 스크립트를 실행할 수 있습니다. 이 접근 방법은 [Reporting Services를 사용한 스크립팅 및 PowerShell](../tools/scripting-and-powershell-with-reporting-services.md)을 참조하세요.  
  
-   WMI 공급자를 호출하여 데이터베이스 간에 데이터를 복사하는 코드를 작성합니다. 이 접근 방법은 [Reporting Services WMI 공급자 액세스](../tools/access-the-reporting-services-wmi-provider.md)를 참조하세요.  
  
-   항목 수가 적은 경우 보고서, 보고서 모델 및 공유 데이터 원본을 보고서 디자이너, 모델 디자이너 및 보고서 작성기에서 새 보고서 서버로 다시 게시할 수 있습니다. 이 경우 역할 할당, 구독, 공유 일정, 보고서 스냅샷 일정, 보고서 또는 기타 항목에서 설정한 사용자 지정 속성, 모델 항목 보안 및 보고서 서버에서 설정한 속성을 다시 만들어야 합니다. 보고서 기록 및 보고서 실행 로그 데이터는 손실됩니다.  
  
 ![맨 위 링크와 함께 사용 되는 화살표 아이콘](../../2014-toc/media/uparrow16x16.gif "맨 위 링크와 함께 사용 되는 화살표 아이콘") [이 항목의 합니다.](#bkmk_top)  
  
##  <a name="bkmk_additional_resources"></a> 추가 리소스  
  
> [!NOTE]  
>  SharePoint 데이터베이스 연결 업그레이드에 대한 자세한 내용은 다음을 참조하십시오.  
  
-   [SharePoint 2013으로 업그레이드 프로세스 개요](https://go.microsoft.com/fwlink/p/?LinkId=256688) (https://go.microsoft.com/fwlink/p/?LinkId=256688) 합니다.  
  
-   [SharePoint 2013으로 업그레이드 하기 전에 정리 준비](https://go.microsoft.com/fwlink/p/?LinkId=256689) (https://go.microsoft.com/fwlink/p/?LinkId=256689) 합니다.  
  
-   [SharePoint 2010에서 SharePoint 2013으로 데이터베이스 업그레이드](https://go.microsoft.com/fwlink/p/?LinkId=256690) (https://go.microsoft.com/fwlink/p/?LinkId=256690) 합니다.  
  
 ![맨 위 링크와 함께 사용 되는 화살표 아이콘](../../2014-toc/media/uparrow16x16.gif "맨 위 링크와 함께 사용 되는 화살표 아이콘") [이 항목의 합니다.](#bkmk_top)  
  
## <a name="see-also"></a>관련 항목  
 [보고서 업그레이드](../../reporting-services/install-windows/upgrade-reports.md)   
 [업그레이드 하려면 SQL Server 2014 설치 마법사를 사용 하 여 &#40;설치&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  
