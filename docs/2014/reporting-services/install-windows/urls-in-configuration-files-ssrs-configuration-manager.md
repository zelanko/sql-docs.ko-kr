---
title: 구성 파일의 URL(SSRS 구성 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- URL configuration [Reporting Services]
ms.assetid: 4f5e7fe0-b5b1-4665-93d4-80dce12d6b14
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c4df71d3110a878467c6dfd3a3281b4d597f2b7b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108586"
---
# <a name="urls-in-configuration-files--ssrs-configuration-manager"></a>구성 파일의 URL(SSRS 구성 관리자)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 RSReportServer.config 파일에 응용 프로그램 설정을 저장합니다. 이 파일에는 URL과 URL 예약, 두 가지에 대한 구성 설정이 포함됩니다. 이 두 구성 설정의 용도와 수정 규칙은 완전히 다릅니다. 구성 파일을 수정한 배포 튜닝에 익숙하다면 이 항목을 통해 각 URL 설정을 사용하는 방법을 보다 쉽게 이해할 수 있습니다.  
  
## <a name="url-settings-in-rsreportserverconfig-file"></a>RSReportServer.config 파일의 URL 설정  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 응용 프로그램 및 보고서에 액세스하고 웹 프런트 엔드 구성 요소를 백 엔드 보고서 서버에 연결하는 데 사용되는 URL을 저장합니다.  
  
#### <a name="urls-for-application-access"></a>애플리케이션 액세스용 URL  
 URL은 보고서 서버 웹 서비스 및 보고서 관리자에 액세스하는 데 사용됩니다. URL을 구성하려면 Reporting Services 구성 도구를 사용해야 합니다. 이 도구를 통해 HTTP.SYS에 각 응용 프로그램에 대한 URL 예약을 만들고 RSReportServer.config의 `URLReservations` 섹션에 URL에 대한 항목을 추가합니다.  
  
-   각 요소에 대 한 설명은 합니다 `URLReservations` 섹션을 참조 하십시오 [RSReportServer Configuration File](../report-server/rsreportserver-config-configuration-file.md) 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Onl 온라인 설명서.  
  
-   만의 구문에 대 한 자세한 내용은 `UrlString` 요소를 참조 하세요 [URL 예약 구문 &#40;SSRS 구성 관리자&#41;](url-reservation-syntax-ssrs-configuration-manager.md)합니다.  
  
-   애플리케이션 액세스를 위한 URL을 구성하는 방법은 [URL 구성&amp;#40;SSRS 구성 관리자&amp;#41;](configure-a-url-ssrs-configuration-manager.md)에 액세스하는 데 사용됩니다.  
  
#### <a name="urls-for-report-access"></a>보고서 액세스용 URL  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에는 보고서 링크나 첨부 파일을 보낼 때 사용할 수 있는 보고서 서버 전자 메일 배달 확장 프로그램이 포함되어 있습니다. 보고서 링크는 보고서가 배달될 때 생성됩니다. 보고서 서버 전자 메일 배달 확장 프로그램은 구성 파일의 `UrlRoot` 설정을 사용하여 링크를 만듭니다. `UrlRoot`는 무인 보고서 처리를 통해 생성된 렌더링된 보고서의 링크를 확인하는 데에도 사용됩니다.  
  
 `UrlRoot`는 응용 프로그램 액세스를 위한 URL을 구성하면 RSReportServer.config 파일에 자동으로 지정됩니다. 구성 파일에서 이 값을 수정하려면 배달하려는 보고서가 하위 보고서 서버 데이터베이스에 연결된 보고서 서버 웹 서비스에 대한 올바른 URL 주소를 지정해야 합니다. 보고서 서버 인스턴스당 하나의 `UrlRoot`만 지정할 수 있습니다. 따라서 지정된 보고서 서버 인스턴스의 RSReportServer.config 파일에는 하나의 `UrlRoot` 항목만 존재할 수 있습니다. 보고서 서버 웹 서비스에 여러 개의 URL이 예약된 경우 `UrlRoot`에 사용할 하나를 선택해야 합니다.  
  
 대부분의 경우 `UrlRoot`를 수정할 필요는 없습니다. 그러나 보고서 서버에 정규화 된 URL을 통해 액세스할 수는 정규화 된 사이트 이름으로 호스트 헤더를 사용 하는 URL을 구성 하지 않은 경우 RSReportServer.config를 수동으로 편집 해야 합니다는 `UrlRoot` 정규화 하려면 보고서를 렌더링 하는 데 사용할 된 보고서 서버 URL (예를 들어 https://www.adventure-works.com/mywebapp/reportserver)합니다.  
  
#### <a name="urls-connecting-report-manager-and-web-parts-to-the-report-server-web-service"></a>보고서 관리자 및 웹 파트를 보고서 서버 웹 서비스에 연결하는 URL  
 Reporting Services의 SharePoint 2.0 웹 파트와 보고서 관리자는 보고서 서버에 연결되는 웹 프런트 엔드 구성 요소입니다. 백 엔드 보고서 서버에 연결하는 데 사용되는 URL은 다음과 같습니다.  
  
-   `ReportServerUrl`(보고서 관리자에서 사용함)  
  
-   `ReportServerExternalUrl`(웹 파트에서 사용함)  
  
> [!NOTE]  
>  이전 버전의 Reporting Services에는 `ReportServerVirtualDirectory` 요소가 포함되었습니다. 이 값은 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서 더 이상 사용되지 않습니다. 기존 설치를 업그레이드하고 이 설정을 포함하는 구성 파일을 사용하면 보고서 서버는 더 이상 이 값을 읽지 않습니다.  
  
 다음 표에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 파일에 지정할 수 있는 모든 URL을 요약하여 보여 줍니다.  
  
|설정|사용법|Description|  
|-------------|-----------|-----------------|  
|`ReportServerUrl`|(선택 사항) 이 요소는 사용자가 직접 추가하지 않는 한 RSReportServer.config 파일에 포함되지 않습니다. 다음 시나리오 중 하나를 구성하는 경우에만 이 요소를 설정합니다.<br /><br /> 보고서 관리자가 다른 컴퓨터 또는 같은 컴퓨터의 다른 인스턴스에서 실행되는 보고서 서버 웹 서비스에 대한 웹 프런트 엔드 액세스를 제공하는 경우.<br /><br /> 보고서 서버에 대한 여러 URL이 있고, 보고서 관리자가 특정 URL을 사용하도록 하려는 경우.<br /><br /> 모든 보고서 관리자 연결에서 사용하도록 할 특정 보고서 서버 URL이 있는 경우.<br /><br /> 예를 들어 보고서 관리자가 로컬 연결을 통해 보고서 서버에 연결하도록 하면서 네트워크의 모든 컴퓨터에 대해 보고서 관리자 액세스를 활성화할 수 있습니다. 이 경우 구성할 수 있습니다 `ReportServerUrl` 에 "http://localhost/reportserver"입니다.<br /><br /> <br /><br /> 이러한 시나리오를 구현 하는 방법에 지침은 [보고서 관리자 구성 &#40;기본 모드&#41; ](../report-server/configure-web-portal.md) 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인입니다.|이 값은 보고서 서버 웹 서비스에 대한 URL을 지정합니다. 보고서 관리자 애플리케이션은 시작할 때 이 값을 읽습니다. 이 값을 설정하면 보고서 관리자는 URL에 지정된 보고서 서버에 연결됩니다.<br /><br /> 기본적으로 보고서 관리자는 보고서 관리자와 동일한 보고서 서버 인스턴스 내에서 실행되는 보고서 서버 웹 서비스에 대한 웹 프런트 엔드 액세스를 제공합니다. 다른 인스턴스에 속하거나 다른 컴퓨터의 인스턴스에서 실행되는 보고서 서버 웹 서비스에서 보고서 관리자를 사용하려면 이 URL을 설정하여 외부 보고서 서버 웹 서비스에 연결하도록 보고서 관리자에 지시하면 됩니다.<br /><br /> 연결하려는 보고서 서버에 SSL(Secure Sockets Layer) 인증서가 설치된 경우 `ReportServerUrl` 값은 해당 인증서에 등록된 서버의 이름이어야 합니다. 오류를 받게 되 면 "기본 연결이 닫혔습니다. 설정할 수 없습니다 SSL/TLS 보안 채널에 대 한 트러스트 관계 "를 설정 `ReportServerUrl` SSL 인증서가 발급 된 서버의 정규화 된 도메인 이름입니다. 예를 들어 인증서가 **https:\//adventure-works.com.onlinesales**에 등록된 경우 보고서 서버 URL은 **https:\//adventure-works.com.onlinesales/reportserver**가 됩니다.|  
|`ReportServerExternalUrl`|(선택 사항) 이 요소는 사용자가 직접 추가하지 않는 한 RSReportServer.config 파일에 포함되지 않습니다.<br /><br /> SharePoint 2.0 웹 파트를 사용 중이고, 사용자가 보고서를 검색하여 새 브라우저 창에서 열 수 있도록 하려는 경우에만 이 요소를 설정합니다.<br /><br /> <`ReportServerUrl`> 요소 아래에 <`ReportServerExternalUrl`>을 추가한 다음 별도의 브라우저 창에서 액세스할 때 보고서 서버 인스턴스로 확인되는 정규화된 보고서 서버 이름으로 설정합니다. <`ReportServerUrl`>을 삭제하지 마십시오.<br /><br /> 다음 예에서는 구문을 보여 줍니다.<br /><br /> `<ReportServerExternalUrl>http://myserver/reportserver</ReportServerExternalUrl>`|이 값은 SharePoint 2.0 웹 파트에서 사용됩니다.<br /><br /> 이전 릴리스에서는 인터넷 연결 보고서 서버에 보고서 작성기를 배포하기 위해 이 값을 설정하는 것이 권장되었습니다. 이는 테스트되지 않은 배포 시나리오입니다. 보고서 작성기에 대한 인터넷 액세스를 지원하기 위해 과거에 이 설정을 사용했다면 대체 전략을 고려해야 합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [보고서 서버 URL 구성&#40;SSRS 구성 관리자&#41;](configure-report-server-urls-ssrs-configuration-manager.md)   
 [URL 구성&#40;SSRS 구성 관리자&#41;](configure-a-url-ssrs-configuration-manager.md)  
  
  
