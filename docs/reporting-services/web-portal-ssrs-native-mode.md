---
title: "웹 포털(SSRS 기본 모드) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: 7349e626-6ed5-4d21-b05f-cf042ad9ad70
caps.latest.revision: 15
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: dcf26be9dc2e502b2d01f5d05bcb005fd7938017
ms.openlocfilehash: e3dff8b613f933caa84522b31bdc862aa9c799f7
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="web-portal-ssrs-native-mode"></a>웹 포털(SSRS 기본 모드)

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Reporting Services 웹 포털은 보고서, 모바일 보고서, KPI를 보고 보고서 서버 인스턴스에 있는 요소로 이동할 수 있는 웹 기반 환경입니다. 웹 포털을 사용하여 단일 보고서 서버 인스턴스를 관리할 수도 있습니다.

![ssRSPortal](../reporting-services/media/ssrsportal.png)

## <a name="what-is-the-web-portal"></a>웹 포털이란?

웹 포털을 사용하여 다음 작업을 수행할 수 있습니다.

- 보고서 보기, 검색, 인쇄, 구독

- 서버의 항목을 체계적으로 구성하도록 폴더 계층 구조 생성, 보안 설정 및 유지 관리

- 항목 및 작업에 대한 액세스 권한을 결정하는 역할 기반 보안 구성

- 보고서 실행 속성, 보고서 기록, 보고서 매개 변수 구성

- 일정 및 데이터 원본 연결을 편리하게 관리하기 위해 공유 일정 및 공유 데이터 원본 만들기

- 다수의 받는 사람 목록에 보고서를 전달하는 데이터 기반 구독 만들기

- 기존 보고서를 다른 방식으로 다시 사용하고 용도를 변경하기 위해 링크된 보고서 만들기

- 보고서 작성기, 모바일 보고서 게시자 등의 공통 도구 다운로드

- [KPI 만들기](../reporting-services/working-with-kpis-in-reporting-services.md)

- 피드백 보내기 또는 기능 요청

웹 포털을 사용하여 보고서 서버 폴더를 찾아보거나 특정 보고서를 검색할 수 있습니다. 보고서, 해당 일반 속성 및 보고서 기록에 캡처된 보고서의 지난 복사본을 볼 수 있습니다. 권한에 따라 보고서를 구독하여 전자 메일 받은 편지함 또는 파일 시스템의 공유 폴더로 배달되도록 할 수도 있습니다.

> [!NOTE]
> 지원되는 브라우저와 버전에 대한 자세한 내용은 [Reporting Services 브라우저 지원 계획](../reporting-services/browser-support-for-reporting-services-and-power-view.md)을 참조하십시오.

웹 포털은 기본 모드로 실행되는 보고서 서버에만 사용되며 SharePoint 통합 모드용으로 구성된 보고서 서버에 대해서는 지원되지 않습니다.

일부 웹 포털 기능은 지정된 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion.md)]에서만 사용할 수 있습니다. 자세한 내용은 [SQL Server 2016 버전에서 지원하는 Reporting Services 기능](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)을 참조하세요.

새로 설치하는 경우 로컬 관리자에게만 내용 및 설정을 사용할 수 있는 권한이 부여됩니다. 다른 사용자에게 사용 권한을 부여하려면 로컬 관리자가 보고서 서버에 대한 액세스 권한을 제공하는 역할 할당을 만들어야 합니다. 사용자가 이후에 액세스할 수 있는 응용 프로그램 페이지 및 태스크는 해당 사용자에 대한 역할 할당에 따라 달라집니다. 자세한 내용은 [사용자에게 보고서 서버에 대한 액세스 권한 부여](security/grant-user-access-to-a-report-server-report-manager.md)를 참조하세요.

> [!NOTE]
> 서버가 실행 중인 로컬 컴퓨터에서 웹 포털을 탐색하는 경우 이 폴더를 볼 수 없다는 메시지가 표시될 수 있습니다. 이유는 UAC(Universal Access Control) 때문이거나 브라우저를 관리자로 실행하고 있지 않기 때문일 수 있습니다. Edge는 관리자 자격으로 실행할 수 없습니다. Internet Explorer를 사용해야 합니다. 서버를 원격으로 탐색하거나 Internet Explorer를 관리자 자격으로 시작하고 웹 포털을 탐색할 수 있습니다. 웹 포털을 원격에서 사용하려는 경우 계정 내용 관리자에게 폴더에 권한을 부여해야 합니다.  

## <a name="start-and-use-the-web-portal"></a>웹 포털 시작 및 사용

