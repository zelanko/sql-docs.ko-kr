---
title: "웹 포털을 구성 | Microsoft Docs"
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- the web portal [Reporting Services], configuring
ms.assetid: e918986c-af15-48f6-8178-256aed829c6a
caps.latest.revision: 28
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: c0c6cc27711140e96bbf4420e8de596af53ddfcd
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="configure-the-web-portal"></a>웹 포털 구성

웹 포털은 보고서 보기, 보고서 서버 내용을 관리 및 기본 모드 보고서 서버에 대 한 사용자 액세스 권한을 부여 하는 데 사용 하는 웹 프런트 엔드 응용 프로그램. 웹 포털을 동일한 보고서 서버 인스턴스 내에서 보고서 서버 웹 서비스와 함께 설치 하 고 선택 하면 필요에 따라 구성의 **기본 모드 기본 구성 설치** 설치 프로그램의 옵션입니다. 설치 후 태스크로 웹 포털을 구성할 수도 있습니다. 이 항목에서는 다음에 대 한 정보는 웹 포털 구성 시나리오:

## <a name="prerequisites"></a>필수 구성 요소

웹 포털을 사용 하려면 다음과 같은 전제 조건을 충족 해야 합니다.

- 최소한으로 구성된 보고서 서버가 있어야 합니다. 보고서 서버를 최소한으로 구성 하는 방법에 대 한 자세한 내용은 참조 [보고서 서버 구성](../../reporting-services/report-server/configure-a-report-server-reporting-services-native-mode.md)합니다.

- 보고서 서버를 기본 모드로 실행해야 합니다. SharePoint 통합 모드로 구성 된 보고서 서버와 웹 포털을 사용할 수 없습니다. SQL Server 2012 에서는 보고서 서버를 한 모드에서 다른 모드로 전환할 수 없습니다. 환경에 사용되는 보고서 서버 유형을 변경하려면 원하는 보고서 서버 모드를 설치하고 보고서 항목을 새 보고서 서버로 복사하거나 이동해야 합니다. 이러한 프로세스를 일반적으로 '마이그레이션'이라고 합니다. 마이그레이션하는 데 필요한 단계는 마이그레이션할 모드 및 원본 버전에 따라 달라집니다. 자세한 내용은 [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)을 참조하세요.

- Internet Explorer 11 있어야 하거나 이상 스크립팅이 사용 하도록 설정 합니다. 자세한 내용은 [Reporting Services 및 파워 뷰에 대한 브라우저 지원](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)을 참조하세요.

## <a name="configure-the-web-portal-to-use-the-default-url"></a>기본 URL을 사용 하려면 웹 포털 구성

웹 포털은 사용자가 웹 브라우저에서 액세스 하는 웹 응용 프로그램. 적어도 브라우저 창에서 이 응용 프로그램을 여는 데 사용되는 URL은 정의해야 합니다. URL은 호스트 이름, 포트 및 가상 디렉터리로 구성됩니다. 이 URL에 대한 기본값에는 보고서 서버 웹 서비스 URL에 대해 정의된 호스트 이름 및 포트 값과 **reports** 가상 디렉터리 이름이 포함됩니다. 명명된 인스턴스가 있을 경우 가상 디렉터리는 **reports_instance**입니다. 여기서 **instance** 는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스의 이름입니다.

기본적으로는 웹 포털 URL은 고유한 가상 디렉터리 이름과 동일 인스턴스에서 실행 되는 보고서 서버 웹 서비스에 대해 정의 된 포트 및 호스트 이름입니다. 대부분의 경우 호스트 이름은 보고서 서버 컴퓨터의 네트워크 이름이지만 이 컴퓨터를 식별하는 IP 주소나 호스트 헤더가 될 수도 있습니다. 기본 URL을 사용 하려면 웹 포털을 구성 하려면 사용 된 **웹 포털 URL** 페이지에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구입니다.

> [!TIP]
> 원격 컴퓨터에서 웹 포털에 액세스 하려고 하면 브라우저에서 연결 오류 메시지를 수신 하는 경우 일반적인 원인으로 방화벽 설정이입니다. 자세한 내용은 [보고서 서버 액세스를 위한 방화벽 구성](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)을 참조하세요.

#### <a name="to-configure-the-default-the-web-portal-url-and-virtual-directory"></a>기본 웹 포털을 구성 하려면 URL 및 가상 디렉터리

1. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 시작한 다음 보고서 서버 인스턴스에 연결합니다.

