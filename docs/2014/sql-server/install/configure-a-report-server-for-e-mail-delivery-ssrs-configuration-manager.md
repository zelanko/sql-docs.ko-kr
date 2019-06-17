---
title: 보고서 서버 전자 메일 배달 (SSRS 구성 관리자) 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], distributing
- report servers [Reporting Services], e-mail delivery
- remote SMTP service [Reporting Services]
- distributing reports [Reporting Services], e-mail
- CDO
- Collaboration Data Objects
- SMTP settings [Reporting Services]
- e-mail [Reporting Services]
- sending reports
- mail [Reporting Services]
- local SMTP service [Reporting Services]
ms.assetid: b838f970-d11a-4239-b164-8d11f4581d83
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 196bfdc78ea29b1d334660a732f087a50ae9c2ee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66096117"
---
# <a name="configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager"></a>전자 메일 배달을 위한 보고서 서버 구성(SSRS 구성 관리자)


  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에는 전자 메일을 통해 보고서를 배포할 수 있는 전자 메일 배달 확장 프로그램이 있습니다. 전자 메일 구독을 정의하는 방법에 따라 배달은 알림, 링크, 첨부 파일 또는 포함된 보고서로 구성될 수 있습니다. 전자 메일 배달 확장 프로그램은 기존 메일 서버 기술을 사용합니다. 메일 서버는 SMTP 서버 또는 전달자여야 합니다. 보고서 서버는 운영 체제에서 제공하는 CDO(Collaboration Data Objects) 라이브러리(cdosys.dll)를 통해 SMTP 서버에 연결합니다.  
  
 보고서 서버 전자 메일 배달 확장 프로그램은 기본적으로 구성되어 있지 않습니다. 따라서 Reporting Services 구성 관리자를 사용하여 확장 프로그램을 최소한으로 구성해야 합니다. 고급 속성을 설정하려면 `RSReportServer.config` 파일을 편집해야 합니다. 이 확장 프로그램을 사용할 수 있도록 보고서 서버를 구성할 수 없는 경우에는 보고서를 공유 폴더로 배달할 수 있습니다. 자세한 내용은 [File Share Delivery in Reporting Services](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md)을 참조하세요.  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드|  
  
 
  
##  <a name="bkmk_configuration_requirements"></a> 구성 요구 사항  
  
