---
title: "사용자 지정 인증 쿠키를 전달 하려면 웹 포털 구성 | Microsoft Docs"
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
caps.latest.revision: 18
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 0f1131c191fa64c6dc6f2a074a9cd5db7a8b0e1b
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="configure-the-web-portal-to-pass-custom-authentication-cookies"></a>웹 포털에서 사용자 지정 인증 쿠키를 전달하도록 구성

사용자 지정 인증 확장 프로그램을 사용 하는 경우 사용자 지정 인증 쿠키를 전송 하려면 웹 포털을 구성 해야 합니다. 그렇지 않으면 웹 포털에서 보고서 서버에 특정 HTTP 요청을 통해 쿠키만 전송 합니다. 추가 쿠키를 전송하려면 RSReportServer.Config 파일을 수정해야 합니다.

## <a name="modifying-the-rsreportserverconfig-file"></a>RSReportServer.Config 파일 수정

사용 하도록 설정할 수는 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 추가 하 여 보고서 서버를 통해 추가 쿠키를 전송 하는 \< **PassThroughCookies**> 요소는 RSReportServer.config 파일의 웹 포털 구성 설정입니다. 추가 쿠키 전송은 보고서 서버 인증 쿠키뿐만 아니라 타사 인증 시스템의 쿠키도 필요한 Single Sign-On 인증 솔루션에 유용합니다.

웹 포털을 사용 하는 경우 HTTP 요청을 통해 전송 될 추가 쿠키를 사용 하도록 설정 하려면 RSReportServer.config 파일에 다음 요소를 설정 합니다.
  
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
[구성 및 보고서 서버 &#40; 관리 SSRS 기본 모드 &#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
문의: [Reporting Services 포럼을 시도 하십시오.](http://go.microsoft.com/fwlink/?LinkId=620231)
