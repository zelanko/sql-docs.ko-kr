---
title: Reporting Services 구성 파일 | Microsoft Docs
ms.date: 05/30/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- deploying [Reporting Services], configuration files
- configuration options [Reporting Services]
- modifying configuration files
- configuration files [Reporting Services]
ms.assetid: 21e5c32f-ad67-4917-b55a-8e21bd64f5a6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 25b695456bbac34e2c6ce8bf8c312c4108dd852e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66506649"
---
# <a name="reporting-services-configuration-files"></a>Reporting Services 구성 파일
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 설치 중에 파일 시스템으로 복사되는 구성 파일과 레지스트리에 구성 요소 정보를 저장합니다. 구성 파일에는 내부 전용 값과 사용자 정의 값의 조합이 들어 있습니다. 사용자 정의 값은 설치 프로그램, 구성 도구, 명령줄 유틸리티를 통해 지정하거나 구성 파일을 수동으로 편집하여 지정합니다.  
  
 고급 설정을 추가하거나 구성하는 경우에만 구성 파일을 수정해야 합니다. 구성 설정은 XML 요소나 특성으로 지정됩니다. XML과 구성 파일에 대해 이해하고 있으면 텍스트나 코드 편집기를 사용하여 사용자 정의 가능한 설정을 수정할 수 있습니다. 구성 파일을 수정하는 방법 또는 보고서 서버가 새 구성 설정/업데이트된 구성 설정을 읽는 방법에 대한 자세한 내용은 [Reporting Services 구성 파일 수정&#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)를 참조하세요.  
  
> [!NOTE]  
> 이전 버전에서 보고서 관리자에는 RSWebApplication.config라는 자체 구성 파일이 있었습니다. 이 파일은 이제 사용되지 않습니다. 이전 설치에서 업그레이드한 경우 이 파일이 삭제되지 않지만 보고서 서버가 해당 파일에서 설정을 읽지 않습니다. 파일이 컴퓨터에 있는 경우 삭제해야 합니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서 모든 보고서 관리자 및 웹 포털 구성 설정은 RSReportServer.config 파일에 저장되고 이 파일에서 읽힙니다. 삭제 또는 이동된 설정 목록을 검토하려면 [SQL Server 2016에서 SQL Server Reporting Services의 주요 변경 내용](../../reporting-services/breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)을 참조하세요.  
  
 이 문서의 내용  
  
-   [구성 파일의 요약(기본 모드)](#bkmk_config_file_Summary_native_mode)  
  
-   [구성 파일의 요약(SharePoint 모드)](#bkmk_config_file_Summary_sharepoint_mode)  
  
##  <a name="bkmk_config_file_Summary_native_mode"></a> 구성 파일의 요약(기본 모드)  
 다음 표에서는 구성 설정이 저장되는 위치에 대한 설명을 제공합니다. 대부분의 구성 설정은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 포함된 구성 파일에 저장됩니다. 기본적으로 설치 디렉터리는 다음과 같습니다.  
  
' ' 경로 설치 합니다.  
C:\Program Files\Microsoft SQL Server\MSRSxx.MSSQLSERVER (여기서 xx는 MS SQL 버전 번호) 또는  
C:\Program Files\Microsoft SQL Server Reporting Services\SSRS  
  SSRS 버전에 따라
```  
  
|Stored in:|Description|Location|  
|----------------|-----------------|--------------|  
|RSReportServer.config|Stores configuration settings for feature areas of the Report Server service: Report Manager or the web portal, the Report Server Web service, and background processing. For more information about each setting, see [RsReportServer.config Configuration File](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).|\<Installation directory> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|Stores the code access security policies for the server extensions. For more information about this file, see [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Installation directory> \Reporting Services \ReportServer|  
|RSMgrPolicy.config|Stores the code access security policies for the web portal. For more information about this file, see [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Installation directory> \Reporting Services \ReportManager|  
|Web.config for the Report Server Web service|Includes only those settings that are required for ASP.NET.|\<Installation directory> \Reporting Services \ReportServer|  
|Web.config for Report Manager|Includes only those settings that are required for ASP.NET if applicable for the SSRS version.|\<Installation directory> \Reporting Services \ReportManager|  
|ReportingServicesService.exe.config|Stores configuration settings that specify the trace levels and logging options for the Report Server service. For more information about the elements in this file, see [ReportingServicesService Configuration File](../../reporting-services/report-server/reportingservicesservice-configuration-file.md).|\<Installation directory> \Reporting Services \ReportServer \Bin|  
|Registry settings|Stores configuration state and other settings used to uninstall Reporting Services. If you are troubleshooting an installation or configuration problem, you can view these settings to get information about how the report server is configured.<br /><br /> Do not modify these settings directly as this can invalidate your installation.|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<InstanceID\> \Setup<br /><br /> **- And -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Services\ReportServer|  
|RSReportDesigner.config|Stores configuration settings for Report Designer. For more information, see [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md).|\<drive>:\Program Files \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies.|  
|RSPreviewPolicy.config|Stores the code access security policies for the server extensions used during report preview. For more information about this file, see [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|C:\Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssembliesr|  
  
##  <a name="bkmk_config_file_Summary_sharepoint_mode"></a> Summary of configuration Files (SharePoint mode)  
 The following table provides a description of configuration files used for a SharePoint mode report server. Most configuration settings are stored in SharePoint service application databases. For more information, see [Reporting Services SharePoint Service and Service Applications](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md).  
  
 By default, the installation directory for SharePoint mode is the following:  
  
```Install path
C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting  
```  
  
|저장 위치|설명|위치|  
|----------------|-----------------|--------------|  
|RSReportServer.config|보고서 서버 서비스의 기능 영역인 보고서 관리자 또는 웹 포털, 보고서 서버 웹 서비스 및 백그라운드 처리에 대한 구성 설정을 저장합니다. 각 설정에 대한 자세한 내용은 [RsReportServer.config 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)을 참조하세요.|\<Installation directory> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|서버 확장 프로그램에 대한 코드 액세스 보안 정책을 저장합니다. 이 파일에 대한 자세한 내용은 [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)을 참조하세요.|\<Installation directory> \Reporting Services \ReportServer|  
|보고서 서버 웹 서비스용 Web.config|SSRS 버전에 해당 하는 경우에 ASP.NET에 대 한 필요한 설정만을 포함 되어 있습니다.|\<Installation directory> \Reporting Services \ReportServer|  
|레지스트리 설정|Reporting Services 제거에 사용되는 구성 상태 및 기타 설정을 저장합니다. 각 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션에 대한 정보도 저장합니다.<br /><br /> 설치가 무효화될 수 있으므로 이러한 설정을 직접 수정하지 마세요.|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<InstanceID\> \Setup<br /><br /> 예제 인스턴스 ID: MSSQL13.MSSQLSERVER<br /><br /> **-및-**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Reporting Services\Service Applications|  
|RSReportDesigner.config|보고서 디자이너에 대한 구성 설정을 저장합니다. 자세한 내용은 [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)을 참조하세요.|\<drive>:\Program Files \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies.|  
  
## <a name="see-also"></a>관련 항목:  
 [Reporting Services 보고서 서버&#40;기본 모드&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Reporting Services 확장 프로그램](../../reporting-services/extensions/reporting-services-extensions.md)   
 [rsconfig 유틸리티&#40;SSRS&#41;](../../reporting-services/tools/rsconfig-utility-ssrs.md)   
 [보고서 서버 서비스 시작 및 중지](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)  
  
  
