---
title: "보고서 서버에서 사용자 지정 또는 폼 인증 구성 | Microsoft Docs"
ms.custom: 
ms.date: 04/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Forms authentication, configuring
- custom authentication [Reporting Services]
ms.assetid: e8601a8f-e66d-4649-8e4d-a46ca20ec7d0
caps.latest.revision: 20
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 325b7d6f1015b6e5e81565df37d1c02d20e5802f
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="configure-custom-or-forms-authentication-on-the-report-server"></a>보고서 서버에서 사용자 지정 또는 폼 인증 구성

Reporting Services에서는 사용자 지정 또는 폼 기반 인증 모듈을 추가할 수 있는 확장 가능한 아키텍처를 제공합니다. 배포 요구 사항에 Windows 통합 보안이나 기본 인증이 포함되지 않은 경우 사용자 지정 인증 확장 프로그램을 구현할 수 있습니다. 사용자 지정 인증을 사용하는 가장 일반적인 시나리오는 웹 응용 프로그램에 대한 인터넷 또는 엑스트라넷 액세스를 지원하려는 경우입니다. 기본 Windows 인증 확장 프로그램을 사용자 지정 인증 확장 프로그램으로 바꾸면 외부 사용자에게 보고서 서버에 대한 액세스 권한을 부여하는 방법을 보다 자세히 제어할 수 있습니다.  

실제로 사용자 지정 인증 확장 프로그램을 배포하려면 어셈블리 및 응용 프로그램 파일 복사, 구성 파일 수정 및 테스트 등의 여러 단계를 거쳐야 합니다. 이 항목에서는 구성 파일에 지정하는 인증 설정에만 초점을 맞춥니다.  

> [!NOTE]
>  사용자 지정 인증 확장 프로그램을 만들려면 사용자 지정 코드와 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 보안 관련 지식이 필요합니다. 사용자 지정 인증 확장 프로그램을 만들지 않으려는 경우 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory 그룹 및 계정을 사용할 수 있지만, 이렇게 하려면 보고서 서버 배포 범위를 대폭 줄여야 합니다. 사용자 지정 인증에 대한 자세한 내용은 [Implementing a Security Extension](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)을 참조하십시오.

또한 SharePoint 제품과 통합 되는 SQL Server Reporting Services 환경에서 폼 인증이 나 사용자 지정 인증 확장 프로그램을 사용 하려는 경우 선택 하는 인증 방법을 사용 하려면 SharePoint 사이트를 구성 해야 합니다. SharePoint에서 인증을 구성하는 방법은 MSDN( [Developer Network)에서](http://go.microsoft.com/fwlink/?LinkId=115575) 인증 예제 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 를 참조하세요.



### <a name="to-configure-a-report-server-to-use-custom-authentication"></a>사용자 지정 인증을 사용하도록 보고서 서버를 구성하려면

1.  텍스트 편집기에서 RSReportServer.config를 엽니다.

2.  찾을 \< **인증**> 합니다.

3.  다음 XML 구조를 복사합니다.

    ```
    <Authentication>
          <AuthenticationTypes>
                 <Custom />
          </AuthenticationTypes>
          <EnableAuthPersistence>true</EnableAuthPersistence>
    </Authentication>
    ```

4.  에 대 한 기존 항목에 붙여넣습니다 \< **인증**> 합니다.

     **Custom** 은 다른 인증 유형과 함께 사용할 수 없습니다.

5.  파일을 저장합니다.

6.  보고서 서버의 Web.config 파일을 엽니다. 기본적으로 이 파일은 \Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\ReportServer에 있습니다.

7.  **authentication mode** 를 찾아 **Forms**로 설정합니다.

    ```
    <authentication mode = "Forms" />
    ```

8.  **identity impersonate** 를 찾아 **False**로 설정합니다.

    ```
    <identity impersonate = "false" />  
    ```
9. 구성 파일에 **PassThroughCookies** 요소 구조를 추가합니다. 자세한 내용은 참조 [사용자 지정 인증 쿠키를 전달 하려면 웹 포털 구성](../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)
  
10. 파일을 저장합니다.  
  
11. 확장 배포를 구성한 경우 배포의 다른 보고서 서버에서 위의 모든 단계를 반복합니다.  
  
12. 보고서 서버를 다시 시작하여 현재 열려 있는 모든 세션을 지웁니다.  

## <a name="see-also"></a>관련 항목:

[보안 확장 프로그램 구현](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)  
[Reporting Services 사용자 지정 보안 예제 (GitHub)](https://github.com/Microsoft/Reporting-Services/tree/master/CustomSecuritySample)  
[보고서 서버 인증](../../reporting-services/security/authentication-with-the-report-server.md)   
[RsReportServer.config 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[보고서 서버의 기본 인증 구성](../../reporting-services/security/configure-basic-authentication-on-the-report-server.md)   
[보고서 서버에서 Windows 인증을 구성 합니다.](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)  
문의: [Reporting Services 포럼을 시도 하십시오.](http://go.microsoft.com/fwlink/?LinkId=620231)
