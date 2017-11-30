---
title: "웹 포털에서 사용자 지정 인증 쿠키를 전달하도록 구성 | Microsoft Docs"
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
- authentication [Reporting Services]
- extensions [Reporting Services], custom security
ms.assetid: 91aeb053-149e-4562-ae4c-a688d0e1b2ba
caps.latest.revision: "18"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.openlocfilehash: 0f1131c191fa64c6dc6f2a074a9cd5db7a8b0e1b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="configure-the-web-portal-to-pass-custom-authentication-cookies"></a>웹 포털에서 사용자 지정 인증 쿠키를 전달하도록 구성

사용자 지정 인증 확장 프로그램을 사용하는 경우 웹 포털에서 사용자 지정 인증 쿠키를 전송하도록 구성해야 합니다. 그렇게 하지 않으면 웹 포털에서 HTTP 요청을 통해 보고서 서버 관련 쿠키만 전송합니다. 추가 쿠키를 전송하려면 RSReportServer.Config 파일을 수정해야 합니다.

## <a name="modifying-the-rsreportserverconfig-file"></a>RSReportServer.Config 파일 수정

RSReportServer.config 파일의 웹 포털 구성 설정에 \<**PassThroughCookies**> 요소를 추가하여 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]에서 추가 쿠키를 보고서 서버에 전송하도록 설정할 수 있습니다. 추가 쿠키 전송은 보고서 서버 인증 쿠키뿐만 아니라 타사 인증 시스템의 쿠키도 필요한 Single Sign-On 인증 솔루션에 유용합니다.

웹 포털 사용 시 HTTP 요청을 통해 추가 쿠키를 전송하려면 RSReportServer.config 파일에서 다음 요소를 설정합니다.
  
```  
<UI>  
   <CustomAuthenticationUI>  
      ...  
      <PassThroughCookies>  
         <PassThroughCookie>cookiename1</PassThroughCookie>  
         <PassThroughCookie>cookiename2</PassThroughCookie>  
      </PassThroughCookies>  
   </CustomAuthenticationUI>  
      ...  
</UI>  
```  
  
## <a name="see-also"></a>관련 항목:

[보고서 서버 인증](../../reporting-services/security/authentication-with-the-report-server.md)   
[RsReportServer.config 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[보안 확장 프로그램 개요](../../reporting-services/extensions/security-extension/security-extensions-overview.md)   
[보고서 서버 구성 및 관리&#40;SSRS 기본 모드&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
추가 질문이 있으신가요? [Reporting Services 포럼을 이용해 보세요.](http://go.microsoft.com/fwlink/?LinkId=620231)