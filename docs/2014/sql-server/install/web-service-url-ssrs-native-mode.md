---
title: 웹 서비스 URL (SSRS 기본 모드) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.reportservervirtualdirectory.F1
helpviewer_keywords:
- Reporting Services, Web service
ms.assetid: 9d210b5d-2a08-4e56-a4f5-c16715b00d79
caps.latest.revision: 9
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 21a9ede5ef83169d312bb59e84bfd3f33619dafb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37270239"
---
# <a name="web-service-url-ssrs-native-mode"></a>웹 서비스 URL(SSRS 기본 모드)
  웹 서비스 URL 페이지에서는 보고서 서버에 액세스하는 데 사용되는 URL을 구성하거나 수정할 수 있습니다. *URL 예약* 은 지정된 URL을 기준으로 만들어집니다. URL 예약에는 다음에 보고서 서버 웹 서비스에 액세스할 때 사용할 수 있는 모든 URL에 대한 구문과 규칙이 정의되어 있으며, 보고서 서버 웹 서비스에 대한 접두사, 호스트, 포트 및 가상 디렉터리가 지정되어 있습니다. 호스트를 지정하는 방식에 따라 하나의 예약에 대해 여러 개의 URL을 사용할 수도 있습니다. 호스트 기본값에는 강력한 와일드카드가 지정되어 있습니다. 강력한 와일드카드를 사용하면 보고서 서버를 호스팅하는 컴퓨터로 확인될 수 있는 호스트 이름을 URL에 지정할 수 있습니다. URL 구성 및 예약에 대 한 자세한 내용은 참조 하세요. [URL 구성 &#40;SSRS 구성 관리자&#41; ](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) 하 고 [보고서 서버 Url 구성 &#40;&AMP;#40;SSRS 구성 관리자&#41; ](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md).  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드입니다.  
  
 이 페이지를 열려면 시작 합니다 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager 및 클릭 **웹 서비스 URL** 탐색 창에서. 자세한 내용은 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)을 참조하세요.  
  
 이 페이지는 보고서 서버 URL에 일반적으로 사용되는 값을 제공합니다. URL을 추가로 만들려면 호스트 헤더를 사용하거나 특정 형식으로 IP 주소를 지정하고 **고급**을 클릭하십시오.  
  
 **적용**을 클릭하면 웹 서비스 링크가 이 페이지에 표시됩니다. 보고서 서버 데이터베이스를 만들기 전에 이 링크를 클릭하면 "페이지를 찾을 수 없음" 오류 메시지가 표시될 수 있습니다. 이 오류는 데이터베이스 구성되면 더 이상 표시되지 않습니다. 자세한 내용은 [기본 모드 보고서 서버 데이터베이스 만들기&#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)를 참조하세요.  
  
 다시 설치 했는데 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 기본 IP 주소 값인 모두 할당 됨과 포트 80 사용 하려고 하면 오류가 발생을 일반적으로 서비스를 다시 시작한 후 URL을 다시 만들어 오류를 해결할 수 있습니다.  
  
## <a name="options"></a>변수  
 **가상 디렉터리**  
 보고서 서버 웹 서비스의 가상 디렉터리 이름을 지정합니다. 같은 컴퓨터에서는 각 보고서 서버 웹 서비스 인스턴스에 대한 가상 디렉터리 이름을 한 개만 지정할 수 있습니다.  
  
 **IP 주소**  
 TCP/IP 네트워크의 보고서 서버 컴퓨터를 식별합니다. 유효한 값은 다음과 같습니다.  
  
-   **모두 할당됨** - 컴퓨터에 할당된 모든 IP 주소를 보고서 서버 응용 프로그램을 가리키는 URL에 사용할 수 있도록 지정합니다. 또한 이 값은 도메인 이름 서버에서 확인할 수 있는 호스트 이름(예: 컴퓨터 이름)부터 컴퓨터에 할당된 IP 주소까지 포함합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL에 대한 기본값입니다.  
  
-   **모두 할당되지 않음** - IP 주소 또는 호스트 이름과 정확하게 일치하지 않는 모든 요청을 보고서 서버에서 받아들이도록 지정합니다. 다른 웹 응용 프로그램에서 이미 이 값을 사용하고 있는 경우에는 사용하지 마십시오. 그럴 경우 다른 응용 프로그램의 서비스가 중단됩니다.  
  
-   **127.0.0.1** - localhost 액세스에 사용되며 보고서 서버 컴퓨터에 대한 로컬 관리를 지원합니다. 이 값만 선택할 경우 보고서 서버 컴퓨터에 로컬로 로그온한 사용자만 응용 프로그램에 액세스할 수 있습니다.  
  
-   *Nnn.nnn.nnn.nnn* - 컴퓨터에 설치된 네트워크 어댑터 카드의 IPv4 주소입니다. 네트워크에서 IPv6 주소에 IP 주소에 8 개의 4 바이트 필드로 다음 형식으로 128 비트 값 됩니다: \<머리글 >:*nnnn:nnnn:nnnn:nnnn*  
  
     카드가 여러 개인 경우 카드 하나당 한 개의 IP 주소가 표시됩니다. IP 주소를 한 개만 선택할 경우 해당 IP 주소와 도메인 이름 서버가 이 IP 주소에 매핑한 호스트 이름만 응용 프로그램에 액세스할 수 있습니다. localhost를 사용하여 보고서 서버에 액세스할 수 없으며, 보고서 서버 컴퓨터에 설치된 다른 네트워크 어댑터 카드의 IP 주소를 사용할 수 없습니다.  
  
 **TCP 동적 포트**  
 보고서 서버 가상 디렉터리 이름이 포함된 URL의 HTTP 요청에 대해 보고서 서버가 모니터링하는 포트를 지정합니다.  
  
 **SSL 인증서**  
 지정한 IP 주소에 인증서를 바인딩합니다. 인증서는 컴퓨터에 설치되어 구성되어 있어야 합니다. Reporting Services는 인증서 관리 기능을 제공하지 않으므로 인증서는 IP 주소로 확인되는 호스트 이름 또는 컴퓨터 이름으로 발급되어야 합니다. 예를 들어 발급 된 인증서를 사용 하도록 http://salesreports, 지정한 IP 주소가 "salesreports" 라는 서버로 확인 되어야 합니다.  
  
 인증서를 사용 하는 경우 수정 해야 합니다 `UrlRoot` RSReportServer.config 구성 설정 파일에 인증서가 등록 되어 있는 컴퓨터의 정규화 된 이름을 지정 합니다. 자세한 내용은 [온라인 설명서의](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md) 기본 모드 보고서 서버에서 SSL 연결 구성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 참조하세요.  
  
 **SSL 포트**  
 SSL 연결용 포트를 지정합니다.  
  
 **Url**  
 현재 보고서 서버 인스턴스에 대해 정의된 URL을 표시합니다.  
  
 **고급**  
 현재 응용 프로그램 인스턴스에 대한 URL을 추가로 만들려면 클릭합니다.  
  
> [!NOTE]  
>  기존 SSL 바인딩 및 URL 예약이 있는 상태에서 SSL 바인딩을 변경하려면(예: 다른 인증서 또는 호스트 헤더를 사용하는 경우) 다음 단계를 순서대로 수행하는 것이 좋습니다.  
>   
>  1.  먼저 모든 URL 예약을 제거합니다.  
> 2.  모든 SSL 바인딩을 제거합니다.  
> 3.  그런 다음 URL 및 SSL 바인딩을 다시 만듭니다.  
>   
>  이전 단계는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 완료할 수 있습니다.  
>   
>  Microsoft Windows는 포트 조합에 대한 각 IP 주소에 대해 하나의 바인딩을 지원합니다. 특정 호스트 헤더 값을 사용하도록 보고서 서버를 구성하고 IP 주소 조합에 대한 포트의 인증서가 다른 호스트 헤더 값으로 발급되는 경우 인증서가 사용 중인 URL과 일치하지 않음을 나타내는 경고가 브라우저에 표시됩니다.  
>   
>  이 문제를 해결하려면 모든 바인딩을 삭제하고 고유한 설정을 사용하여 새 바인딩을 만들거나 와일드카드를 사용하여 Reporting Services URL 등록을 구성합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 구성 관리자 F1 도움말 항목 &#40;SSRS 기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [보고서 서버 URL 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
