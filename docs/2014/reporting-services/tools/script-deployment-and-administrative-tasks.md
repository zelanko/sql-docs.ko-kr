---
title: 배포 및 관리 작업 스크립팅 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- scripts [Reporting Services]
- moving reports
- report servers [Reporting Services], duplicating settings
- deploying [Reporting Services], scripts
- copying report server settings
- administrative tasks [Reporting Services]
- duplicating report server environment
- migrating reports [Reporting Services]
- scripts [Reporting Services], deployments
- transferrng reports
- reports [Reporting Services], migrating
ms.assetid: d0416c9e-e3f9-456d-9870-2cfd2c49039b
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 6bf10f8ef0b748582aeef2e790207dcb287d3bdc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48167289"
---
# <a name="script-deployment-and-administrative-tasks"></a>배포 및 관리 태스크 스크립팅
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 스크립트를 사용하여 일반적인 설치, 배포 및 관리 태스크를 자동화할 수 있습니다. 보고서 서버를 배포하려면 여러 단계를 수행해야 합니다. 여러 가지 도구와 프로세스를 사용하여 배포를 구성해야 하며 모든 태스크를 자동화하는 데 사용할 수 있는 단일 프로그램이나 방법은 없습니다.  
  
 모든 단계가 자동화되는 것은 아닙니다. 일부 경우에는 단계를 수동으로 수행하거나 그래픽 도구를 통해 수행하는 것이 가장 간단하고 효과적인 방법입니다. 예를 들어 많은 보고서와 모델을 배포하려면 보고서 서버 환경을 다시 만드는 코드를 작성하는 것보다 보고서 서버 데이터베이스를 복사하는 것이 더 좋습니다.  
  
 일부 단계에서는 사용자 지정 코드가 필요합니다. 예를 들어 웹 서비스에 대한 URL과 보고서 관리자를 구성하는 단계를 자동화할 수 있지만 이렇게 하려면 보고서 서버 WMI(Windows Management Instrumentation) 공급자를 호출하는 사용자 지정 코드를 작성해야 합니다. 코드를 작성하지 않으려면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 사용하여 해당 단계를 수행해야 합니다.  
  
 보고서 서버를 구성하는 스크립트를 실행하려면 구성하는 컴퓨터의 로컬 관리자여야 합니다. 자세한 내용은 [원격 관리를 위한 보고서 서버 구성](../report-server/configure-a-report-server-for-remote-administration.md)을 참조하세요.  
  
 이 항목에서는 특정 단계를 자동화하는 권장 방법에 대해 설명합니다. 많은 프로그램 및 프로그래밍 인터페이스가 소개되어 있으며 이 항목의 뒷부분에서는 각 프로그램 및 인터페이스에 대해 설명합니다.  
  
## <a name="deployment-tasks-and-how-to-automate-them"></a>배포 태스크와 배포 태스크 자동화 방법  
 다음 표에서는 보고서 서버를 배포하는 데 필요한 설치 및 구성 태스크를 요약하여 보여 줍니다. 이 표에서 특정 태스크를 자동화하거나 무인 모드로 수행하는 데 사용할 수 있는 방법을 찾아 볼 수 있습니다.  
  
