---
title: "보고서 서버에 대 한 서비스 사용자 이름 (SPN) 등록 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dda91d4f-77cc-4898-ad03-810ece5f8e74
caps.latest.revision: 7
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9518d1bd3ee166a0f21292ca08130214afc841be
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="register-a-service-principal-name-spn-for-a-report-server"></a>보고서 서버의 SPN(서비스 사용자 이름) 등록
  상호 인증에 Kerberos 프로토콜을 사용하는 네트워크에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 배포하는 경우 도메인 사용자 계정으로 실행되도록 보고서 서버 서비스 SPN(서비스 사용자 이름)을 구성하려면 보고서 서버 서비스에 대한 SPN을 만들어야 합니다.  
  
## <a name="about-spns"></a>SPN 정보  
 SPN은 Kerberos 인증을 사용하는 네트워크에서 고유한 서비스 식별자로 서비스 클래스, 호스트 이름, 포트로 구성됩니다. Kerberos 인증을 사용하는 네트워크에서 서버에 대한 SPN은 기본 제공 컴퓨터 계정(예: NetworkService 또는 LocalSystem) 또는 사용자 계정에서 등록되어야 합니다. 기본 제공 계정에 대해서는 SPN이 자동으로 등록됩니다. 그러나 도메인 사용자 계정에서 서비스를 실행할 경우 사용할 계정에 대한 SPN을 수동으로 등록해야 합니다.  
  
 SPN을 만들려면 **SetSPN** 명령줄 유틸리티를 사용할 수 있습니다. 자세한 내용은 다음 항목을 참조하세요.  
  
-   [Setspn](http://technet.microsoft.com/library/cc731241\(WS.10\).aspx) (http://technet.microsoft.com/library/cc731241(WS.10).aspx).  
  
-   [SPN(서비스 사용자 이름) SetSPN 구문(Setspn.exe)](http://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx) (http://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx)  
  
 도메인 컨트롤러에서 이 유틸리티를 실행하려면 도메인 관리자여야 합니다.  
  
## <a name="syntax"></a>구문  
 SetSPN 유틸리티를 사용하여 보고서 서버의 SPN을 만드는 명령 구문은 다음과 같습니다.  
  
```  
Setspn -s http/<computername>.<domainname>:<port> <domain-user-account>  
```  
  
 **SetSPN** 은 Windows Server에서 사용할 수 있습니다. **-s** 인수는 중복이 없는지 확인한 후 SPN을 추가합니다. **참고: -s** 는 Windows Server(Windows Server 2008부터)에서 사용할 수 있습니다.  
  
 **HTTP** 는 서비스 클래스입니다. 보고서 서버 웹 서비스는 HTTP.SYS에서 실행됩니다. HTTP용 SPN을 만들면 HTTP.SYS에서 실행되는 같은 컴퓨터에 있는 모든 웹 응용 프로그램(IIS에서 호스팅되는 응용 프로그램 포함)에 도메인 사용자 계정을 기반으로 하는 티켓이 부여됩니다. 이러한 서비스가 다른 계정에서 실행되면 인증 요청이 실패합니다. 이 문제를 방지하려면 같은 계정에서 실행되도록 모든 HTTP 응용 프로그램을 구성하거나 응용 프로그램마다 호스트 헤더를 만든 다음 호스트 헤더별로 SPN을 만드십시오. 호스트 헤더를 구성할 때는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성과 관계없이 DNS를 변경해야 합니다.  
  
 에 대 한 지정 하는 값 \< *computername*>, \< *domainname*>, 및 \< *포트*> 보고서 서버를 호스트 하는 컴퓨터의 고유 네트워크 주소를 식별 합니다. 이는 로컬 호스트 이름이거나 FQDN(정규화된 도메인 이름)일 수 있습니다. 한 도메인만 있고 포트 80을 사용 하는 경우 생략할 수 있습니다 \< *domainname*> 및 \< *포트*> 명령줄에서. \<*도메인 사용자 계정*>는 보고서 서버 서비스를 실행 하 고 있는 SPN을 등록 해야 하는 사용자 계정입니다.  
  
## <a name="register-an-spn-for-domain-user-account"></a>도메인 사용자 계정에 대한 SPN 등록  
  
#### <a name="to-register-an-spn-for-a-report-server-service-running-as-a-domain-user"></a>도메인 사용자로 실행 중인 보고서 서버 서비스에 대한 SPN을 등록하려면  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 설치하고 도메인 사용자 계정으로 실행되도록 보고서 서버 서비스를 구성합니다. 다음 단계를 완료해야 보고서 서버에 연결할 수 있습니다.  
  
2.  도메인 관리자로 도메인 컨트롤러에 로그온합니다.  
  
3.  명령 프롬프트 창을 엽니다.  
  
4.  다음 명령을 복사하되 자리 표시자 값은 사용자의 네트워크에 유효한 실제 값으로 대체합니다.  
  
    ```  
    Setspn -s http/<computer-name>.<domain-name>:<port> <domain-user-account>  
    ```  
  
     예를 들어 `Setspn -s http/MyReportServer.MyDomain.com:80 MyDomainUser`  
  
5.  명령을 실행합니다.  
  
6.  **RsReportServer.config** 파일을 열고 `<AuthenticationTypes>` 섹션을 찾습니다.  
  
7.  `<RSWindowsNegotiate/>` 를 이 섹션의 첫 번째 항목으로 추가하여 NTLM을 활성화합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [구성 서비스 계정 &#40; SSRS 구성 관리자 &#41;](http://msdn.microsoft.com/library/25000ad5-3f80-4210-8331-d4754dc217e0)   
 [보고서 서버 서비스 계정 &#40; 구성 합니다. SSRS 구성 관리자 &#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Reporting Services 기본 모드 보고서 서버를 관리 합니다.](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  
  
  
