---
title: 보고서 설계 및 보고서 배포 계획(보고 서비스 2014) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 1c1e265e-52a2-4de3-96fd-ca4abae01c02
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d3047dba3e54d384f2f52733e8cf49308b793190
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2020
ms.locfileid: "80380824"
---
# <a name="plan-for-report-design-and-report-deployment-reporting-services-2014"></a>보고서 디자인 및 보고서 배포 계획(Reporting Services 2014)
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 는 보고서를 작성하고 배포하기 위한 몇 가지 방법을 제공합니다. 이 항목에서는 보고서 작성 환경과 보고서 서버가 함께 작동하도록 계획할 수 있습니다. 이 항목은 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 구성 요소에서 지원되는 보고서 정의에 대한 개요를 보여 줍니다. 보고서 정의는 RDL(Report Definition Language) 또는 RDLC(Report Definition Language for Clients)로 작성된 XML 파일입니다. 각 보고서 정의는 파일의 첫 부분에 나열되어 있는 특정 스키마 버전을 따릅니다.  
  
 RDL 파일은 [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] 프로젝트의 보고서 디자이너 및 보고서 작성기 3.0에서 작성됩니다. RDLC 파일은 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]에 포함된 ReportViewer 컨트롤을 사용해서 작성됩니다.  
  
 이 항목의 내용:  
  
-   [RDL 스키마 버전](#bkmk_rdl_schema_versions)  
  
-   [보고서 서버 및 RDL 스키마 지원](#bkmk_report_server_rdl_schema_support)  
  
-   [보고서 작성 및 배포 지원](#bkmk_report_authoring_and_deployment)  
  
-   [보고서 뷰어 컨트롤](#bkmk_reportviewer)  
  
##  <a name="rdl-schema-versions"></a><a name="bkmk_rdl_schema_versions"></a> RDL 스키마 버전  
 다음 표에서는 사용 가능한 스키마 버전과 이 항목의 나머지 부분에서 사용되는 약어를 나열합니다.  
  
|약어|스키마 버전|  
|------------------|--------------------|  
|2010 RDL|`https://schemas.microsoft.com/sqlserver/reporting/2010/01/reportdefinition`|  
|2008 RDL|`https://schemas.microsoft.com/sqlserver/reporting/2008/01/reportdefinition`|  
|2005 RDL<br /><br /> 2005 RDLC|`https://schemas.microsoft.com/sqlserver/reporting/2005/01/reportdefinition`|  
|2000 RDL|`https://schemas.microsoft.com/sqlserver/reporting/2003/10/reportdefinition`|  
  
 RDL 및 RDL 스키마에 대한 자세한 내용은 다음을 참조하세요.  
  
-   [Microsoft SQL Server XML 스키마](https://go.microsoft.com/fwlink/?LinkId=31850)  
  
-   [보고서 정의 언어 사양](https://go.microsoft.com/fwlink/?linkid=116865)  
  
-   [보고서 정의 언어&#40;SSRS&#41;](reports/report-definition-language-ssrs.md)  
  
 ReportViewer 컨트롤에 대한 자세한 내용은 [ReportViewer 컨트롤(Visual Studio)](https://msdn.microsoft.com/library/ms251671.aspx)을 참조하세요.  
  
##  <a name="report-server-and-rdl-schema-support"></a><a name="bkmk_report_server_rdl_schema_support"></a> 보고서 서버 및 RDL 스키마 지원  
 다음과 같은 방법으로 보고서 정의 파일을 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 보고서 서버에 배포할 수 있습니다.  
  
-   **보고서 디자이너:**[!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)]의 보고서 디자이너에서 보고서를 배포합니다.  
  
-   **보고서 작성기:** 보고서 작성기의 보고서 서버에 보고서를 저장합니다.  
  
-   **보고서 관리자:** 보고서 관리자의 기본 모드 보고서 서버로 보고서를 업로드합니다.  
  
-   **SharePoint:** SharePoint 모드 보고서 서버로 구성된 SharePoint 사이트에 보고서를 업로드합니다.  
  
-   **프로그래밍 방식:** SOAP API 인터페이스를 사용해서 보고서 서버에 보고서를 프로그래밍 방식으로 게시합니다. 자세한 내용은 [Report Server Web Service](report-server-web-service/report-server-web-service.md)을 참조하세요.  
  
 다음 표에서는 보고서 서버 버전별로 지원되는 rdl 스키마 버전을 보여 줍니다.  
  
|보고서 서버 버전|RDL 스키마 버전|  
|---------------------------|------------------------|  
|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]<br /><br /> 또는<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]<br /><br /> 또는<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|2010 RDL<br /><br /> 2008 RDL<br /><br /> 2005 RDL<br /><br /> 2000 RDL|  
|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]|2008 RDL<br /><br /> 2005 RDL<br /><br /> 2000 RDL|  
|[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]|2005 RDL<br /><br /> 2000 RDL|  
  
 보고서 서버에 보고서 정의를 업로드하거나 기존 보고서가 포함된 보고서 서버를 업그레이드할 때 보고서 서버는 원래 형식으로 보고서 정의를 보존합니다. **처음 사용할 때**, 보고서 서버는 보고서 서버 데이터베이스의 보고서를 이후 검토를 위해 보존되는 이진 형식으로 업그레이드합니다. 보고서 정의(.rdl) 자체는 업그레이드되지 않습니다.  
  
 보고서 정의 파일(.rdl)의 읽기 전용 복사본을 보고서 서버에서 추출할 수 있습니다. 기본 모드 보고서 서버에서는 보고서 관리자로 이동해서 보고서를 선택하고 **다운로드**를 클릭합니다. SharePoint 모드 배포에서는 문서 라이브러리로 이동해서 보고서를 선택하고 **복사본 다운로드**를 클릭합니다.  
  
 보고서 정의를 업그레이드하려면 보고서 제작 환경에서 해당 보고서를 열고 저장해야 합니다.  
  
 보고서 업그레이드 및 지원되는 스키마 버전에 대한 자세한 내용은 [보고서 업그레이드](install-windows/upgrade-reports.md)를 참조하세요.  
  
##  <a name="report-authoring-and-deployment-support"></a><a name="bkmk_report_authoring_and_deployment"></a> 보고서 제작 및 배포 지원  
 보고서 작성 환경은 [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] 프로젝트의 보고서 디자이너 및 보고서 작성기입니다. 보고서 제작 환경에서는 보고서 업그레이드, 보고서 디자인, 로컬 모드로 보고서 미리 보기, 보고서 서버에서 보고서 미리 보기 및 보고서 배포를 위한 다양한 지원 기능을 제공합니다.  
  
 다음 표에는 다양한 스키마 버전을 위한 보고서 정의 제작 및 배포에 대한 지원 기능이 요약되어 있습니다.  
  
|제작 환경|작성된 RDL 버전|배포 RDL 버전|보고서 서버에 배포 버전|  
|---------------------------|--------------------------|------------------------|--------------------------------------|  
|SQL Server 2014 Data Tools의 보고서 디자이너 - Microsoft 다운로드 센터의 Microsoft Visual Studio 2012용 Business Intelligence.<br /><br /> 또는<br /><br /> SQL Server 2012 Data Tools의 보고서 디자이너 - Microsoft 다운로드 센터의 Microsoft Visual Studio 2012용 Business Intelligence.<br /><br /> 또는<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 에 포함된 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]Data Tools의 보고서 디자이너|저자 2010 RDL. 기존 RDL 열기:<br /><br /> 2000 RDL, 2010 RDL로 업그레이드<br /><br /> 2005 RDL, 2010 RDL로 업그레이드<br /><br /> 2008 RDL, 2010 RDL로 업그레이드|2008 RDL<br /><br /> 2010 RDL|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] Business Intelligence Development Studio의 보고서 디자이너|저자 2010 RDL. 기존 RDL 열기:<br /><br /> 2000 RDL, 2010 RDL로 업그레이드<br /><br /> 2005 RDL, 2010 RDL로 업그레이드<br /><br /> 2008 RDL, 2010 RDL로 업그레이드|2008 RDL<br /><br /> 2010 RDL|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] Business Intelligence Development Studio의 보고서 디자이너|저자 2008 RDL. 기존 RDL 열기:<br /><br /> 2000 RDL, 2008 RDL로 업그레이드<br /><br /> 2005 RDL, 2008 RDL로 업그레이드|2008 RDL|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]|  
|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 보고서 작성기|저자 2010 RDL. 기존 RDL 열기:<br /><br /> 2000 RDL, 2010 RDL로 업그레이드<br /><br /> 2005 RDL, 2010 RDL로 업그레이드<br /><br /> 2008 RDL, 2010 RDL로 업그레이드|2010 RDL|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|  
|Visual Studio RDLC 보고서 디자이너 보고서 디자이너|2005 RDLC|해당 없음|해당 없음|  
  
 [!INCLUDE[ss_dtbi_vs2013](../includes/ss-dtbi-vs2013-md.md)]에 대한 자세한 내용은 다음을 참조하세요.  
  