2. 에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구 **웹 포털 URL** URL을 구성 하기 위한 페이지를 엽니다.

3. 웹 포털에 대 한 고유한 가상 디렉터리 이름을 입력 합니다.

4. **적용**을 클릭합니다.

5. 사용 중인 경우 [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] 또는 Windows Server 2008 추가 단계가 필요할 수도 웹 포털을 사용할 수 있습니다. 자세한 내용은 [로컬 관리에 대해 기본 모드 보고서 서버 구성&#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)를 참조하세요.

## <a name="configure-the-web-portal-to-use-a-specific-report-server-url"></a>특정 보고서 서버 URL을 사용 하려면 웹 포털 구성

기본적으로 웹 포털 동일한 보고서 서버 서비스에서 실행 되는 보고서 서버 웹 서비스에 연결 합니다. 웹 포털 연결을 만들 보고서 서버 웹 서비스 URL을 사용 합니다. 보고서 서버 웹 서비스에 대 한 여러 개의 Url을 정의 하는 경우 웹 포털 정의 된 마지막 하나를 사용 합니다. 그러나 일부 배포의 경우 항상 정적 URL 통해 웹 서비스에 연결 하려면 웹 포털을 할 수 있습니다. 특정 포트 또는 IP 주소에 대한 패킷 필터링을 구성한 후 보고서 서버에 대한 모든 연결이 사용자가 정의한 필터 규칙을 통과하도록 하려는 경우를 예로 들 수 있습니다.

Url을 구성할 때의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구, 웹 포털 자동으로 검색 하 고 동일한 서버 인스턴스에서 실행 되는 보고서 서버에 대 한 새로운 기능과 업데이트 된 Url을 사용 하 여 합니다. 배포에서 모든 보고서 서버 요청에 대해 단일 정적 URL을 사용해야 하는 경우 RSReportServer.config 파일에 해당 URL을 지정하면 됩니다.

#### <a name="to-configure-a-static-report-server-url"></a>정적 보고서 서버 URL을 구성하려면

1. 텍스트 편집기에서 **RSReportServer.config** 파일을 엽니다. 기본적으로 \program files\microsoft SQL Server\MSRS12 커서가 있습니다. \< *instancename*> services\reportserver입니다.  

2. **ReportServerURL**을 찾습니다.

3. 이 URL을 보고서 서버 인스턴스의 URL로 바꿉니다.

4. 변경 내용을 저장하고 파일을 닫습니다.

구성 파일에 대한 자세한 내용은 [Reporting Services 구성 파일 수정&#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) 및 [RsReportServer.config 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)을 참조하세요.

## <a name="customize-styles-or-application-title"></a>스타일 또는 응용 프로그램 제목 사용자 지정

웹 포털에 사용 되는 색상을 변경 하는 사용자 지정 브랜드 패키지를 만들 수 있습니다. 자세한 내용은 참조 [웹 포털 브랜딩](../branding-the-web-portal.md)

#### <a name="to-modify-application-title"></a>응용 프로그램 제목을 수정하려면

1. 보고서 서버에 대한 **시스템 관리자** 권한이 할당된 계정을 사용하여 로그온합니다.

2. Internet Explorer를 엽니다.

3. 웹 포털을 시작 URL입니다. 기본적으로는 http://\<**사용자 서버 이름**> 없는데도 명명 된 인스턴스의 경우 기본 URL로 Reporting Services를 설치 하는 경우 보고서에는 http:// 됩니다 /\<**사용자 서버 이름**> / r\<**_instancename**> 합니다.

4. **사이트 설정**을 선택합니다.

5. **일반** 탭의 **이름**에서 **SQL Server Reporting Services** 를 다른 이름으로 바꿉니다.

6. **적용**을 선택합니다.

## <a name="next-steps"></a>다음 단계

[웹 포털](../../reporting-services/web-portal-ssrs-native-mode.md)  
[Reporting Services 브라우저 지원](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)
[URL 구성](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
[Reporting Services 설치 확인](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)   
[Reporting Services 기능 설정 또는 해제](../../reporting-services/report-server/turn-reporting-services-features-on-or-off.md)   
[Reporting Services 기본 모드 보고서 서버 관리](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)   
[RsReportServer.config 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[로컬 관리를 위한 기본 모드 보고서 서버 구성](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)

 문의: [Reporting Services 포럼에서 질문](http://go.microsoft.com/fwlink/?LinkId=620231)

