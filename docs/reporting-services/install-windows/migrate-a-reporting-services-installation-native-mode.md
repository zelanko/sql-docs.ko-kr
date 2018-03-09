---
title: "Reporting Services 설치 마이그레이션(기본 모드) | Microsoft Docs"
ms.custom: 
ms.date: 08/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- manual Reporting Services migrations
- Report Server Windows service
- custom Reporting Services installations
- automatic Reporting Services migrations
- Reporting Services, upgrades
- upgrading Reporting Services
- migrating Reporting Services
ms.assetid: a6fc56c1-c504-438d-a2b0-5ed29c24e7d6
caps.latest.revision: "54"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: b05058e8d0254939f0c2018a484a12f458213f0b
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="migrate-a-reporting-services-installation-native-mode"></a>Reporting Services 설치 마이그레이션(기본 모드)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

이 항목에서는 다음과 같은 지원되는 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드 배포 중 하나를 새로운 SQL Server Reporting Services 인스턴스로 마이그레이션하는 데 필요한 단계별 지침을 제공합니다.  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드 배포 마이그레이션에 대한 자세한 내용은 [Reporting Services 설치 마이그레이션&#40;SharePoint 모드&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md)을 참조하세요.  
  
 마이그레이션은 응용 프로그램 데이터 파일을 새 SQL Server 인스턴스로 이동하는 것을 말합니다. 설치를 마이그레이션해야 하는 일반적인 원인은 다음과 같습니다.  
  
-   광범위한 배포 또는 작동 시간이 필요합니다.  
  
-   설치에 대한 하드웨어 또는 토폴로지를 변경할 예정입니다.  
  
-   업그레이드를 막는 문제가 발생했습니다.

## <a name="bkmk_nativemode_migration_overview"></a> 기본 모드 마이그레이션 개요

 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 마이그레이션 프로세스에는 수동 단계와 자동 단계가 포함됩니다. 다음은 보고서 서버 마이그레이션의 일부 태스크입니다.  
  
-   데이터베이스, 응용 프로그램 및 구성 파일을 백업합니다.  
  
-   암호화 키를 백업합니다.  
  
-   새 SQL Server 인스턴스를 설치합니다. 같은 하드웨어를 사용 중인 경우 SQL Server를 기존 설치와 함께 설치할 수 있습니다(지원되는 버전 중 하나인 경우).  
  
    > [!TIP]  
    >  함께 설치하려면 SQL Server를 명명된 인스턴스로 설치해야 합니다.  
  
-   보고서 서버 데이터베이스 및 기타 응용 프로그램 파일을 기존 설치에서 새 SQL Server 설치로 이동합니다.  
  
-   모든 사용자 지정 응용 프로그램 파일을 새 설치로 이동합니다.  
  
-   보고서 서버를 구성합니다.  
  
-   이전 설치의 모든 사용자 지정 설정을 포함하도록 **RSReportServer.config** 를 편집합니다.  
  
-   선택적으로 새 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Windows 서비스 그룹에 대한 사용자 지정 ACL(액세스 제어 목록)을 구성합니다.  
  
-   새 인스턴스가 완벽하게 작동하는지 확인한 후 사용하지 않는 응용 프로그램과 도구를 제거합니다.  
  
 보고서 서버 데이터베이스를 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전은 제한되어 있습니다. 이전 설치에서 만든 보고서 서버 데이터베이스를 다시 사용하는 경우에는 다음 항목을 검토하십시오.  
  
-   [보고서 서버 데이터베이스 만들기](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)  
  
##  <a name="bkmk_fixed_database_name"></a> 고정 데이터베이스 이름  
 보고서 서버 데이터베이스의 이름은 바꿀 수 없습니다. 데이터베이스 ID는 데이터베이스를 만들 때 보고서 서버 저장 프로시저에 기록됩니다. 보고서 서버의 기본 또는 임시 데이터베이스의 이름을 바꾸면 프로시저를 실행할 때 오류가 발생하고 보고서 서버 설치가 무효화됩니다.  
  
 기존 설치의 데이터베이스 이름이 새 설치에 적합하지 않은 경우 이름이 지정된 새 데이터베이스를 만든 다음 아래에 나열된 기술을 사용하여 기존 응용 프로그램 데이터를 로드해야 합니다.  
  
-   보고서 서버 웹 서비스 SOAP 메서드를 호출하여 데이터베이스 간에 데이터를 복사하는 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 스크립트를 작성합니다. RS.exe 유틸리티를 사용하여 이 스크립트를 실행할 수 있습니다. 이 접근 방법은 [Reporting Services를 사용한 스크립팅 및 PowerShell](../../reporting-services/tools/scripting-and-powershell-with-reporting-services.md)을 참조하세요.  
  
-   WMI 공급자를 호출하여 데이터베이스 간에 데이터를 복사하는 코드를 작성합니다. 이 접근 방법은 [Reporting Services WMI 공급자 액세스](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md)를 참조하세요.  
  
-   항목 수가 적은 경우 보고서, 보고서 모델 및 공유 데이터 원본을 보고서 디자이너, 모델 디자이너 및 보고서 작성기에서 새 보고서 서버로 다시 게시할 수 있습니다. 이 경우 역할 할당, 구독, 공유 일정, 보고서 스냅숏 일정, 보고서 또는 기타 항목에서 설정한 사용자 지정 속성, 모델 항목 보안 및 보고서 서버에서 설정한 속성을 다시 만들어야 합니다. 보고서 기록 및 보고서 실행 로그 데이터는 손실됩니다.  
  
##  <a name="bkmk_before_you_start"></a> 시작하기 전에  
 설치를 업그레이드하는 것이 아니라 마이그레이션하는 경우에도 기존 설치에서 업그레이드 관리자를 실행하여 마이그레이션에 영향을 미칠 수 있는 모든 문제를 쉽게 파악할 수 있습니다. 이러한 단계는 특히 본인이 설치하거나 구성하지 않은 보고서 서버를 마이그레이션하는 경우에 유용합니다. 업그레이드 관리자를 실행하면 새 SQL Server 설치에서 지원되지 않는 사용자 지정 설정을 찾을 수 있습니다.  
  
 또한 설치를 마이그레이션하는 방법에 영향을 줄 수 있는 SQL Server Reporting Services의 몇 가지 주요 변경 내용에 대해서도 알아야 합니다.
 
- 새 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 에서는 보고서 관리자가 대체됩니다.
  
- [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]이상에서는 IIS가 더 이상 필수 구성 요소가 아닙니다. 보고서 서버 설치를 새 컴퓨터로 마이그레이션하는 경우 웹 서버 역할을 추가할 필요가 없습니다. 또한 URL과 인증을 구성하는 단계는 물론, 문제를 진단하고 해결하는 기법과 도구도 이전 릴리스와 다릅니다.  
  
- 보고서 서버 웹 서비스, [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]및 보고서 서버 Windows 서비스는 동일한 계정으로 실행됩니다. 모두 RSReportServer.config 파일에서 구성 설정을 읽습니다. 
  
- [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 와 SQL Server Management Studio가 기능이 중복되지 않도록 다시 디자인되었습니다. 각 도구는 별도의 작업 집합을 지원합니다.
  
- ISAPI 필터는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 이상 버전에서 지원되지 않습니다. ISAPI 필터를 사용하는 경우 마이그레이션 전에 보고 솔루션을 다시 디자인해야 합니다.  
  
- IP 주소 제한은 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 이상 버전에서 지원되지 않습니다. IP 주소 제한을 사용할 경우 마이그레이션 전에 보고 솔루션을 다시 디자인하거나 방화벽, 라우터 또는 NAT(네트워크 주소 변환)와 같은 기술을 사용하여 보고서 서버에 액세스할 수 없도록 제한된 주소를 구성해야 합니다.  
  
- 클라이언트 SSL(Secure Sockets Layer) 인증서는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 이상 버전에서 지원되지 않습니다. 클라이언트 SSL 인증서를 사용하는 경우 마이그레이션 전에 보고 솔루션을 다시 디자인해야 합니다.  
  
- Windows 통합 인증 이외의 인증 유형을 사용할 경우 `<AuthenticationTypes>` RSReportServer.config **파일의** 요소를 지원되는 인증 유형으로 업데이트해야 합니다. 지원되는 인증 유형은 NTLM, Kerberos, 협상 및 기본 인증입니다. 익명, .NET Passport 및 다이제스트 인증은 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 이상 버전에서 지원되지 않습니다.  
  
- 보고 환경에서 사용자 지정 CSS 스타일시트 파일을 사용할 경우 이 파일이 마이그레이션되지 않습니다. 이 파일은 마이그레이션 후에 수동으로 이동해야 합니다.  
  
SQL Server Reporting Services의 변경 내용에 대한 자세한 내용은 업그레이드 관리자 설명서 및 [Reporting Services의 새로운 기능 ](../../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)을 참조하세요.  

## <a name="bkmk_backup"></a> 파일 및 데이터 백업

 새 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]인스턴스를 설치하기 전에 현재 설치의 모든 파일을 백업하십시오.  
  
1.  보고서 서버 데이터베이스에 대한 암호화 키를 백업합니다. 이 단계는 성공적인 마이그레이션을 위해 매우 중요합니다. 나중에 마이그레이션 프로세스에서 보고서 서버가 암호화된 데이터에 다시 액세스할 수 있도록 이 키를 복원해야 하기 때문입니다. 키를 백업하려면 Reporting Services 구성 관리자를 사용합니다.  
  
2.  지원되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 백업 방법을 사용하여 보고서 데이터베이스를 백업합니다. 자세한 내용은 [다른 컴퓨터로 보고서 서버 데이터베이스 이동&#40;SSRS 기본 모드&#41;](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md)에 설명된 보고서 서버 데이터베이스 백업 방법에 대한 지침을 참조하세요.  
  
3.  보고서 서버 구성 파일을 백업합니다. 백업할 파일에는 다음이 포함됩니다.  
  
    1.  RSReportServer.config  
  
    2.  Rswebapplication.config  
  
    3.  Rssvrpolicy.config  
  
    4.  Rsmgrpolicy.config  
  
    5.  Reportingservicesservice.exe.config  
  
    6.  보고서 서버 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 응용 프로그램용 Web.cofig  
  
    7.  [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 용 Machine.config(보고서 서버 작업을 위해 이 파일을 수정한 경우)  

## <a name="bkmk_install_ssrs"></a> SQL Server Reporting Services 설치

 새 보고서 서버 인스턴스를 기본값 이외의 값을 사용하여 구성할 수 있도록 파일만 모드로 설치합니다. 명령줄 설치의 경우에는 **FilesOnly** 인수를 사용합니다. 설치 마법사에서 **구성 없이 설치**옵션을 선택합니다.  
  
 새 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]인스턴스를 설치하는 방법에 대한 지침을 보려면 다음 링크 중 하나를 클릭하십시오.  
  
-   [설치 마법사에서 SQL Server 2016 설치&#40;설치 프로그램&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)  
  
-   [명령 프롬프트에서 SQL Server 2016 설치](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  

## <a name="bkmk_move_database"></a> 보고서 서버 데이터베이스 이동

 보고서 서버 데이터베이스에는 게시된 보고서, 모델, 공유 데이터 원본, 일정, 리소스, 구독 및 폴더가 포함됩니다. 또한 보고서 서버 내용에 대한 액세스 권한과 시스템 및 항목 속성도 포함됩니다.  
  
 다른 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 마이그레이션에 사용하는 경우에는 보고서 서버 데이터베이스를 새 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스로 이동해야 합니다. 동일한 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 사용하는 경우 [사용자 지정 어셈블리 또는 확장 프로그램 이동](#bkmk_move_custom)섹션으로 건너뜁니다.  
  
 보고서 서버 데이터베이스를 이동하려면 다음을 수행하십시오.  
  
1.  사용할 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 선택합니다. SQL Server Reporting Services에서 보고서 서버 데이터베이스를 호스트하려면 다음 버전 중 하나를 사용해야 합니다.  
  
    -   SQL Server 2016  
  
    -   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
    -   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
    -   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
    -   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
2.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 시작하고 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
3.  **에서 보고서 서버 데이터베이스를 호스트한 적이 없는 경우에는 시스템 데이터베이스에** RSExecRole [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 만듭니다. 자세한 내용은 [RSExecRole 만들기](../../reporting-services/security/create-the-rsexecrole.md)를 참조하세요.  
  
4.  [다른 컴퓨터로 보고서 서버 데이터베이스 이동&#40;SSRS 기본 모드&#41;](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md)의 지침을 따릅니다.  
  
 보고서 서버 데이터베이스와 임시 데이터베이스는 상호 종속적이므로 함께 이동해야 합니다. 데이터베이스를 복사할 경우 모든 보안 설정이 새 설치로 옮겨지지 않으므로 데이터베이스를 복사하지 마십시오. 예약된 보고서 서버 작업에 해당하는 SQL Server 에이전트 작업은 이동하지 마십시오. 이러한 작업은 보고서 서버가 자동으로 다시 만듭니다.  

## <a name="bkmk_move_custom"></a> 사용자 지정 어셈블리 또는 확장 프로그램 이동

 설치에 사용자 지정 보고서 항목, 어셈블리 또는 확장 프로그램이 포함되어 있는 경우에는 이러한 사용자 지정 구성 요소를 다시 배포해야 합니다. 사용자 지정 구성 요소를 사용하고 있지 않은 경우에는 [보고서 서버 구성](#bkmk_configure_reportserver)섹션으로 건너뛰십시오.  
  
 사용자 지정 구성 요소를 다시 배포하려면 다음을 수행하십시오.  
  
1.  어셈블리가 지원되거나 어셈블리를 다시 컴파일해야 하는지 확인합니다.

    -  사용자 지정 보안 확장 프로그램은 [IAuthenticationExtension2](https://msdn.microsoft.com/library/microsoft.reportingservices.interfaces.iauthenticationextension2.aspx) 인터페이스를 사용하여 다시 작성 해야 합니다.
  
    -   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에 대한 사용자 지정 렌더링 확장 프로그램은 ROM(렌더링 개체 모델)을 사용하여 다시 작성해야 합니다.  
  
    -   HTML 3.2 및 HTML OWC 렌더러는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 이상 버전에서 지원되지 않습니다.  
  
    -   다른 사용자 지정 어셈블리는 다시 컴파일할 필요가 없습니다.  
  
2.  어셈블ㄹ를 새 보고서 서버 \bin 폴더로 이동합니다. SQL Server에서 보고서 서버 이진 파일은 기본 보고서 서버 인스턴스의 경우 다음 위치에 있습니다.  
  
     `\Program files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer\bin`  
  
3.  구성 파일을 수정하여 사용자 지정 구성 요소에 대한 항목을 추가합니다. 항목은 사용 중인 어셈블리의 유형에 따라 달라집니다. 파일을 저장하고 구성 항목을 추가하는 위치에 대한 자세한 내용은 다음을 참조하십시오.  
  
    1.  [사용자 지정 어셈블리 배포](../../reporting-services/custom-assemblies/deploying-a-custom-assembly.md)  
  
    2.  [방법: 사용자 지정 보고서 항목 배포](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
    3.  [데이터 처리 확장 프로그램 배포](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)  
  
    4.  [배달 확장 프로그램 배포](../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)  
  
    5.  [렌더링 확장 프로그램 배포](../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
    6.  [보안 확장 프로그램 구현](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)  

## <a name="bkmk_configure_reportserver"></a> 보고서 서버 구성

 보고서 서버 웹 서비스 및 웹 포털의 URL을 구성하고 보고서 서버 데이터베이스에 대한 연결을 구성합니다.  
  
 스케일 아웃 배포를 마이그레이션하는 경우 모든 보고서 서버 노드를 오프라인으로 만들고 각 서버를 한 번에 하나씩 마이그레이션해야 합니다. 마이그레이션된 첫 번째 보고서 서버가 보고서 서버 데이터베이스에 성공적으로 연결되면 보고서 서버 데이터베이스 버전이 SQL Server 데이터베이스 버전으로 자동 업그레이드됩니다.  
  
> [!IMPORTANT]  
>  스케일 아웃 배포에 있는 보고서 서버 중 일부가 온라인이고 마이그레이션되지 않은 경우 업그레이드된 버전에 연결하면 이전 스키마가 사용되어 rsInvalidReportServerDatabase 예외가 발생할 수 있습니다.  
  
> [!NOTE]  
>  마이그레이션한 보고서 서버가 스케일 아웃 배포를 위한 공유 데이터베이스로 구성된 경우에는 보고서 서버 서비스를 구성하기 전에 **ReportServer** 데이터베이스의 **Keys** 테이블에서 이전 암호화 키를 삭제해야 합니다. 키를 제거하지 않으면 마이그레이션된 보고서 서버가 스케일 아웃 배포 모드에서 초기화됩니다. 자세한 내용은 [확장 배포의 암호화 키 추가 및 제거&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md) 및 [암호화 키 구성 및 관리&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)를 참조하세요.  
>   
>  확장 키는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 삭제할 수 없습니다. SQL Server Management Studio를 사용하여 **Keys** 데이터베이스의 **ReportServer** 테이블에서 이전 키를 삭제해야 합니다. Keys 테이블의 모든 행을 삭제합니다. 그러면 테이블이 지워지므로 다음 단계에서 설명하는 대로 대칭 키만 복원할 수 있습니다.  
>   
>  키를 삭제하기 전에 먼저 대칭 암호화 키를 백업하는 것이 좋습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 키를 백업할 수 있습니다. 구성 관리자를 열고 **암호화 키** 탭을 클릭한 다음 **백업** 단추를 클릭합니다. WMI 명령을 스크립팅하여 암호화 키를 백업할 수도 있습니다. WMI에 대한 자세한 내용은 [BackupEncryptionKey 메서드&#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-backupencryptionkey.md)을 참조하세요.  
  
1.  Reporting Services 구성 관리자를 시작하고 방금 설치한 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스에 연결합니다. 자세한 내용은 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)을 참조하세요.  
  
2.  보고서 서버와 웹 포털의 URL을 구성합니다. 자세한 내용은 [URL 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)을 참조하세요.  
  
3.  이전 설치에서 기존 보고서 서버 데이터베이스를 선택하여 보고서 서버 데이터베이스를 구성합니다. 구성을 성공적으로 마치면 보고서 서버 서비스가 다시 시작되고, 보고서 서버 데이터베이스에 대한 연결이 설정되면 데이터베이스가 SQL Server Reporting Services로 자동 업그레이드됩니다. 보고서 서버 데이터베이스를 만들거나 선택하는 데 사용하는 데이터베이스 변경 마법사를 실행하는 방법은 [기본 모드 보고서 서버 데이터베이스 만들기](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)를 참조하세요.  
  
4.  암호화 키를 복원합니다. 이 단계는 이미 보고서 서버 데이터베이스에 있는 기존의 연결 문자열 및 자격 증명에 해독 가능한 암호화를 설정하기 위해 필요합니다. 자세한 내용은 [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)을 참조하세요.  
  
5.  새 컴퓨터에 보고서 서버를 설치한 후 Windows 방화벽을 사용 중인 경우에는 보고서 서버가 수신하는 TCP 포트를 열어야 합니다. 기본값은 포트 80입니다. 자세한 내용은 [보고서 서버 액세스를 위한 방화벽 구성](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)을 참조하세요.  
  
6.  기본 모드 보고서 서버를 로컬로 관리하려는 경우 웹 포털에서 로컬 관리가 가능하도록 운영 체제를 구성해야 합니다. 자세한 내용은 [로컬 관리용으로 기본 모드 보고서 서버 구성](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)을 참조하세요.  

## <a name="bkmk_copy_custom_config"></a> RSReportServer.config 파일에 사용자 지정 구성 설정 복사

이전 설치에서 RSReportServer.config 파일 또는 RSWebApplication.config 파일을 수정한 경우 새 RSReportServer.config 파일도 동일하게 수정해야 합니다. 다음 목록에서는 이전 구성 파일을 수정하게 되는 이유를 간략히 설명하며, SQL Server 2016에서 동일한 설정을 구성하는 방법에 대한 추가 정보 링크도 제공합니다.  
  
|사용자 지정|정보|  
|-------------------|-----------------|  
|사용자 지정 설정으로 보고서 서버 전자 메일 배달|[전자 메일 설정 - Reporting Services 기본 모드](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md).|  
|장치 정보 설정|[RSReportServer.Config의 렌더링 확장 프로그램 매개 변수 사용자 지정](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)|

## <a name="bkmk_windowsservice_group"></a> Windows 서비스 그룹 및 보안 ACL

 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]에 있는 유일한 서비스 그룹인 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Windows 서비스 그룹은 SQL Server Reporting Services에 설치된 모든 레지스트리 키, 파일 및 폴더에 대한 보안 ACL을 만드는 데 사용됩니다. 이 Windows 그룹 이름은 SQLServerReportServerUser$\<*computer_name*>$\<*instance_name*> 형식으로 표시됩니다.  

## <a name="bkmk_verify"></a> 배포 확인

1.  브라우저를 열고 URL 주소를 입력하여 보고서 서버 및 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 가상 디렉터리를 테스트해 봅니다. 자세한 내용은 [Reporting Services 설치 확인](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)을 참조하세요.  
  
2.  보고서를 테스트하고 해당 보고서에 원하는 데이터가 포함되어 있는지 확인합니다. 데이터 원본 정보를 검토하여 데이터 원본 연결 정보가 지정되어 있는지 확인합니다. 보고서 서버는 보고서 개체 모델을 사용하여 보고서를 처리하고 렌더링하지만 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 또는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 구문을 새 보고서 정의 언어 요소로 대체하지 않습니다. 기존 보고서가 새 버전의 보고서 서버에서 실행되는 방식에 대한 자세한 내용은 [보고서 업그레이드](../../reporting-services/install-windows/upgrade-reports.md)를 참조하세요.  

## <a name="bkmk_remove_unused"></a> 사용하지 않는 프로그램 및 파일 제거

보고서 서버를 새로운 인스턴스로 마이그레이션하고 나면 다음 단계를 수행하여 더 이상 필요하지 않은 프로그램 및 파일을 제거할 수 있습니다.  
  
1.  이전 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 가 더 이상 필요하지 않은 경우 제거합니다. 이 단계에서는 다음 항목들이 삭제되지 않지만 더 이상 필요하지 않은 경우 이를 수동으로 제거할 수 있습니다.  
  
    -   오래된 보고서 서버 데이터베이스  
  
    -   RsExec 역할  
  
    -   보고서 서버 서비스 계정  
  
    -   보고서 서버 웹 서비스에 대한 응용 프로그램 풀  
  
    -   보고서 관리자 및 보고서 서버에 대한 가상 디렉터리  
  
    -   보고서 서버 로그 파일  
  
2.  이 컴퓨터에서 IIS가 더 이상 필요하지 않은 경우 제거합니다.

## <a name="next-steps"></a>다음 단계

[Reporting Services 설치 마이그레이션](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md)   
[보고서 서버 데이터베이스](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
[Reporting Services 업그레이드 및 마이그레이션](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
[Reporting Services의 이전 버전과의 호환성](../../reporting-services/reporting-services-backward-compatibility.md)   
[Reporting Services 구성 관리자](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