-   [SQL Server Data Tools의 배포 및 버전 지원&#40;SSRS&#41;](tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)  
  
-   [마이크로소프트 SQL 서버 데이터 도구 - 비주얼 스튜디오 2012.](https://www.microsoft.com/download/details.aspx?id=36843)  
  
##  <a name="reportviewer-controls"></a><a name="bkmk_reportviewer"></a>보고서 뷰어 컨트롤  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ReportViewer 컨트롤은 로컬 미리 보기 모드 또는 원격 미리 보기 모드로 .rdlc 보고서를 표시할 수 있으며, 이 컨트롤은 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서 서버에서 호스팅되는 .rdl 파일을 표시할 수 있습니다. 다음 표에서는 로컬 처리를 위한 ReportViewer 컨트롤(.rdlc)에서 지원되는 RDL 버전 목록을 보여 줍니다. 서버 쪽 RDL 지원은 [보고서 서버 및 RDL 스키마 지원](#bkmk_report_server_rdl_schema_support)섹션에 요약되어 있습니다.  
  
|제품의 ReportViewer 컨트롤|로컬 미리 보기를 위한 RDL 버전|  
|-------------------------------------|--------------------------------------|  
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 2013<br /><br /> 또는<br /><br /> [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 2012<br /><br /> 또는<br /><br /> [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)]|2008 RDL|  
|[!INCLUDE[vsprvslong](../includes/vsprvslong-md.md)]<br /><br /> 또는<br /><br /> [!INCLUDE[vsOrcas](../includes/vsorcas-md.md)]|2005 RDL|  
  
 자세한 내용은  
  
-   [RDLC 파일을 RDL 파일로 변환](https://msdn.microsoft.com/library/ms252109.aspx)  
  
-   [ReportViewer 컨트롤(Visual Studio)](https://msdn.microsoft.com/library/ms251671.aspx)  
  
-   [ReportViewer 컨트롤 추가 및 구성](https://msdn.microsoft.com/library/ms252104.aspx)  
  
## <a name="see-also"></a>관련 항목  
 [보고서 작성자 및 SSRS &#40;보고서 작성기 및 SSRS&#41;보고서, 보고서 부품 및 보고서 정의](report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [보고 서비스 도구](tools/reporting-services-tools.md)   
 [보고서 정의 언어&#40;SSRS&#41;](reports/report-definition-language-ssrs.md)  
  
  