|태스크|방법|  
|----------|--------------|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]설치|명령줄에서 설치 프로그램을 실행하여 무인 설치를 수행할 수 있습니다.<br /><br /> 설치 프로그램을 사용하여 보고서 서버 설치와 구성을 모두 수행할 수 있지만 이렇게 하려면 기본 구성 옵션을 지정해야 하며 시스템이 해당 설치 유형의 요구 사항을 모두 만족해야 합니다. 기본 구성을 설치할 수 없는 경우에는 "파일만" 옵션으로 설치를 수행해야 합니다.|  
|서비스 계정 구성|서비스 계정은 설치 프로그램을 통해 처음 구성됩니다. 서비스 계정에 대한 변경을 설치 후 태스크로 자동화하려면 보고서 서버 WMI 공급자를 호출하는 사용자 지정 코드를 작성해야 합니다. 서비스 계정을 프로그래밍 방식으로 구성하기 위한 명령 프롬프트 유틸리티나 스크립트 템플릿은 없습니다.<br /><br /> 코딩 요구 사항 때문에 이 단계를 자동화할 수 없는 경우 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 실행하여 계정을 손쉽게 수동으로 구성할 수 있습니다. 자세한 내용은 [서비스 계정 구성&#40;SSRS Configuration Manager&#41;](../../sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)를 참조하세요.|  
|보고서 서버 웹 서비스 및 보고서 관리자 URL 구성|보고서 서버 WMI 공급자를 호출하는 사용자 지정 코드를 작성해야 합니다. URL을 구성하기 위한 명령줄 유틸리티나 스크립트 템플릿은 없습니다.<br /><br /> 코드를 작성하지 않으려면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 실행하여 URL을 수동으로 구성할 수 있습니다. 자세한 내용은 [URL 구성&#40;SSRS 구성 관리자&#41;](../install-windows/configure-a-url-ssrs-configuration-manager.md)을 참조하세요.|  
|보고서 서버 데이터베이스 만들기|보고서 서버 WMI 공급자를 호출하는 사용자 지정 코드를 작성해야 합니다. 보고서 서버 데이터베이스와 RSExecRole을 만들기 위한 명령 프롬프트 유틸리티나 스크립트 템플릿은 없습니다.<br /><br /> 코드를 작성하지 않으려면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 실행하여 데이터베이스를 수동으로 만들 수 있습니다. 자세한 내용은 [기본 모드 보고서 서버 데이터베이스 만들기&#40;SSRS Configuration Manager&#41;](../install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)를 참조하세요.|  
|보고서 서버 데이터베이스 연결 구성|연결 문자열, 계정이나 암호 또는 인증 유형을 변경하려면 **rsconfig** 유틸리티를 실행하여 연결을 구성합니다. 자세한 내용은 [보고서 서버 데이터베이스 연결 구성&#40;SSRS 구성 관리자&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md) 및 [rsconfig 유틸리티&#40;SSRS&#41;](rsconfig-utility-ssrs.md)를 참조하세요.<br /><br /> rsconfig.exe를 사용하여 데이터베이스를 만들거나 업그레이드할 수는 없습니다. 데이터베이스와 RSExecRole은 이미 있어야 합니다.|  
|스케일 아웃 배포 구성|다음 방법 중 하나를 사용하여 스케일 아웃 배포를 자동화할 수 있습니다.<br /><br /> rskeymgmt.exe 유틸리티를 실행하여 보고서 서버 인스턴스를 기존 설치에 추가합니다. 자세한 내용은 [스케일 아웃 배포의 암호화 키 추가 및 제거&#40;SSRS Configuration Manager&#41;](../install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)를 참조하세요.<br /><br /> 보고서 서버 WMI 공급자에 대해 실행되는 사용자 지정 코드를 작성합니다.|  
|암호화 키 백업|다음 방법 중 하나를 사용하여 암호화 키 백업을 자동화할 수 있습니다.<br /><br /> rskeymgmt.exe 유틸리티를 실행하여 키를 백업합니다. 자세한 내용은 [Back Up and Restore Reporting Services Encryption Keys](../install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)을 참조하세요.<br /><br /> 보고서 서버 WMI 공급자에 대해 실행되는 사용자 지정 코드를 작성합니다.|  
|보고서 서버 전자 메일 구성|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI 공급자에 대해 실행되는 사용자 지정 코드를 작성합니다. 이 공급자에서는 전자 메일 구성 설정의 하위 집합을 지원합니다.<br /><br /> RSReportServer.config 파일에 모든 설정이 포함되어 있지만 이 파일을 자동화 방법으로 사용하지 마십시오. 특히 배치 파일을 사용하여 파일을 다른 보고서 서버로 복사하지 마십시오. 각 구성 파일에는 현재 인스턴스와 관련된 값이 포함되어 있으며 이러한 값은 다른 보고서 서버 인스턴스에서 유효하지 않습니다.<br /><br /> 설정에 대 한 자세한 내용은 참조 하세요. [전자 메일 배달을 위한 보고서 서버 구성 &#40;SSRS 구성 관리자&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)합니다.|  
|무인 실행 계정을 구성합니다.|다음 방법 중 하나를 사용하여 무인 처리 계정 구성을 자동화할 수 있습니다.<br /><br /> rsconfig.exe 유틸리티를 실행하여 계정을 구성합니다. 자세한 내용은 [무인 실행 계정 구성&#40;SSRS 구성 관리자&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)을 참조하세요.<br /><br /> 보고서 서버 WMI 공급자를 호출하는 사용자 지정 코드를 작성합니다.|  
|폴더 계층, 역할 할당, 보고서, 구독, 일정, 데이터 원본 및 리소스를 비롯한 다른 보고서 서버의 기존 내용 배포|기존 보고서 서버 환경을 다시 만드는 가장 좋은 방법은 보고서 서버 데이터베이스를 새 보고서 서버 인스턴스에 복사하는 것입니다.<br /><br /> 또는 기존 보고서 서버 내용을 프로그래밍 방식으로 다시 만드는 사용자 지정 코드를 작성할 수 있습니다. 그러나 구독, 보고서 스냅숏 및 보고서 기록은 프로그래밍 방식으로 다시 만들 수 없습니다.<br /><br /> 일부 경우에는 이 두 가지 방법을 함께 사용하여 배포하는 것이 유용할 수 있습니다. 즉, 보고서 서버 데이터베이스를 복원한 다음 특정 설치에 맞게 보고서 서버 데이터베이스를 수정할 수 있습니다.<br /><br /> 자세한 예는 [보고서 서버 간 콘텐츠 마이그레이션을 위한 예제 Reporting Services rs.exe](sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)를 참조하세요.<br /><br /> 보고서 서버 데이터베이스를 재배치하는 방법은 [다른 컴퓨터로 보고서 서버 데이터베이스 이동&#40;SSRS 기본 모드&#41;](../report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md)를 참조하세요. 보고서 서버 환경을 프로그래밍 방식으로 만드는 방법은 이 항목의 "스크립트를 사용하여 보고서 서버 내용 및 폴더 마이그레이션" 섹션을 참조하십시오.|  
  
## <a name="tools-and-technologies-for-automating-server-deployment"></a>서버 배포를 자동화하기 위한 도구 및 기술  
 다음 목록에는 배포 및 유지 관리 태스크를 자동화하는 데 사용할 수 있는 프로그램과 인터페이스가 요약되어 있습니다.  
  
-   설치 프로그램을 무인 모드에서 실행하면 보고서 서버 구성 요소를 설치하고 일부 경우에는 구성도 할 수 있습니다. 설치 프로그램에서 보고서 서버 인스턴스를 구성하도록 하려면 파일만 설치 옵션을 사용해야 합니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI 공급자와 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 명령줄 유틸리티를 사용하면 로컬 및 원격 서버를 구성할 수 있습니다.  
  
     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI 공급자에서는 서비스 계정 지정, URL 구성, 보고서 서버 데이터베이스 생성 및 구성, 메일 배달을 위한 보고서 서버 구성 등을 포함하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치의 모든 측면을 구성할 수 있는 클래스, 속성 및 메서드를 노출합니다. WMI 공급자를 사용하려면 사용자 지정 코드나 스크립트를 작성해야 합니다. 자세한 내용은 [Reporting Services WMI 공급자 액세스](access-the-reporting-services-wmi-provider.md)를 참조하세요.  
  
     코드를 작성하는 대신 명령줄 유틸리티인 rsconfig.exe와 rskeymgmt.exe를 사용할 수도 있습니다. 유틸리티를 실행하는 배치 파일을 만들 수도 있습니다. 이러한 유틸리티를 사용하면 일부 구성 작업을 자동화할 수 있지만 모든 구성 태스크를 자동화할 수 있는 것은 아닙니다.  
  
-   보고서 서버 스크립트 호스트 도구(rs.exe)에서는 보고서 서버의 내용을 다시 만들거나 한 보고서 서버의 기존 내용을 다른 보고서 서버로 이동하도록 작성한 사용자 지정 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 코드를 실행할 수 있습니다. 이 방법을 사용하면 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]에서 스크립트를 만들고 이를 .rss 파일로 저장한 후 대상 보고서 서버에서 rs.exe를 사용하여 해당 스크립트를 실행할 수 있습니다. 작성하는 스크립트는 보고서 서버 웹 서비스에 대한 SOAP 인터페이스를 호출할 수 있습니다. 이 방법을 사용하면 보고서 서버 폴더 네임스페이스 및 내용을 다시 만들고 역할 기반 보안을 다시 만들 수 있으므로 배포 스크립트는 이 방법을 사용하여 작성합니다.  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 릴리스에서는 SharePoint 통합 모드에 대한 PowerShell cmdlet이 도입되었습니다. PowerShell을 사용하면 SharePoint 통합을 구성하고 관리할 수 있습니다.  자세한 내용은 [Reporting Services SharePoint 모드용 PowerShell cmdlet](../powershell-cmdlets-for-reporting-services-sharepoint-mode.md)합니다.  
  
## <a name="use-scripts-to-migrate-report-server-content-and-folders"></a>스크립트를 사용하여 보고서 서버 내용 및 폴더 마이그레이션  
 다른 보고서 서버 인스턴스의 보고서 서버 환경을 복제하는 스크립트를 작성할 수 있습니다. 배포 스크립트는 일반적으로 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 으로 작성한 다음 보고서 서버 스크립트 호스트 유틸리티를 사용하여 처리합니다.  
  
 자세한 예는 [보고서 서버 간 콘텐츠 마이그레이션을 위한 예제 Reporting Services rs.exe](sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)를 참조하세요.  
  
 스크립트를 사용하여 한 서버의 폴더, 공유 데이터 원본, 리소스, 보고서, 역할 할당 및 설정을 다른 서버로 복사할 수 있습니다. 하나의 보고서 서버 인스턴스에 대해 스크립트를 작성한 다음 이를 다른 서버에서 실행하여 보고서 서버 네임스페이스를 다시 만듭니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 배포에 여러 보고서 서버가 있는 경우 각 서버에서 개별적으로 스크립트를 실행하여 모든 서버를 동일한 방법으로 구성할 수 있습니다.  
  
 다음 목록에서는 서버 간 보고서 마이그레이션 단계에 대해 설명합니다.  
  
1.  스크립트 변수를 원본 보고서 서버의 URL로 설정합니다.  
  
2.  <xref:ReportService2010.ReportingService2010.GetItemDefinition%2A> 및 <xref:ReportService2010.ReportingService2010.GetProperties%2A> 메서드를 사용하여 보고서 정의 및 보고서 속성을 검색합니다.  
  
3.  URL이 대상 서버를 가리키도록 설정합니다.  
  
4.  <xref:ReportService2010.ReportingService2010.CreateCatalogItem%2A> 메서드를 사용하여 <xref:ReportService2010.ReportingService2010.GetProperties%2A>에서 반환한 속성 및 <xref:ReportService2010.ReportingService2010.GetItemDefinition%2A>에서 반환한 보고서 정의를 전달합니다.  
  
 가져오기 및 만들기 방법을 조합하여 설정, 폴더, 공유 데이터 원본 및 리소스를 마이그레이션하는 것과 유사한 단계를 수행할 수 있습니다. 사용 가능한 메서드에 대한 자세한 내용은 [기술 참조&#40;SSRS&#41;](../technical-reference-ssrs.md)를 참조하세요.  
  
> [!NOTE]  
>  자격 증명을 명시적으로 설정하지 않는 한 스크립트는 해당 스크립트를 실행하는 사용자의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 자격 증명으로 실행됩니다.  
  
 서식을 지정 하 고 스크립트 파일을 실행 하는 방법에 대 한 자세한 내용은 참조 하세요. [유틸리티 및 웹 서비스는 rs.exe를 사용 하 여 스크립트](script-with-the-rs-exe-utility-and-the-web-service.md)합니다.  
  
## <a name="using-scripts-to-set-server-properties"></a>스크립트를 사용하여 서버 속성 설정  
 보고서 서버의 시스템 속성을 설정하는 스크립트를 작성할 수 있습니다. 다음 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET 스크립트에서는 속성을 설정하는 한 가지 방법을 보여 줍니다. 이 예에서는 RSClientPrint ActiveX 컨트롤을 사용 하지 않도록 설정 하지만 바꿀 수 있습니다 `EnableClientPrinting` 고 `False` 다른 유효한 속성 이름 및 값을 사용 하 여 합니다. 서버 속성의 전체 목록을 참조 하십시오 [보고서 서버 시스템 속성](../report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)합니다.  
  
 스크립트를 사용하려면 .rss 확장명을 가진 파일로 저장한 다음 rs.exe 명령 프롬프트 유틸리티를 사용하여 보고서 서버에서 해당 파일을 실행합니다. 스크립트는 컴파일되지 않으므로 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]을 설치할 필요는 없습니다. 이 예에서는 보고서 서버를 호스팅하는 로컬 컴퓨터에 대한 권한이 사용자에게 있다고 가정합니다. 권한을 가진 계정으로 로그온하지 않은 경우, 추가 명령줄 인수를 통해 계정 정보를 지정해야 합니다. 자세한 내용은 [RS.exe 유틸리티&#40;SSRS&#41;](rs-exe-utility-ssrs.md)를 참조하세요.  
  
> [!TIP]  
>  자세한 예는 [보고서 서버 간 콘텐츠 마이그레이션을 위한 예제 Reporting Services rs.exe](sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)를 참조하세요.  
  
```  
Public Sub Main()  
        Dim props(0) As [Property]  
        Dim setProp As New [Property]  
        setProp.Name = "EnableClientPrinting"  
        setProp.Value = “False”   
        props(0) = setProp  
        Try  
            rs.SetSystemProperties(props)  
        Catch ex As System.Web.Services.Protocols.SoapException  
            Console.Write(ex.Detail.InnerXml)  
        Catch e as Exception  
            Console.Write(e.Message)  
        End Try  
End Sub  
```  
  
## <a name="see-also"></a>관련 항목  
 [GenerateDatabaseCreationScript 메서드 &#40;WMI MSReportServer_ConfigurationSetting&#41;](../wmi-provider-library-reference/configurationsetting-method-generatedatabasecreationscript.md)   
 [GenerateDatabaseRightsScript 메서드 &#40;WMI MSReportServer_ConfigurationSetting&#41;](../wmi-provider-library-reference/configurationsetting-method-generatedatabaserightsscript.md)   
 [GenerateDatabaseUpgradeScript 메서드 &#40;WMI MSReportServer_ConfigurationSetting&#41;](../wmi-provider-library-reference/configurationsetting-method-generatedatabaseupgradescript.md)   
 [명령 프롬프트에서 SQL Server 2014 설치](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
 [Reporting Services 기본 모드 보고서 서버 설치](../install-windows/install-reporting-services-native-mode-report-server.md)   
 [Reporting Services 보고서 서버&#40;기본 모드&#41;](../report-server/reporting-services-report-server-native-mode.md)   
 [보고서 서버 명령 프롬프트 유틸리티 &#40;SSRS&#41;](report-server-command-prompt-utilities-ssrs.md)   
 [Reporting Services 및 파워 뷰 브라우저 지원 계획 &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)   
 [Reporting Services 도구](reporting-services-tools.md)  
  
  
