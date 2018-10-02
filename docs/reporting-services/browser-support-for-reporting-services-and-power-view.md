---
title: Reporting Services 및 파워 뷰에 대한 브라우저 지원 | Microsoft Docs
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
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
ms.openlocfilehash: 96c7e313bea6d36d62267413618b4a90bfdd2d74
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47695911"
---
# <a name="browser-support-for-reporting-services-and-power-view"></a>Reporting Services 및 파워 뷰 브라우저 지원

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

SQL Server Reporting Services, ReportViewer 컨트롤 및 파워 뷰 관리 및 확인을 위해 지원되는 브라우저 버전에 대해 알아봅니다.

> [!NOTE]
> SQL Server 2016 이후부터 SharePoint와의 Reporting Services 통합을 사용할 수 없습니다.

## <a name="browser-requirements-for-the-web-portal"></a>웹 포털에 대한 브라우저 요구 사항

다음은 웹 포털에 대해 지원되는 브라우저의 현재 목록입니다.

**Microsoft Windows**  
*Windows 7, 8.1, 10; Windows Server 2008 R2, 2012, 2012 R2*
- Microsoft Edge(+)
- Microsoft Internet Explorer 10 또는 11
- Google Chrome(+)
- Mozilla Firefox(+)

**Apple OS X**  
*OS X 10.9-10.11*

- Apple Safari(+)
- Google Chrome(+)
- Mozilla Firefox(+)

**Apple iOS**  
*iOS 9이 설치된 iPhone 및 iPad*

- Apple Safari(+)

**Google Android**  
*Android 4.4(KitKat) 이상이 설치된 휴대폰 및 태블릿*

- Google Chrome(+)

 **(+)** 최신 공개 릴리스 버전

## <a name="browser-requirements-for-the-reportviewer-web-control-2015"></a>ReportViewer 웹 컨트롤(2015)에 대한 브라우저 요구 사항

 다음은 ReportViewer 웹 컨트롤(2015)에 대해 지원되는 브라우저의 현재 목록입니다. 보고서 뷰어에서는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 웹 포털 및 SharePoint 라이브러리의 보고서를 볼 수 있습니다.  

**Microsoft Windows**  
*Windows 7, 8.1, 10; Windows Server 2008 R2, 2012, 2012 R2*

- Microsoft Edge(+)
- Microsoft Internet Explorer 10 또는 11
- Google Chrome(+)
- Mozilla Firefox(+)

**Apple OS X**  
*OS X 10.9-10.11*

