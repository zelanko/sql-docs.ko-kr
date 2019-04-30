---
title: Reporting Services 구성 파일 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- deploying [Reporting Services], configuration files
- configuration options [Reporting Services]
- modifying configuration files
- configuration files [Reporting Services]
ms.assetid: 21e5c32f-ad67-4917-b55a-8e21bd64f5a6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 63d2dff214ed1125450ec319dff4ad7f7dc36990
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63190901"
---
# <a name="reporting-services-configuration-files"></a>Reporting Services 구성 파일
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 설치 중에 파일 시스템으로 복사되는 구성 파일과 레지스트리에 구성 요소 정보를 저장합니다. 구성 파일에는 내부 전용 값과 사용자 정의 값의 조합이 들어 있습니다. 사용자 정의 값은 설치 프로그램, 구성 도구, 명령줄 유틸리티를 통해 지정하거나 구성 파일을 수동으로 편집하여 지정합니다.  
  
 고급 설정을 추가하거나 구성하는 경우에만 구성 파일을 수정해야 합니다. 구성 설정은 XML 요소나 특성으로 지정됩니다. XML과 구성 파일에 대해 이해하고 있으면 텍스트나 코드 편집기를 사용하여 사용자 정의 가능한 설정을 수정할 수 있습니다. 구성 파일을 수정하는 방법 또는 보고서 서버가 새 구성 설정/업데이트된 구성 설정을 읽는 방법에 대한 자세한 내용은 [Reporting Services 구성 파일 수정&#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md)를 참조하세요.  
  
> [!NOTE]  
>  이전 버전에서 보고서 관리자에는 RSWebApplication.config라는 자체 구성 파일이 있었습니다. 이 파일은 이제 사용되지 않습니다. 이전 설치에서 업그레이드한 경우 이 파일이 삭제되지 않지만 보고서 서버가 해당 파일에서 설정을 읽지 않습니다. 파일이 컴퓨터에 있는 경우 삭제해야 합니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서 모든 보고서 관리자 구성 설정은 RSReportServer.config 파일에 저장되고 이 파일에서 읽힙니다. 삭제 또는 이동 된 설정 목록을 참조 하세요 [SQL Server 2014에서 SQL Server Reporting Services의 주요 변경 내용](../breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)합니다.  
  
 항목 내용  
  
-   [구성 파일의 요약(기본 모드)](#bkmk_config_file_Summary_native_mode)  
  
-   [구성 파일의 요약(SharePoint 모드)](#bkmk_config_file_Summary_sharepoint_mode)  
  
##  <a name="bkmk_config_file_Summary_native_mode"></a> 구성 파일의 요약(기본 모드)  
 다음 표에서는 구성 설정이 저장되는 위치에 대한 설명을 제공합니다. 대부분의 구성 설정은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 포함된 구성 파일에 저장됩니다. 기본적으로 설치 디렉터리는 다음과 같습니다.  
  
```  
C:\Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER  
```  
  
|저장 위치|Description|위치|  
|----------------|-----------------|--------------|  
|RSReportServer.config|보고서 서버 서비스의 기능 영역에 대 한 구성 설정을 저장합니다. 보고서 관리자, 보고서 서버 웹 서비스 및 백그라운드 처리 합니다. 각 설정에 대한 자세한 내용은 [RSReportServer Configuration File](rsreportserver-config-configuration-file.md)을 참조하세요.|\<Installation directory> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|서버 확장 프로그램에 대한 코드 액세스 보안 정책을 저장합니다. 이 파일에 대한 자세한 내용은 [Using Reporting Services Security Policy Files](../extensions/secure-development/using-reporting-services-security-policy-files.md)을 참조하세요.|\<Installation directory> \Reporting Services \ReportServer|  
|RSMgrPolicy.config|보고서 관리자에 대한 코드 액세스 보안 정책을 저장합니다. 이 파일에 대한 자세한 내용은 [Using Reporting Services Security Policy Files](../extensions/secure-development/using-reporting-services-security-policy-files.md)을 참조하세요.|\<Installation directory> \Reporting Services \ReportManager|  
|보고서 서버 웹 서비스용 Web.config|ASP.NET에 필요한 설정만 포함합니다.|\<Installation directory> \Reporting Services \ReportServer|  
|보고서 관리자용 Web.config|ASP.NET에 필요한 설정만 포함합니다.|\<Installation directory> \Reporting Services \ReportManager|  
|ReportingServicesService.exe.config|보고서 서버 서비스에 대한 추적 수준 및 로깅 옵션을 지정하는 구성 설정을 저장합니다. 이 파일의 요소에 대한 자세한 내용은 [ReportingServicesService Configuration File](reportingservicesservice-configuration-file.md)을 참조하세요.|\<Installation directory> \Reporting Services \ReportServer \Bin|  
|레지스트리 설정|Reporting Services 제거에 사용되는 구성 상태 및 기타 설정을 저장합니다. 설치 또는 구성 문제를 해결하는 경우 이러한 설정을 확인하여 보고서 서버가 구성된 방식에 대한 정보를 얻을 수 있습니다.<br /><br /> 설치가 무효화될 수 있으므로 이러한 설정을 직접 수정하지 마세요.|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<InstanceID\> \Setup<br /><br /> **-및-**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Services\ReportServer|  
|RSReportDesigner.config|보고서 디자이너에 대한 구성 설정을 저장합니다. 자세한 내용은 [RSReportDesigner Configuration File](rsreportdesigner-configuration-file.md)을 참조하세요.|\<drive>:\Program Files \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies.|  
|RSPreviewPolicy.config|보고서 미리 보기 중에 사용되는 서버 확장 프로그램에 대한 코드 액세스 보안 정책을 저장합니다. 이 파일에 대한 자세한 내용은 [Using Reporting Services Security Policy Files](../extensions/secure-development/using-reporting-services-security-policy-files.md)을 참조하세요.|C:\Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssembliesr|  
  
##  <a name="bkmk_config_file_Summary_sharepoint_mode"></a> 구성 파일의 요약(SharePoint 모드)  
 다음 표에서는 SharePoint 모드 보고서 서버에 사용되는 구성 파일에 대한 설명을 제공합니다. 대부분의 구성 설정은 SharePoint 서비스 애플리케이션 데이터베이스에 저장됩니다. 자세한 내용은 [Reporting Services SharePoint Service 및 서비스 애플리케이션](../reporting-services-sharepoint-service-and-service-applications.md)을 참조하세요.  
  
 기본적으로 SharePoint 모드의 설치 디렉터리는 다음과 같습니다.  
  
```  
C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting  
```  
  
|저장 위치|Description|위치|  
|----------------|-----------------|--------------|  
|RSReportServer.config|보고서 서버 서비스의 기능 영역에 대 한 구성 설정을 저장합니다. 보고서 관리자, 보고서 서버 웹 서비스 및 백그라운드 처리 합니다. 각 설정에 대한 자세한 내용은 [RSReportServer Configuration File](rsreportserver-config-configuration-file.md)을 참조하세요.|\<Installation directory> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|서버 확장 프로그램에 대한 코드 액세스 보안 정책을 저장합니다. 이 파일에 대한 자세한 내용은 [Using Reporting Services Security Policy Files](../extensions/secure-development/using-reporting-services-security-policy-files.md)을 참조하세요.|\<Installation directory> \Reporting Services \ReportServer|  
|보고서 서버 웹 서비스용 Web.config|ASP.NET에 필요한 설정만 포함합니다.|\<Installation directory> \Reporting Services \ReportServer|  
|레지스트리 설정|Reporting Services 제거에 사용되는 구성 상태 및 기타 설정을 저장합니다. 각 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션에 대한 정보도 저장합니다.<br /><br /> 설치가 무효화될 수 있으므로 이러한 설정을 직접 수정하지 마세요.|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<InstanceID\> \Setup<br /><br /> 예제 인스턴스 ID: MSSQL12.MSSQLSERVER<br /><br /> **-및-**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Reporting Services\Service Applications|  
|RSReportDesigner.config|보고서 디자이너에 대한 구성 설정을 저장합니다. 자세한 내용은 [RSReportDesigner Configuration File](rsreportdesigner-configuration-file.md)을 참조하세요.|\<drive>:\Program Files \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies.|  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 보고서 서버&#40;기본 모드&#41;](reporting-services-report-server-native-mode.md)   
 [Reporting Services 확장 프로그램](../extensions/reporting-services-extensions.md)   
 [rsconfig 유틸리티&#40;SSRS&#41;](../tools/rsconfig-utility-ssrs.md)   
 [보고서 서버 서비스 시작 및 중지](start-and-stop-the-report-server-service.md)  
  
  
