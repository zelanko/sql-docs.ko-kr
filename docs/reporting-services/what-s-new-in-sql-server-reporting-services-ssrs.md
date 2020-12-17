---
title: Reporting Services의 새로운 기능 | Microsoft Docs
description: 주요 기능 영역에 대한 변경 내용을 포함하여 다양한 SQL Server Reporting Services 버전의 새로운 기능에 대해 알아봅니다.
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.custom: ''
ms.date: 12/05/2019
ms.openlocfilehash: b225576a95784fbd109af4683ff6c1548ad67471
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464484"
---
# <a name="whats-new-in-sql-server-reporting-services-ssrs"></a>SSRS(SQL Server Reporting Services)의 새로운 기능

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../includes/ssrs-appliesto-not-pbirs.md)]

다양한 버전의 SQL Server [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]의 새로운 기능에 대해 알아봅니다. 이 문서에서는 주요 기능 영역을 설명하고 출시된 새 항목에 맞게 업데이트되었습니다.

Power BI Report Server에 대한 정보는 [Power BI Report Server란?](https://docs.microsoft.com/power-bi/report-server/get-started)을 참조하세요.

::: moniker range=">=sql-server-ver15"

## <a name="sql-server-2019-reporting-services"></a>SQL Server 2019 Reporting Services

**다운로드** :::image type="icon" source="https://docs.microsoft.com/analysis-services/analysis-services/media/download.png":::

[SQL Server 2019 Reporting Services](https://www.microsoft.com/download/details.aspx?id=100122)는 Microsoft 다운로드 센터에서 다운로드할 수 있습니다.

### <a name="azure-sql-managed-instance-support"></a>Azure SQL Managed Instance 지원

이제 VM 또는 데이터 센터에서 호스트되는 Azure SQL Managed Instance(MI)에서 SQL Server Reporting Services(SSRS)에 사용되는 데이터베이스 카탈로그를 호스트할 수 있습니다. 지원은 SQL Server에 대한 연결 시 데이터베이스 자격 증명 사용으로 제한됩니다.

### <a name="power-bi-premium-dataset-support"></a>Power BI Premium 데이터 세트 지원

Microsoft 보고서 작성기 또는 SSDT(SQL Server Data Tools) 중 하나를 사용하여 Power BI 데이터 세트에 연결할 수 있습니다. 그런 다음 SQL Server Analysis Services 연결을 사용하여 이러한 보고서를 SSRS 2019에 게시할 수 있습니다. 사용자는 저장된 Windows 사용자 이름 및 암호를 사용하여 시나리오를 사용하도록 설정해야 합니다.

### <a name="alttext-alternative-text-support-for-report-elements"></a>AltText(대체 텍스트)가 보고서 요소 지원

보고서를 작성할 때 도구 설명을 사용하여 보고서의 각 요소에 대한 텍스트를 지정할 수 있습니다. 화면 읽기 프로그램 기술은 이러한 도구 설명을 올바르게 식별합니다.

### <a name="azure-active-directory-application-proxy-support"></a>Azure Active Directory 애플리케이션 프록시 지원

Azure Active Directory 애플리케이션 프록시를 사용하면 더 이상 웹 또는 모바일 앱을 통한 보안 액세스를 허용하기 위해 웹 애플리케이션 프록시를 관리할 필요가 없습니다.

### <a name="custom-headers"></a>사용자 지정 헤더

지정된 regex 패턴과 일치하는 모든 URL에 대한 헤더 값을 설정합니다. 사용자는 유효한 XML로 사용자 지정 헤더 값을 업데이트하여 선택한 요청 URL에 대한 헤더 값을 설정할 수 있습니다. 관리자는 XML에 원하는 수의 헤더를 추가할 수 있습니다. 자세한 내용은 **서버 속성 고급 페이지** 문서의 [사용자 지정 헤더](tools/server-properties-advanced-page-reporting-services.md#customheaders)를 참조하세요.

### <a name="transparent-database-encryption"></a>투명한 데이터베이스 암호화

SQL Server 2019는 이제 Enterprise 및 Standard Edition용 SSRS 카탈로그 데이터베이스에서 투명 데이터베이스 암호화를 지원합니다. 

### <a name="microsoft-report-builder-update"></a>Microsoft 보고서 작성기 업데이트

새로 릴리스된 보고서 작성기 버전은 Reporting Services의 2016, 2017 및 2019 버전과 완전히 호환됩니다. 또한 Power BI Report Server의 모든 릴리스 및 지원 버전과도 호환됩니다.

::: moniker-end

::: moniker range=">=sql-server-2017"

## <a name="sql-server-2017-reporting-services"></a>SQL Server 2017 Reporting Services

**다운로드** :::image type="icon" source="https://docs.microsoft.com/analysis-services/analysis-services/media/download.png":::

SQL Server 2017 Reporting Services를 다운로드하려면 **[Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=55252)** 로 이동하세요.

### <a name="comments-on-reports"></a>보고서에 대한 주석

이제 보고서에서 주석을 사용하여 큐브 뷰를 추가하고 다른 사용자와 협업할 수 있습니다. 주석에 첨부 파일도 포함할 수 있습니다.

![보고서 서버 내의 주석](media/what-s-new-in-sql-server-reporting-services-ssrs/report-server-comments.png)

자세한 내용은 [보고서 서버에서 보고서에 주석 추가](https://powerbi.microsoft.com/documentation/reportserver-add-comments/)를 참조하세요.

### <a name="dax-queries-in-reporting-tools"></a>보고 도구의 DAX 쿼리

보고서 작성기 및 SQL Server Data Tools의 최신 릴리스에서 SQL Server Analysis Services 테이블 형식 데이터 모델에 대한 네이티브 DAX 쿼리를 만들 수 있습니다. 쿼리 디자이너에서 필드를 끌어서 놓을 수 있습니다. [Reporting Services blog](https://blogs.msdn.microsoft.com/sqlrsteamblog/2017/03/09/query-designer-support-for-dax-now-available-in-report-builder-and-sql-server-data-tools/)(Reporting Services 블로그)를 참조하세요.

### <a name="rest-api-support"></a>REST API 지원

최신 애플리케이션 및 사용자 지정 개발을 사용하기 위해 SQL Server Reporting Services는 이제 완벽하게 OpenAPI 규격 RESTful API를 지원합니다. 전체 API 사양 및 설명서는 이제 [SwaggerHub](https://app.swaggerhub.com/apis/microsoft-rs/SSRS/2.0)에서 확인할 수 있습니다.

### <a name="query-designer-support-for-dax-now-in-report-builder-and-sql-server-data-tools"></a>보고서 작성기 및 SQL Server Data Tools에서 DAX에 대한 쿼리 디자이너 지원

이제 보고서 작성기와 SQL Server Data Tools에서 지원되는 SQL Server Analysis Services 테이블 형식 데이터 모델에 대한 네이티브 DAX 쿼리를 만들 수 있습니다. 두 도구 모두에서 쿼리 디자이너를 사용하여 원하는 필드를 끌어서 놓을 수 있습니다. 그런 다음, DAX 쿼리를 생성합니다.

[Reporting Services 블로그](https://blogs.msdn.microsoft.com/sqlrsteamblog/2017/03/09/query-designer-support-for-dax-now-available-in-report-builder-and-sql-server-data-tools/)를 참고하세요.

* [SQL Server 보고서 작성기](https://go.microsoft.com/fwlink/?LinkId=734968)를 다운로드합니다.
* [SQL Server Data Tools - 릴리스 후보](https://docs.microsoft.com/sql/ssdt/sql-server-data-tools-ssdt-release-candidate)를 다운로드합니다.

> [!NOTE]
> SSAS 테이블 형식 데이터 원본 기본 제공 SQL Server 2016+에서만 DAX에 대한 쿼리 디자이너를 사용할 수 있습니다.
::: moniker-end

## <a name="ssrs-2016"></a>SSRS 2016

### <a name="reporting-services-ssrswebportal-non-markdown"></a>Reporting Services [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)]  

새 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)]을 사용할 수 있습니다. 업데이트된 웹 포털에는 다음이 포함됩니다.
- KPI
- 모바일 보고서
- 페이지를 매긴 보고서
- Excel 파일
- Power BI Desktop 파일

[!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 은 이전 릴리스의 보고서 관리자를 대체한 것입니다.

모바일 보고서를 만들려면 [!INCLUDE[SS_MobileReptPub_Short](../includes/ss-mobilereptpub-short.md)]가 필요합니다.

[!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)]에 대한 자세한 내용은 [웹 포털(SSRS 기본 모드)](../reporting-services/web-portal-ssrs-native-mode.md)을 참조하세요.  

![SQL Server Reporting Services 포털을 보여 주는 스크린샷](../reporting-services/media/ssrsportal.png "ssRSPortal")  

#### <a name="custom-branding-for-the-ssrswebportal-non-markdown"></a>[!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)]에 대한 사용자 지정 브랜딩 

브랜딩 팩을 사용하여 조직의 로고 및 색상으로 [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] 을 사용자 지정할 수 있습니다.  

사용자 지정 브랜딩에 대한 자세한 내용은 [웹 포털 브랜딩](https://msdn.microsoft.com/6dac97f7-02a6-4711-81a3-e850a6b40bf1)을 참조하세요.

#### <a name="key-performance-indicators-kpi-in-the-ssrswebportal-non-markdown"></a>[!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)]의 KPI(핵심 성과 지표) 

현재 폴더 상황에 맞는 [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)]에 KPI를 직접 만들 수 있습니다. KPI를 만들 때 데이터 세트 필드를 선택하고 해당 값을 요약할 수 있습니다. 드릴수루할 관련 콘텐츠를 선택하여 세부 정보를 공개할 수도 있습니다.

![SQL Server Reporting Services 포털에서 KPI를 보여 주는 스크린샷](../reporting-services/media/ssrs-webportal-kpi.png)

자세한 내용은 [웹 포털에서 KPI 사용](https://msdn.microsoft.com/a28cf500-6d47-4268-a248-04837e7a09eb)을 참조하세요.

### <a name="mobile-reports"></a>모바일 보고서

Reporting Services 모바일 보고서는 다양한 폼 팩터에 최적화된 전용 보고서로서, 모바일 디바이스에서 보고서에 액세스하는 사용자에게 최적의 환경을 제공합니다. 모바일 보고서는 시간, 범주 및 비교 차트부터 트리 맵 및 사용자 지정 맵까지의 다양한 시각화 기능을 사용합니다. 온-프레미스 SQL Server Analysis Services 다차원 및 테이블 형식 데이터를 포함하여 모바일 보고서를 다양한 데이터 원본에 연결합니다. 표 행과 열을 조정하여 디자인 화면에 모바일 보고서용 필드를 배치할 수 있습니다. 유연한 모바일 보고서 요소는 모든 화면 크기에 맞게 자동으로 조정합니다. 보바일 보고서를 Reporting Service 서버에 저장하고 브라우저 또는 Power BI 모바일 앱에서 이를 보고 상호 작용할 수 있습니다. 지원되는 디바이스에는 다음이 포함됩니다.

- iPad
- iPhone
- Android 휴대폰
- 또는 모든 Windows 10 디바이스

#### <a name="mobile-report-publisher"></a>모바일 보고서 게시자  

[!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)]를 사용하여 SQL Server 모바일 보고서를 만들고 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)]에 게시할 수 있습니다.  

![SS_MRP_LayoutTabSmall](../reporting-services/media/ss-mrp-layouttabsm.png "SS_MRP_LayoutTabSmall")  

자세한 내용은 [SQL Server 모바일 보고서 게시자를 사용하여 모바일 보고서 만들기](../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)를 참조하세요.  

#### <a name="sql-server-mobile-reports-hosted-in-reporting-services-available-in-power-bi-mobile-app"></a>Power BI 모바일 앱에서 사용할 수 있는 Reporting Services에서 호스트되는 SQL Server 모바일 보고서  

이제 iPad 및 iPhone의 iOS용 Power BI 모바일 앱에서 로컬 보고서 서버에서 호스트되는 SQL Server 모바일 보고서를 표시할 수 있습니다.  

![SS_MRP_iPad_HomeSm](../reporting-services/media/ss-mrp-ipad-homesm.png "SS_MRP_iPad_HomeSm")  

일부 구성 변경 없이는 기본적으로 연결할 수 없습니다. Power BI 모바일 앱을 보고서 서버에 연결하는 방법에 대한 자세한 내용은 [Power BI 모바일 액세스가 가능하도록 보고서 서버 설정](../reporting-services/report-server/enable-a-report-server-for-power-bi-mobile-access.md)을 참조하세요.

### <a name="support-of-sharepoint-mode-and-sharepoint-2016"></a>SharePoint 모드 및 SharePoint 2016 지원  

[!INCLUDE[ssSQL15](../includes/sssql15-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]는 SharePoint 2013 및 SharePoint 2016과의 통합을 지원합니다.

자세한 내용은 다음을 참조하세요.  

- [지원되는 SharePoint와 Reporting Services 서버 및 추가 기능의 조합&#40;SQL Server 2016&#41;](../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  

- [SharePoint 제품용 Reporting Services 추가 기능 검색 위치](../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  

- [Reporting Services SharePoint 모드 설치](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)  

### <a name="microsoft-net-framework-4-support"></a>Microsoft .NET Framework 4 지원  

[!INCLUDE[ssRSCurrent-md](../includes/ssrscurrent-md.md)]는 버전 4.0 및 4.5.1을 포함한 현재 버전의 Microsoft .NET Framework 4를 지원합니다. .Net Framework 4.x 버전이 아직 설치되지 않은 경우 [!INCLUDE[ssNoVersion-md](../includes/ssnoversion-md.md)]에서 기능 설치 단계 중에 .NET 4.0을 설치합니다.  

### <a name="report-improvements"></a>보고서 고급 기능

**HTML 5 렌더링 엔진:** 최신 웹 "완전" 표준 모드 및 최신 브라우저를 대상으로 하는 새로운 HTML5 렌더링 엔진이 제공됩니다.  새 렌더링 엔진은 몇몇 이전 브라우저에서 사용하는 쿼크 모드에 더 이상 의존하지 않습니다.

브라우저 지원에 대한 자세한 내용은 [Reporting Services 및 파워 뷰에 대한 브라우저 지원](../reporting-services/browser-support-for-reporting-services-and-power-view.md)을 참조하세요.  

**페이지가 매겨진 세련된 보고서:** 차트, 계기, 지도 및 기타 데이터 시각화에 대한 새롭고 최신 스타일을 사용하여 페이지가 매겨진 세련된 보고서를 디자인할 수 있습니다.

**트리 맵과 선버스트 차트:** 트리 맵 ![ssrs_treemap_icon](../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon") 및 선버스트 ![ssrs_sunburst_icon](../reporting-services/media/ssrs-sunburst-icon.png "ssrs_sunburst_icon") 차트를 사용하여 보고서를 개선합니다. 계층적 데이터를 표시하는 데 유용한 방법입니다. 자세한 내용은 [Tree Map and Sunburst Charts in Reporting Services](../reporting-services/report-design/tree-map-and-sunburst-charts-in-reporting-services.md)를 참조하세요.  

**보고서 포함:** 이제 URL 매개 변수와 함께 iframe을 사용하여 다른 웹 페이지와 애플리케이션에 모바일 및 페이지가 매겨진 보고서를 포함할 수 있습니다.  

**Power BI 대시보드에 보고서 항목 고정:**[!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]에서 보고서를 보는 동안 보고서 항목을 선택하여 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 대시보드에 고정할 수 있습니다.   고정할 수는 항목은 차트, 계기 패널, 지도 및 이미지입니다. 다음을 수행할 수 있습니다.

1. 고정하려는 대시보드가 포함된 그룹을 선택합니다.
2. 항목을 고정할 대시보드를 선택합니다.
3. 대시보드에서 타일을 업데이트할 빈도를 선택합니다.

![참고](https://docs.microsoft.com/analysis-services/analysis-services/instances/install-windows/media/ssrs-fyi-note.png "참고") 새로 고침은 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 구독에 의해 관리되며 항목이 고정된 후 구독을 편집하고 다른 새로 고침 일정을 구성할 수 있습니다.

![Power BI 대시보드에 고정 대화 상자를 보여 주는 스크린샷](../reporting-services/media/ssrs-pin-to-powerbi.png) 

자세한 내용은 [Power BI 보고서 서버 통합&#40;Configuration Manager&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md) 및 [Power BI 대시보드에 Reporting Services 항목 고정](../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md)을 참조하세요.  

**PowerPoint 렌더링 및 내보내기:** Microsoft PowerPoint(PPTX) 형식은 새로운 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 렌더링 확장입니다. 일반적인 애플리케이션(보고서 작성기, 보고서 디자이너 (SSDT), [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)])에서 PPTX 형식으로 보고서를 내보낼 수 있습니다. 예를 들어 다음 이미지는 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]의 내보내기 메뉴를 보여 줍니다. 

![PowerPoint 옵션이 호출된 내보내기 드롭다운 목록을 보여 주는 스크린샷](../reporting-services/media/ssrs-export-powerpoint.png) 

구독 출력에 대해 PPTX 형식을 선택한 후 보고서 서버 URL 액세스를 사용하여 보고서를 렌더링하고 내보낼 수도 있습니다. 예를 들어 브라우저의 다음 URL 명령은 보고서 서버의 명명된 인스턴스에서 보고서를 내보냅니다.  

```https
https://servername/ReportServer_THESQLINSTANCE/Pages/ReportViewer.aspx?%2freportfolder%2freport+name+with+spaces&rs:Format=pptx  
```  

자세한 내용은 [Export a Report Using URL Access](../reporting-services/export-a-report-using-url-access.md)를 참조하세요.

**원격 인쇄용 ActiveX를 대체하는 PDF:** 이제 보고서 뷰어 도구 모음이 ActiveX 컨트롤 대신 PDF를 통해 출력됩니다. 새 보고서 뷰어는 Microsoft Edge를 비롯한 대부분의 최신 브라우저에서 지원됩니다. 다운로드할 ActiveX 컨트롤이 없습니다! 사용하는 브라우저와 설치한 PDF 보기 애플리케이션 및 서비스에 따라 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 보고서를 인쇄할 인쇄 대화 상자를 열거나 .PDF 파일을 다운로드하라는 메시지가 표시됩니다. 관리자는 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]에서 클라이언트 쪽 인쇄를 사용하지 않도록 설정할 수 있습니다.

자세한 내용은 [Reporting Services에 대한 클라이언트 쪽 인쇄 기능 설정 및 해제](../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)를 참조하세요.

![인쇄 대화 상자의 스크린샷](../reporting-services/media/ssrs-pdf-printing.png)

### <a name="subscription-improvements"></a>구독 개선 사항  

|기능|지원되는 서버 모드|  
|-------------|---------------------------|  
|**구독 설정 및 해제**. 새로운 사용자 인터페이스 옵션을 통해 신속하게 구독을 설정하고 해제할 수 있습니다. 해제된 구독에는 일정과 같은 다른 구성 속성이 유지되며 손쉽게 설정이 가능합니다.<br /><br /> ![사용, 사용 안 함 및 삭제 옵션을 보여 주는 스크린샷](../reporting-services/media/ssrs-enable-disable-subscriptions.png)<br /><br /> 자세한 내용은 [Disable or Pause Report and Subscription Processing](../reporting-services/subscriptions/disable-or-pause-report-and-subscription-processing.md)를 참조하세요.|기본 모드|  
|**구독 설명**. 새 구독을 만들 때 이제 구독 속성의 일부로 보고서에 대한 설명을 포함할 수 있습니다. 설명은 구독 요약 페이지에 포함됩니다.|SharePoint 모드 및 기본 모드|  
|**구독 소유자 변경**. 구독 소유자를 신속하게 변경할 수 있도록 사용자 인터페이스가 향상되었습니다. 이전 버전의 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 에서는 관리자가 스크립트를 사용하여 구독 소유자를 변경할 수 있습니다. [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 릴리스부터 사용자 인터페이스 또는 스크립트를 사용하여 구독 소유자를 변경할 수 있습니다. 구독 소유자 변경은 사용자가 퇴사하거나 조직에서 역할이 변경된 경우에 수행되는 일반적인 관리 작업입니다.|SharePoint 모드 및 기본 모드|  
|**파일 공유 구독에 대한 공유 자격 증명**. 이제 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 파일 공유 구독에서 사용할 수 있는 두 가지 워크플로가 있습니다.<br /><br /> 이 릴리스의 새로운 기능으로, [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 관리자는 여러 구독에서 사용할 수 있는 단일 파일 공유 계정을 구성할 수 있습니다. 파일 공유 계정은 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 네이티브 모드 구성 관리자 **파일 공유 계정 지정** 에서 구성됩니다. 구독 구성 페이지에서 사용자는 **파일 공유 계정 사용** 을 선택합니다.<br /><br /> 대상 파일 공유에 대한 특정 자격 증명으로 개별 구독을 구성합니다.<br /><br /> 또한, 두 가지 방법을 혼용하여 일부 파일 공유 구독은 중앙식 파일 공유 계정을 사용하고 다른 구독은 특정 자격 증명을 사용하도록 할 수 있습니다.|기본 모드|

### <a name="sql-server-data-tools-ssdt"></a>SSDT(SQL Server Data Tools)

SSDT의 새 릴리스에는 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]의 프로젝트 템플릿이 포함되어 있습니다. 보고서 서버 프로젝트 마법사 및 보고서 서버 프로젝트. SSDT를 다운로드하는 방법에 대한 자세한 내용은 [Visual Studio 2015용 SQL Server Data Tools](https://go.microsoft.com/fwlink/?LinkId=827542)를 참조하세요.  

### <a name="report-builder-improvements"></a>보고서 작성기 고급 기능

**새 보고서 작성기 사용자 인터페이스:** 핵심 [!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)] 사용자 인터페이스가 이제 간소화된 UI 요소가 포함된 세련된 디자인으로 바뀌었습니다.  

|새로 만들기|Previous|  
|-|-|  
|![ssrs_rbfacelift_new](../reporting-services/media/ssrs-rbfacelift-new.png "ssrs_rbfacelift_new")|![ssrs_rbfacelift_old](../reporting-services/media/ssrs-rbfacelift-old.png "ssrs_rbfacelift_old")|  

**사용자 지정 매개 변수 창:** 이제 매개 변수 창을 사용자 지정할 수 있습니다. 보고서 작성기의 디자인 화면을 사용하여 매개 변수 창의 특정 열과 행에 매개 변수를 끌어 넣을 수 있습니다. 열을 추가하거나 제거하여 창 레이아웃을 변경할 수 있습니다. 자세한 내용은 [보고서에서 매개 변수 창 사용자 지정&#40;보고서 작성기&#41;](../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md)에서 만드는 모바일 보고서에서 보고서 매개 변수를 사용할 수 있습니다.  

![보고서 데이터 창 및 매개 변수 창의 매개 변수 목록](../reporting-services/media/ssrs-customizeparameter-parameterlist-reportdatapane.png "보고서 데이터 창 및 매개 변수 창의 매개 변수 목록")  

**높은 DPI 지원:** [!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)]는 높은 DPI(인치당 도트 수) 배율 및 디바이스를 지원합니다.  높은 DPI에 대한 자세한 내용은 다음을 참조하세요.  

- [Windows 8.1 DPI 배율 향상된 기능](https://blogs.windows.com/windowsexperience/2013/07/15/windows-8-1-dpi-scaling-enhancements/)  

- [높은 DPI 및 Windows 8.1](https://technet.microsoft.com/library/dn528848.aspx)  

## <a name="next-steps"></a>다음 단계

[Analysis Services의 새로운 기능](https://msdn.microsoft.com/aa69c299-b8f4-4969-86d8-b3292fe13f08)  
[이전 버전과의 호환성](reporting-services-backward-compatibility.md)  
[SQL Server 버전에서 지원하는 Reporting Services 기능](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)  
[Reporting Services 업그레이드 및 마이그레이션](../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)  
[Reporting Services](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
