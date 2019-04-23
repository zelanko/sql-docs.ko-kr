---
title: URL 예약 및 등록 정보(SSRS 구성 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- URL reservations
- URL registration
- Report Server service, URL reservations
ms.assetid: c2c460c3-e749-4efd-aa02-0f8a98ddbc76
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f81ac60dbd6ea315bab70d2f65e4953b456f3034
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59968289"
---
# <a name="about-url-reservations-and-registration--ssrs-configuration-manager"></a>URL 예약 및 등록 정보(SSRS 구성 관리자)
  Reporting Services 애플리케이션의 URL은 HTTP.SYS에서 URL 예약으로 정의됩니다. URL 예약은 웹 애플리케이션에 대한 URL 엔드포인트 구문을 정의합니다. 보고서 서버에서 애플리케이션을 구성하는 경우 보고서 서버 웹 서비스와 보고서 관리자 모두에 대해 URL 예약이 정의됩니다. 설치 프로그램 또는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 통해 URL을 구성하면 URL 예약이 자동으로 생성됩니다.  
  
-   설치 프로그램은 기본값을 사용하여 URL 예약을 만듭니다. 설치 프로그램이 기본 구성을 설치할 경우 두 개의 URL이 예약되는데 하나는 보고서 서버 웹 서비스에 대한 URL이고 다른 하나는 보고서 관리자에 대한 URL입니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 사용하여 URL을 더 추가하거나 설치 프로그램에서 만든 기본 URL을 수정할 수 있습니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구는 **웹 서비스 URL** 또는 **보고서 관리자 URL** 페이지에 지정된 URL을 기준으로 URL 예약을 만듭니다.  
  
 설치 프로그램과 구성 도구는 또한 보고서 서버 URL에 대한 권한을 할당하고 중복된 인스턴스가 있는지 확인하며 URL 예약을 HTTP.SYS에 추가합니다. HttpCfg.exe 또는 다른 도구를 사용하여 Reporting Services URL 예약을 직접 만들거나 수정하지 마세요. 단계를 건너뛰거나 잘못된 값을 설정할 경우 진단하거나 수정하기 어려운 문제가 발생합니다.  
  
> [!NOTE]  
>  HTTP.SYS는 네트워크 요청을 수신한 다음 이를 요청 큐로 라우팅하는 운영 체제 구성 요소입니다. 이 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]릴리스에서 HTTP.SYS는 보고서 서버 웹 서비스와 보고서 관리자에 대한 요청 큐를 설정하고 유지 관리합니다. 인터넷 정보 서비스(IIS)는 더 이상 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 애플리케이션을 호스팅하거나 액세스하는 데 사용되지 않습니다. HTTP.SYS 기능에 대한 자세한 내용은 MSDN의 [HTTP Server API](https://go.microsoft.com/fwlink/?LinkId=92652) 를 참조하세요.  
  
##  <a name="ReportingServicesURLs"></a> Reporting Services에서의 URL  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치에서는 URL을 통해 다음 도구, 응용 프로그램 및 항목에 액세스할 수 있습니다.  
  
-   보고서 서버 웹 서비스  
  
-   보고서 관리자  
  
-   보고서 작성기  
  
-   보고서 서버에 게시된 보고서  
  
 모델 및 공유 데이터 원본과 같은 다른 게시된 URL 주소 지정 가능 항목은 URL을 통해 독립 실행형 항목으로 액세스할 수 없습니다. 브라우저 창에서 볼 때 보고서 서버는 이러한 항목을 의미 있는 형식으로 표시하지 않습니다.  
  
> [!NOTE]  
>  이 항목에서는 보고서 작성기 또는 보고서 서버에 저장된 특정 보고서에 대한 URL 액세스에 대해서는 설명하지 않습니다. 이러한 항목의 URL 액세스에 대한 자세한 내용은 [온라인 설명서의](../access-report-server-items-using-url-access.md) URL 액세스를 사용하여 보고서 서버 항목 액세스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 참조하세요.  
  
##  <a name="URLreservation"></a> URL 예약 및 등록  
 URL 예약은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 애플리케이션에 액세스할 때 사용할 수 있는 URL을 정의합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]는 HTTP.SYS에 보고서 서버 웹 서비스와 보고서 관리자에 대한 URL을 한 개 이상 예약한 다음 서비스가 시작될 때 이를 등록합니다. 보고서 작성기와 보고서에 대한 URL은 보고서 서버 웹 서비스 URL 예약을 기준으로 합니다. URL에 매개 변수를 추가하면 웹 서비스를 통해 보고서 작성기나 보고서를 열 수 있습니다. 예약 및 등록은 HTTP.SYS에서 제공합니다. 자세한 내용은 MSDN의 [네임스페이스 예약, 등록 및 라우팅(Namespace Reservations, Registration, and Routing)](https://go.microsoft.com/fwlink/?LinkId=92653) 을 참조하세요.  
  
 *URL 예약* 은 웹 응용 프로그램에 대한 URL 엔드포인트가 HTTP.SYS에 생성되고 저장되는 프로세스입니다. HTTP.SYS는 컴퓨터에 정의된 모든 URL 예약의 공용 리포지토리로서 고유한 URL 예약을 보장하는 일반 규칙 집합을 정의합니다.  
  
 *URL 등록* 은 서비스가 시작될 때 발생합니다. 그러면 요청 큐가 생성되고 HTTP.SYS에서는 요청을 요청 큐로 라우팅합니다. URL 엔드포인트는 URL 엔드포인트로 전달되는 요청이 큐에 추가되기 전에 등록되어야 합니다. 보고서 서버 서비스가 시작되면 설정된 모든 애플리케이션용으로 예약된 URL이 모두 등록됩니다. 즉 등록이 발생하려면 웹 서비스가 설정되어 있어야 합니다. 정책 기반 관리의 Reporting Services 패싯에 대한 노출 영역 구성에서 **WebServiceAndHTTPAccessEnabled** 속성을 **False**로 설정한 경우에는 서비스가 시작될 때 웹 서비스의 URL이 등록되지 않습니다.  
  
 서비스를 중단하거나 웹 서비스 또는 보고서 관리자 애플리케이션 도메인을 재활용하는 경우 URL 등록이 취소됩니다. 서비스가 실행 중일 때 URL 예약을 수정한 경우 이전 URL 등록이 취소되고 새 URL이 사용될 수 있도록 보고서 서버가 애플리케이션 도메인을 즉시 재활용합니다.  
  
 몇 가지 간단한 예를 통해 URL 예약의 개념과 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 애플리케이션에 사용되는 URL 주소와 URL 예약의 관계를 알 수 있습니다. 유념해야 할 사항은 애플리케이션 액세스에 사용되는 URL과 URL 예약의 구문은 서로 다르다는 점입니다.  
  
|HTTP.SYS에서의 URL 예약|URL|설명|  
|---------------------------------|---------|-----------------|  
|http://+:80/reportserver|http://\<computername>/reportserver<br /><br /> http://\<IPAddress>/reportserver<br /><br /> http://localhost/reportserver|이 URL 예약은 포트 80에 와일드카드(+)를 지정하며, 포트 80에서 보고서 서버 컴퓨터로 확인되는 호스트를 지정하는 들어오는 모든 요청을 보고서 서버 큐에 추가합니다. 이 URL 예약을 사용하면 원하는 수의 URL을 사용하여 보고서 서버에 액세스할 수 있습니다.<br /><br /> 이 URL은 대부분의 운영 체제에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버에 대한 기본 URL 예약입니다.|  
|http://123.45.67.0:80/reportserver|http://123.45.67.0/reportserver|이 URL 예약은 IP 주소를 지정하며 와일드카드 URL 예약보다 훨씬 제한적입니다. IP 주소를 포함하는 URL만 보고서 서버에 연결하는 데 사용할 수 있습니다. 이 URL 예약을 http:// 보고서 서버에 요청\<컴퓨터 이름 > / reportserver 또는 http://localhost/reportserver 하지 못합니다.|  
  
##  <a name="DefaultURLs"></a> 기본 URL  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 기본 구성으로 설치할 경우 설치 프로그램이 보고서 서버 웹 서비스와 보고서 관리자에 대한 URL을 예약합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구에서 URL 예약을 정의하는 경우 이러한 기본값을 그대로 사용할 수도 있습니다. [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]를 설치하거나[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 명명된 인스턴스로 설치할 경우 기본 URL에 인스턴스 이름이 포함됩니다.  
  
> [!IMPORTANT]  
>  밑줄 문자(`_`)가 인스턴스 문자로 사용됩니다.  
  
 URL 예약에는 포트 번호가 포함됩니다. , 및 운영 체제에서는  
  
1.  [!INCLUDE[win8srv](../../includes/win8srv-md.md)]  
  
2.  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]  
  
