---
title: "전자 메일 설정-Reporting Services 기본 모드 (구성 관리자) | Microsoft Docs"
ms.custom: 
ms.date: 06/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.rsconfigtool.emailsettings.F1
helpviewer_keywords:
- SQL11.rsconfigtool.emailsettings.F1
ms.assetid: cdad1529-bfa6-41fb-9863-d9ff1b802577
caps.latest.revision: 13
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 45aad2cc5dbdbc23fa28f1f70b138da4ec05f281
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="e-mail-settings---reporting-services-native-mode-configuration-manager"></a>전자 메일 설정 - Reporting Services 기본 모드(구성 관리자)
Reporting Service에는 메일을 통해 보고서를 배포할 수 있는 메일 배달 확장 프로그램이 있습니다. 전자 메일 구독을 정의하는 방법에 따라 배달은 알림, 링크, 첨부 파일 또는 포함된 보고서로 구성될 수 있습니다. 전자 메일 배달 확장 프로그램은 기존 메일 서버 기술을 사용합니다. 메일 서버는 SMTP 서버 또는 전달자여야 합니다. 보고서 서버는 운영 체제에서 제공하는 CDO(Collaboration Data Objects) 라이브러리(cdosys.dll)를 통해 SMTP 서버에 연결합니다.

보고서 서버 전자 메일 배달 확장 프로그램은 기본적으로 구성되어 있지 않습니다. 따라서 Reporting Services 구성 관리자를 사용하여 확장 프로그램을 최소한으로 구성해야 합니다. 고급 속성을 설정하려면 RSReportServer.config 파일을 편집해야 합니다. 이 확장 프로그램을 사용할 수 있도록 보고서 서버를 구성할 수 없는 경우에는 보고서를 공유 폴더로 배달할 수 있습니다. 자세한 내용은 Reporting Services의 파일 공유 배달을 참조하세요.

## <a name="configuration-requirements"></a>구성 요구 사항

