---
title: 확장된 보호를 사용하여 데이터베이스 엔진에 연결 | Microsoft Docs
ms.custom: ''
ms.date: 05/21/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- spoofing attacks
- service binding
- luring attacks
- Schannel
- channel binding
- Extended Protection
ms.assetid: ecfd783e-7dbb-4a6c-b5ab-c6c27d5dd57f
author: VanMSFT
ms.author: vanto
manager: jroth
ms.openlocfilehash: 5fd3ec3c17e20980b695fbcdd2364e49065732e5
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66767942"
---
# <a name="connect-to-the-database-engine-using-extended-protection"></a>확장된 보호를 사용하여 데이터베이스 엔진에 연결
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 **버전부터는** 확장된 보호 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]가 지원됩니다. **인증에 대한 확장된 보호** 는 운영 체제에서 구현하는 네트워크 구성 요소의 기능입니다. **확장된 보호** 는 Windows 7 및 Windows Server 2008 R2에서 지원됩니다. **확장된 보호** 는 이전 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 운영 체제의 경우에는 서비스 팩에 포함되어 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 확장된 보호 **를 사용하여 연결하면**의 보안이 강화됩니다.  
  
> [!IMPORTANT]  
> Windows에서는 기본적으로 **확장된 보호** 를 사용할 수 없습니다. Windows에서 **확장된 보호** 를 사용하는 방법은 [인증에 대한 확장된 보호](/dotnet/framework/wcf/feature-details/extended-protection-for-authentication-overview)를 참조하십시오.
  
## <a name="description-of-extended-protection"></a>확장된 보호 설명  
 **확장된 보호** 는 서비스 바인딩 및 채널 바인딩을 사용하여 인증 릴레이 공격을 방지합니다. 인증 릴레이 공격에서는 NTLM 인증을 수행할 수 있는 클라이언트(예: Windows 탐색기, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Outlook, .NET SqlClient 애플리케이션 등)가 악의적인 CIFS 파일 서버 등의 공격자에 연결하면, 공격자가 클라이언트 자격 증명을 사용해 클라이언트로 가장하여 서비스(예: [!INCLUDE[ssDE](../../includes/ssde-md.md)] 서비스의 인스턴스)로 인증하게 됩니다.  
  
 이 공격에는 두 가지 변형이 있습니다.  
  
-   유인 공격에서는 클라이언트가 공격자에게 자발적으로 연결하도록 유인됩니다.  
  
-   스푸핑 공격에서는 클라이언트가 올바른 서비스에 연결하려고 하지만 DNS와 IP 라우팅 중 하나 또는 둘 모두가 공격자에 대한 연결로 리디렉션되도록 감염되어 있음을 알지 못합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 서비스 바인딩 및 채널 바인딩을 사용해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 이러한 공격을 줄이는 데 도움을 줍니다.  
  
### <a name="service-binding"></a>서비스 바인딩  
 서비스 바인딩은 클라이언트가 연결하려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스의 서명된 SPN(서비스 사용자 이름)을 보내야 하도록 함으로써 유인 공격을 해결합니다. 서비스는 인증 응답의 일부분으로 패킷에서 받은 SPN이 자체 SPN과 일치하는지 확인합니다. 클라이언트가 공격자에게 연결하도록 유인되는 경우에는 공격자의 서명된 SPN이 클라이언트에 포함됩니다. 이렇게 클라이언트가 공격자의 SPN을 포함하므로 공격자는 패킷을 릴레이해 실제 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 클라이언트로 인증할 수 없습니다. 서비스 바인딩은 한 번만 수행하면 되고 비용도 미미하지만 스푸핑 공격은 해결할 수 없습니다. 클라이언트 애플리케이션에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하는 데 암호화를 사용하지 않을 경우 서비스 바인딩이 수행됩니다.  
  
