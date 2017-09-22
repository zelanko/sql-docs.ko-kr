---
title: "보고서 디자인 및 보고서 배포 계획 | Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 09/12/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: 1c1e265e-52a2-4de3-96fd-ca4abae01c02
caps.latest.revision: 19
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 0a59b89b558922f27c91fb2452df157f7baa3918
ms.contentlocale: ko-kr
ms.lasthandoff: 09/21/2017

---
# <a name="plan-for-report-design-and-report-deployment--reporting-services"></a>보고서 디자인 및 보고서 배포 계획 | Reporting Services
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 에서는 페이지를 매긴 보고서를 여러 가지 방법으로 작성 및 배포할 수 있습니다. 보고서 제작 및 함께 작동하는 보고서 서버 환경을 계획하는 방법을 알아봅니다.

이 항목은 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 구성 요소에서 지원되는 보고서 정의에 대한 개요를 보여 줍니다. 보고서 정의는 RDL(Report Definition Language) 또는 RDLC(Report Definition Language for Clients)로 작성된 XML 파일입니다. 각 보고서 정의는 파일의 첫 부분에 나열되어 있는 특정 스키마 버전을 따릅니다.  
  
 RDL 파일은 [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] 프로젝트의 보고서 디자이너 및 보고서 작성기에서 작성됩니다. RDLC 파일은 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]에 포함된 ReportViewer 컨트롤을 사용해서 작성됩니다.
  
##  <a name="bkmk_rdl_schema_versions"></a> RDL 스키마 버전  
 다음 표에서는 사용 가능한 스키마 버전과 이 항목의 나머지 부분에서 사용되는 약어를 나열합니다.  
  
|약어|스키마 버전|  
|------------------|--------------------|  
|2016 RDL|`http://schemas.microsoft.com/sqlserver/reporting/2016/01/reportdefinition`|
|2010 RDL|`http://schemas.microsoft.com/sqlserver/reporting/2010/01/reportdefinition`|  
|2008 RDL|`http://schemas.microsoft.com/sqlserver/reporting/2008/01/reportdefinition`|  
|2005 RDL<br /><br /> 2005 RDLC|`http://schemas.microsoft.com/sqlserver/reporting/2005/01/reportdefinition`|  
|2000 RDL|`http://schemas.microsoft.com/sqlserver/reporting/2003/10/reportdefinition`|  
  
 RDL 및 RDL 스키마에 대한 자세한 내용은 다음을 참조하세요.  
  
-   [Microsoft SQL Server XML 스키마](http://go.microsoft.com/fwlink/?LinkId=31850)  
  
-   [보고서 정의 언어 사양](http://go.microsoft.com/fwlink/?linkid=116865)  
  
-   [RDL(Report Definition Language)&#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)  
  
 ReportViewer 컨트롤에 대한 자세한 내용은 [ReportViewer 컨트롤(Visual Studio)](http://msdn.microsoft.com/library/ms251671.aspx)을 참조하세요.  
  
##  <a name="bkmk_report_server_rdl_schema_support"></a> 보고서 서버 및 RDL 스키마 지원  
 다음과 같은 방법으로 보고서 정의 파일을 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 보고서 서버에 배포할 수 있습니다.  
  
-   **보고서 디자이너:** [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)]의 보고서 디자이너에서 보고서를 배포합니다.  
  
-   **보고서 작성기:** 보고서 작성기의 보고서 서버에 보고서를 저장합니다.  
  
-   **웹 포털:** [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]의 기본 모드 보고서 서버로 보고서를 업로드합니다.  
  
-   **SharePoint:** SharePoint 모드 보고서 서버로 구성된 SharePoint 사이트에 보고서를 업로드합니다.  
  
-   **프로그래밍 방식:** SOAP API 인터페이스를 사용해서 보고서 서버에 보고서를 프로그래밍 방식으로 게시합니다. 자세한 내용은 [Report Server Web Service](../reporting-services/report-server-web-service/report-server-web-service.md)을 참조하세요.  
  
 다음 표에서는 보고서 서버 버전별로 지원되는 rdl 스키마 버전을 보여 줍니다.  
  
|보고서 서버 버전|RDL 스키마 버전|  
|---------------------------|------------------------|  
|SQL Server 2016|2016 RDL<br /><br />2010 RDL<br /><br /> 2008 RDL<br /><br /> 2005 RDL<br /><br /> 2000 RDL
|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]<br /><br /> 또는<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]<br /><br /> 또는<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|2010 RDL<br /><br /> 2008 RDL<br /><br /> 2005 RDL<br /><br /> 2000 RDL|  
|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]|2008 RDL<br /><br /> 2005 RDL<br /><br /> 2000 RDL|  
  
 보고서 서버에 보고서 정의를 업로드하거나 기존 보고서가 포함된 보고서 서버를 업그레이드할 때 보고서 서버는 원래 형식으로 보고서 정의를 보존합니다. **처음 사용할 때**, 보고서 서버는 보고서 서버 데이터베이스의 보고서를 이후 검토를 위해 보존되는 이진 형식으로 업그레이드합니다. 보고서 정의(.rdl) 자체는 업그레이드되지 않습니다.  
  
 보고서 정의 파일(.rdl)의 읽기 전용 복사본을 보고서 서버에서 추출할 수 있습니다. 기본 모드 보고서 서버에서는 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]로 이동해서 보고서를 선택하고 **다운로드**를 클릭합니다. SharePoint 모드 배포에서는 문서 라이브러리로 이동해서 보고서를 선택하고 **복사본 다운로드**를 클릭합니다.  
  
 보고서 정의를 업그레이드하려면 보고서 제작 환경(예: SQL Server Data Tools 또는 보고서 작성기)에서 해당 보고서를 열고 저장해야 합니다.  
  
 보고서 업그레이드 및 지원되는 스키마 버전에 대한 자세한 내용은 [보고서 업그레이드](../reporting-services/install-windows/upgrade-reports.md)를 참조하세요.  
  
