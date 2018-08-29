---
title: 사용자 지정 보안 확장 프로그램 설치 방법 | Microsoft Docs
ms.custom: ''
ms.date: 07/10/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: extensions
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: bfa0a35b-ccfb-4279-bae6-106c227c5f16
caps.latest.revision: 3
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: a830d8fe28aec04b5c0ded2e382e41db535fd0e2
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40410497"
---
# <a name="how-to-install-custom-security-extensions"></a>사용자 지정 보안 확장 프로그램 설치 방법

[!INCLUDE[ssrs-appliesto](../../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../../includes/ssrs-appliesto-pbirs.md)]

Reporting Services 2016은 새로운 Odata API를 호스트하고 모바일 보고서 및 KPI와 같은 새 보고서 작업 부하를 호스트하기 위해 새 웹 포털을 도입하였습니다. 이 새로운 포털은 최신 기술을 사용하며, 별도의 프로세스로 실행하여 친숙한 ReportingServicesService로부터 격리됩니다. 이 프로세스는 ASP.NET 호스팅 응용 프로그램이 아니므로 기존 사용자 지정 보안 확장 프로그램에서의 가정을 중단합니다. 또한 사용자 지정 보안 확장 프로그램에 대한 현재 인터페이스는 외부 컨텍스트가 전달되는 것을 허용하지 않아 구현자는 잘 알려진 전역 ASP.NET 개체를 검사해야만 하며, 이를 위해 인터페이스를 일부 변경해야 합니다.

## <a name="what-changed"></a>변경된 것은?

인증과 관련된 의사 결정을 위해 확장 프로그램에서 사용되는 더 많은 공용 속성을 포함한 IRSRequestContext를 제공하는 구현 가능한 새 인터페이스가 도입되었습니다.

이전 버전에서 보고서 관리자는 프런트 엔드이며 자체 사용자 지정 로그인 페이지로 구성될 수 있습니다. Reporting Services 2016에서는 reportserver에서 호스트되는 한 페이지만 지원되며 두 응용 프로그램을 모두 인증해야 합니다.

## <a name="implementation"></a>구현

이전 버전에서 확장 프로그램은 ASP.NET 개체를 쉽게 사용할 수 있는 공용 가정을 사용합니다. 새 포털은 ASP.NET에서 실행되지 않으므로, 확장 프로그램에서 개체가 NULL이 되는 문제가 발생할 수 있습니다.

가장 일반적인 예는 헤더 및 쿠키와 같은 요청 정보를 읽는 HttpContext.Current에 액세스하는 것입니다. 확장 프로그램이 동일한 의사 결정을 하도록 허용하기 위해 요청 정보를 제공하고 포털에서 인증할 때 호출되는 새로운 방법을 확장 프로그램에 도입했습니다. 

확장 프로그램은 이를 이용하기 위해 <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension2> 인터페이스를 구현해야 합니다. 확장 프로그램은 reportserver 컨텍스트에서 호출되고 웹 호스트 프로세스에서 사용되는 것처럼 <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension.GetUserInfo%2A> 메서드의 두 버전을 모두 구현해야 합니다. 아래 샘플에 reportserver로 해결된 ID가 사용되는 포털의 간단한 구현 중 하나가 나와 있습니다.

``` 
public void GetUserInfo(IRSRequestContext requestContext, out IIdentity userIdentity, out IntPtr userId)
{
    userIdentity = null;
    if (requestContext.User != null)
    {
        userIdentity = requestContext.User;
    }

    // initialize a pointer to the current user id to zero
    userId = IntPtr.Zero;
}
```

## <a name="deployment-and-configuration"></a>배포 및 구성

사용자 지정 보안 확장 프로그램에 필요한 기본 구성은 이전 릴리스와 동일합니다. web.config 및 rsreportserver.config에 대한 변경이 필요합니다. 자세한 내용은 [보고서 서버에서 사용자 지정 또는 폼 인증 구성](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)을 참조하세요.

보고서 관리자에 대한 별도의 web.config는 없어지고, 포털은 reportserver 엔드포인트와 동일한 설정을 상속하게 됩니다.

## <a name="machine-keys"></a>컴퓨터 키

인증 쿠키의 암호를 해독해야 하는 폼 인증의 경우 두 프로세스 모두 같은 컴퓨터 키 및 암호 해독 알고리즘을 사용하여 구성해야 합니다. 이는 이전에 설치한 Reporting Services를 스케일 아웃 환경에서 작동한 사용자에게 익숙한 단계였으나, 이제는 단일 컴퓨터에 배포하는 경우에도 필요한 단계입니다.

배포에 대해 특정한 유효성 검사 키를 사용해야 합니다. IIS(인터넷 정보 서비스) 관리자와 같은 키를 생성하는 여러 가지 도구가 있습니다. 다른 도구는 인터넷에서 찾을 수 있습니다.

### <a name="sql-server-reporting-services-2017-and-later"></a>SQL Server Reporting Services 2017 이상

**\ReportServer\rsReportServer.config**

`<configuration>` 아래에 추가합니다.

```
<machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

### <a name="sql-server-reporting-services-2016"></a>SQL Server Reporting Services 2016

**\ReportServer\web.config**

`<system.web>` 아래에 추가합니다.
    
```
    <machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

**\RSWebApp\Microsoft.ReportingServices.Portal.WebHost.exe.config**

`<configuration>` 아래에 추가합니다.

```
    <system.web>
        <machineKey validationKey=="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
    </system.web>
```

### <a name="power-bi-report-server"></a>Power BI 보고서 서버

현재 2017년 6월(빌드 14.0.600.301) 릴리스부터 사용할 수 있습니다.

**\ReportServer\rsReportServer.config**

`<configuration>` 아래에 추가합니다.

```
<machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

## <a name="configure-passthrough-cookies"></a>통과 쿠키 구성

새 포털과 reportserver는 일부 작업에 대해 내부 soap API를 사용하여 통신합니다(이전 버전의 보고서 관리자와 유사). 추가 쿠키를 포털에서 서버로 전달해야 하는 경우 PassThroughCookies 속성을 계속 사용할 수 있습니다. 자세한 내용은 [웹 포털에서 사용자 지정 인증 쿠키를 전달하도록 구성](../../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)을 참조하세요.

```
<UI>
   <CustomAuthenticationUI>
      <PassThroughCookies>
         <PassThroughCookie>sqlAuthCookie</PassThroughCookie>
      </PassThroughCookies>
   </CustomAuthenticationUI>
</UI>
```

## <a name="next-steps"></a>다음 단계

[보고서 서버에서 사용자 지정 또는 폼 인증 구성](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)  
[보고서 관리자에서 사용자 지정 인증 쿠키를 전달하도록 구성](../../security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
