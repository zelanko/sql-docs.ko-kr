---
title: 2014 SQL Server SQL Server Reporting Services의 주요 변경 내용 Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Me.Value references
- Reporting Services, backward compatibility
- breaking changes [Reporting Services]
ms.assetid: 39c7aafd-dcb9-4317-b8f7-d15828eb4f9a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0d86c9bb07a52aba0cd93b006fc33edf4d1aa885
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109927"
---
# <a name="breaking-changes-in-sql-server-reporting-services-in-sql-server-2014"></a>SQL Server 2014에서 SQL Server Reporting Services의 주요 변경 내용
  이 항목에서는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]의 주요 변경 내용에 대해 설명합니다. 이러한 변경 내용에 따라 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 기반을 둔 애플리케이션, 스크립트 또는 기능을 사용하지 못할 수도 있습니다. 이러한 문제는 업그레이드할 때나 사용자 지정 스크립트 또는 보고서에서 발생할 수 있습니다. 자세한 내용은 [Use Upgrade Advisor to Prepare for Upgrades](../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)을 참조하세요.  
  
 **항목 내용**  
  
-   [SQL Server 2014 Reporting Services 주요 변경 내용](#bkmk_sql14)  
  
-   [SQL Server 2012 Reporting Services의 주요 변경 내용](#bkmk_rc0)  
  
-   [SQL Server 2008 R2 Reporting Services의 주요 변경 내용](#bkmk_kj)  
  
##  <a name="sssql14-reporting-services-breaking-changes"></a><a name="bkmk_sql14"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Reporting Services 주요 변경 내용  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 에서 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]기능에는 주요 변경 내용이 없습니다.  
  
##  <a name="sssql11-reporting-services-breaking-changes"></a><a name="bkmk_rc0"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Reporting Services 주요 변경 내용  
  
### <a name="sharepoint-mode-server-references-require-the-sharepoint-site"></a>SharePoint 모드 서버 참조에 SharePoint 사이트가 필요함  
 URL 경로에 가상 디렉터리 이름을 사용하여 보고서 서버로 직접 이동하거나 보고서 서버를 직접 참조할 수 없습니다. 예를 들어:  
  
 `http://<Server name>/ReportServer`  
  
 이제 URL 경로에 SharePoint 사이트를 포함해야 합니다. 예를 들어 사이트 이름이 '`videos`'이 고 '`sites`' 접두사를 사용한 경우 URL은 다음과 유사 합니다.  
  
 `http://<Server Name>/sites/videos/_vti_bin/ReportServer`  
  
### <a name="changes-to-sharepoint-mode-command-line-installation"></a>SharePoint 모드 명령줄 설치에 대한 변경 내용  
 입력 설정 **/RSINSTALLMODE** 는 이제 기본 모드 설치에서만 작동하고 SharePoint 모드 설치에서는 작동하지 않습니다. 예를 들어 다음은 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] **/RSINSTALLMODE = "DefaultSharePointMode"** 에서 지원 되지 않습니다. 이 입력 설정 대신 **/RSSHPINSTALLMODE="DefaultSharePointMode"** 를 사용하십시오.  
  
 다음 문은 전체 설치 명령 및 매개 변수 집합의 예입니다. **setup/ACTION = install/FEATURES = SQL, RS/InstanceName = Denali_INST1 ..../RSSHPINSTALLMODE = "DefaultSharePointMode"**  
  
 명령줄 설치에 대 한 자세한 내용은 [Reporting Services SharePoint 모드 및 기본 모드의 명령 프롬프트 설치](install-windows/install-reporting-services-at-the-command-prompt.md)를 참조 하세요.  
  
### <a name="the-reporting-services-wmi-provider-no-longer-supports-configuration-of-sharepoint-mode"></a>Reporting Services WMI 공급자에서 더 이상 SharePoint 모드 구성을 지원하지 않음  
 이제 PowerShell cmdlet 및 SharePoint 중앙 관리를 사용하여 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 구성이 완료됩니다. 새 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 모드 아키텍처는 SharePoint 서비스 아키텍처를 활용합니다. SharePoint에서 WMI 인터페이스를 지원하지 않습니다.  
  
 다음은 이러한 변경으로 인해 영향을 받는 구성 요소 및 워크플로의 목록입니다.  
  
-   SharePoint 모드의 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 에 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] WMI 공급자를 사용하는 사용자 지정 애플리케이션  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 구성 관리자, rskeymgmt.exe 및 rsconfig.exe [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 모드 구성에 이러한 유틸리티를 사용하는 대신 SharePoint 중앙 관리 및 PowerShell을 사용합니다.  
  
-   SQL Server Management Studio: 고객은 <machine_name>/<instance_name>와 비슷한 구문을 사용 하 여 서버를 참조할 수 없습니다. [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 릴리스부터 권장되는 방법은 SharePoint 사이트 URL을 사용하는 것입니다. 예를 들어 **http://<sharepoint_server>/<sharePoint_site>** 합니다. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]부터는 SharePoint 사이트 URL이 지원되는 유일한 구문입니다.  
  
### <a name="report-model-designer-is-not-available-in-sql-server-data-tools"></a>보고서 모델 디자이너를 SQL Server Data Tools에서 사용할 수 없음  
 보고서 모델 프로젝트가 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 더 이상 지원되지 않습니다. 보고서 모델 디자이너는 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]에서 사용할 수 없습니다. [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 에서 새 보고서 모델 프로젝트를 만들거나 기존 프로젝트를 열 수 없으며, 보고서 모델을 만들거나 업데이트할 수 없습니다. 보고서 모델을 업데이트하려는 경우 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 또는 이전 도구를 사용할 수 있습니다. 보고서 작성기 및 보고서 디자이너와 같은 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 도구에서 승인된 보고서에서 보고서 모델을 데이터 원본으로 계속 사용할 수 있습니다. 보고서 모델에서 보고서 데이터를 추출하기 위해 쿼리를 만드는 데 사용하는 쿼리 디자이너는 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 계속 사용할 수 있습니다.  
  
##  <a name="sql-server-2008-r2-reporting-services-breaking-changes"></a><a name="bkmk_kj"></a>SQL Server 2008 R2 Reporting Services 주요 변경 내용  
 이 섹션에서는의 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]주요 변경 내용에 대해 설명 합니다.  
  
> [!NOTE]  
>  SQL Server 2008 R2는 SQL Server 2008의 부 버전 업그레이드이므로 SQL Server 2008 섹션의 내용도 검토하는 것이 좋습니다.  
  
### <a name="expanded-csv-data-renderer"></a>확장된 CSV 데이터 렌더러  
 에서 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]CSV 파일에는 차트 및 계기 데이터가 포함 되어 있습니다. 차트 및 계기 열의 추가로 인해 이전의 CSV 파일 구조에 기반한 애플리케이션은 더 이상 작동하지 않습니다.  
  
 자세한 내용은 [CSV 파일로 내보내기&#40;보고서 작성기 및 SSRS&#41;](report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md)에서 이 데이터로 작업할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2014의 SQL Server Reporting Services에 대 한 동작 변경 내용](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
 [새로운 기능 &#40;Reporting Services&#41;](what-s-new-reporting-services.md)   
 [SQL Server 2014의 SQL Server Reporting Services에서 사용 되지 않는 기능](deprecated-features-in-sql-server-reporting-services-ssrs.md)   
 [SQL Server 2014의 SQL Server Reporting Services에서 중단된 기능](discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)  
  
  
