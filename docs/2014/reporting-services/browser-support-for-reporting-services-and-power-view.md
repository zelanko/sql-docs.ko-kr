---
title: Reporting Services 및 파워 뷰 브라우저 지원 (Reporting Services 2014)에 대 한 계획 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- displaying reports
- scripts [Reporting Services], requirements
- viewing reports
- browsers [Reporting Services]
- Web browsers [Reporting Services], about browser support
- browsing reports [Reporting Services]
- components [Reporting Services], browsers
- Web browsers [Reporting Services]
ms.assetid: 48a75bbb-0029-4c43-891d-dc8f4fc0ebe1
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 975c396eb3c0bfa7414e3af4249338d2790754b4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48157043"
---
# <a name="planning-for-reporting-services-and-power-view-browser-support-reporting-services-2014"></a>Reporting Services 및 Power View 브라우저 지원 계획(Reporting Services 2014)
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], 웹 브라우저를 사용 하 여 보고서를 보고 보고서 관리자를 실행 합니다. 모든 브라우저에서 모든 보고서 기능을 지원하는 것은 아닙니다. 이 항목에서는 보고서 관리자 관리 기능, 보고서 보기 및 Visual Studio의 보고서 뷰어 컨트롤에 대한 지원 및 요구 사항에 대해 설명합니다. 또한 이 항목에는 지원되는 브라우저, 인증 요구 사항 및 스크립트 요구 사항에 대한 기능 가용성이 요약되어 있습니다.  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 모드 | [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기본 모드  
  
 **항목 내용:**  
  
-   [Power View 브라우저 시나리오](#bkmk_powerview)  
  
-   [보고서 관리자 브라우저 요구 사항 (기본 모드)](#bkmk_reportmanager)  
  
-   [보고서를 보기 위한 브라우저 요구 사항](#bkmk_reportviewer)  
  
-   [인증 요구 사항](#bkmk_authentication)  
  
-   [Visual Studio의 ReportViewer 웹 서버 컨트롤에 대 한 브라우저 지원](#bkmk_controls)  
  
##  <a name="bkmk_powerview"></a> Power View 브라우저 시나리오  
 지원 되는 브라우저 및 브라우저 버전을 나열 하는 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 지원, 어떤 유형의 문서를 열에 따라 달라 집니다. Excel 2013 통합 문서 및 "**.rdlx**" 파일은 다른 구성 요소를 사용합니다.  
  
|문서 유형|환경|브라우저 지원|  
|-------------------|-----------------|---------------------|  
|Power View 보고서(.RDLX)|**SharePoint 서버:** [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 에서 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 통합 모드 및 파워 뷰 웹 응용 프로그램입니다.|참조 [파워 뷰 SharePoint Server 및 Reporting Services SharePoint 통합된 모드에서](#bkmk_powerview_on_SSRS)합니다.|  
|Power View 시트가 있는 Excel 2013 통합 문서|**SharePoint 서버:** [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] Excel 서비스에서.<br /><br /> **SharePoint Online (Office 365):** [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] Excel Web App의 합니다.|참조 [뷰는 Excel services 또는 SharePoint의 Excel Web App을 온라인 Power](#bkmk_powerview_on_ExcelServices)합니다.|  
  
###  <a name="bkmk_powerview_on_SSRS"></a> SharePoint Server 및 Reporting Services SharePoint 통합된 모드의 power View  
 다음 표에는 사용자가 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 서비스 응용 프로그램 및 설치 및 구성된 SharePoint의 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 추가 기능이 있는 SharePoint 팜에서 Power View 보고서(.RDLX)를 여는 경우 지원되는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]의 브라우저 버전이 요약되어 있습니다.  
  
-   표는 SharePoint 2010 및 SharePoint 2013에 적용됩니다.  
  
-   SharePoint 2013 브라우저 지원에 대 한 자세한 내용은 참조 하세요. [SharePoint 2013의 브라우저 지원 계획](http://technet.microsoft.com//library/cc263526\(office.15\).aspx) (http://technet.microsoft.com/library/cc263526(office.15).aspx)합니다.  
  
-   SharePoint 2010 브라우저 지원에 대 한 자세한 내용은 참조 하세요. [브라우저 지원 계획 (SharePoint Server 2010)](http://technet.microsoft.com/library/cc263526\(office.14\).aspx) (http://technet.microsoft.com/library/cc263526(office.14).aspx)합니다.  
  
|**브라우저**|**Windows 8 및 8.1**|**Windows 7**|**Windows Server 2012 및 2012 R2**|**Windows Server 2008 R2**|**Windows Server 2008**|**Mac OS X 10.6 – 10.9**|  
|-----------------|---------------------------|-------------------|-----------------------------------------|--------------------------------|-----------------------------|------------------------------|  
|**Internet Explorer 11 (데스크톱용)**|32비트, 64비트|32비트, 64비트|32비트, 64비트|32비트, 64비트|지원되지 않음|지원되지 않음|  
|**Internet Explorer 10 (데스크톱용)**|32비트, 64비트|32비트, 64비트|32비트, 64비트|32비트, 64비트|지원되지 않음|지원되지 않음|  
|**Internet Explorer 9**|지원되지 않음|32비트, 64비트|지원되지 않음|32비트, 64비트|32비트, 64비트|지원되지 않음|  
|**Internet Explorer 8**|지원되지 않음|32비트, 64비트|지원되지 않음|32비트, 64비트|32비트, 64비트|지원되지 않음|  
|**Mozilla Firefox (최신 공개 릴리스 버전)**|32비트|32비트|32비트|32비트|32비트|지원되지 않음|  
|**Apple Safari (최신 공개 릴리스 버전)**|지원되지 않음|지원되지 않음|지원되지 않음|지원되지 않음|지원되지 않음|32비트, 64비트|  
  
> [!NOTE]  
>  "32비트"는 운영 체제가 아닌 브라우저를 가리킵니다. 예를 들어 64비트 Windows 7에서 32비트 Internet Explorer 9를 사용할 수 있습니다.  
  
#### <a name="inprivate-browsing-feature-in-internet-explorer"></a>Internet Explorer의 InPrivate 브라우징 기능  
 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]에서는 [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer 8 및 Internet Explorer 9의 InPrivate 브라우징 기능을 지원하지 않습니다. InPrivate 브라우징에 대 한 자세한 내용은 참조 하세요. [InPrivate 브라우징 이란?](http://windows.microsoft.com/Windows7/What-is-InPrivate-Browsing) (http://windows.microsoft.com/Windows7/What-is-InPrivate-Browsing).  
  
###  <a name="bkmk_powerview_on_ExcelServices"></a> Excel Services 또는 SharePoint Online의 Excel Web App의 power View  
 다음 표에서 지원 되는 브라우저 버전에 대 한 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 사용자가 Excel 2013 통합 문서를 Excel Services를 실행 하는 SharePoint 서버에서 Power View 시트가 포함 된 열:  
  
-   SharePoint 2013 브라우저 지원에 대 한 자세한 내용은 참조 하세요. [SharePoint 2013의 브라우저 지원 계획](http://technet.microsoft.com/library/cc263526\(office.15\).aspx) (http://technet.microsoft.com/library/cc263526(office.15).aspx)합니다.  
  
|**브라우저**|**Windows 8 및 8.1**|**Windows 7**|**Windows Server 2012 및 2012 R2**|**Windows Server 2008 R2**|**Windows Server 2008**|**Mac OS X 10.6 – 10.9**|  
|-----------------|---------------------------|-------------------|-----------------------------------------|--------------------------------|-----------------------------|------------------------------|  
|**Internet Explorer 11 (데스크톱용)**|32비트, 64비트|32비트, 64비트|32비트, 64비트|32비트, 64비트|지원되지 않음|지원되지 않음|  
|**Internet Explorer 10 (데스크톱용)**|32비트, 64비트|32비트, 64비트|32비트, 64비트|32비트, 64비트|지원되지 않음|지원되지 않음|  
|**Internet Explorer 9**|지원되지 않음|32비트, 64비트|지원되지 않음|32비트, 64비트|32비트, 64비트|지원되지 않음|  
|**Internet Explorer 8**|지원되지 않음|32비트, 64비트|지원되지 않음|32비트, 64비트|32비트, 64비트|지원되지 않음|  
|**Mozilla Firefox (최신 공개 릴리스 버전)**|32비트|32비트|32비트|32비트|32비트|32비트, 64비트|  
|**Apple Safari (최신 공개 릴리스 버전)**|지원되지 않음|지원되지 않음|지원되지 않음|지원되지 않음|지원되지 않음|32비트, 64비트|  
|**Google Chrome (최신 공개 릴리스 버전)**|32 비트 **(\*)** 제한 시간|32 비트 **(\*)** 제한 시간|32 비트 **(\*)** 제한 시간|32 비트 **(\*)** 제한 시간|32 비트 **(\*)** 제한 시간|지원되지 않음|  
  
 **(\*)** Chrome의 Silverlight를 사용한는 Netscape 플러그 인 API (NPAPI)를 지 원하는 중지 됩니다. 파워 뷰는 Silverlight에 종속됩니다.  자세한 내용은 [NPAPI 지원 종료 최종 알림](http://blog.chromium.org/2014/11/the-final-countdown-for-npapi.html)을 참조하세요.  
  
##  <a name="bkmk_reportmanager"></a> 보고서 관리자 브라우저 요구 사항 (기본 모드)  
 다음은 현재 목록을 실행 하 여 지원 되는 브라우저는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기본 모드 보고서 관리자에서 보고서 및 보고서 서버를 관리 하도록 합니다.  
  
|브라우저|  
|-------------|  
|Internet Explorer 7 이상 및 스크립팅 사용.|  
|Mozilla FireFox(최신 공개 릴리스 버전)|  
|Apple Safari(최신 공개 릴리스 버전)|  
|Google Chrome(최신 공개 릴리스 버전)|  
  
##  <a name="bkmk_reportviewer"></a> 보고서를 보기 위한 브라우저 요구 사항  
 다음은 보고서 뷰어에서 지원되는 기능 및 브라우저에 대한 현재 목록입니다. 보고서 뷰어에서에서 보고서를 볼 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서 관리자 및 SharePoint 라이브러리입니다.  
  
|**브라우저**|**Windows 8 및 8.1**|**Windows 7**|**Windows Server 2012 및 2012 R2**|**Windows Server 2008 R2**|**Windows Server 2008**|**Mac OS X 10.6 – 10.9**|**iPad 용 iOS 6-7**|  
|-----------------|---------------------------|-------------------|-----------------------------------------|--------------------------------|-----------------------------|------------------------------|----------------------------|  
|**Internet Explorer 11 (데스크톱용)**|32비트, 64비트|32비트, 64비트|32비트, 64비트|지원되지 않음|지원되지 않음|지원되지 않음|지원되지 않음|  
|**Internet Explorer 10 (데스크톱용)**|32비트, 64비트|32비트, 64비트|32비트, 64비트|지원되지 않음|지원되지 않음|지원되지 않음|지원되지 않음|  
|**Internet Explorer 9**|지원되지 않음|32비트, 64비트|지원되지 않음|32비트, 64비트|32비트, 64비트|지원되지 않음|지원되지 않음|  
|**Internet Explorer 8**|지원되지 않음|32비트, 64비트|지원되지 않음|32비트, 64비트|32비트, 64비트|지원되지 않음|지원되지 않음|  
|**Internet Explorer 7**|지원되지 않음|지원되지 않음|지원되지 않음|지원되지 않음|32비트, 64비트|지원되지 않음|지원되지 않음|  
|**Mozilla Firefox (최신 공개 릴리스 버전)**|32비트|32비트|32비트|32비트|32비트|지원되지 않음|지원되지 않음|  
|**Apple Safari (최신 공개 릴리스 버전)**|지원되지 않음|지원되지 않음|지원되지 않음|지원되지 않음|지원되지 않음|32비트, 64비트|제한 된 기능을 사용 하 여 지원 <sup>(1)</sup>|  
|**Google Chrome (최신 공개 릴리스 버전)**|32비트|32비트|32비트|32비트|32비트|지원되지 않음|지원되지 않음|  
  
 **<sup>(1) </sup>**  다음 기능이 지원 됩니다.  
  
-   PDF 및 TIFF 형식으로 내보내기.  
  
-   iOS 장치의 Apple Safari에서 대화형으로 보고서 보기. 기능 지원에는 확대/축소, 매개 변수 창 및 대화형 정렬이 포함됩니다.  
  
-   자세한 내용은 [Reporting Services 보고서 보기 Microsoft Surface 장치 및 Apple iOS 장치에서](../../2014/reporting-services/view-reporting-services-reports-surface-ios-devices.md)합니다.  
  
 **참고** Macintosh 컴퓨터에서 보고서 서버에 액세스하는 경우 Safari를 사용하는 것이 좋습니다. 통합 된 SharePoint 제품을 사용 하는 경우 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]를 참조 하세요 [(Windows SharePoint Services) 브라우저 지원 계획](http://go.microsoft.com/fwlink/?LinkId=183583)합니다.  
  
### <a name="url-access-for-viewing-reports"></a>보고서 보기에 대한 URL 액세스  
 보고서를 보고서 관리자를 통해 보지 않고 직접 보려면 URL 액세스를 사용하여 보고서 및 보고서 뷰어에 연결합니다. URL 액세스는 다양한 브라우저를 지원합니다.  
  
 URL 액세스에 대한 자세한 내용은 다음 항목을 참조하세요.  
  
-   [URL 액세스 매개 변수 참조](url-access-parameter-reference.md)  
  
###  <a name="bkmk_authentication"></a> 인증 요구 사항  
 브라우저는 클라이언트 요청이 성공하기 위해 보고서 서버에서 처리되어야 하는 특정 인증 체계를 지원합니다. 다음 표에는 Windows 운영 체제에서 실행되는 브라우저가 지원하는 기본 인증 형식이 나와 있습니다.  
  
|**브라우저 종류**|**지원**|**브라우저 기본값**|**서버 기본값**|  
|----------------------|------------------|-------------------------|------------------------|  
|**Internet Explorer**|Negotiated, Kerberos, NTLM, 기본|Negotiate|예 기본 인증 설정이 Internet Explorer에서 작동합니다.|  
|**Firefox**|NTLM, 기본|NTLM|예 기본 인증 설정이 Firefox에서 작동합니다.|  
|**Safari**|Basic|Basic|예 기본 인증 설정이 Safari에서 작동합니다.|  
|**Chrome**|Negotiated, NTLM, 기본|Negotiated|예 기본 인증 설정이 Chrome에서 작동합니다.|  
  
### <a name="script-requirements"></a>스크립트 요구 사항  
 보고서 뷰어를 사용하려면 스크립트를 실행하도록 브라우저를 구성합니다.  
  
 스크립팅을 설정하지 않으면 보고서를 열 때 다음과 비슷한 오류 메시지가 나타납니다.  
  
-   **브라우저가 스크립트를 지원하지 않거나 스크립트를 허용하지 않도록 구성되어 있습니다. 스크립트 없이 이 보고서를 보려면 여기를 클릭하세요**.  
  
 스크립트 지원 없이 보고서를 보도록 선택하면 보고서는 보고서 도구 모음과 문서 구조와 같은 보고서 뷰어 기능 없이 HTML로 렌더링됩니다.  
  
> [!NOTE]  
>  보고서 도구 모음은 HTML 뷰어 구성 요소의 일부입니다. 기본적으로 브라우저 창에서 렌더링되는 모든 보고서의 상단에 도구 모음이 표시됩니다. 보고서 뷰어는 보고서에서 정보를 검색하는 기능, 특정 페이지로 스크롤하는 기능, 보기 편하게 페이지 크기를 조정하는 기능 등을 제공합니다. 보고서 도구 모음 또는 HTML 뷰어에 대한 자세한 내용은 [HTML Viewer and the Report Toolbar](html-viewer-and-the-report-toolbar.md)을 참조하세요.  
  
##  <a name="bkmk_controls"></a> Visual Studio의 ReportViewer 웹 서버 컨트롤에 대 한 브라우저 지원  
 ReportViewer 웹 서버 컨트롤은 ASP.NET 웹 응용 프로그램에 보고 기능을 포함시키는 데 사용됩니다. 컨트롤은 Visual Studio에 포함되어 있으며 이 항목에서 설명하는 기타 구성 요소와 다른 브라우저 및 브라우저 버전을 지원합니다. 응용 프로그램을 보는 데 사용되는 브라우저의 유형은 응용 프로그램에서 사용자가 어떤 종류의 ReportViewer 기능을 제공할 수 있는지를 결정합니다. 이 항목에 제공된 표를 사용하여 지원되는 브라우저 중 어떤 것이 보고 기능 제한 사항의 영향을 받고 어떤 플랫폼이 지원되는지 알아보십시오.  
  
 지원되는 브라우저의 렌더링 엔진 차이로 인해 일부 고급 보고 기능이 지원되는 브라우저마다 다르게 표시될 수 있습니다.  텍스트 회전을 예로 들 수 있습니다.  
  
### <a name="scripting-requirements"></a>스크립팅 요구 사항  
 스크립트 지원이 활성화된 브라우저를 사용합니다. 브라우저에서 스크립트를 실행할 수 없는 경우에는 보고서를 볼 수 없습니다.  
  
### <a name="browser-requirements-for-viewing-reports-with-the-reportviewer-web-server-controls"></a>ReportViewer 웹 서버 컨트롤의 보고서 보기에 대한 브라우저 요구 사항  
 대화형 보고서 기능에 대한 지원은 브라우저 유형에 따라 다릅니다. 다음 지원 표에서는 참고 열에 설명된 제약 조건을 기반으로 플랫폼에 따라 지원되는 브라우저 유형을 보여 줍니다.  
  
|||||||||  
|-|-|-|-|-|-|-|-|  
|**브라우저**|**Windows 8** 및 **Windows 8.1**|**Windows 7**|**Windows Server 2012** 및 **2012 R2**|**Windows Server 2008** 및 **2008 R2**|**Windows Server 2003**|**Mac OS X 10.6 – 10.9**|**참고**|  
|**Internet Explorer 11 (데스크톱용**|사용자 계정 컨트롤|예|사용자 계정 컨트롤|지원되지 않음|지원되지 않음|지원되지 않음|Internet Explorer는 ReportViewer의 모든 기능을 지원합니다.|  
|**Internet Explorer 10 (데스크톱용)**|사용자 계정 컨트롤|예|사용자 계정 컨트롤|지원되지 않음|지원되지 않음|지원되지 않음|Internet Explorer는 ReportViewer의 모든 기능을 지원합니다.|  
|**Internet Explorer 9**|지원되지 않음|사용자 계정 컨트롤|지원되지 않음|사용자 계정 컨트롤|예|사용자 계정 컨트롤|Internet Explorer는 ReportViewer의 모든 기능을 지원합니다.|  
|**Internet Explorer 8.0**|지원되지 않음|사용자 계정 컨트롤|지원되지 않음|사용자 계정 컨트롤|예<sup>1</sup>|지원되지 않음|Internet Explorer는 ReportViewer의 모든 기능을 지원합니다. <sup>1.</sup>|  
|**Internet Explorer 7.0**|지원되지 않음|사용자 계정 컨트롤|지원되지 않음|사용자 계정 컨트롤|예<sup>1</sup>|지원되지 않음|Internet Explorer는 ReportViewer의 모든 기능을 지원합니다. <sup>1.</sup>|  
|**Firefox (최신 공개 릴리스 버전)**|사용자 계정 컨트롤|예|예|예|사용자 계정 컨트롤|지원되지 않음|인쇄 및 확대/축소는 지원되지 않습니다.|  
|**Safari (최신 공개 릴리스 버전)**|지원되지 않음|지원되지 않음|지원되지 않음|지원되지 않음|지원되지 않음|사용자 계정 컨트롤|인쇄 및 확대/축소는 지원되지 않습니다.<br /><br /> 매개 변수가 있는 보고서에서 날짜를 선택하는 데 사용되는 달력 컨트롤은 이 브라우저에서 사용되지 않습니다. 사용자는 사용하려는 날짜를 수동으로 매개 변수 프롬프트 영역에 입력해야 합니다.|  
|**Chrome (최신 공개 릴리스 버전)**|사용자 계정 컨트롤|예|예|예|사용자 계정 컨트롤|지원되지 않음|인쇄 및 확대/축소는 지원되지 않습니다.|  
  
 <sup>1</sup>표준 모드에서 Internet Explorer 7.0 및 8.0 표시 되지 않습니다 보고서의 사선이 합니다. 보고서에서 사선을 사용하는 경우 ASP.NET 페이지가 Internet Explorer의 쿼크 모드에서 실행되도록 설정하세요. 이 작업을 수행 하려면는 \<! DOCTYPE > ASP.NET 페이지의 태그입니다. 또는 마스터 페이지를 사용하는 경우 .master 파일에서 태그를 찾을 수 있습니다. 이 태그는 다음과 같습니다.  
  
```  
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">  
```  
  
 대체는 \<! DOCTYPE > 다음 태그를 사용 하 여 태그:  
  
```  
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">  
```  
  
 Internet Explorer의 호환성 모드에 대 한 자세한 내용은 참조 하세요. [문서 호환성 정의](http://go.microsoft.com/fwlink/?LinkId=180380) (http://go.microsoft.com/fwlink/?LinkId=180380)합니다.  
  
 ReportViewer 컨트롤 사용에 대 한 자세한 내용은 참조 하세요. [보고서 및 ReportViewer 컨트롤 배포](http://msdn.microsoft.com/library/ms251723.aspx) (http://msdn.microsoft.com/library/ms251723.aspx)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 도구](tools/reporting-services-tools.md)   
 [보고서 관리자 &#40;SSRS 기본 모드&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [HTML 뷰어 및 보고서 도구 모음](html-viewer-and-the-report-toolbar.md)   
 [URL 액세스 매개 변수 참조](url-access-parameter-reference.md)  
  
  
