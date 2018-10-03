---
title: 사용 되지 않는 SQL Server 2014에서에서 SQL Server Reporting Services의 기능 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, backward compatibility
- deprecated features [Reporting Services]
- HTML OWC rendering extension [Reporting Services]
- Report Server Web service, endpoints
ms.assetid: 3876c01e-f81d-4cce-9104-5106a8c369e6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 93d31c4f9f8f712834131136034541bf469e0014
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48119883"
---
# <a name="deprecated-features-in-sql-server-reporting-services-in-sql-server-2014"></a>SQL Server 2014의 SQL Server Reporting Services에서 지원되지 않는 기능
  이 항목에서는 지원되지 않는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기능에 대해 설명합니다. 이러한 기능은 지원되지 않는 버전에서 계속 사용할 수 있지만 이후 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 기능이 제거될 예정입니다. 새 응용 프로그램에는 이러한 기능을 사용하면 안 됩니다.  
  
 항목 내용  
  
-   [SQL Server 2014 Reporting Services에서 지원되지 않는 기능](#bkmk_2014)  
  
-   [SQL Server 2012 SP1 Reporting Services에서 사용 되지 않는 기능](#bkmk_2012sp1)  
  
-   [SQL Server 2012 Reporting Services에서 지원되지 않는 기능](#bkmk_2012)  
  
-   [SQL Server 2008 R2 Reporting Services에서 사용 되지 않는 기능](#bkmk_kj)  
  
##  <a name="bkmk_2014"></a> SQL Server 2014 Reporting Services에서 사용 되지 않는 기능  
  
### <a name="features-not-supported-in-the-next-version-of-sql-server"></a>다음 버전의 SQL Server에서 지원되지 않는 기능  
 다음 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기능에서 지원 되지 것입니다 합니다 **다음** 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]합니다. 새 개발 작업에서는 이러한 기능을 사용하지 말고, 현재 이러한 기능을 사용하는 응용 프로그램은 가능한 한 빨리 수정하세요.  
  
#### <a name="html-rendering-extension-device-information-settings"></a>HTML 렌더링 확장 프로그램 장치 정보 설정  
 HTML 렌더링 확장 프로그램에 대한 다음 장치 정보 설정은 지원되지 않습니다.  
  
-   ActionScript  
  
-   ActiveXControls  
  
-   GetImage  
  
-   OnlyVisibleStyles  
  
-   ReplacementRoot  
  
-   ResourceStreamRoot  
  
-   StreamRoot  
  
-   UsePx  
  
-   확대/축소  
  
 HTML 렌더링 확장 프로그램에 대 한 자세한 내용은 참조 하세요. [HTML Device Information Settings](html-device-information-settings.md)  
  
#### <a name="microsoft-word-and-microsoft-excel-1997-2003-rendering"></a>Microsoft Word 및 Microsoft Excel 1997-2003 렌더링  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] BIFF8 렌더링 확장 프로그램 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고 하는 [!INCLUDE[msCoName](../includes/msconame-md.md)] 단어 및 [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel 1997-2003에 바이너리 교환 파일 형식을 합니다. [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 렌더링 확장 프로그램이 포함 되어는 [!INCLUDE[msCoName](../includes/msconame-md.md)] Office 2007-2010 Open XML 형식입니다.  
  
#### <a name="report-definition-language-rdl-2005-and-earlier"></a>RDL(Report Definition Language) 2005 및 이전  
 RDL(Report Definition Language) 2005 및 이전 버전은 지원되지 않습니다. RDL에 대 한 자세한 내용은 참조 하세요. [Report Definition Language &#40;SSRS&#41;](reports/report-definition-language-ssrs.md)합니다.  
  
 보고서 업그레이드에 대 한 자세한 내용은 참조 하세요. [Upgrade Reports](install-windows/upgrade-reports.md)합니다.  
  
#### <a name="sql-server-2005-and-earlier-custom-report-items"></a>SQL Server 2005 및 이전 사용자 지정 보고서 항목  
 사용자 지정 보고서 항목 (CRI) 용으로 컴파일된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2005 및 이전 버전은 사용 되지 않습니다.  
  
#### <a name="reporting-services-snapshots-2005-and-earlier"></a>Reporting Services 스냅숏 2005 및 이전 버전  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 스냅숏을 사용 하 여 렌더링 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2005 및 이전 버전은 사용 되지 않습니다.  
  
#### <a name="report-models"></a>보고서 모델  
 SMDL(Semantic Modeling Language) 보고서 모델은 더 이상 사용되지 않습니다. 기존 보고서 모델에서 데이터 원본으로 사용 하도록 할 수 있지만 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서를 보고서 모델에서 해당 종속성을 제거 하려면 보고서를 업데이트 하는 것이 좋습니다.  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에는 보고서 모델을 만들거나 업데이트하기 위한 도구가 포함되지 않았습니다. 자세한 내용은 [SQL Server 2014에서 SQL Server Reporting Services의 주요 변경 내용](breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)합니다.  
  
#### <a name="deprecated-methods-in-the-web-service-endpoint"></a>웹 서비스 엔드포인트에서 사용되지 않는 메서드  
 다음 작업에서 사용 되지 않는 <xref:ReportService2010.ReportingService2010> 웹 서비스 끝점:  
  
-   <xref:ReportService2010.ReportingService2010.GetProperties%2A>  
  
-   <xref:ReportService2010.ReportingService2010.IsSSLRequired%2A>  
  
#### <a name="sharepoint-web-parts"></a>SharePoint 웹 파트  
 cab 파일에서 추출할 수 있는 설치 캐비닛 파일 **RSWebParts.cab** 및 SharePoint 웹 파트는 사용되지 않습니다. 사용 되지 않는 웹 파트 보고서 탐색기는 (**SPExplorer.dwp**) 및 보고서 뷰어 (**SPViewer.dwp**).  
  
 사용 되지 않는 웹 파트에 대 한 자세한 내용은 참조 하세요. [보기 및 탐색 기본 모드 보고서를 사용 하 여 SharePoint 웹 파트 (SSRS)](http://msdn.microsoft.com/library/ms159772.aspx)  
  
### <a name="features-not-supported-in-a-future-version-of-sql-server"></a>이후 버전의 SQL Server에서 지원되지 않는 기능  
 아래의 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기능은 다음 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 지원되지만 이후 버전에서는 제거될 예정입니다. 어떤 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 제거될지는 결정되지 않았습니다.  
  
 아니오 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기능에서 사용 되지 않는 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]합니다.  
  
##  <a name="bkmk_2012sp1"></a> SQL Server 2012 SP1 Reporting Services에서 사용 되지 않는 기능  
 이 섹션에서는 설명 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 에서 사용 되지 않는 기능 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]합니다. 아래의 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기능은 다음 버전의 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 지원되지만 이후 버전에서는 제거될 예정입니다. 어떤 버전의 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 에서 제거될지는 결정되지 않았습니다.  
  
### <a name="sharepoint-web-parts"></a>SharePoint 웹 파트  
 cab 파일에서 추출할 수 있는 설치 캐비닛 파일 **RSWebParts.cab** 및 SharePoint 웹 파트는 사용되지 않습니다. 사용 되지 않는 웹 파트 보고서 탐색기는 (**SPExplorer.dwp**) 및 보고서 뷰어 (**SPViewer.dwp**).  
  
 사용 되지 않는 웹 파트에 대 한 자세한 내용은 참조 하세요. [보기 및 탐색 기본 모드 보고서를 사용 하 여 SharePoint 웹 파트 (SSRS)](http://msdn.microsoft.com/library/ms159772.aspx)  
  
##  <a name="bkmk_2012"></a> SQL Server 2012 Reporting Services에서 사용 되지 않는 기능  
 이 섹션에서는 설명 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 에서 사용 되지 않는 기능 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]합니다.  
  
### <a name="html-rendering-extension-device-information-settings"></a>HTML 렌더링 확장 프로그램 장치 정보 설정  
 HTML 렌더링 확장 프로그램에 대한 다음 장치 정보 설정은 지원되지 않습니다.  
  
-   ActionScript  
  
-   ActiveXControls  
  
-   GetImage  
  
-   OnlyVisibleStyles  
  
-   ReplacementRoot  
  
-   ResourceStreamRoot  
  
-   StreamRoot  
  
-   UsePx  
  
-   확대/축소  
  
 HTML 렌더링 확장 프로그램에 대 한 자세한 내용은 참조 하세요. [HTML Device Information Settings](html-device-information-settings.md)  
  
### <a name="microsoft-word-and-microsoft-excel-1997-2003-rendering"></a>Microsoft Word 및 Microsoft Excel 1997-2003 렌더링  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] BIFF8 렌더링 확장 프로그램 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고 하는 [!INCLUDE[msCoName](../includes/msconame-md.md)] 단어 및 [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel 1997-2003에 바이너리 교환 파일 형식을 합니다. [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 렌더링 확장 프로그램이 포함 되어는 [!INCLUDE[msCoName](../includes/msconame-md.md)] Office 2007-2010 Open XML 형식입니다.  
  
### <a name="report-definition-language-rdl-2005-and-earlier"></a>RDL(Report Definition Language) 2005 및 이전  
 RDL(Report Definition Language) 2005 및 이전 버전은 지원되지 않습니다. RDL에 대 한 자세한 내용은 참조 하세요. [Report Definition Language &#40;SSRS&#41;](reports/report-definition-language-ssrs.md)합니다.  
  
 보고서 업그레이드에 대 한 자세한 내용은 참조 하세요. [Upgrade Reports](install-windows/upgrade-reports.md)합니다.  
  
### <a name="sql-server-2005-and-earlier-custom-report-items"></a>SQL Server 2005 및 이전 사용자 지정 보고서 항목  
 사용자 지정 보고서 항목 (CRI) 용으로 컴파일된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2005 및 이전 버전은 사용 되지 않습니다.  
  
### <a name="reporting-services-snapshots-2005-and-earlier"></a>Reporting Services 스냅숏 2005 및 이전 버전  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 스냅숏을 사용 하 여 렌더링 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2005 및 이전 버전은 사용 되지 않습니다.  
  
### <a name="report-models"></a>보고서 모델  
 SMDL(Semantic Modeling Language) 보고서 모델은 더 이상 사용되지 않습니다. 기존 보고서 모델에서 데이터 원본으로 사용 하도록 할 수 있지만 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서를 보고서 모델에서 해당 종속성을 제거 하려면 보고서를 업데이트 하는 것이 좋습니다.  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에는 보고서 모델을 만들거나 업데이트하기 위한 도구가 포함되지 않았습니다. 자세한 내용은 [SQL Server 2014에서 SQL Server Reporting Services의 주요 변경 내용](breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)합니다.  
  
### <a name="deprecated-methods-in-the-web-service-endpoint"></a>웹 서비스 엔드포인트에서 사용되지 않는 메서드  
 다음 작업에서 사용 되지 않는 <xref:ReportService2010.ReportingService2010> 웹 서비스 끝점:  
  
-   <xref:ReportService2010.ReportingService2010.GetProperties%2A>  
  
-   <xref:ReportService2010.ReportingService2010.IsSSLRequired%2A>  
  
##  <a name="bkmk_kj"></a> SQL Server 2008 R2 Reporting Services에서 사용 되지 않는 기능  
  
> [!NOTE]  
>  SQL Server 2008 R2는 SQL Server 2008의 부 버전 업그레이드이므로 SQL Server 2008 섹션의 내용도 검토하는 것이 좋습니다.  
  
### <a name="report-server-web-service-endpoints"></a>보고서 서버 웹 서비스 엔드포인트  
 웹 서비스 <xref:ReportService2005.ReportingService2005> 고 <xref:ReportService2006.ReportingService2006> 이 릴리스에서 더 이상 사용 되지 되었습니다. 이러한 끝점은 새 끝점으로 대체 되었습니다: <xref:ReportService2010.ReportingService2010>합니다.  
  
 새 엔드포인트에는 사용되지 않는 엔드포인트에서 제공하던 모든 기능과 SQL Server 2008 R2에 추가된 새 기능이 모두 포함됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [새로운 &#40;Reporting Services&#41;](what-s-new-reporting-services.md)   
 [이전 버전과의 호환성](../getting-started/backward-compatibility.md)   
 [SQL Server 2014에서에서 SQL Server Reporting Services 동작 변경 내용](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
 [SQL Server 2014에서 SQL Server Reporting Services에 지원되지 않는 기능](discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)  
  
  