- Apple Safari(+)

 **(+)** 최신 공개 릴리스 버전

 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]와 통합된 SharePoint 제품을 사용하는 경우에는  [SharePoint 2016의 브라우저 지원 계획](http://technet.microsoft.com//library/cc263526\(v=office.16\).aspx)을 참조하세요.

### <a name="authentication-requirements"></a>인증 요구 사항

 브라우저는 클라이언트 요청이 성공하기 위해 보고서 서버에서 처리되어야 하는 특정 인증 체계를 지원합니다. 다음 표에는 Windows 운영 체제에서 실행되는 브라우저가 지원하는 기본 인증 형식이 나와 있습니다.

|**브라우저 종류**|**지원**|**브라우저 기본값**|**서버 기본값**|
|----------------------|------------------|-------------------------|------------------------|
|**Microsoft Edge** (+)|Negotiate, Kerberos, NTLM, Basic|Negotiate|예 Edge에서는 기본 인증 설정이 사용됩니다.|
|**Microsoft Internet Explorer**|Negotiate, Kerberos, NTLM, Basic|Negotiate|예 기본 인증 설정이 Internet Explorer에서 작동합니다.|
|**Google Chrome**(+)|Negotiate, NTLM, Basic|Negotiate|예 기본 인증 설정이 Chrome에서 작동합니다.|
|**Mozilla Firefox**(+)|NTLM, 기본|NTLM|예 기본 인증 설정이 Firefox에서 작동합니다.|
|**Apple Safari**(+)|NTLM, 기본|Basic|예 기본 인증 설정이 Safari에서 작동합니다.|

 **(+)** 최신 공개 릴리스 버전

### <a name="script-requirements-for-viewing-reports"></a>보고서 보기를 위한 스크립트 요구 사항

 보고서 뷰어를 사용하려면 스크립트를 실행하도록 브라우저를 구성합니다.

 스크립팅을 설정하지 않으면 보고서를 열 때 다음과 비슷한 오류 메시지가 나타납니다.

- **브라우저가 스크립트를 지원하지 않거나 스크립트를 허용하지 않도록 구성되어 있습니다. 스크립트 없이 이 보고서를 보려면 여기를 클릭하세요**.

 스크립트 지원 없이 보고서를 보도록 선택하면 보고서는 보고서 도구 모음과 문서 구조와 같은 보고서 뷰어 기능 없이 HTML로 렌더링됩니다.

> [!NOTE]
> 보고서 도구 모음은 HTML 뷰어 구성 요소의 일부입니다. 기본적으로 브라우저 창에서 렌더링되는 모든 보고서의 상단에 도구 모음이 표시됩니다. 보고서 뷰어는 보고서에서 정보를 검색하는 기능, 특정 페이지로 스크롤하는 기능, 보기 편하게 페이지 크기를 조정하는 기능 등을 제공합니다. 보고서 도구 모음 또는 HTML 뷰어에 대한 자세한 내용은 [HTML Viewer and the Report Toolbar](../reporting-services/html-viewer-and-the-report-toolbar.md)을 참조하세요.

## <a name="browser-support-for-reportviewer-web-server-controls-in-visual-studio"></a>Visual Studio의 ReportViewer 웹 서버 컨트롤에 대한 브라우저 지원

 ReportViewer 웹 서버 컨트롤은 ASP.NET 웹 응용 프로그램에 보고 기능을 포함시키는 데 사용됩니다. 컨트롤은 Visual Studio에 포함되어 있으며 이 항목에서 설명하는 기타 구성 요소와 다른 브라우저 및 브라우저 버전을 지원합니다. 응용 프로그램을 보는 데 사용되는 브라우저의 유형은 응용 프로그램에서 사용자가 어떤 종류의 ReportViewer 기능을 제공할 수 있는지를 결정합니다. 이 항목에 제공된 표를 사용하여 지원되는 브라우저 중 어떤 것이 보고 기능 제한 사항의 영향을 받고 어떤 플랫폼이 지원되는지 알아보세요.  

 스크립트 지원이 활성화된 브라우저를 사용합니다. 브라우저에서 스크립트를 실행할 수 없는 경우에는 보고서를 볼 수 없습니다.

**Microsoft Windows**  
*Windows 7, 8.1, 10; Windows Server 2008 R2, 2012, 2012 R2*

- Microsoft Edge(+)
- Microsoft Internet Explorer 10 또는 11
- Google Chrome(+)
- Mozilla Firefox(+)

 **(+)** 최신 공개 릴리스 버전

## <a name="power-view-browser-support"></a>파워 뷰 브라우저 지원

**Microsoft Windows**  
*Windows 7, 8.1, 10; Windows Server 2008 R2, 2012, 2012 R2*

- Microsoft Internet Explorer 10 또는 11
- Mozilla Firefox(+)

**Apple OS X**  
*OS X 10.9-10.11*

- Apple Safari(+)

 **(+)** 최신 공개 릴리스 버전

 SharePoint 2016 브라우저 지원에 대한 자세한 내용은 [SharePoint 2013의 브라우저 지원 계획](http://technet.microsoft.com//library/cc263526\(v=office.16\).aspx)을 참조하세요.

## <a name="next-steps"></a>다음 단계

[웹 포털에서 보고서 찾기 및 보기](report-builder/finding-and-viewing-reports-in-the-web-portal-report-builder-and-ssrs.md)  
[Reporting Services 도구](../reporting-services/tools/reporting-services-tools.md)  
[웹 포털(SSRS 기본 모드)](http://msdn.microsoft.com/7349e626-6ed5-4d21-b05f-cf042ad9ad70)  
[HTML Viewer and the Report Toolbar](../reporting-services/html-viewer-and-the-report-toolbar.md)  
[URL 액세스 매개 변수 참조](../reporting-services/url-access-parameter-reference.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)