- 보고서 서버 전자 메일 배달은 CDO(Collaboration Data Object)에 구현되며 로컬 또는 원격 SMTP(Simple Mail Transfer Protocol) 서버나 SMTP 전달자가 있어야 합니다. SMTP를 지원하지 않는 운영 체제도 있습니다. Windows Server 2008의 Itanium 기반 버전을 사용하는 경우 SMTP가 지원되지 않습니다. CDO를 통해 제공되는 구성 옵션에 대한 자세한 내용은 MSDN에서 [CoClass 구성(Configuration CoClass)](http://go.microsoft.com/fwlink/?LinkId=98237) 을 참조하십시오.

메일을 보내려면 구성된 인증 계정에 SMTP 서버에 대한 권한이 있어야 합니다.

- 전자 메일 배달 확장 프로그램은 전자 메일 첨부 파일에 UTF-8 인코딩을 사용합니다. HTML 렌더링 확장 프로그램에서 UTF-8만 지원하기 때문에 인코딩은 수정할 수 없습니다.

> [!NOTE] 
> 기본 전자 메일 배달 확장 프로그램은 디지털 서명 또는 보내는 메일 메시지 암호화를 지원하지 않습니다.

## <a name="setting-configuration-options-for-e-mail-delivery"></a>전자 메일 배달을 위한 구성 옵션 설정
보고서 서버 전자 메일 배달을 사용하려면 먼저 사용할 SMTP 서버에 대한 정보를 제공하는 구성 값을 설정해야 합니다.

전자 메일 배달을 위한 보고서 서버를 구성하려면 다음을 수행합니다.

- SMTP 서버와 전자 메일을 보낼 수 있는 권한이 있는 사용자 계정만 지정하는 경우 Reporting Services 구성 관리자를 사용합니다. 이는 보고서 서버 전자 메일 배달 확장 프로그램을 구성하는 데 필요한 최소 설정입니다.

- 텍스트 편집기를 사용하여 RSreportserver.config 파일에 추가 설정을 지정합니다(옵션). 이 파일에는 보고서 서버 전자 메일 배달을 위한 모든 구성 설정이 포함되어 있습니다. 로컬 SMTP 서버를 사용하거나 전자 메일 배달을 특정 호스트로 제한하는 경우 이러한 파일에 추가 설정을 지정해야 합니다. 구성 파일을 찾아서 수정하는 방법은 SQL Server 온라인 설명서의 [Reporting Services 구성 파일 수정(RSreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) 을 참조하세요.

> [!NOTE] 
> 보고서 서버 전자 메일 설정은 CDO를 기반으로 합니다. 특정 설정에 대한 세부 정보를 보려면 CDO 제품 설명서를 참조하십시오.

## <a name="a-namersconfigmanconfigure-report-server-e-mail-using-the-reporting-services-configuration-manager"></a><a name="rsconfigman"/>Reporting Services 구성 관리자를 사용하여 보고서 서버 메일 구성

1. Reporting Services 구성 관리자를 시작한 후 보고서 서버 인스턴스에 연결합니다.

2. **보낸 사람 주소**에 생성된 메일의 **보낸 사람:** 필드에 사용할 메일 주소를 입력합니다. 

     SMTP 서버에서 메일을 보낼 수 있는 권한이 있는 사용자 계정을 지정해야 합니다. **보낸 사람 주소** 에 대해 입력한 값이 rsreportserver.config 파일의 `<From>` 필드에 저장됩니다.  

3.  **SMTP 서버**에서 사용할 SMTP 서버 또는 게이트웨이를 지정합니다. 

     이 값은 IP 주소, 회사 인트라넷에 있는 컴퓨터의 NetBIOS 이름 또는 정규화된 도메인 이름일 수 있습니다. **SMTP 서버** 에 대해 입력한 값이 rsreportserver.config 파일의 `<SMTPServer>` 필드에 저장됩니다.

4. **인증** 드롭다운을 사용하여 SMTP 서버에 인증하는 방법을 지정합니다. 이 

     - **인증 없음** 을 선택하면 지정된 메일 서버에 익명으로 연결됩니다.
     
          이 옵션을 선택하면 rsreportserver.config에서 `<SendUsing>` 값은 **2** 로, `<SMTPAuthenticate>` 값은 **0** 으로 설정됩니다.
     
     - **사용자 이름 및 암호(기본)** 를 선택하면 메일 서버에 연결할 때 사용할 사용자 이름 및 암호를 지정할 수 있습니다. **보안 연결 사용** 을 선택하여 암호화된 연결을 통해 메일 서버에 연결할 수도 있습니다.
     
          이 옵션을 선택하면 rsreportserver.config에서 `<SendUsing>` 값은 **2** 로, `<SMTPAuthenticate>` 값은 **1** 로 설정됩니다. **보안 연결 사용** 을 선택하면 `SMTPUseSSL` 이 **True**로 설정됩니다. **사용자 이름** 은 암호화된 값으로 `<SendUserName>` 에 설정됩니다. **암호** 는 암호화된 값으로 `<SendPassword>` 에 설정됩니다.
     
     - **NTLM(보고서 서버 서비스 계정)** 은 보고서 서버에 대해 지정한 서비스 계정을 사용합니다. 인증을 위해 보고서 서버 서비스 계정을 사용하는 경우 서비스 계정에 SMTP 서버에 대한 **Send As** 권한이 있는지 확인합니다.
     
          이 옵션을 선택하면 rsreportserver.config에서 `<SendUsing>` 값은 **2** 로, `<SMTPAuthenticate>` 값은 **2** 로 설정됩니다.

5. **적용**을 선택합니다.

6. rsreportserver.config 내에 메일 구성에 대한 추가 필드를 필요에 따라 조정할 수 있습니다.

## <a name="example-report-server-e-mail-configuration"></a>보고서 서버 전자 메일 구성의 예
다음 예에서는 원격 SMTP 서버에 대한 RSreportserver.config 파일 설정을 보여 줍니다. 설정에 대한 설명 및 유효한 값에 대한 자세한 내용은 SQL Server 온라인 설명서의 [Rsreportserver.config 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) 을 참조하세요.

```
<RSEmailDPConfiguration>
     <SMTPServer>mySMTPServer.Adventure-Works.com</SMTPServer>
     <SMTPServerPort></SMTPServerPort>
     <SMTPAccountName></SMTPAccountName>
     <SMTPConnectionTimeout></SMTPConnectionTimeout>
     <SMTPServerPickupDirectory></SMTPServerPickupDirectory>
     <SMTPUseSSL>False</SMTPUseSSL>
     <SendUsing>2</SendUsing>
     <SMTPAuthenticate>2</SMTPAuthenticate>
     <From>my-rs-email-account@Adventure-Works.com</From>
     <EmbeddedRenderFormats>
          <RenderingExtension>MHTML</RenderingExtension>
     </EmbeddedRenderFormats>
     <PrivilegedUserRenderFormats></PrivilegedUserRenderFormats>
     <ExcludedRenderFormats>
          <RenderingExtension>HTMLOWC</RenderingExtension>
          <RenderingExtension>NULL</RenderingExtension>
          <RenderingExtension>RGDI</RenderingExtension>
     </ExcludedRenderFormats>
     <SendEmailToUserAlias>True</SendEmailToUserAlias>
     <DefaultHostName></DefaultHostName>
     <PermittedHosts>
          <HostName>Adventure-Works.com</HostName>
          <HostName>hotmail.com</HostName>
     </PermittedHosts>
     <SendUserName></SendUserName>
     <SendPassword></SendPassword>
</RSEmailDPConfiguration>
```
## <a name="configuration-options-for-setting-the-to-field-in-a-message"></a>메시지의 받는 사람: 필드 설정을 위한 구성 옵션
개인 구독 관리 태스크에 의해 부여된 권한에 따라 만들어진 사용자 정의 구독에는 도메인 사용자 계정에 따라 사전 설정된 사용자 이름이 들어 있습니다. 사용자가 구독을 생성할 때 구독을 생성하는 사람의 도메인 사용자 계정이 **받는 사람:** 필드의 수신자 이름으로 자동으로 삽입됩니다.

도메인 사용자 계정과는 다른 전자 메일 계정을 사용하는 SMTP 서버 또는 전달자를 사용하는 경우 SMTP 서버가 보고서를 해당 사용자에게 배달할 수 없습니다.

이 문제를 해결하려면 사용자가 **받는 사람:** 필드에 이름을 입력할 수 있도록 구성 설정을 수정해야 합니다.

1. 텍스트 편집기에서 RSReportServer.config를 엽니다.

2. `<SendEmailToUserAlias>` 를 **False**로 설정합니다.

3. `<DefaultHostName>` 을 DNS(Domain Name System) 이름이나 SMTP 서버 또는 전달자의 IP 주소로 설정합니다.

4. 파일을 저장합니다.

## <a name="configuration-options-for-remote-smtp-service"></a>원격 SMTP 서비스를 위한 구성 옵션
보고서 서버와 SMTP 서버 또는 전달자 간의 연결은 다음과 같은 구성 설정에 의해 결정됩니다.

- `<SendUsing>` 은 메시지를 보내는 방법을 지정합니다. 네트워크 SMTP 서비스나 로컬 SMTP 서비스 선택 디렉터리 중에서 선택할 수 있습니다. 원격 SMTP 서비스를 사용하려면 RSReportServer.config 파일에서 이 값을 **2** 로 설정해야 합니다.
- `<SMTPServer>` 는 원격 SMTP 서버 또는 전달자를 지정합니다. 이 값은 원격 SMTP 서버 또는 전달자를 사용할 때 필요합니다.
- `<From>` 은 메일 메시지의 **보낸 사람:** 줄에 표시할 값을 설정합니다. 이 값은 원격 SMTP 서버 또는 전달자를 사용할 때 필요합니다.

원격 SMTP 서비스에 사용되는 기타 값은 다음과 같습니다. 기본값을 재설정하지 않으려면 이 값을 지정할 필요가 없습니다.

- `<SMTPServerPort>` 는 기본적으로 포트 25에 대해 구성되어 있습니다.
- `<SMTPAuthenticate>` 는 보고서 서버에서 원격 SMTP 서버에 연결하는 방법을 지정합니다. 기본값은 **0** (인증 없음)입니다. 이 경우 익명 액세스를 통해 연결이 설정됩니다. 도메인 구성에 따라 보고서 서버와 SMTP 서버가 동일한 도메인의 멤버여야 할 수도 있습니다.
- 제한된 메일 그룹(예: 인증된 계정에서 보낸 메시지만 허용하는 메일 그룹)에 메일을 보내려면 `<SMTPAuthenticate>` 를 **1** 또는 **2**로 설정합니다. **1**로 설정하면 `<SendUserName>` 및 `<SendPassword>`도 설정해야 합니다. `<SendUserName>` 및 `<SendPassword>`에 대한 값을 암호화하므로 Reporting Services 구성 관리자를 통해 이 작업을 수행하는 것이 좋습니다.

### <a name="to-configure-a-remote-smtp-service-for-the-report-server"></a>보고서 서버에 대해 원격 SMTP 서비스를 구성하려면

> [!NOTE] 
> Reporting Services 구성 관리자를 통해 메일 서버를 구성하는 것이 좋습니다.

1. 보고서 서버 Windows 서비스에 SMTP 서버에 대한 **Send As** 권한이 있는지 확인합니다.

2. 텍스트 편집기에서 RSReportServer.config 파일을 엽니다.

3. `<UrlRoot>` 가 보고서 서버 URL 주소로 설정되어 있는지 확인합니다. 이 값은 보고서 서버를 구성할 때 설정되므로 이미 채워져 있을 것입니다. 그렇지 않으면 보고서 서버 URL 주소를 입력합니다.

4. 배달 섹션에서 `<RSEmailDPConfiguration>`을 찾습니다.
     
5. `<SMTPServer>`에 SMTP 서버 이름을 입력합니다. 이 값은 IP 주소, 회사 인트라넷에 있는 컴퓨터의 UNC 이름 또는 정규화된 도메인 이름일 수 있습니다.

6. 보고서 서버에 대한 서비스 계정을 사용하려면 `<SendUsing>` 의 값을 **2** 로 설정합니다. 기본 인증을 위해 `<SendUsing>` 의 값을 **1** 로 설정합니다. **1**로 설정하면 `<SendUserName>` 및 `<SendPassword>`값을 추가로 제공해야 합니다. 해당 값을 암호화하려면 Reporting Services 구성 관리자 내에서 인증을 설정합니다.

7. `<SMTPAuthenticate>` 을 1 또는 2로 설정하는 경우 **의 값을** 1 `<SendUsing>` 로 설정합니다.

7. `<From>`을 설정합니다. SMTP 서버에서 메일을 보낼 수 있는 권한이 있는 사용자 계정을 지정해야 합니다.

8. 파일을 저장합니다.

     보고서 서버가 자동으로 새 설정을 사용하므로 서비스를 다시 시작할 필요가 없습니다. 추가 SMTP 설정을 지정하여 보고서 서버 전자 메일 배달에 SMTP 서버가 사용되는 방법을 추가로 구성할 수 있습니다.

## <a name="configuration-options-for-local-smtp-service"></a>로컬 SMTP 서비스를 위한 구성 옵션
보고서 서버 전자 메일 배달을 테스트하거나 문제를 해결하려면 로컬 SMTP 서비스를 구성하는 것이 효율적입니다. 로컬 SMTP 서비스는 기본적으로 활성화되어 있지 않습니다.

보고서 서버와 로컬 SMTP 서버 또는 전달자 간의 연결은 다음과 같은 구성 설정에 의해 결정됩니다.

- **SendUsing** 을 **1**로 설정합니다.
- **SMTPServerPickupDirectory** 를 로컬 드라이브의 폴더로 설정합니다.

  > [!NOTE] 
  > 로컬 SMTP 서버를 사용하는 경우 SMTPServer를 설정하지 마세요.

- **From** 은 메일 메시지의 **보낸 사람:** 줄에 표시할 값을 설정합니다. 이 값은 필수 사항입니다.

### <a name="to-configure-a-local-smtp-service-for-the-report-server"></a>보고서 서버에 대해 로컬 SMTP 서비스를 구성하려면

1. **역할 및 기능 추가 마법사** 를 시작하려면 제어판에서 **Windows 기능 사용/사용 안 함**을 선택합니다.

2. **역할 기반 또는 기능 기반 설치** 를 선택하고 **다음**을 선택합니다.

3. IIS(인터넷 정보 서버)를 설치할 서버를 선택하고 **다음**을 선택합니다.

4. **서버 역할** * 페이지에서 *다음*을 선택합니다.
     
5. *기능* 페이지에서 **SMTP 서버** 를 선택하고 **다음**을 선택합니다.

     SMTP 서버에 필요한 추가 기능을 설치할지 묻는 메시지가 표시되면 **기능 추가**를 선택합니다.

6. **웹 서버 역할(IIS)** 페이지에서 *다음* 을 선택합니다.

7. **역할 서비스** 페이지에서 *다음* 을 선택합니다.

8. **확인** 페이지에서 **설치** 를 선택합니다.

9. **SMTP(Simple Mail Transfer Protocol)** Windows 서비스가 서비스 콘솔에서 실행되고 있는지 확인합니다.

     로컬 SMTP 서버를 구성하려면 관리 도구에서 IIS 6.0 관리자를 사용해야 합니다.

10. 텍스트 편집기에서 RSReportServer.config 파일을 엽니다.

11. `<UrlRoot>` 가 보고서 서버 URL 주소로 설정되어 있는지 확인합니다. 이 값은 보고서 서버를 구성할 때 설정되므로 이미 채워져 있을 것입니다. 설정되어 있지 않은 경우 보고서 서버에 대한 웹 서비스 URL 주소를 입력합니다.

12. 배달 섹션에서 `<RSEmailDPConfiguration>`을 찾습니다.
     
13. `<SMTPServer>` 가 존재하지만 비어 있는지 확인합니다.
     
14. `<SendUsing>` 을 1로 설정합니다.
     
14. `<SMTPAuthenticate>` 를 0으로 설정합니다.
     
15. `<SMTPServerPickupDirectory>` 를 SMTP 서비스 픽업 폴더로 설정합니다.
     
     기본 위치는 *C:\inetpub\mailroot\Pickup*이 됩니다.
     
16. `<From>`을 설정합니다. 이는 메일 메시지의 **보낸 사람:** 줄에 표시할 값을 설정합니다.
     
17. 파일을 저장합니다.
  
## <a name="see-also"></a>참고 항목  
[Reporting Services 구성 관리자(기본 모드)](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  
[Reporting Services 구성 파일 (rsreportserver.config)를 수정 합니다.](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  
[Rsreportserver.config 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)
  
  

