---
title: 주체 대체 이름을 사용하도록 Reporting Services 구성 | Microsoft Docs
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 493abba0e4396b6f12670dd3214d19e4767c4d0d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "65580013"
---
# <a name="configure-reporting-services-to-use-a-subject-alternative-name"></a>주체 대체 이름을 사용하도록 Reporting Services 구성

이 항목에서는 rsreportserver.config 파일을 수정하고 Netsh.exe 도구를 사용하여 Reporting Services(SSRS)를 구성하고 SAN(주체 대체 이름)을 사용하는 방법에 대해 설명합니다.

이 지침은 보고 서비스 URL과 웹 서비스 URL에 적용됩니다.

SAN을 사용하려면 서버에 SSL 인증서를 등록 및 서명하고 프라이빗 키를 가지고 있어야 합니다. 자체 서명된 인증서를 사용할 수 없습니다.  
  
 Reporting Services의 URL은 SSL 인증서를 사용하도록 구성할 수 있습니다. 인증서에는 일반적으로 SSL(Secure Sockets Layer) 세션에 대해 하나의 URL만 허용하는 주체 이름만 있습니다. SAN은 SSL 서비스에서 여러 URL을 수신하도록 허용하며 다른 애플리케이션과 SSL 포트를 공유하도록 허용하는 인증서의 추가 필드입니다. SAN은 `www.s2.com`과 같습니다.  
  
 Reporting Services의 SSL 설정에 대한 자세한 내용은 [기본 모드 보고서 서버에서 SSL 연결 구성](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)을 참조하세요.  
  
## <a name="configure-ssrs-to-use-a-subject-alternative-name-for-web-service-url"></a>웹 서비스 URL에 대해 주체 대체 이름을 사용하도록 SSRS 구성
  
1.  Reporting Services 구성 관리자를 시작합니다.  
  
     자세한 내용은 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)을 참조하세요.  
  
2.  **웹 서비스 URL** 페이지에서 SSL 포트 및 SSL 인증서를 선택합니다.  
  
     ![Reporting Services 구성 관리자](../../reporting-services/report-server-sharepoint/media/reportingservices-configurationmanager.png "Reporting Services 구성 관리자")  
  
     구성 관리자가 포트에 대해 SSL 인증서를 등록합니다.  
  
3.  rsreportserver.config 파일을 엽니다.  
  
     SSRS 기본 모드의 경우 파일은 기본적으로 다음 폴더에 있습니다.  
  
    ```  
    \Program Files\Microsoft SQL Server\MSRS11.MSSQLSERVER\Reporting Services\ReportServer  
    ```  
  
4.  보고서 서버 웹 서비스 애플리케이션의 URL 섹션을 복사합니다.  
  
     예를 들어 다음은 원래 URL 섹션입니다.  
  
    ```  
        <URL>  
         <UrlString>https://localhost:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
  
    ```  
  
     다음은 수정된 URL 섹션입니다.
  
    ```  
    <URL>  
         <UrlString>https://www.s1.com:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
        <URL>  
         <UrlString>https://www.s2.com:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
  
    ```  
  
5.  rsreportserver.config 파일을 저장합니다.  
  
6.  관리자로 명령 프롬프트를 시작하고 Netsh.exe 도구를 실행합니다.  
  
    ```  
    C:\windows\system32\netsh  
    ```  
  
7.  다음을 입력하여 http 컨텍스트로 전환합니다.  
  
    ```  
    Netsh>http  
    ```  
  
8.  다음을 입력하여 기존 urlacls를 표시합니다.
  
    ```  
    Netsh http>show urlacl  
    ```  
  
     다음과 같은 항목이 나타납니다.  
  
    ```  
    Reserved URL            : https:// www.s1.com:443/ReportServer/  
        User: NT SERVICE\ReportServer  
            Listen: Yes  
            Delegate: No  
            SDDL: D:(A;;GX;;;S-1-5-80-1234567890-123456789-123456789-123456789-1234567890)  
    ```  
  
     urlacl은 예약된 URL의 DACL(임의 액세스 제어 목록)입니다.  
  
9. 다음을 입력하여 기존 항목으로 같은 사용자와 SDDL을 사용하여 주체 대체 이름에 대해 새 항목을 만듭니다.  
  
    ```  
    netsh http>add urlacl  url=https://www.s2.com:443/ReportServer    
    user="NT Service\ReportServer" sddl=D:(A;;GX;;;S-1-5-80-1234567980-12346579-123456789-123456789-1234567890)  
  
    ```  
  
10. Reporting Services 구성 관리자의 **보고서 서버 상태** 페이지에서 **중지** 를 클릭한 다음 **시작** 을 클릭하여 보고서 서버를 다시 시작합니다.  
  
## <a name="see-also"></a>참고 항목

 [RsReportServer.config 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Reporting Services 구성 관리자](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Reporting Services 구성 파일 수정](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [보고서 서버 URL 구성](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
