---
title: "Reporting을 설치 하 고 인터넷 정보 서비스 함께 | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deploying [Reporting Services], IIS
ms.assetid: 9b651fa5-f582-4f18-a77d-0dde95d9d211
caps.latest.revision: 40
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 1818a4b076dd6e1c81c0a9b39b781516bdf718e0
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---

# <a name="install-reporting-and-internet-information-services-side-by-side"></a>Reporting을 설치 하 고 인터넷 정보 서비스 함께

[!INCLUDE[ssrs-appliesto-sql2016-preview](../../includes/ssrs-appliesto-sql2016-preview.md)]

  설치 하 고 동일한 컴퓨터에서 SQL Server Reporting Services (SSRS) 및 인터넷 정보 서비스 (IIS)를 실행할 수 있습니다. 사용하는 IIS 버전에 따라 해결해야 하는 상호 운용성 문제가 결정됩니다.  
  
|IIS 버전|문제|설명|  
|-----------------|------------|-----------------|  
|8.0, 8.5|한 응용 프로그램을 대상으로 하는 요청이 다른 응용 프로그램에 받아들여집니다.<br /><br /> HTTP.SYS는 URL 예약에 대한 선행 규칙을 적용합니다. URL 예약이 다른 응용 프로그램의 URL 예약에 비해 약한 경우에는 가상 디렉터리 이름이 동일하며 포트 80을 함께 모니터링하는 응용 프로그램으로 전송된 요청이 의도한 대상에 도달하지 않을 수 있습니다.|상황에 따라 URL 예약 스키마의 다른 URL 끝점을 대체하는 등록된 끝점이 다른 응용 프로그램을 대상으로 하는 HTTP 요청을 받을 수 있습니다.<br /><br /> 보고서 서버 웹 서비스 및 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] 에 고유한 가상 디렉터리 이름을 사용하면 이러한 충돌을 방지할 수 있습니다.<br /><br /> 이 시나리오에 대한 자세한 내용은 이 항목에 제공되어 있습니다.|  
  
## <a name="precedence-rules-for-url-reservations"></a>URL 예약에 대한 선행 규칙  
 IIS와 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]간 상호 운용성 문제를 해결하려면 먼저 URL 예약 선행 규칙을 이해해야 합니다. 선행 규칙은 다음과 같이 일반화할 수 있습니다. 더 명시적으로 정의된 값이 있는 URL 예약이 해당 URL과 일치하는 요청을 가장 먼저 받습니다.  
  
-   가상 디렉터리를 지정하는 URL 예약은 가상 디렉터리를 생략하는 URL 예약보다 명시적입니다.  
  
-   IP 주소, 정규화된 도메인 이름, 네트워크 컴퓨터 이름 또는 호스트 이름을 통해 단일 주소를 지정하는 URL 예약은 와일드카드보다 명시적입니다.  
  
-   강력한 와일드카드를 지정하는 URL 예약은 약한 와일드카드보다 명시적입니다.  
  
 다음 예에서는 가장 명시적인 것부터 차례로 URL 예약의 범위를 보여 줍니다.  
  
|예제|요청|  
|-------------|-------------|  
|`http://123.234.345.456:80/reports`|로 전송 된 모든 요청을 받고 `http://123.234.345.456/reports` 또는 `http://\<computername>/reports` 도메인 이름 서비스가 해당 호스트 이름으로 IP 주소를 확인할 수 있는 경우.|  
|`http://+:80/reports`|URL에 "reports" 가상 디렉터리 이름이 포함되어 있는 한 해당 컴퓨터에 대해 유효한 IP 주소 또는 호스트 이름으로 전송된 모든 요청을 받습니다.|  
|`http://123.234.345.456:80`|지정 하는 모든 요청을 받습니다 `http://123.234.345.456` 또는 `http://\<computername>` 도메인 이름 서비스가 해당 호스트 이름으로 IP 주소를 확인할 수 있는 경우.|  
|`http://+:80`|**모두 할당됨**에 매핑된 응용 프로그램 끝점에 대해 다른 응용 프로그램이 아직 받지 않은 요청을 받습니다.|  
|`http://*:80`|**모두 할당되지 않음**에 매핑된 응용 프로그램 끝점에 대해 다른 응용 프로그램이 아직 받지 않은 요청을 받습니다.|  
  
 'System.IO.FileLoadException: 파일이 다른 프로세스에서 사용되고 있으므로 프로세스에서 파일에 액세스할 수 없습니다 (예외가 발생한 HRESULT: 0x80070020)'.라는 오류 메시지가 표시되면 포트 충돌이 발생한 것입니다.  
  