3.  [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]  
  
4.  [!INCLUDE[win7](../../includes/win7-md.md)]  
  
5.  [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)]  
  
|인스턴스 유형|애플리케이션|기본 URL|HTTP.SYS의 실제 URL 예약|  
|-------------------|-----------------|-----------------|----------------------------------------|  
|기본 인스턴스|보고서 서버 웹 서비스|http://\<servername>/reportserver|http://\<servername>:80/reportserver|  
|기본 인스턴스|보고서 관리자|http://\<servername>/reportserver|http://\<servername>:80/reportserver|  
|명명된 인스턴스|보고서 서버 웹 서비스|http://\<servername>/reportserver_\<instancename>|http://\<servername>:80/reportserver_\<instancename>|  
|명명된 인스턴스|보고서 관리자|http://\<servername>/reports_\<instancename>|http://\<servername>:80/reports_\<instancename>|  
|SQL Server Express|보고서 서버 웹 서비스|http://\<servername>/reportserver_SQLExpress|http://\<servername>:80/reportserver_SQLExpress|  
|SQL Server Express|보고서 관리자|http://\<servername>/reports_SQLExpress|http://\<servername>:80/reports_SQLExpress|  
  
##  <a name="URLPermissionsAccounts"></a> Reporting Services URL에 대한 인증 및 서비스 ID  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL 예약은 보고서 서버 서비스의 서비스 계정을 지정합니다. 서비스가 실행되는 계정은 같은 인스턴스에 실행되는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 애플리케이션용으로 생성된 모든 URL에 사용됩니다. 보고서 서버 인스턴스의 서비스 ID는 RSReportServer.config 파일에 저장됩니다.  
  
 서비스 계정에는 기본값이 없습니다. 그러나 설치 중 서비스 계정을 지정해야 하며 서버를 파일만 모드에서 설치한 경우라도 서비스 계정은 RSReportServer.config의 `URLReservation`에 지정되어 있습니다. 서비스 계정으로 유효한 값은 도메인 사용자 계정, `LocalSystem` 또는 `NetworkService`입니다.  
  
 기본 보안이 `RSWindowsNegotiate`이므로 익명 액세스는 허용되지 않습니다. 인트라넷 액세스의 경우 보고서 서버 URL에 네트워크 컴퓨터 이름이 사용됩니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 인터넷 연결용으로 구성하려는 경우 다른 설정을 사용해야 합니다. 인증에 대한 자세한 내용은 [온라인 설명서의](../security/authentication-with-the-report-server.md) 보고서 서버 인증 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 참조하세요.  
  