### <a name="channel-binding"></a>채널 바인딩  
 채널 바인딩에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 인스턴스와 클라이언트 간에 보안 채널(Schannel)을 설정합니다. 서비스는 해당 채널과 관련된 클라이언트의 CBT(채널 바인딩 토큰)를 자체 CBT와 비교하여 클라이언트의 신뢰성을 확인합니다. 채널 바인딩을 수행하면 유인 공격과 스푸핑 공격을 모두 해결할 수 있습니다. 그러나 모든 세션 트래픽에 대해 TLS(전송 계층 보안) 암호화를 수행해야 하므로 런타임 비용이 많이 듭니다. 클라이언트 애플리케이션에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하는 데 암호화를 사용하는 경우에는 암호화를 클라이언트에서 적용하는지 서버에서 적용하는지에 관계없이 채널 바인딩이 수행됩니다.  
  
> [!WARNING]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 공급자는 TLS 1.0 및 SSL 3.0을 지원합니다. 운영 체제 SChannel 계층을 변경하여 다른 프로토콜 (예: TLS 1.1 또는 TLS 1.2)를 적용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대한 연결이 실패할 수 있습니다.  
  
### <a name="operating-system-support"></a>운영 체제 지원  
 다음 링크에서는 Windows에서 **확장된 보호**를 지원하는 방법에 대해 자세히 설명합니다.  
  
-   [확장된 보호를 사용하는 Windows 통합 인증(Integrated Windows Authentication with Extended Protection)](https://msdn.microsoft.com/library/dd639324.aspx)  
  
-   [Microsoft 보안 공지(973811), 인증에 대한 확장된 보호.](/security-updates/SecurityAdvisories/2009/973811)
  
## <a name="settings"></a>설정  
 세 가지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 설정이 서비스 바인딩과 채널 바인딩에 영향을 줍니다. 이러한 설정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자 또는 WMI를 사용하여 구성할 수 있으며, 정책 기반 관리의 **서버 프로토콜 설정** 패싯을 사용해 볼 수 있습니다.  
  
-   **암호화 적용**  
  
     가능한 값은 **설정** 및 **해제**입니다. 채널 바인딩을 사용하려면 **암호화 적용** 을 **설정**으로 설정해야 하며, 그러면 모든 클라이언트에서 암호화가 적용됩니다. 값이 **해제**인 경우에는 서비스 바인딩만 보장됩니다. **암호화 적용** 은 **구성 관리자의** MSSQLSERVER 속성에 대한 프로토콜(플래그 탭) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 있습니다.  
  
-   **확장된 보호**  
  
     가능한 값은 **해제**, **허용**및 **필수**입니다. 사용자는 **확장된 보호** 변수를 사용하여 각 **인스턴스에 대한** 확장된 보호 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 수준을 구성할 수 있습니다. **확장된 보호** 는 **구성 관리자의** MSSQLSERVER 속성에 대한 프로토콜(고급 탭) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 있습니다.  
  
    -   **해제**로 설정하면 **확장된 보호** 를 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스는 클라이언트 보호 여부에 관계없이 모든 클라이언트로부터의 연결을 허용합니다. **해제** 는 패치되지 않은 이전 운영 체제와 호환되지만 안전성은 떨어집니다. 클라이언트 운영 체제에서 확장된 보호를 지원하지 않는 경우 이 설정을 사용하십시오.  
  
    -   **허용**으로 설정하면 **확장된 보호** 를 지원하는 운영 체제로부터의 연결에 대해 **확장된 보호**를 사용해야 합니다. **확장된 보호** 를 지원하지 않는 운영 체제로부터의 연결에 대해서는 **확장된 보호**가 무시됩니다. 보호된 클라이언트 운영 체제에서 실행되는 보호되지 않는 클라이언트 애플리케이션으로부터의 연결은 거부됩니다. 이 설정은 **해제**보다는 안전하지만 가장 안전한 설정은 아닙니다. **확장된 보호** 를 지원하는 운영 체제와 지원하지 않은 운영 체제가 혼합되어 있는 환경에서는 이 설정을 사용하십시오.  
  
    -   **필수**로 설정하면 보호된 운영 체제에서 실행되는 보호된 애플리케이션으로부터의 연결만 허용됩니다. 이 설정은 가장 안전하지만 **확장된 보호** 를 지원하지 않는 운영 체제 또는 애플리케이션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결할 수 없습니다.  
  
-   **허용되는 NTLM SPN**  
  
     **허용되는 NTLM SPN** 변수는 서버가 여러 SPN을 사용하는 경우 필요합니다. 클라이언트가 서버에서 사용하지 않는 유효한 SPN을 통해 서버에 연결하려고 시도하면 서비스 바인딩이 실패합니다. 이러한 문제를 방지하기 위해 사용자는 **허용되는 NTLM SPN**을 사용하여 서버를 표시하는 여러 SPN을 지정할 수 있습니다. **허용되는 NTLM SPN** 은 세미콜론으로 구분되는 일련의 SPN입니다. 예를 들어 **MSSQLSvc/ HostName1.Contoso.com** 및 **MSSQLSvc/ HostName2.Contoso.com**SPN을 허용하려면 **허용되는 NTLM SPN** 상자에 **MSSQLSvc/HostName1.Contoso.com;MSSQLSvc/HostName2.Contoso.com** 을 입력합니다. 변수의 최대 길이는 2,048자입니다. **허용되는 NTLM SPN** 은 **구성 관리자의** MSSQLSERVER 속성에 대한 프로토콜(고급 탭) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 있습니다.  
  
## <a name="enabling-extended-protection-for-the-database-engine"></a>데이터베이스 엔진에 대해 확장된 보호 사용  
 **확장된 보호**를 사용하려면 서버와 클라이언트 둘 다에 **확장된 보호**를 지원하는 운영 체제가 설치되어 있어야 하며, 이들 운영 체제에서 **확장된 보호** 를 사용하도록 설정해야 합니다. 운영 체제에 대해 **확장된 보호** 를 사용하도록 설정하는 방법에 대한 자세한 내용은 [인증에 대한 확장된 보호](/dotnet/framework/wcf/feature-details/extended-protection-for-authentication-overview)를 참조하십시오.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 **버전부터는** 확장된 보호 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]가 지원됩니다. 일부 이전 버전**에 대해서는 향후 업데이트에서** 확장된 보호 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 제공될 예정입니다. 서버 컴퓨터에서 **확장된 보호** 를 사용하도록 설정한 후에는 다음 단계를 수행하여 **확장된 보호**를 사용하도록 설정합니다.  
  