## <a name="url-reservations-for-iis-80-85-with-sql-server-reporting-services"></a>IIS 8.0, 8.5에 SQL Server Reporting Services에 대 한 URL 예약  
 이전 섹션에 요약된 우선 순위 규칙을 기반으로 Reporting Services 및 IIS에 대해 정의된 URL 예약이 상호 운용성을 향상시키는 방식을 이해할 수 있습니다. Reporting Services는 해당 응용 프로그램의 가상 디렉터리 이름을 명시적으로 지정하는 요청을 받습니다. IIS는 나머지 요청을 모두 받은 다음 이를 IIS 프로세스 모델 내에서 실행되는 응용 프로그램으로 전송할 수 있습니다.  
  
|응용 프로그램|URL 예약|설명|요청 수신|  
|-----------------|---------------------|-----------------|---------------------|  
|보고서 서버|`http://+:80/ReportServer`|포트 80에서 ReportServer 가상 디렉터리가 있는 강력한 와일드카드입니다.|포트 80에서 ReportServer 가상 디렉터리를 지정하는 모든 요청을 받습니다. 보고서 서버 웹 서비스 http:// 모든 요청을 받으며\<컴퓨터 이름 > / reportserver입니다.|  
|웹 포털|`http://+:80/Reports`|포트 80에서 Reports 가상 디렉터리가 있는 강력한 와일드카드입니다.|포트 80에서 Reports 가상 디렉터리를 지정하는 모든 요청을 받습니다. [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] http:// 모든 요청을 받으며\<컴퓨터 이름 > / r 합니다.|  
|IIS|`http://*:80/`|포트 80의 약한 와일드카드입니다.|포트 80에서 다른 응용 프로그램이 받지 않은 모든 나머지 요청을 받습니다.|  

## <a name="side-by-side-deployments-of-sql-server-reporting-services-on-iis-80-85"></a>IIS 8.0, 8.5에서 SQL Server Reporting Services의-병렬 배포

 IIS와 Reporting Services 간 상호 운용성 문제는 IIS 웹 사이트의 가상 디렉터리 이름이 Reporting Services에 사용되는 가상 디렉터리 이름과 같을 경우 발생합니다. 예를 들어 다음과 같은 구성이 있다고 가정합니다.  
  
-   포트 80에 할당된 IIS의 웹 사이트 및 "Reports"라는 가상 디렉터리  
  
-   여기서 URL 예약은 포트 80을 지정 하는 기본 구성으로 설치 된 보고서 서버 인스턴스 및 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] 응용 프로그램으로도 "Reports" 가상 디렉터리 이름에 대 한 사용 합니다.  
  
 이 구성 http://에 전송 된 요청\<컴퓨터 이름 >: 80/reports에서 수신할는 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]합니다. 더 이상 응용 프로그램 IIS의 Reports 가상 디렉터리를 통해 액세스 되는 보고서 서버 인스턴스가 설치 된 후 요청을 받지 않습니다.  
  
 이전 버전 및 최신 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]배포를 함께 실행하는 경우 방금 설명한 라우팅 문제가 발생할 가능성이 높습니다. 이는 모든 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 가 "ReportServer" 및 "Reports"를 보고서 서버 및 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] 응용 프로그램의 가상 디렉터리 이름으로 사용하여 IIS에 "reports" 및 "reportserver" 가상 디렉터리가 있을 가능성이 높아지기 때문입니다.  
  
 모든 응용 프로그램이 요청을 받도록 하려면 다음 지침을 따릅니다.  
  
-   Reporting Services 설치의 경우 Reporting Services와 동일한 포트에서 IIS 웹 사이트에 아직 사용되지 않은 가상 디렉터리 이름을 사용합니다. 충돌이 발생하면 설치 완료 후 가상 디렉터리를 구성할 수 있도록 Reporting Services를 "파일만" 모드로 설치합니다(설치를 사용하지만 설치 마법사에서 서버 옵션 구성 안 함). System.IO.FileLoadException: 파일이 다른 프로세스에서 사용되고 있으므로 프로세스에서 파일에 액세스할 수 없습니다. (예외가 발생한 HRESULT: 0x80070020).라는 오류 메시지가 표시되면 구성 충돌이 발생한 것입니다.  
  
-   수동으로 구성하는 설치의 경우 구성하는 URL에 기본 명명 규칙을 적용합니다. [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 를 명명된 인스턴스로 설치하는 경우 가상 디렉터리를 만들 때 인스턴스 이름을 포함합니다.  

## <a name="next-steps"></a>다음 단계

[보고서 서버 Url 구성](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
[URL 구성](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
[Reporting Services 기본 모드 보고서 서버 설치](../../reporting-services/install-windows/install-reporting-services-native-mode-report-server.md)  

문의: [Reporting Services 포럼에서 질문](http://go.microsoft.com/fwlink/?LinkId=620231)