웹 포털은 브라우저 창의 주소 표시줄에 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] URL을 입력하여 여는 웹 응용 프로그램입니다. [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]을 시작하면 보고서 서버에 대한 권한을 기준으로 표시되는 페이지, 링크, 옵션이 달라집니다. 특정 태스크를 수행하기 위해서는 해당 태스크를 포함하는 역할이 할당되어야 합니다.  모든 권한이 있는 역할이 할당된 사용자는 보고서 서버를 관리하는 데 사용할 수 있는 응용 프로그램의 모든 메뉴와 페이지에 액세스할 수 있습니다. 그러나 보고서를 보고 실행할 수 있는 권한이 있는 역할이 할당된 사용자는 이러한 작업을 지원하는 메뉴와 페이지만 볼 수 있습니다. 각 사용자는 각 보고서 서버에 대해 다른 역할을 할당 받을 수 있으며, 단일 보고서 서버에 저장된 여러 보고서 및 폴더에 대해서도 각기 다른 역할을 할당 받을 수 있습니다.

역할에 대해 자세히 알아보려면 [기본 모드 보고서 서버에 대한 사용 권한 부여](../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)를 참조하십시오.

### <a name="start-the-web-portal"></a>웹 포털 시작

브라우저에서 웹 포털을 시작하려면 다음을 수행합니다.

1. 웹 브라우저를 엽니다. 지원되는 웹 브라우저를 보려면 [Reporting Services 브라우저 지원 계획](../reporting-services/browser-support-for-reporting-services-and-power-view.md)을 참조하십시오.

2. 웹 브라우저의 주소 표시줄에 웹 포털 URL을 입력합니다.

    기본적으로 이 URL은 *http://[ComputerName]/reports*입니다.

    특정 포트를 사용하도록 보고서 서버를 구성할 수 있습니다. 예: *http://[ComputerName]:80/reports* 또는 *http://[ComputerName]:8080/reports*을 참조하십시오.

## <a name="grouping-by-categories"></a>범주별 그룹화

웹 포털은 그룹 항목을 여러 범주로 그룹화합니다. 사용 가능한 범주는 다음과 같습니다.

- KPI
- 모바일 보고서
- 페이지를 매긴 보고서
- Power BI Desktop 보고서
- Excel 통합 문서
- 데이터 집합
- 데이터 원본
- 리소스

오른쪽 상단에서 **보기** 를 선택하여 표시되는 항목을 관리할 수 있습니다. 숨김 표시를 선택할 경우 해당 항목은 흐린 색으로 표시됩니다.

![ssRSWebPortal-view](../reporting-services/media/ssrswebportal-view.png)

![ssRSWebPortal-hidden](../reporting-services/media/ssrswebportal-hidden.png)

### <a name="power-bi-desktop-reports-and-excel-workbooks"></a>Power BI Desktop 보고서 및 Excel 통합 문서

Power BI Desktop 보고서 및 Excel 통합 문서에 대한 권한을 업로드, 구성, 관리할 수 있습니다. 이러한 권한은 웹 포털 안에서 그룹화됩니다.

![ssRSWebPortal-view-pbi-and-excel](../reporting-services/media/ssrswebportal-view-pbi-and-excel.png)

파일은 다른 리소스 파일과 마찬가지로 Reporting Services 안에 저장됩니다. 이러한 항목 중 하나를 선택하면 데스크톱에 로컬로 다운로드됩니다. 변경 사항이 있을 경우 보고서 서버에 다시 업로드하면 변경 사항이 저장됩니다.

## <a name="search-for-items"></a>항목 검색

검색어를 입력하면 액세스할 수 있는 모든 항목이 표시됩니다. 결과는 KPI, 보고서, 데이터 집합, 기타 항목으로 분류됩니다. 그런 다음 결과와 상호 작용하여 즐겨찾기에 추가할 수 있습니다.

![ssRSWebPortal-Search](../reporting-services/media/ssrswebportal-search.png)

## <a name="web-portal-tasks"></a>웹 포털 작업

[웹 포털 브랜딩](../reporting-services/branding-the-web-portal.md)

[KPI 작업](../reporting-services/working-with-kpis-in-reporting-services.md)

[공유 데이터 집합 작업](../reporting-services/work-with-shared-datasets-web-portal.md)

## <a name="see-also"></a>참고 항목

[SQL Server 모바일 보고서 게시자를 사용하여 모바일 보고서 만들기](../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
[URL 구성(SSRS 구성 관리자)](../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
[Reporting Services 도구](../reporting-services/tools/reporting-services-tools.md)  
[Reporting Services 브라우저 지원 계획](../reporting-services/browser-support-for-reporting-services-and-power-view.md)  
[SQL Server 2016 버전에서 지원하는 Reporting Services 기능](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)  

추가 질문이 있으신가요? [Reporting Services 포럼을 이용해 보세요](http://go.microsoft.com/fwlink/?LinkId=620231).
