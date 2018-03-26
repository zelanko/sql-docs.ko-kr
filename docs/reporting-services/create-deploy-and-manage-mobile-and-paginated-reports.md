---
title: Reporting Services(SSRS) | Microsoft Docs
description: 온-프레미스에서 모바일 및 페이지가 매겨진 Reporting Services 보고서와 Power BI 보고서에 대한 도구 및 서비스에 대해 알아봅니다.
ms.custom: ''
ms.date: 07/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: ''
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
helpviewer_keywords:
- reports [Reporting Services]
- SSRS
- reports [Reporting Services], about reports
- Reporting Services
- SQL Server Reporting Services
ms.assetid: b8d18d3d-9db0-43e7-8286-7b46cc3a37ed
caps.latest.revision: ''
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Active
ms.openlocfilehash: 6deaece7d2dd01ebf831820c2e026044f80651de
ms.sourcegitcommit: 3ed9be04cc7fb9ab1a9ec230c298ad2932acc71b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/17/2018
---
# <a name="what-is-sql-server-reporting-services-ssrs"></a>SSRS(SQL Server Reporting Services)란?

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../includes/ssrs-previous-versions.md)]

SSRS(SQL Server Reporting Services)에서 제공하는 즉시 사용 가능한 폭넓은 도구 및 서비스를 통해 프레미스에서 모바일 보고서 및 페이지를 매긴 Reporting Services 보고서를 만들고 배포하고 관리할 수 있습니다.

![SQL Server Reporting Services 모두 함께](../reporting-services/media/ss-reporting-services-all-together.png "SQL Server Reporting Services 모두 함께")

## <a name="create-deploy-and-manage-mobile-and-paginated-reports"></a>모바일 및 페이지가 매겨진 보고서 만들기, 배포 및 관리

SQL Server Reporting Services는 고객이 보고서를 만들고, 게시하고, 관리한 다음 웹 브라우저에서 보거나, 모바일 장치에서 보거나, 받은 편지함에서 메일로 보는지에 관계없이 다양한 방식으로 적절한 사용자에게 제공하기 위해 자신의 프레미스에 배포하는 솔루션입니다.

SQL Server 2016의 Reporting Services에서는 업데이트된 제품군을 제공합니다.

* **"기존" 페이지를 매긴 보고서** 최신 상태로 전환되므로 보고서를 만드는 업데이트된 도구 및 새 기능을 사용하여 현대적인 모양의 보고서를 만들 수 있습니다.
* **새 모바일 보고서** 보고서를 보유하는 다양한 장치 및 다양한 방식에 맞게 조정되는 반응형 레이아웃을 사용합니다.
* **최신 웹 포털** 모든 최신 브라우저에서 볼 수 있습니다. 새 포털에서 모바일 및 페이지가 매겨진 Reporting Services 보고서 및 KPI를 구성하고 표시할 수 있습니다. 포털에서 Excel 통합 문서를 저장할 수도 있습니다.

각각에 대한 자세한 내용은 계속 읽어보세요.

