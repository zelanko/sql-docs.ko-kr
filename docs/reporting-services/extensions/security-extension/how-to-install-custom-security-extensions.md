---
title: "사용자 지정 보안 확장 프로그램을 설치 하는 방법 | Microsoft Docs"
ms.custom: 
ms.date: 07/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: bfa0a35b-ccfb-4279-bae6-106c227c5f16
caps.latest.revision: 3
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 47182ebd082dfae0963d761e54c4045be927d627
ms.openlocfilehash: 58cfeef7d74e0641b965c307551f0fba4a7ff09c
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---

# <a name="how-to-install-custom-security-extensions"></a>사용자 지정 보안 확장 프로그램을 설치 하는 방법

[!INCLUDE[ssrs-appliesto](../../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../../includes/ssrs-appliesto-pbirs.md)]

Reporting Services 2016 새로운 Odata Api를 호스트 하 고도 모바일 보고서 및 KPI와 같은 새 보고서 작업 부하를 호스트 하기 위해 새 웹 포털을 도입 되었습니다. 이 새로운 포털 최신 기술에 의존 하며 별도의 프로세스로 실행 하 여 친숙 한 ReportingServicesService 으로부터 격리 됩니다. 이 프로세스는 호스팅되는 ASP.NET 응용 프로그램 아니며 따라서 기존 사용자 지정 보안 확장 프로그램을 가정을 중단 합니다. 또한 사용자 지정 보안 확장 프로그램에 대 한 현재 인터페이스 허용 안 함 전달 되도록 모든 외부 컨텍스트에 대해 구현자만 선택 전역 하는 잘 알려진 ASP.NET 개체를 검사 하는 그대로 두고이 필수 인터페이스를 변경 합니다.

## <a name="what-changed"></a>변경 기능

도입 된 새로운 인터페이스를 구현할 수 인증과 관련 된 결정을 내릴 수 확장에서 사용 하는 보다 일반적인 속성을 제공 하는 IRSRequestContext 제공 하는 합니다.

이전 버전에서는 보고서 관리자 프런트 엔드 이었으며 자체 사용자 지정 로그인 페이지를 구성할 수 있습니다. Reporting Services 2016에서 응용 프로그램에서 모두 인증 해야 및 reportserver에서 호스트 한 페이지만 지원 됩니다.

## <a name="implementation"></a>구현

이전 버전에서는 확장 일반적인 ASP.NET 개체를 즉시 사용할 수 있다고 가정에 의존 수 없습니다. 새 포털 ASP.NET에서 실행 되지 않으면, 이후 확장 개체가 NULL이 될 문제 였으며 수 있습니다.

가장 일반적인 예는 헤더 및 쿠키와 같은 요청 정보를 읽을 수는 HttpContext.Current에 액세스 하는 합니다. 확장 같은 결정을 할 수 있도록 포털에서 인증 될 때 호출 및 요청 정보를 제공 하는 확장에는 새로운 방법이 도입 되었습니다. 

확장에는 구현 하는 <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension2> 이 이용 하려면 인터페이스입니다. 확장의 두 버전을 구현 해야 합니다 <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension.GetUserInfo%2A> 메소드 reportserver 컨텍스트 및 웹 호스트 프로세스에 사용 된 기타 의해 호출 됩니다. 다음 예제는 reportserver 하 여 해결 하는 id가 사용 되는 포털에 대 한 간단한 구현 중 하나를 보여 줍니다.

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

사용자 지정 보안 확장 프로그램에 필요한 기본 구성으로 이전 릴리스와 동일 합니다. Web.config 및 rsreportserver.config에 대 한 변경이 필요한: 자세한 내용은 참조 [구성 사용자 지정 또는 보고서 서버에서 폼 인증](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)합니다.

더 이상 별도 보고서 관리자에 대 한 web.config를 포털 reportserver 끝점으로 동일한 설정을 상속 합니다.

## <a name="machine-keys"></a>컴퓨터 키

인증 쿠키의 암호를 해독 해야 하는 폼 인증의 경우 두 프로세스를 같은 컴퓨터 키 및 암호 해독 알고리즘을 사용 하 여 구성 해야 합니다. 이 이전에 설치 Reporting Services 확장 환경에서 작동 하도록 수 있었지만 이제는 단일 컴퓨터에 배포 하는 경우에 요구 사항이 사용자에 게 친숙 한 단계입니다.

인터넷 정보 서비스 관리자 (IIS)와 같은 키를 생성 하는 여러 가지 도구도 하면 배포에 대 한 유효성 검사 키 특정을 사용 하도록 합니다. 인터넷에서 다른 도구를 찾을 수 있습니다.

### <a name="sql-server-reporting-services-2017-and-later"></a>SQL Server Reporting Services 2017 이상

**\ReportServer\rsReportServer.config**

아래에서 추가 `<configuration>`합니다.

```
<machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

### <a name="sql-server-reporting-services-2016"></a>SQL Server Reporting Services 2016

**\ReportServer\web.config**

아래에서 추가 `<system.web>`합니다.
    
```
    <machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

**\RSWebApp\Microsoft.ReportingServices.Portal.WebHost.exe.config**

아래에서 추가 `<configuration>`합니다.

```
    <system.web>
        <machineKey validationKey=="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
    </system.web>
```

### <a name="power-bi-report-server"></a>Power BI 보고서 서버

이 현재 2017 년 6 월 (빌드 14.0.600.301) 릴리스에서 사용할 수 있습니다.

**\ReportServer\rsReportServer.config**

아래에서 추가 `<configuration>`합니다.

```
<machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

## <a name="configure-passthrough-cookies"></a>통과 쿠키를 구성 합니다.

새 포털 및 reportserver는 일부 작업 (이전 버전의 보고서 관리자와 유사)에 대 한 내부 soap Api를 사용 하 여 통신 합니다. 추가 쿠키는 포털에서 서버에 전달 해야 하는 경우에 PassThroughCookies 속성은 계속 사용할 수 있습니다. 자세한 내용은 참조 [사용자 지정 인증 쿠키를 전달 하려면 웹 포털 구성](../../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)합니다.

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
[사용자 지정 인증 쿠키를 전달 하도록 보고서 관리자 구성](https://msdn.microsoft.com/library/ms345241(v=sql.120).aspx)

문의: [Reporting Services 포럼에서 질문](http://go.microsoft.com/fwlink/?LinkId=620231)

