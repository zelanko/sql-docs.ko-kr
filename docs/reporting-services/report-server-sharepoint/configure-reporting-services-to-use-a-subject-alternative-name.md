---
title: SAN(주체 대체 이름)을 사용하도록 Reporting Services 구성 | Microsoft Docs
description: rsreportserver.config 파일을 수정하고 Netsh.exe 도구를 사용하여 SAN을 사용하도록 SQL Server Reporting Services 및 Power BI Report Server를 구성하는 방법을 알아봅니다.
ms.date: 09/27/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cf1db4f6e07609ce6da38569732f7dba333f86ff
ms.sourcegitcommit: b93beb4f03aee2c1971909cb1d15f79cd479a35c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91497207"
---
# <a name="configure-reporting-services-to-use-a-subject-alternative-name-san"></a>SAN(주체 대체 이름)을 사용하도록 Reporting Services 구성

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

이 문서에서는 rsreportserver.config 파일을 수정하고 Netsh.exe 도구를 사용하여 SAN(주체 대체 이름)을 사용하도록 Reporting Services(SSRS) 및 Power BI Report Server를 구성하는 방법을 설명합니다.

지침은 웹 서비스 URL 및 보고서 서버 구성 관리자 도구의 웹 포털 URL에 적용됩니다.

SAN을 사용하려면 서버에 TLS/SSL 인증서를 등록 및 서명하고 프라이빗 키를 가지고 있어야 합니다. 자체 서명된 인증서를 사용할 수 없습니다.

Reporting Services 및 Power BI Report Server의 URL은 TLS/SSL 인증서를 사용하도록 구성할 수 있습니다. 인증서에는 일반적으로 이전에 SSL(Secure Sockets Layer)로 알려진 TLS(전송 계층 보안) 세션에 대해 하나의 URL만 허용하는 주체 이름만 있습니다. SAN은 TLS 서비스에서 여러 URL을 수신하도록 허용하며 다른 애플리케이션과 TLS 포트를 공유하도록 허용하는 인증서의 추가 필드입니다. 예를 들어 SAN은 `www.myreports.com`과 같이 표시될 수 있습니다.

Reporting Services의 TLS 설정에 대한 자세한 내용은 [기본 모드 보고서 서버에서 TLS 연결 구성](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)을 참조하세요.  
  
## <a name="configure-to-use-a-subject-alternative-name-for-web-service-url"></a>웹 서비스 URL에 주체 대체 이름을 사용하도록 구성
  
1.  보고서 서버 구성 관리자를 시작합니다.  
  
     자세한 내용은 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)을 참조하세요.  
  
2.  **웹 서비스 URL** 페이지에서 TLS/SSL 포트 및 TLS/SSL 인증서를 선택합니다.  
  
     ![Reporting Services 구성 관리자](../../reporting-services/report-server-sharepoint/media/reportingservices-configurationmanager.png "Reporting Services 구성 관리자")  
  
     구성 관리자가 포트에 대해 TLS/SSL 인증서를 등록합니다.  
  
3.  rsreportserver.config 파일을 엽니다.  
  
     SSRS 2016 기본 모드의 경우 파일은 기본적으로 다음 폴더에 있습니다.  
  
    ```  
    \Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer  
    ```  
  
     SSRS 2017 이상의 경우 파일은 기본적으로 다음 폴더에 있습니다.  
  
    ```  
    \Program Files\Microsoft SQL Server Reporting Services\SSRS\ReportServer  
    ```  
    
     Power BI Report Server의 경우 파일은 기본적으로 다음 폴더에 있습니다.  
  
    ```  
    \Program Files\Microsoft Power BI Report Server\PBIRS\ReportServer  
    ```  
  
