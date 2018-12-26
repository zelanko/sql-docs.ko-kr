---
title: 보안 확장 프로그램 개요(SSRS) | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- security [Reporting Services], extensions
ms.assetid: 24ccd795-6506-457c-93ac-6a9dd6bb9a46
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b6ed33ec1aac9b875a4c26b3aa3b209faf118267
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47636671"
---
# <a name="security-extensions-overview---reporting-services-ssrs"></a>보안 확장 프로그램 개요 - Reporting Services(SSRS)
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 보안 확장 프로그램은 사용자 또는 그룹에 대한 인증 및 권한 부여를 제공합니다. 즉, 여러 사용자들이 보고서 서버에 로그온한 다음 각자의 ID에 준하여 서로 다른 태스크나 작업을 수행할 수 있습니다. 기본적으로 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]는 Windows 계정 프로토콜을 사용하여 시스템에 계정을 보유하고 있다고 주장하는 사용자의 신원을 확인하는 방식의 Windows 기반 인증 확장 프로그램을 사용합니다. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]는 역할 기반 보안 시스템을 사용하여 사용자에게 권한을 부여합니다. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 역할 기반 보안 모델은 다른 기술의 역할 기반 보안 모델과 비슷합니다.  
  
 보안 확장 프로그램은 확장 가능한 개방형 API를 기반으로 하므로 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서 새 인증 및 권한 부여 확장 프로그램을 만들 수 있습니다. 다음은 Forms 기반 인증 및 권한 부여를 사용하는 일반적인 보안 확장 구현의 예입니다.  
  
 ![Reporting Services 보안 확장 프로세스](../../../reporting-services/extensions/security-extension/media/rosettasecurityextensionflow.gif "Reporting Services 보안 확장 프로세스")  
  
 그림에서 볼 수 있듯이 인증 및 권한 부여는 다음과 같이 발생합니다.  
  
1.  사용자가 URL을 사용하여 웹 포털에 액세스하려고 하자 클라이언트 애플리케이션에 대한 사용자 자격 증명을 수집하는 폼으로 리디렉션됩니다.  
  
2.  사용자가 폼에 자격 증명을 제출합니다.  
  
3.  사용자 자격 증명이 <xref:ReportService2010.ReportingService2010.LogonUser%2A> 메서드를 통해 Reporting Services 웹 서비스로 제출됩니다.  
  
4.  웹 서비스에서 고객이 제공한 보안 확장 프로그램을 호출하고 사용자 이름과 암호가 사용자 지정 보안 기관에 존재하는지 확인합니다.  
  
5.  인증 후 웹 서비스가 인증 티켓(일명 "쿠키")을 만들고, 티켓을 관리하고, 웹 포털의 홈 페이지에 대해 사용자의 역할을 검증합니다.  
  
6.  웹 서비스가 브라우저로 쿠키를 반환하고 웹 포털에 적절한 사용자 인터페이스를 표시합니다.  
  
7.  사용자가 인증된 후 브라우저에서 HTTP 헤더에 쿠키를 전송하는 동안 웹 포털에 요청을 합니다. 이 요청은 웹 포털 내에서 사용자 동작에 응답하여 이루어진 것입니다.  
  
8.  요청된 사용자 작업과 함께 웹 서비스로 쿠키가 HTTP 헤더에 전송됩니다.  
  
9. 쿠키가 검증되고 유효한 경우, 보고서 서버가 보고서 서버 데이터베이스에서 보안 설명자 및 기타 요청된 작업과 관련한 정보를 반환합니다.  
  
10. 쿠키가 유효한 경우 보고서 서버가 보안 확장 프로그램을 호출하여 사용자에게 특정 작업을 수행할 권한이 부여되었는지 확인합니다.  
  
11. 사용자에게 권한이 부여된 경우 보고서 서버가 요청된 작업을 수행하고 호출자에게 제어를 반환합니다.  
  
12. 사용자가 인증된 후 보고서 서버에 대한 URL 액세스에서 같은 쿠키를 사용합니다. 쿠키가 HTTP 헤더에 전송됩니다.  
  
13. 세션이 종료될 때까지 사용자가 계속해서 보고서 서버에 작업을 요청합니다.  
  
## <a name="when-to-implement-a-security-extension"></a>보안 확장 프로그램 구현 시기  
 가능하면 Windows 인증을 사용하는 것이 좋습니다. 그러나 다음 두 가지 경우에는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에 사용자 지정 인증 및 권한 부여가 적합할 수 있습니다.  
  
-   인터넷 또는 엑스트라넷 애플리케이션에서 Windows 계정을 사용할 수 없는 경우  
  
-   사용자가 정의한 사용자 및 역할이 있고 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서 대응하는 권한 부여 체계를 제공해야 하는 경우  
  
## <a name="see-also"></a>참고 항목  
 [보안 확장 프로그램 구현](../../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)   
  
  
