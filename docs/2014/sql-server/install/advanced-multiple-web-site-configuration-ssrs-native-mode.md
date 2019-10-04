---
title: 고급 다중 웹 사이트 구성 (SSRS 기본 모드) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.advancedmultiplewebsiteconfig.F1
ms.assetid: af4ede43-2225-45b5-ae7e-9202411551ba
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: b331015abd90fbff4c3810118666dbc9b356369b
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952676"
---
# <a name="advanced-multiple-web-site-configuration-ssrs-native-mode"></a>고급 다중 웹 사이트 구성(SSRS 암호 모드)
  이 대화 상자에서는 보고서 서버 또는 보고서 관리자에 액세스할 때 사용되는 URL을 만들고 관리할 수 있습니다. **고급 다중 웹 사이트 구성** 대화 상자는 호스트 헤더 이름을 포함하는 사용자 지정 URL, 추가 URL을 만들거나 IP 주소를 IPv4 또는 IPv6 형식으로 지정하는 데 사용됩니다.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드입니다.  
  
 여러 가지 방법으로 보고서 서버에 액세스하도록 구성하려는 경우 URL을 여러 개 만드는 것이 좋습니다. 예를 들어 일반적으로 인트라넷 및 익스트라넷 연결을 통해 보고서 서버에 액세스하려면 각 유형의 연결마다 다른 URL을 사용해야 합니다.  
  
 **고급 다중 웹 사이트 구성** 대화 상자를 열려면 **구성 관리자의** 웹 서비스 URL **또는** 보고서 관리자 URL **페이지에서** 고급 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 을 클릭합니다. **고급 다중 웹 사이트 구성** 대화 상자가 열리면 **추가** 또는 **편집** 을 클릭하여 새 URL을 정의하거나 기존 URL을 삭제할 수 있습니다.  
  
 **확인** 을 클릭하여 변경 내용을 저장합니다. URL을 추가하거나 제거한 후 **확인**을 클릭하지 않고 대화 상자를 닫으면 변경 내용이 손실됩니다.  
  
## <a name="options"></a>변수  
 **IP 주소**  
 TCP/IP 네트워크의 보고서 서버 컴퓨터를 식별합니다. 유효한 값은 다음과 같습니다.  
  
-   **모두 할당됨** - 컴퓨터에 할당된 모든 IP 주소를 보고서 서버 응용 프로그램을 가리키는 URL에 사용할 수 있도록 지정합니다. 또한 이 값은 도메인 이름 서버에서 확인할 수 있는 호스트 이름(예: 컴퓨터 이름)부터 컴퓨터에 할당된 IP 주소까지 포함합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL에 대한 기본값입니다.  
  
-   **모두 할당되지 않음** - IP 주소 또는 호스트 이름과 정확하게 일치하지 않는 모든 요청을 보고서 서버에서 받아들이도록 지정합니다. 다른 웹 애플리케이션에서 이미 이 값을 사용하고 있는 경우에는 사용하지 마십시오. 그럴 경우 다른 애플리케이션의 서비스가 중단됩니다.  
  
-   **127.0.0.1** - localhost 액세스에 사용되며 보고서 서버 컴퓨터에 대한 로컬 관리를 지원합니다. 이 값만 선택할 경우 보고서 서버 컴퓨터에 로컬로 로그온한 사용자만 애플리케이션에 액세스할 수 있습니다.  
  
-   *Nnn.nnn.nnn.nnn* - 컴퓨터에 설치된 네트워크 어댑터 카드의 IPv4 주소입니다. 네트워크에서 IPv6 주소 지정을 사용 하는 경우 IP 주소는 \<header >:*nnnn: nnnn: nnnn: nnnn*형식과 비슷한 8 4 바이트 필드의 128 비트 값입니다.  
  
     카드가 여러 개인 경우 카드 하나당 한 개의 IP 주소가 표시됩니다. IP 주소를 한 개만 선택할 경우 해당 IP 주소와 도메인 이름 서버가 이 IP 주소에 매핑한 호스트 이름만 애플리케이션에 액세스할 수 있습니다. localhost를 사용하여 보고서 서버에 액세스할 수 없으며, 보고서 서버 컴퓨터에 설치된 다른 네트워크 어댑터 카드의 IP 주소를 사용할 수 없습니다.  
  
 **포트**  
 보고서 서버에서 요청을 모니터링하는 포트를 지정합니다. 기본 포트는 포트 80입니다. 포트 80을 사용할 경우 URL에 포트 번호를 포함시킬 필요가 없습니다. 다른 포트 번호를 사용 하는 경우 URL에 항상 포함 해야 합니다 (예: http://localhost:8181/reports) ).  
  
 **호스트 헤더**  
 컴퓨터로 확인되는 도메인 이름 서버에 호스트 헤더가 이미 정의되어 있는 경우 보고서 서버 액세스용으로 구성되는 호스트 헤더를 URL에 지정할 수 있습니다.  
  
 호스트 헤더란 여러 웹 사이트에서 단일 IP 주소와 포트를 공유할 수 있도록 하는 고유한 이름으로, IP 주소와 포트 번호에 비해 기억하기 쉬울 뿐 아니라 입력하기도 쉽습니다. 호스트 헤더 이름의 예로는 www.adventure-works.com을 들 수 있습니다.  
  
 **SSL 포트**  
 SSL 연결용 포트를 지정합니다. SSL용 기본 포트는 443입니다.  
  
 **SSL 인증서**  
 이 컴퓨터에 설치된 SSL 인증서의 인증서 이름을 지정합니다. 인증서가 와일드카드에 매핑될 경우 이 인증서를 보고서 서버 연결에 사용할 수 있습니다.  
  
 인증서가 등록되어 있는 정규화된 컴퓨터 이름을 지정합니다. 지정하는 이름은 인증서가 등록된 이름과 같아야 합니다.  
  
 이 옵션을 사용하려면 인증서가 설치되어 있어야 합니다. RSReportServer.config 파일에서 UrlRoot 구성 설정도 수정하여 인증서가 등록되어 있는 컴퓨터의 정규화된 이름을 지정하도록 해야 합니다. 자세한 내용은 [온라인 설명서의](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md) 기본 모드 보고서 서버에서 SSL 연결 구성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 참조하세요.  
  
 **발급 대상**  
 인증서를 만든 컴퓨터의 이름을 표시합니다.  
  
 **추가**  
 추가 URL을 정의합니다.  
  
 **편집**  
 URL 구문의 특정 부분을 수정합니다.  
  
 **제거**  
 목록에서 URL 항목을 지웁니다.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [URL 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [보고서 서버 URL 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