4.  **ReportServerWebService** 애플리케이션의 URL 섹션을 복사합니다.
  
     예를 들어 다음은 원래 URL 섹션입니다.  
  
    ```  
        <URL>  
         <UrlString>https://+:443</UrlString>  
         <AccountSid>S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051</AccountSid>  
         <AccountName>NT Service\ReportServer</AccountName>  
        </URL>  
  
    ```  
  
     다음은 수정된 URL 섹션입니다.
  
    ```  
    <URL>  
         <UrlString>https://+:443</UrlString>  
         <AccountSid>S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051</AccountSid>  
         <AccountName>NT Service\ReportServer</AccountName>  
        </URL>  
        <URL>  
         <UrlString>https://www.myreports.com:443</UrlString>  
         <AccountSid>S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051/AccountSid>  
         <AccountName>NT Service\ReportServer</AccountName>  
        </URL>  
  
    ```  
  
  > [!TIP]  
>  * SSRS 2017 이상의 경우 `AccountSid` 값은 `S-1-5-80-4050220999-2730734961-1537482082-519850261-379003301`이며 `AccountName` 값은 `NT SERVICE\SQLServerReportingServices`입니다.
>  * Power BI Report Server의 경우 `AccountSid` 값은 `S-1-5-80-1730998386-2757299892-37364343-1607169425-3512908663`이며 `AccountName` 값은 `NT SERVICE\PowerBIReportServer`입니다.
  
5.  rsreportserver.config 파일을 저장합니다.  
  
6.  **관리자 권한으로 실행**을 사용하여 명령 프롬프트를 시작하고 Netsh.exe 도구를 실행합니다.  
  
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
    Reserved URL            : https://+:443/ReportServer/  
        User: NT SERVICE\ReportServer  
            Listen: Yes  
            Delegate: No  
            SDDL: D:(A;;GX;;;S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051)  
    ```  
  
     urlacl은 예약된 URL의 DACL(임의 액세스 제어 목록)입니다.  
  
9. 다음을 입력하여 기존 항목과 사용자와 SDDL이 동일한 주체 대체 이름의 새 항목을 만듭니다.  
  
    ```  
    netsh http>add urlacl  url=https://www.myreports.com:443/ReportServer    
    user="NT Service\ReportServer" sddl=D:(A;;GX;;;S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051)  
  
    ```  
  
10. **웹 포털 URL**의 경우 다음을 입력하여 주체 대체 이름의 새 항목을 만듭니다.

    ```  
    netsh http>add urlacl  url=https://www.myreports.com:443/Reports  
    user="NT Service\ReportServer" sddl=D:(A;;GX;;;S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051)  
  
    ```  
> [!TIP]  
>  * SSRS 2017 이상의 경우 `user` 값은 `NT SERVICE\SQLServerReportingServices`이며 `sddl` 값은 `D:(A;;GX;;;S-1-5-80-4050220999-2730734961-1537482082-519850261-379003301)`입니다.
>  * Power BI Report Server의 경우 `user` 값은 `NT SERVICE\PowerBIReportServer`이며 `sddl` 값은 `S-1-5-80-1730998386-2757299892-37364343-1607169425-3512908663`입니다.

> [!NOTE]  
> Power BI Report Server의 경우 다음을 입력하여 주체 대체 이름의 추가 항목 두 개를 만들어야 합니다.
>  * `add urlacl url=https://www.myreports.com:443/PowerBI user="NT SERVICE\PowerBIReportServer" sddl=D:(A;;GX;;;S-1-5-80-1730998386-2757299892-37364343-1607169425-3512908663)`
>  * `add urlacl url=https://www.myreports.com:443/wopi user="NT SERVICE\PowerBIReportServer" sddl=D:(A;;GX;;;S-1-5-80-1730998386-2757299892-37364343-1607169425-3512908663)`

11. 보고서 서버 구성 관리자의 **보고서 서버 상태** 페이지에서 **중지**를 클릭한 다음, **시작**을 클릭하여 보고서 서버를 다시 시작합니다.  
  
## <a name="see-also"></a>참고 항목

 [RsReportServer.config 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Reporting Services 구성 관리자](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Reporting Services 구성 파일 수정](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [보고서 서버 URL 구성](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