-   보고서 서버 전자 메일 배달은 CDO(Collaboration Data Object)에 구현되며 로컬 또는 원격 SMTP(Simple Mail Transfer Protocol) 서버나 SMTP 전달자가 있어야 합니다. SMTP를 지원하지 않는 운영 체제도 있습니다. Windows Server 2008의 Itanium 기반 버전을 사용하는 경우 SMTP가 지원되지 않습니다. CDO를 통해 제공되는 구성 옵션에 대한 자세한 내용은 MSDN에서 [CoClass 구성(Configuration CoClass)](https://go.microsoft.com/fwlink/?LinkId=98237) 을 참조하십시오.  
  
-   메일을 보내려면 보고서 서버 서비스 계정이 SMTP 서버에 대한 권한을 가지고 있어야 합니다.  
  
-   전자 메일 배달 확장 프로그램은 전자 메일 첨부 파일에 UTF-8 인코딩을 사용합니다. HTML 렌더링 확장 프로그램에서 UTF-8만 지원하기 때문에 인코딩은 수정할 수 없습니다.  
  
> [!NOTE]  
>  기본 전자 메일 배달 확장 프로그램은 디지털 서명 또는 보내는 메일 메시지 암호화를 지원하지 않습니다.  
  
 
  
##  <a name="bkmk_configure_for_local_or_remote_SMTP"></a> 로컬 또는 원격 SMTP 서비스를 위한 보고서 서버를 구성합니다.  
 로컬 SMTP 서비스나 원격 SMTP 서버 또는 전달자를 사용하여 전자 메일 배달을 지원할 수 있습니다. 기존 원격 SMTP 서버에 대한 액세스 권한이 있을 경우 이 서버를 사용할 것을 고려해야 합니다. 사용할 수 있는 SMTP 서버가 없거나 이후에 컴퓨터 연결 실패의 원인이 될 수 있는 보고서 배달 오류가 발생할 경우 로컬 SMTP 서비스를 사용하도록 전환해야 합니다. 로컬 또는 원격 서비스를 위해 보고서 서버를 구성하는 방법에 대해서는 이 항목의 뒷부분에서 자세히 설명합니다.  
  
  
  
##  <a name="bkmk_setting_email_delivery"></a> 전자 메일 배달 위한 구성 옵션 설정  
 보고서 서버 전자 메일 배달을 사용하려면 먼저 사용할 SMTP 서버에 대한 정보를 제공하는 구성 값을 설정해야 합니다.  
  
 전자 메일 배달을 위한 보고서 서버를 구성하려면 다음을 수행합니다.  
  
-   SMTP 서버와 전자 메일을 보낼 수 있는 권한이 있는 사용자 계정만 지정하는 경우 Reporting Services 구성 관리자를 사용합니다. 이는 보고서 서버 전자 메일 배달 확장 프로그램을 구성하는 데 필요한 최소 설정입니다. 자세한 내용은 [전자 메일 설정-Configuration Manager &#40;SSRS 기본 모드&#41; ](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md) 하 고 [Reporting Services의 전자 메일 배달](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md).  
  
-   텍스트 편집기를 사용하여 RSreportserver.config 파일에 추가 설정을 지정합니다(옵션). 이 파일에는 보고서 서버 전자 메일 배달을 위한 모든 구성 설정이 포함되어 있습니다. 로컬 SMTP 서버를 사용하거나 전자 메일 배달을 특정 호스트로 제한하는 경우 이러한 파일에 추가 설정을 지정해야 합니다. 찾기 및 구성 파일을 수정 하는 방법에 대 한 자세한 내용은 참조 하세요. [Reporting Services 구성 파일 수정 &#40;RSreportserver.config&#41; ](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) SQL Server 온라인 설명서의 합니다.  
  
> [!NOTE]  
>  보고서 서버 전자 메일 설정은 CDO를 기반으로 합니다. 특정 설정에 대한 세부 정보를 보려면 CDO 제품 설명서를 참조하십시오.  
  

  
##  <a name="bkmk_example_config_file"></a> 예제 보고서 서버 전자 메일 구성  
 다음 예에서는 원격 SMTP 서버에 대한 RSreportserver.config 파일 설정을 보여 줍니다. 설정에 대한 설명 및 유효한 값에 대한 자세한 내용은 [RSReportServer Configuration File](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) 온라인 설명서의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Onl온라인 설명서의e or the CDO product documentation.  
  
```  
<RSEmailDPConfiguration>  
     <SMTPServer>mySMTPServer.Adventure-Works.com</SMTPServer>  
     <SMTPServerPort></SMTPServerPort>  
     <SMTPAccountName></SMTPAccountName>  
     <SMTPConnectionTimeout></SMTPConnectionTimeout>  
     <SMTPServerPickupDirectory></SMTPServerPickupDirectory>  
     <SMTPUseSSL></SMTPUseSSL>  
     <SendUsing>2</SendUsing>  
     <SMTPAuthenticate></SMTPAuthenticate>  
     <From>my-rs-email-account@Adventure-Works.com</From>  
     <EmbeddedRenderFormats>  
          <RenderingExtension>MHTML</RenderingExtension>  
     </EmbeddedRenderFormats>  
     <PrivilegedUserRenderFormats></PrivilegedUserRenderFormats>  
     <ExcludedRenderFormats>  
          <RenderingExtension>HTMLOWC</RenderingExtension>  
          <RenderingExtension>NULL</RenderingExtension>  
     </ExcludedRenderFormats>  
     <SendEmailToUserAlias>True</SendEmailToUserAlias>  
     <DefaultHostName></DefaultHostName>  
     <PermittedHosts>  
          <HostName>Adventure-Works.com</HostName>  
          <HostName>hotmail.com</HostName>  
     </PermittedHosts>  
</RSEmailDPConfiguration>  
```  
  

  
##  <a name="bkmk_setting_TO_field"></a> 설정에 대 한 구성 옵션을 하려면: 구성 옵션  
 **개인 구독 관리** 태스크에 의해 부여된 권한에 따라 만들어진 사용자 정의 구독에는 도메인 사용자 계정에 따라 사전 설정된 사용자 이름이 들어 있습니다. 사용자가 구독을 생성할 때 구독을 생성하는 사람의 도메인 사용자 계정이 **받는 사람:** 필드의 수신자 이름으로 자동으로 삽입됩니다.  
  
 도메인 사용자 계정과는 다른 전자 메일 계정을 사용하는 SMTP 서버 또는 전달자를 사용하는 경우 SMTP 서버가 보고서를 해당 사용자에게 배달할 수 없습니다.  
  
 이 문제를 해결하려면 사용자가 **받는 사람:** 필드에 이름을 입력할 수 있도록 구성 설정을 수정해야 합니다.  
  
1.  텍스트 편집기에서 RSReportServer.config를 엽니다.  
  
2.  `SendEmailToUserAlias`를 `False`로 설정합니다.  
  
3.  `DefaultHostName` 을 DNS(Domain Name System) 이름이나 SMTP 서버 또는 전달자의 IP 주소로 설정합니다.  
  
4.  파일을 저장합니다.  
  
  
  
##  <a name="bkmk_options_remote_SMTP"></a> 원격 SMTP 서비스에 대 한 구성 옵션  
 보고서 서버와 SMTP 서버 또는 전달자 간의 연결은 다음과 같은 구성 설정에 의해 결정됩니다.  
  
-   `SendUsing` 은 메시지를 보내는 방법을 지정합니다. 네트워크 SMTP 서비스나 로컬 SMTP 서비스 선택 디렉터리 중에서 선택할 수 있습니다. 원격 SMTP 서비스를 사용하려면 RSReportServer.config 파일에서 이 값을 **2** 로 설정해야 합니다.  
  
-   `SMTPServer` 는 원격 SMTP 서버 또는 전달자를 지정합니다. 이 값은 원격 SMTP 서버 또는 전달자를 사용할 때 필요합니다.  
  
-   `From` 은 메일 메시지의 **보낸 사람:** 줄에 표시할 값을 설정합니다. 이 값은 원격 SMTP 서버 또는 전달자를 사용할 때 필요합니다.  
  
 원격 SMTP 서비스에 사용되는 기타 값은 다음과 같습니다. 기본값을 재설정하지 않으려면 이 값을 지정할 필요가 없습니다.  
  
-   **SMTPServerPort** 는 포트 25에 대해 구성되어 있습니다.  
  
-   **SMTPAuthenticate** 는 보고서 서버에서 원격 SMTP 서버에 연결하는 방법을 지정합니다. 기본값은 0(인증 없음)입니다. 이 경우 익명 액세스를 통해 연결이 설정됩니다. 도메인 구성에 따라 보고서 서버와 SMTP 서버가 동일한 도메인의 멤버여야 할 수도 있습니다.  
  
     제한된 메일 그룹(예: 인증된 계정에서 보낸 메시지만 허용하는 메일 그룹)에 전자 메일을 보내려면 **SMTPAuthenticate** 를 **2**로 설정합니다.  
  

  
##  <a name="bkmk_options_local_SMTP"></a> 로컬 SMTP 서비스에 대 한 구성 옵션  
 보고서 서버 전자 메일 배달을 테스트하거나 문제를 해결하려면 로컬 SMTP 서비스를 구성하는 것이 효율적입니다. 로컬 SMTP 서비스는 기본적으로 활성화되어 있지 않습니다. 를 사용 하도록 설정 하는 방법에 대 한 참조 [(SSRS 구성 관리자) 전자 메일 배달을 위한 보고서 서버 구성](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md) 하 고 [전자 메일 설정-Configuration Manager &#40;SSRS 기본 모드&#41; ](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md) .  
  
 보고서 서버와 로컬 SMTP 서버 또는 전달자 간의 연결은 다음과 같은 구성 설정에 의해 결정됩니다.  
  
-   `SendUsing` 로 설정 되어 **1**합니다.  
  
-   **SMTPServerPickupDirectory** 를 로컬 드라이브의 폴더로 설정합니다.  
  
    > [!NOTE]  
    >  설정 하지 않으면 `SMTPServer` 로컬 SMTP 서버를 사용 하는 경우.  
  
-   `From` 은 메일 메시지의 **보낸 사람:** 줄에 표시할 값을 설정합니다. 이 값은 필수 사항입니다.  
  
 
  
##  <a name="bkmk_use_configuration_manager"></a> Reporting Services 구성 관리자를 사용 하 여 보고서 서버 전자 메일을 구성 하려면  
  
1.  보고서 서버 Windows 서비스에 SMTP 서버에 대한 `Send As` 권한이 있는지 확인합니다.  
  
2.  Reporting Services 구성 관리자를 시작한 후 보고서 서버 인스턴스에 연결합니다.  
  
3.  전자 메일 설정 페이지에서 SMTP 서버의 이름을 입력합니다. 이 값은 IP 주소, 회사 인트라넷에 있는 컴퓨터의 UNC 이름 또는 정규화된 도메인 이름일 수 있습니다.  
  
4.  **보낸 사람 주소** 에 SMTP 서버에서 전자 메일을 보낼 수 있는 권한이 있는 계정의 이름을 입력합니다.  
  
5.  **적용**을 클릭합니다.  
  

  
##  <a name="bkmk_confiugre_remote_SMTP"></a> 보고서 서버에 대 한 원격 SMTP 서비스를 구성 하려면  
  
1.  보고서 서버 Windows 서비스에 SMTP 서버에 대한 `Send As` 권한이 있는지 확인합니다.  
  
2.  텍스트 편집기에서 RSReportServer.config 파일을 엽니다.  
  
3.  확인 <`UrlRoot`> 보고서 서버 URL 주소로 설정 됩니다. 이 값은 보고서 서버를 구성할 때 설정되므로 이미 채워져 있을 것입니다. 그렇지 않으면 보고서 서버 URL 주소를 입력합니다.  
  
4.  배달 섹션에서 찾을 <`ReportServerEmail`>.  
  
5.  <`SMTPServer`>에 SMTP 서버의 이름을 입력 합니다. 이 값은 IP 주소, 회사 인트라넷에 있는 컴퓨터의 UNC 이름 또는 정규화된 도메인 이름일 수 있습니다.  
  
6.  확인 <`SendUsing`>이 2로 설정 합니다. 다른 값으로 설정되어 있으면 보고서 서버에서 원격 SMTP 서비스를 사용하도록 구성되지 않은 것입니다.  
  
7.  <`From`>을 SMTP 서버에서 전자 메일을 보낼 수 있는 권한이 있는 계정의 이름을 입력 합니다.  
  
8.  파일을 저장합니다.  
  
     보고서 서버가 자동으로 새 설정을 사용하므로 서비스를 다시 시작할 필요가 없습니다. 추가 SMTP 설정을 지정하여 보고서 서버 전자 메일 배달에 SMTP 서버가 사용되는 방법을 추가로 구성할 수 있습니다. 자세한 내용은 [Configur온라인 설명서의g a Report Server for E-Mail Delivery](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md) 및 [RSReportServer Configuration File](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) 온라인 설명서의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Onl온라인 설명서의e.  
  

  
##  <a name="bkmk_confiugre_local_SMTP"></a> 보고서 서버에 대 한 로컬 SMTP 서비스를 구성 하려면  
  
1.  제어판에서 **프로그램 추가/제거**를 클릭합니다.  
  
2.  **Windows 구성 요소 추가/제거** 를 클릭하여 Windows 구성 요소 마법사를 시작합니다.  
  
3.  **애플리케이션 서버** 를 선택하고 **자세히**를 클릭합니다.  
  
4.  **인터넷 정보 서비스(IIS)** 를 선택하고 **자세히** 를 클릭합니다.  
  
5.  **SMTP 서비스** 확인란을 선택하고 **확인** 을 클릭합니다.  
  
6.  Windows 구성 요소 마법사에서 **다음**을 클릭합니다. **마침**을 클릭합니다.  
  
7.  서비스가 **서비스** 콘솔에서 실행되고 있는지 확인합니다.  
  
8.  텍스트 편집기에서 **RSReportServer.config** 파일을 엽니다.  
  
9. `<UrlRoot>` 가 보고서 서버 URL 주소로 설정되어 있는지 확인합니다. 이 값은 보고서 서버를 구성할 때 설정되므로 이미 채워져 있을 것입니다. 그렇지 않으면 보고서 서버 URL 주소를 입력합니다.  
  
10. 배달 섹션에서 `<ReportServerEmail>.`을 찾습니다.  
  
11. `<SMTPServer>`에서 이 설정의 모든 값을 지웁니다. 이때 태그는 삭제하지 않습니다.  
  
12. `<SendUsing>` 을 1로 설정합니다. 다른 값으로 설정되어 있으면 보고서 서버에서 로컬 SMTP 서비스를 사용하도록 구성되지 않은 것입니다.  
  
13. `<SMTPServerPickupDirectory>` 를 로컬 드라이브의 폴더로 설정합니다.  
  
14. `<From>` 을 SMTP 서버에서 전자 메일을 보낼 수 있는 권한이 있는 계정으로 설정합니다.  
  
15. 파일을 저장합니다.  
  
 
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