##  <a name="bkmk_report_authoring_and_deployment"></a> 보고서 제작 및 배포 지원  
 보고서 작성 환경은 [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] 프로젝트의 보고서 디자이너 및 보고서 작성기입니다. 보고서 제작 환경에서는 보고서 업그레이드, 보고서 디자인, 로컬 모드로 보고서 미리 보기, 보고서 서버에서 보고서 미리 보기 및 보고서 배포를 위한 다양한 지원 기능을 제공합니다.  
  
 다음 표에는 다양한 스키마 버전을 위한 보고서 정의 제작 및 배포에 대한 지원 기능이 요약되어 있습니다.  
  
|제작 환경|작성된 RDL 버전|배포 RDL 버전|보고서 서버에 배포 버전|  
|---------------------------|--------------------------|------------------------|--------------------------------------|  
|SQL Server 2016 보고서 작성기|Authors 2016 RDL<br /><br /> 이전 RDL 버전을 2016 RDL로 업그레이드합니다.|2016 RDL|SQL Server 2016|
|SQL Server 2016 Data Tools의 보고서 디자이너 - Microsoft Visual Studio 2015용 Business Intelligence|Authors 2016 RDL<br /><br /> 이전 RDL 버전을 2016 RDL로 업그레이드합니다.|2016 RDL|SQL Server 2016|
|SQL Server 2014 Data Tools의 보고서 디자이너 - Microsoft Visual Studio 2012용 Business Intelligence<br /><br /> 또는<br /><br /> SQL Server 2012 Data Tools의 보고서 디자이너 - Microsoft Visual Studio 2012용 Business Intelligence<br /><br /> 또는<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 에 포함된 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]Data Tools의 보고서 디자이너|Authors 2010 RDL<br /><br /> 이전 RDL 버전을 2010 RDL로 업그레이드합니다.|2010 RDL|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] Business Intelligence Development Studio의 보고서 디자이너|Authors 2010 RDL<br /><br /> 이전 RDL 버전을 2010 RDL로 업그레이드합니다.|2010 RDL|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] Business Intelligence Development Studio의 보고서 디자이너|Authors 2008 RDL<br /><br /> 이전 RDL 버전을 2008 RDL로 업그레이드합니다.|2008 RDL|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]|
  
 SSDT(SQL Server Data Tools)에 대한 자세한 내용은 다음을 참조하세요.  
  
-   [SQL Server Data Tools의 배포 및 버전 지원&#40;SSRS&#41;](../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)  
  
-   [Visual Studio 2015용 SQL Server Data Tools](/sql-docs/docs/ssdt/download-sql-server-data-tools-ssdt).  
  
##  <a name="bkmk_reportviewer"></a> ReportViewer 컨트롤  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ReportViewer 컨트롤은 로컬 미리 보기 모드 또는 원격 미리 보기 모드로 .rdlc 보고서를 표시할 수 있으며, 이 컨트롤은 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서 서버에서 호스팅되는 .rdl 파일을 표시할 수 있습니다. 다음 표에서는 로컬 처리를 위한 ReportViewer 컨트롤(.rdlc)에서 지원되는 RDL 버전 목록을 보여 줍니다. 서버 쪽 RDL 지원은 [보고서 서버 및 RDL 스키마 지원](#bkmk_report_server_rdl_schema_support)섹션에 요약되어 있습니다.  
  
|제품의 ReportViewer 컨트롤|로컬 미리 보기를 위한 RDL 버전|  
|-------------------------------------|--------------------------------------|  
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 2015 <br/><br/>또는<br/><br/>[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 2013<br /><br /> 또는<br /><br /> [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 2012<br /><br /> 또는<br /><br /> [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)]|2008 RDL|  
|[!INCLUDE[vsprvslong](../includes/vsprvslong-md.md)]<br /><br /> 또는<br /><br /> [!INCLUDE[vsOrcas](../includes/vsorcas-md.md)]|2005 RDL|  
  
 자세한 내용은 다음 항목을 참조하세요.  
  
-   [RDLC 파일을 RDL 파일로 변환](http://msdn.microsoft.com/library/ms252109.aspx)  
  
-   [ReportViewer 컨트롤(Visual Studio)](http://msdn.microsoft.com/library/ms251671.aspx)  
  
-   [ReportViewer 컨트롤 추가 및 구성](http://msdn.microsoft.com/library/ms252104.aspx)  
  
## <a name="see-also"></a>관련 항목:  
 [보고서, 보고서 파트 및 보고서 정의&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [Reporting Services 도구](../reporting-services/tools/reporting-services-tools.md)   
 [RDL(Report Definition Language)&#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  

