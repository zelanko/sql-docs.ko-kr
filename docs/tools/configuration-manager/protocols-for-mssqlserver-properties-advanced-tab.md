---
title: MSSQLSERVER 속성에 대한 프로토콜(고급 탭) | Microsoft Docs
ms.custom: ''
ms.date: 01/24/2019
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: abd5ca68-825f-4c07-b27c-3b3a79d03d74
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: bc5ee796addb8c77170de2e3166aefb74d046ad1
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55044619"
---
# <a name="protocols-for-mssqlserver-properties-advanced-tab"></a>MSSQLSERVER 속성에 대한 프로토콜(고급 탭)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**MSSQLSERVER에 대한 프로토콜 속성** 대화 상자의 **고급** 탭을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 대해 **인증에 대한 확장된 보호** 를 구성할 수 있습니다. **확장된 보호** 는 운영 체제에서 구현하는 네트워크 구성 요소의 기능입니다. **확장된 보호** 는 Windows 7 및 Windows Server 2008 R2에서 사용할 수 있으며 이전 운영 체제의 경우에는 서비스 팩에 포함되어 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 확장된 보호 **를 사용하여 연결하면**의 보안이 강화됩니다. **확장된 보호** 기능의 이점을 활용하려면 **플래그** 탭에서 **암호화 적용** 을 선택해야 합니다.

> [!IMPORTANT]  
> Windows에서는 기본적으로 **확장된 보호** 를 사용할 수 없습니다. 사용 하도록 설정 하는 방법에 대 한 자세한 **확장 된 보호**, 다음을 참조 하세요.
> - [Windows 확장 된 보호 \<extendedProtection\>](https://docs.microsoft.com/iis/configuration/system.webserver/security/authentication/windowsauthentication/extendedprotection/)
> - [인증에 대한 확장된 보호 개요](https://docs.microsoft.com/dotnet/framework/wcf/feature-details/extended-protection-for-authentication-overview)

기타 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 구성하는 방법과 **확장된 보호**에 대한 전체 설명을 보려면 [Microsoft.com](https://go.microsoft.com/fwlink/?LinkId=177752)의 최신 정보를 참조하십시오.

**확장된 보호** 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client( [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]이상)를 통해 완벽하게 지원됩니다. 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개의 클라이언트 제공 업체를위한 **개의 확장 된 보호** 에 대한 지원은 현재 지원되지 않습니다.

## <a name="options"></a>옵션

### <a name="extended-protection"></a>버전부터는

세 가지 값을 사용할 수 있습니다.  

- **Off**: 의미 **확장 된 보호** 을 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스는 클라이언트 보호 여부에 관계없이 모든 클라이언트로부터의 연결을 허용합니다. **해제** 는 패치되지 않은 이전 운영 체제와 호환되지만 안전성은 떨어집니다. 클라이언트 운영 체제에서 확장된 보호를 지원하지 않는 경우에만 이 설정을 사용하십시오.

- **허용됨**: **확장된 보호**를 지원하는 운영 체제로부터의 연결에 대해 **확장된 보호**를 사용해야 합니다. 보호된 클라이언트 운영 체제에서 실행되는 보호되지 않는 클라이언트 애플리케이션으로부터의 연결은 거부됩니다. 보호되지 않는 운영 체제로부터의 연결에 대한**확장된 보호** 는 무시됩니다. 이 설정은 **해제**보다는 안전하지만 가장 안전한 설정은 아닙니다. **확장된 보호** 를 지원하는 운영 체제 또는 애플리케이션과 지원하지 않은 운영 체제 또는 애플리케이션이 혼합되어 있는 환경에서는 이 설정을 사용하십시오.

- **필요한**:는 허용할 연결의 경우에 야 보호 된 응용 프로그램에서 보호 된 운영 체제를 의미 합니다. 이 설정은 세 가지 옵션 중 가장 안전 합니다. 하지만 운영 체제를 지원 하지 않는 **확장 된 보호** 에 연결할 수 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.

### <a name="accepted-ntlm-spns"></a>허용되는 NTLM SPN

인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 둘 이상의 NTLM SPN (서비스 주체 이름)으로 식별할 수 있습니다. 세미콜론으로 구분 된 문자열의 일련의 Spn을 나열 합니다. 예를 들어 **MSSQLSvc/HostName1.Contoso.com;MSSQLSvc/HostName2.Contoso.com**값은 클라이언트가 이름이 **MSSQLSvc/HOST1.Contoso.com** 또는 **MSSQLSvc/HOST2.Contoso.com**인 SPN에 연결할 수 있음을 나타냅니다. 변수의 최대 길이는 2048자입니다.

## <a name="see-also"></a>참고 항목

[Reporting Services 인증에 대한 확장된 보호](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)