> [!NOTE]
> Power BI Report Server를 찾고 있나요? [Power BI Report Server 시작](https://powerbi.microsoft.com/documentation/reportserver-get-started/)을 참조하세요.

### <a name="whats-new-in-reporting-services"></a>Reporting Services의 새로운 기능

SQL Server 2016 Reporting Services의 새로운 기능에서는 다음 원본이 최신 상태로 유지됩니다.

* [Reporting Services의 새로운 기능](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)
* [SQL Server Reporting Services 팀 블로그](https://blogs.msdn.microsoft.com/sqlrsteamblog/)
* [Guy in a Cube YouTube 채널](https://www.youtube.com/channel/UCFp1vaKzpfvoGai0vE5VJ0w)

## <a name="paginated-reports"></a>페이지를 매긴 보고서

![ssrs-paginated-reports](../reporting-services/media/ssrs-paginated-reports.png)

Reporting Services는 "기존"의 페이지를 매긴 문서 스타일 보고서와 연결되어 있습니다. 이 보고서에는 더 많은 데이터, 더 많은 테이블의 행, 더 많은 페이지가 있습니다. 따라서 인쇄에 최적화된 고정 레이아웃의 완벽한 픽셀 문서(예: PDF 및 Word 파일)를 생성하는 데 적합합니다.

현재에도 코어 BI 워크로드는 존재하므로 현대화했습니다. 이제 [보고서 작성기](../reporting-services/report-builder/report-builder-in-sql-server-2016.md) 또는 [SSDT(SQL Server Data Tools)](../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md)의 보고서 디자이너를 사용하여 업데이트된 새 기능으로 현대적인 모양의 보고서를 만들 수 있습니다.

* 모든 기본 스타일 및 색상표를 업데이트하여 기본적으로 최소화된 새로운 현대적 스타일로 보고서를 만들 수 있습니다.
* 매개 변수 창을 업데이트하여 원하는 방식대로 매개 변수를 정렬할 수 있습니다.
* PowerPoint 같은 새로운 형식으로 내보낼 수 있습니다. PowerPoint의 Reporting Services 시각화는 스크린샷이 아니라 라이브이고 편집 가능합니다.
* 하이브리드 Power BI/Reporting Services 환경을 만들 수 있습니다. Power BI에서 온-프레미스 Reporting Services 보고서를 다시 만들지 않고 해당 보고서의 시각적 개체를 Power BI 대시보드에 고정할 수 있습니다. 그런 다음 Power BI 대시보드의 한 곳에서 모든 항목을 모니터링할 수 있습니다.

## <a name="mobile-reports"></a>모바일 보고서

![ssrs-mobile-reports](../reporting-services/media/ssrs-mobile-reports.png)

모바일 컴퓨팅으로 인해 작업해야 하는 장치가 이동되었습니다. 즉, 오늘날 사람마다 보고 요구 사항이 다릅니다. 태블릿 및 휴대폰을 도입하는 경우 고정 레이아웃 보고서 환경이 제대로 작동하지 않습니다. 넓은 PC 화면용으로 디자인된 환경은 더 작을 뿐만 아니라 세로 또는 가로 방향이 있는 작은 휴대폰 화면에 적합하지 않습니다.

이렇게 현저하게 다른 화면 폼 팩터에 필요한 환경은 고정 레이아웃이 아니라 다양한 장치 및 다양한 방식에 맞게 조정되는 반응형 레이아웃입니다. 따라서 약 1년 전에 취득한 Datazen 기술을 기반으로 하고 제품에 통합된 모바일 보고서라는 새로운 보고서 종류를 추가했습니다. 기존 Datazen 보고서는 [SQL Server Migration Assistant for Datazen(Datazen용 SQL Server Migration Assistant)](https://www.microsoft.com/download/details.aspx?id=53128)을 사용하여 Reporting Services로 마이그레이션할 수 있습니다. 

새로운 [모바일 보고서 게시자](../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md) 앱에서 이러한 모바일 보고서를 만듭니다. 그런 다음 Windows 10, iOS, Android 및 HTML5에 대한 기본 [모바일 장치용 Power BI 앱](https://powerbi.microsoft.com/documentation/powerbi-power-bi-apps-for-mobile-devices/) 에서 Power BI 클라우드에 있는 데이터 및 온-프레미스 SQL Server 2016 Reporting Services 데이터에 액세스할 수 있습니다. 시각화를 만들면 모바일 보고서 게시자가 각각에 대한 샘플 데이터를 자동으로 생성하므로 시각화에 데이터가 어떻게 표시되는지, 각 시각화에서 어떤 종류의 데이터가 제대로 작동하는지 확인할 수 있습니다.

## <a name="web-portal"></a>웹 포털

![ssrs-web-portal](../reporting-services/media/ssrs-web-portal.png)

기본 모드 Reporting Services의 최종 사용자에게 현관은 모든 최신 브라우저에서 볼 수 있는 최신 웹 포털입니다. 새 포털에서 모든 Reporting Services 모바일 및 페이지가 매겨진 보고서 및 KPI에 액세스할 수 있습니다.

고유한 사용자 지정 브랜딩을 웹 포털에 적용할 수 있습니다. 또한 웹 포털에서 바로 KPI를 만들 수 있습니다. KPI는 보고서를 열지 않고도 주요 비즈니스 메트릭을 한번에 브라우저에 표시할 수 있습니다. 

새 웹 포털은 보고서 관리자를 완전히 다시 작성한 것입니다. 이제 이 웹 포털은 Microsoft Edge, Internet Explorer 10 및 11, Chrome, Firefox, Safari, 모든 주요 브라우저 등 최신 브라우저가 최적화된 단일 페이지의 표준 기반 HTML5 앱입니다.

웹 포털의 콘텐츠는 Reporting Services 모바일 및 페이지를 매긴 보고서 및 KPI, Excel 통합 문서, 공유 데이터 집합 및 보고서의 문서 블록으로 사용할 공유 데이터 원본 등 종류별로 구성됩니다. 여기, 기존 폴더 계층 구조에서 안전하게 저장하고 관리할 수 있습니다. 즐겨찾기에 태그를 지정할 수 있으며, 해당 역할이 있는 경우 콘텐츠를 관리할 수 있습니다.

또한 보고서 처리를 예약하고, 필요할 때 보고서에 액세스하며, 새 웹 포털에서 게시된 보고서를 구독할 수 있습니다.

[웹 포털(SSRS 기본 모드)](../reporting-services/web-portal-ssrs-native-mode.md)에 대해 자세히 알아봅니다.

## <a name="reporting-services-in-sharepoint-integrated-mode"></a>SharePoint 통합 모드의 Reporting Services

SharePoint 통합 모드의 Repoorting Services에 보고서를 게시합니다. 보고서 처리를 예약하고, 필요할 때 보고서에 액세스하며, 게시된 보고서를 구독하고, 보고서를 Microsoft Excel과 같은 다른 응용 프로그램으로 내보낼 수 있습니다. 또한 SharePoint 사이트에 게시된 보고서에 대한 데이터 경고를 만들고 보고서 데이터가 변경되면 전자 메일 메시지를 수신할 수 있습니다.  

[SharePoint 통합 모드의 Reporting Services 보고서 서버](../reporting-services/report-server-sharepoint/reporting-services-report-server-sharepoint-mode.md)에 대해 자세히 알아보세요.

## <a name="includessrsnoversionincludesssrsnoversion-mdmd-programming-features"></a>[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 프로그래밍 기능

[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 프로그래밍 기능을 활용하면 사용자 지정 응용 프로그램에서 데이터 및 보고서 처리 기능을 통합하거나 확장하는 API를 통해 보고 기능을 확장하고 사용자 지정할 수 있습니다.

[Reporting Services 개발자 설명서](../reporting-services/reporting-services-developer-documentation.md)를 참조하세요. 

## <a name="next-steps"></a>다음 단계

* [Reporting Services 설치](../reporting-services/install-windows/install-reporting-services.md)  
* [보고서 작성기 설치](../reporting-services/install-windows/install-report-builder.md)   
* [SSDT(SQL Server Data Tools) 다운로드](http://go.microsoft.com/fwlink/?LinkID=616714)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