##  <a name="URLlocalAdmin"></a> 로컬 관리 URL  
 URL 예약에 대해 강력한 또는 약한 와일드카드를 지정한 경우 http://localhost/reportserver 또는 http://localhost/reports를 사용할 수 있습니다.  
  
 http://localhost URL은 http://127.0.0.1로 해석됩니다. URL 예약을 컴퓨터 이름이나 단일 IP 주소로 해석한 경우 로컬 컴퓨터에 127.0.0.1에 대한 예약을 추가로 만들어야 localhost를 사용할 수 있습니다. 마찬가지로 컴퓨터에서 localhost 또는 127.0.0.1을 사용할 수 없는 경우 해당 URL을 사용할 수 없습니다.  
  
 [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] 및 [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]에는 실수로 프로그램을 높은 권한으로 실행하는 위험을 최소화하는 새로운 보안 기능이 포함되어 있습니다. 이 운영 체제에서 로컬 관리를 사용하려면 추가 단계가 필요합니다. 자세한 내용은 [로컬 관리에 대해 기본 모드 보고서 서버 구성&#40;SSRS&#41;](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)을 참조하세요.  
  
##  <a name="URLSharePoint"></a> SharePoint 통합 모드로 보고서 서버에 대 한 Url  
 보다 큰 규모의 SharePoint 제품 또는 기술 배포 내에서 실행되도록 독립 실행형 보고서 서버를 구성하는 경우 URL 및 가상 디렉터리 생성은 다음과 같이 영향을 받습니다.  
  
-   보고서 및 기타 항목에 대한 URL 주소는 SharePoint 웹 애플리케이션 URL을 통해 지정됩니다. 특정 보고서에 대한 URL 액세스의 경우 사이트 경로, 문서 라이브러리, 항목 이름 및 파일 이름 확장명(예: 보고서의 경우 .rdl)을 포함하는 정규화된 URL을 항상 사용하십시오. 보고서의 공유 데이터 원본 및 모델을 참조하는 경우와 보고서 서버로의 게시 작업에 대한 대상 서버 및 폴더를 지정하는 경우 정규화된 URL을 지정해야 합니다.  
  
-   파일 이름 확장명은 보고서 서버 항목의 서로 다른 유형을 구분하는 데 사용됩니다. 유효한 확장명은 보고서 정의의 경우 .rdl, 보고서 모델의 경우 .smdl, SharePoint 사이트에 대해 생성되는 공유 데이터 원본의 경우 .rsds입니다.  
  
-   SharePoint 제품 및 기술에 대한 URL 예약이 정의되어 있더라도 서버에 게시할 때 예약을 무시할 수 있습니다. SharePoint 웹 애플리케이션의 경우 URL 예약은 내부 작업입니다.  
  
-   단일 서버 배포의 통합된 보고서 서버 및 SharePoint 기술 인스턴스를 동일한 컴퓨터에 설치 되어 있는 경우 사용할 수 없습니다 http://localhost/reportserver합니다. 경우 http://localhost 는 SharePoint 웹 응용 프로그램에 액세스 하는 데에 사용 해야 기본이 아닌 웹 사이트 또는 고유한 포트 할당을 보고서 서버에 액세스할 수 있습니다. 또한 보고서 서버가 SharePoint 팜과 통합되는 경우 원격 컴퓨터에 설치된 배포의 노드에 대해서는 보고서 서버에 대한 localhost 액세스가 확인되지 않습니다.  
  
-   SharePoint 통합 모드에서 실행되는 보고서 서버에 대해서는 보고서 관리자에 대한 URL 예약 및 엔드포인트를 구성할 수 없습니다. 이를 구성하는 경우에는 보고서 서버를 SharePoint 통합 모드로 배포한 후 이 URL 및 가상 디렉터리가 더 이상 작동하지 않습니다. 이 모드에서는 보고서 관리자가 지원되지 않습니다.  
  
 보고서 서버 스케일 아웃 배포를 통합하여 보다 큰 규모의 SharePoint 제품 또는 기술 배포 내에서 실행하는 경우 보고서 서버 노드에 대한 부하를 분산시키고 스케일 아웃 배포에 대한 단일 가상 서버 URL을 정의하세요. 보고서 서버 통합 설정을 통해서만 단일 보고서 URL을 지정할 수 있습니다. 스케일 아웃 배포의 경우 URL은 스케일 아웃 배포의 서버 노드에 대한 액세스 지점이어야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [URL 구성&#40;SSRS 구성 관리자&#41;](configure-a-url-ssrs-configuration-manager.md)   
 [URL 예약 구문&#40;SSRS 구성 관리자&#41;](url-reservation-syntax-ssrs-configuration-manager.md)  
  
  