1.  **시작** 메뉴에서 **모든 프로그램**을 선택하고 **Microsoft SQL Server** 를 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다.  
  
2.  **SQL Server 네트워크 구성**을 확장한 다음, _\<_InstanceName *>* 에 대한 **프로토콜**을 마우스 오른쪽 단추로 클릭한 다음, **속성**을 클릭합니다.  
  
3.  채널 바인딩과 서비스 바인딩 둘 다에 대해 **고급** 탭에서 **확장된 보호** 를 적절한 설정으로 지정합니다.  
  
4.  서버가 여러 SPN을 사용하는 경우 필요하면 “설정” 섹션의 설명에 따라 **고급** 탭에서 **허용되는 NTLM SPN** 필드를 구성합니다.  
  
5.  채널 바인딩에 대해 **플래그** 탭에서 **암호화 적용** 을 **켜기**로 설정합니다.  
  
6.  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 서비스를 다시 시작합니다.  
  
## <a name="configuring-other-sql-server-components"></a>다른 SQL Server 구성 요소 구성  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 구성하는 방법은 [Reporting Services 인증에 대한 확장된 보호](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)를 참조하세요.  
  
 IIS를 사용하여 HTTP 또는 HTTPs 연결을 통해 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터에 액세스할 때 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 IIS에서 제공하는 확장된 보호 기능을 사용할 수 있습니다. IIS에서 확장된 보호를 사용하도록 구성하는 방법에 대한 자세한 내용은 [IIS 7.5에서 확장된 보호 구성](https://go.microsoft.com/fwlink/?LinkId=181105)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [서버 네트워크 구성](../../database-engine/configure-windows/server-network-configuration.md)   
 [클라이언트 네트워크 구성](../../database-engine/configure-windows/client-network-configuration.md)   
 [인증에 대한 확장된 보호 개요](https://go.microsoft.com/fwlink/?LinkID=177943)   
 [확장된 보호를 사용하는 Windows 통합 인증(영문)](https://go.microsoft.com/fwlink/?LinkId=179922)  
  
  
