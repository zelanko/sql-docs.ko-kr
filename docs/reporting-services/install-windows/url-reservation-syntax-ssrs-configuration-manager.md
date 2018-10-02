---
title: URL 예약 구문(SSRS 구성 관리자) | Microsoft Docs
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- URL reservations
ms.assetid: 30e4be2e-e65d-462c-895a-5a0a636d042f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 585a2a14d94382a6b4f7923e8563ddd4d8cae570
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47724701"
---
# <a name="url-reservation-syntax--ssrs-configuration-manager"></a>URL 예약 구문(SSRS 구성 관리자)
  이 항목에서는 보고서 서버 웹 서비스 및 보고서 관리자에서 사용하는 URL 문자열 부분에 대해 설명합니다. 내부적으로 저장되는 URL 문자열의 구조는 브라우저 창의 주소 표시줄에 입력하는 URL과는 다릅니다. URL 예약 문자열은 URL을 구성할 때 Reporting Services 구성 도구의 결과 창 및 RSReportServer.config 파일에 표시됩니다. URL 문자열이 정의되는 방식을 알면 URL 예약 문제를 해결하거나 HTTP.SYS를 쿼리하여 서버에 정의된 내부 URL 문자열 예약을 보는 경우 도움이 됩니다.  
  
## <a name="url-syntax"></a>URL 구문  
 보고서 서버 URL은 **UrlString** 요소와 **VirtualDirectory** 요소에 저장됩니다. **UrlString** 과 **VirtualDirectory** 가 별도의 요소로 구분되는 것은 각 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 응용 프로그램에서 URL 문자열은 여러 개일 수 있지만 가상 디렉터리 이름은 하나뿐이기 때문입니다.  
  
 HTTP.SYS에서 URL 예약은 **UrlString** 과 **VirtualDirectory**를 모두 포함합니다. URL 예약 구문은 다음 부분으로 구성됩니다.  
  
 \<scheme>://\<hostname>:\<port>/\<virtualdirectory>  
  
 다음 표에서는 각 속성과 각 속성에 대한 유효한 값을 보여 줍니다.  
  
|속성|유효한 값|설명|  
|--------------|------------------|-----------------|  
|Scheme|http 또는 https|SSL 및 SSL 이외의 연결에 대한 접두사|  
|Hostname|(+) 강력한 와일드카드, IP 주소의 **(모두 할당됨)** 값과 동일<br /><br /> (\*) 약한 와일드 카드, **(모두 할당되지 않음)** IP 주소와 동일<br /><br /> 정규화된 도메인 이름<br /><br /> 컴퓨터 이름<br /><br /> IP 주소(IPV4)<br /><br /> IP 주소(IPV6)|네트워크에서 서버를 식별합니다.<br /><br /> (+) 강력한 와일드카드가 기본값입니다. HTTP.SYS는 지정된 포트 및 가상 디렉터리 조합에 대해 모든 네트워크 어댑터에서 모든 요청을 수락합니다. 보고서 서버는 포트에 들어오는 모든 요청을 수락합니다.<br /><br /> (\*) 약한 와일드카드. HTTP.SYS는 주어진 포트 및 가상 디렉터리 조합에 대해 모든 네트워크 어댑터의 다른 URL 예약에서 처리되지 않은 모든 요청을 수락합니다.<br /><br /> 컴퓨터 이름은 네트워크에 있는 컴퓨터의 NETBIOS 이름입니다.<br /><br /> 정규화된 도메인 이름에는 도메인 컨트롤러 또는 공용 도메인 이름 서버에 등록된 도메인 주소 및 서버 이름이 포함됩니다.<br /><br /> IP 주소(IPV4)는 컴퓨터에 있는 네트워크 어댑터의 IPV4 형식 IP 주소로, *nnn.nnn.nnn.nnn*형식입니다.<br /><br /> IP 주소(IPV6)는 컴퓨터에 있는 네트워크 어댑터의 IPV6 형식 IP 주소로, \<header>:\<header>:*nnn.nnn.nnn.nnn* 형식입니다.|  
|포트|80<br /><br /> 443<br /><br /> \<custom>|포트 80은 서버에서 HTTP 요청이 들어오고 나가는 표준 포트입니다.<br /><br /> 포트 443은 SSL 연결에 대한 표준 포트입니다.<br /><br /> 다른 응용 프로그램에 예약되지 않은 모든 포트를 사용할 수도 있습니다.|  
|VirtualDirectory|ReportServer *[_InstanceName]*<br /><br /> Reports *[_InstanceName]*<br /><br /> \<custom>|응용 프로그램의 이름을 지정합니다. 이 값은 문자열입니다. 기본적으로 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 보고서 서버 웹 서비스 및 보고서 관리자 응용 프로그램에 대한 응용 프로그램 이름으로 ReportServer와 Reports를 사용합니다. 원하는 경우 다른 이름을 사용할 수도 있습니다.<br /><br /> 이 값은 필수 사항입니다. 응용 프로그램을 식별합니다.<br /><br /> 각 응용 프로그램 인스턴스에 대해 하나의 가상 디렉터리만 지정합니다. 같은 인스턴스에 있는 같은 응용 프로그램에 대해 여러 개의 URL을 만들려면 여러 개의 **UrlString**버전을 만듭니다. 여러 응용 프로그램 인스턴스에 대해 고유한 가상 디렉터리 이름을 만들려면 인스턴스 이름에 밑줄 문자(_)를 추가하여 가상 디렉터리 이름에 인스턴스 이름을 포함하면 됩니다. *InstanceName* 은 선택 사항이지만 같은 컴퓨터에 여러 개의 인스턴스가 있는 경우 권장됩니다. 명명된 인스턴스에 대한 URL 예약을 설정하는 방법은 [다중 인스턴스 보고서 서버 배포를 위한 URL 예약&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/url-reservations-for-multi-instance-report-server-deployments.md)을 참조하세요.<br /><br /> 가상 디렉터리에 대한 값은 대/소문자를 구분하지 않습니다. URL 구분 기호 문자 또는 URL 인코딩을 포함하지 않는다면 어떠한 문자열이라도 사용할 수 있습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [보고서 서버 URL 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [URL 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
  
  
