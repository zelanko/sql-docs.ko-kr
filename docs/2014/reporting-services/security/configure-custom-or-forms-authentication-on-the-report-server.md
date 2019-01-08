---
title: 보고서 서버에서 사용자 지정 또는 폼 인증 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Forms authentication, configuring
- custom authentication [Reporting Services]
ms.assetid: e8601a8f-e66d-4649-8e4d-a46ca20ec7d0
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 591fc282f6e60f97d4b900e3b88f727d554535e9
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53366105"
---
# <a name="configure-custom-or-forms-authentication-on-the-report-server"></a>보고서 서버에서 사용자 지정 또는 폼 인증 구성
  Reporting Services에서는 사용자 지정 또는 폼 기반 인증 모듈을 추가할 수 있는 확장 가능한 아키텍처를 제공합니다. 배포 요구 사항에 Windows 통합 보안이나 기본 인증이 포함되지 않은 경우 사용자 지정 인증 확장 프로그램을 구현할 수 있습니다. 사용자 지정 인증을 사용하는 가장 일반적인 시나리오는 웹 애플리케이션에 대한 인터넷 또는 엑스트라넷 액세스를 지원하려는 경우입니다. 기본 Windows 인증 확장 프로그램을 사용자 지정 인증 확장 프로그램으로 바꾸면 외부 사용자에게 보고서 서버에 대한 액세스 권한을 부여하는 방법을 보다 자세히 제어할 수 있습니다.  
  
 실제로 사용자 지정 인증 확장 프로그램을 배포하려면 어셈블리 및 애플리케이션 파일 복사, 구성 파일 수정 및 테스트 등의 여러 단계를 거쳐야 합니다. 이 항목에서는 구성 파일에 지정하는 인증 설정에만 초점을 맞춥니다.  
  
> [!NOTE]  
>  사용자 지정 인증 확장 프로그램을 만들려면 사용자 지정 코드와 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 보안 관련 지식이 필요합니다. 사용자 지정 인증 확장 프로그램을 만들지 않으려는 경우 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory 그룹 및 계정을 사용할 수 있지만, 이렇게 하려면 보고서 서버 배포 범위를 대폭 줄여야 합니다. 사용자 지정 인증에 대한 자세한 내용은 [Implementing a Security Extension](../extensions/security-extension/implementing-a-security-extension.md)을 참조하십시오.  
  
 또한 SharePoint 제품과 통합된 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 환경에서 폼 인증이나 사용자 지정 인증 확장 프로그램을 사용하려는 경우에는 SharePoint 사이트에서 해당 인증 방법을 사용하도록 구성해야 합니다. SharePoint에서 인증을 구성하는 방법은 MSDN( [Developer Network)에서](https://go.microsoft.com/fwlink/?LinkId=115575) 인증 예제 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 를 참조하세요.  
  
### <a name="to-configure-a-report-server-to-use-custom-authentication"></a>사용자 지정 인증을 사용하도록 보고서 서버를 구성하려면  
  
1.  텍스트 편집기에서 RSReportServer.config를 엽니다.  
  
2.  <`Authentication`>을(를) 찾습니다.  
  
3.  다음 XML 구조를 복사합니다.  
  
    ```  
    <Authentication>  
          <AuthenticationTypes>  
                 <Custom />  
          </AuthenticationTypes>  
          <EnableAuthPersistence>true</EnableAuthPersistence>  
    </Authentication>  
    ```  
  
4.  <`Authentication`>의 기존 항목을 선택하고 붙여넣어 덮어씁니다.  
  
     `Custom`은 다른 인증 유형과 함께 사용할 수 없습니다.  
  
5.  파일을 저장합니다.  
  
6.  보고서 서버의 Web.config 파일을 엽니다. 기본적으로 이 파일은 \Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\ReportServer에 있습니다.  
  
7.  `authentication mode`를 찾아 `Forms`로 설정합니다.  
  
    ```  
    <authentication mode = "Forms" />  
    ```  
  
8.  `identity impersonate`를 찾아 `False`로 설정합니다.  
  
    ```  
    <identity impersonate = "false" />  
    ```  
  
9. 보고서 관리자의 Web.config 파일을 엽니다. 기본적으로 이 파일은 \Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\ReportManager에 있습니다.  
  
10. `authentication mode`를 찾아 `Forms`로 설정합니다.  
  
    ```  
    <authentication mode = "Forms" />  
    ```  
  
11. `identity impersonate`를 찾아 `False`로 설정합니다.  
  
    ```  
    <identity impersonate = "false" />  
    ```  
  
12. 구성 파일에 `PassThroughCookies` 요소 구조를 추가합니다. 자세한 내용은 [보고서 관리자에서 사용자 지정 인증 쿠키를 전달하도록 구성](configure-the-web-portal-to-pass-custom-authentication-cookies.md)을 참조하세요.  
  
13. 파일을 저장합니다.  
  
14. 스케일 아웃 배포를 구성한 경우 배포의 다른 보고서 서버에서 위의 모든 단계를 반복합니다.  
  
15. 보고서 서버를 다시 시작하여 현재 열려 있는 모든 세션을 지웁니다.  
  
## <a name="see-also"></a>관련 항목  
 [보안 확장 프로그램 구현](../extensions/security-extension/implementing-a-security-extension.md)   
 [보고서 서버 인증](authentication-with-the-report-server.md)   
 [RSReportServer 구성 파일](../report-server/rsreportserver-config-configuration-file.md)   
 [보고서 서버의 기본 인증 구성](configure-basic-authentication-on-the-report-server.md)   
 [보고서 서버의 Windows 인증 구성](configure-windows-authentication-on-the-report-server.md)  
  
  
