---
title: "웹 포털 구성 | Microsoft Docs"
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: the web portal [Reporting Services], configuring
ms.assetid: e918986c-af15-48f6-8178-256aed829c6a
caps.latest.revision: "28"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 49c2a379f7baf0ceecb5bf09dd9e903eb61e97be
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="configure-the-web-portal"></a>웹 포털 구성

웹 포털은 보고서를 확인하고 보고서 서버 내용을 관리하며 사용자에게 기본 모드 보고서 서버에 대한 액세스 권한을 부여하는 데 사용되는 웹 프런트 엔드 응용 프로그램입니다. 웹 포털은 보고서 서버 웹 서비스와 동일한 보고서 서버 인스턴스 내에 설치되며 설치 시 **기본값인 기본 모드 구성으로 설치** 옵션을 선택하면 구성됩니다. 웹 포털을 사후 설치 작업으로 구성할 수도 있습니다. 이 항목에서는 다음과 같은 웹 포털 구성 시나리오에 대한 정보를 제공합니다.

## <a name="prerequisites"></a>필수 구성 요소

웹 포털을 사용하려면 다음과 같은 전제 조건을 충족해야 합니다.

- 최소한으로 구성된 보고서 서버가 있어야 합니다. 보고서 서버를 최소한으로 구성하는 방법은 [보고서 서버 구성](../../reporting-services/report-server/configure-a-report-server-reporting-services-native-mode.md)을 참조하세요.

- 보고서 서버를 기본 모드로 실행해야 합니다. SharePoint 통합 모드로 구성된 보고서 서버에서 웹 포털을 사용할 수 없습니다. SQL Server 2012 에서는 보고서 서버를 한 모드에서 다른 모드로 전환할 수 없습니다. 환경에 사용되는 보고서 서버 유형을 변경하려면 원하는 보고서 서버 모드를 설치하고 보고서 항목을 새 보고서 서버로 복사하거나 이동해야 합니다. 이러한 프로세스를 일반적으로 '마이그레이션'이라고 합니다. 마이그레이션하는 데 필요한 단계는 마이그레이션할 모드 및 원본 버전에 따라 달라집니다. 자세한 내용은 [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)을 참조하세요.

- 스크립팅이 사용되는 Internet Explorer 11 이상도 필요합니다. 자세한 내용은 [Reporting Services 및 파워 뷰에 대한 브라우저 지원](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)을 참조하세요.

## <a name="configure-the-web-portal-to-use-the-default-url"></a>기본 URL을 사용하도록 웹 포털 구성

웹 포털은 웹 브라우저에서 사용자가 액세스하는 웹 응용 프로그램입니다. 적어도 브라우저 창에서 이 응용 프로그램을 여는 데 사용되는 URL은 정의해야 합니다. URL은 호스트 이름, 포트 및 가상 디렉터리로 구성됩니다. 이 URL에 대한 기본값에는 보고서 서버 웹 서비스 URL에 대해 정의된 호스트 이름 및 포트 값과 **reports** 가상 디렉터리 이름이 포함됩니다. 명명된 인스턴스가 있을 경우 가상 디렉터리는 **reports_instance**입니다. 여기서 **instance** 는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스의 이름입니다.

기본적으로 웹 포털 URL은 고유한 가상 디렉터리 이름과 동일 인스턴스에서 실행되는 보고서 서버 웹 서비스에 대해 정의된 포트 및 호스트 이름으로 구성됩니다. 대부분의 경우 호스트 이름은 보고서 서버 컴퓨터의 네트워크 이름이지만 이 컴퓨터를 식별하는 IP 주소나 호스트 헤더가 될 수도 있습니다. 웹 포털이 기본 URL을 사용하도록 구성하려면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구의 **웹 포털 URL** 페이지를 사용합니다.

> [!TIP]
> 원격 컴퓨터에서 웹 포털에 액세스할 때 브라우저에 연결 오류 메시지가 표시되는 경우 일반적으로 방화벽 설정이 원인입니다. 자세한 내용은 [보고서 서버 액세스를 위한 방화벽 구성](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)을 참조하세요.

#### <a name="to-configure-the-default-the-web-portal-url-and-virtual-directory"></a>기본 웹 포털 URL 및 가상 디렉터리를 구성하려면

1. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 시작한 다음 보고서 서버 인스턴스에 연결합니다.

2. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구에서 **웹 포털 URL**을 선택하여 URL을 구성하는 페이지를 엽니다.

3. 웹 포털에 고유한 가상 디렉터리 이름을 입력합니다.

4. **적용**을 클릭합니다.

5. [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] 또는 Windows Server 2008을 사용하는 경우 웹 포털을 사용하기 위해서는 추가 단계를 수행해야 할 수 있습니다. 자세한 내용은 [로컬 관리에 대해 기본 모드 보고서 서버 구성&#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)를 참조하세요.

## <a name="configure-the-web-portal-to-use-a-specific-report-server-url"></a>특정 보고서 서버 URL을 사용하도록 웹 포털 구성

기본적으로 웹 포털은 동일한 보고서 서버 서비스에서 실행되는 보고서 서버 웹 서비스에 연결하며, 이 때 보고서 서버 웹 서비스 URL을 사용합니다. 보고서 서버 웹 서비스에 대한 URL을 여러 개 정의한 경우 웹 포털은 사용자가 마지막으로 정의한 것을 사용합니다. 하지만 어떤 배포에서는 웹 포털이 항상 정적 URL을 통해 웹 서비스에 연결하도록 해야 합니다. 특정 포트 또는 IP 주소에 대한 패킷 필터링을 구성한 후 보고서 서버에 대한 모든 연결이 사용자가 정의한 필터 규칙을 통과하도록 하려는 경우를 예로 들 수 있습니다.

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구에서 URL을 구성할 때 웹 포털은 동일한 서버 인스턴스에서 실행되는 보고서 서버에 대한 새 URL 및 업데이트된 URL을 자동으로 검색하여 사용합니다. 배포에서 모든 보고서 서버 요청에 대해 단일 정적 URL을 사용해야 하는 경우 RSReportServer.config 파일에 해당 URL을 지정하면 됩니다.

#### <a name="to-configure-a-static-report-server-url"></a>정적 보고서 서버 URL을 구성하려면

1. 텍스트 편집기에서 **RSReportServer.config** 파일을 엽니다. 기본적으로 이 파일은 \Program Files\Microsoft SQL Server\MSRS12.\<*instancename*>\Reporting Services\ReportServer에 있습니다.  

2. **ReportServerURL**을 찾습니다.

3. 이 URL을 보고서 서버 인스턴스의 URL로 바꿉니다.

4. 변경 내용을 저장하고 파일을 닫습니다.

구성 파일에 대한 자세한 내용은 [Reporting Services 구성 파일 수정&#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) 및 [RsReportServer.config 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)을 참조하세요.

## <a name="customize-styles-or-application-title"></a>스타일 또는 응용 프로그램 제목 사용자 지정

사용자 지정 브랜드 패키지를 만들어서 웹 포털에 사용되는 색상을 변경할 수 있습니다. 자세한 내용은 [웹 포털 브랜딩](../branding-the-web-portal.md)을 참조하세요.

#### <a name="to-modify-application-title"></a>응용 프로그램 제목을 수정하려면

1. 보고서 서버에 대한 **시스템 관리자** 권한이 할당된 계정을 사용하여 로그온합니다.

2. Internet Explorer를 엽니다.

3. 웹 포털 URL을 입력합니다. 기본적으로 이 URL은 http://\<**your-server-name**>/reports이지만 Reporting Services를 명명된 인스턴스로 설치한 경우 기본 URL은 http://\<**your-server-name**>/reports\<**_instancename**>입니다.

4. **사이트 설정**을 선택합니다.

5. **일반** 탭의 **이름**에서 **SQL Server Reporting Services** 를 다른 이름으로 바꿉니다.

6. **적용**을 선택합니다.

## <a name="next-steps"></a>다음 단계

[웹 포털](../../reporting-services/web-portal-ssrs-native-mode.md)  
[Reporting Services에 대한 브라우저 지원](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)
[URL 구성](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
[Reporting Services 설치 확인](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)   
[Reporting Services 기능 설정 또는 해제](../../reporting-services/report-server/turn-reporting-services-features-on-or-off.md)   
[Reporting Services 기본 모드 보고서 서버 관리](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)   
[RSReportServer 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[로컬 관리에 대해 기본 모드 보고서 서버 구성](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)

 추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
