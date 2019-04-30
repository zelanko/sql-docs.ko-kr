---
title: 사용자 지정 인증 쿠키를 전달 하도록 보고서 관리자 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- authentication [Reporting Services]
- extensions [Reporting Services], custom security
ms.assetid: 91aeb053-149e-4562-ae4c-a688d0e1b2ba
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bff2f31eb321a24c184580a6b1565f4dbc76bb1d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242524"
---
# <a name="configure-report-manager-to-pass-custom-authentication-cookies"></a>보고서 관리자에서 사용자 지정 인증 쿠키를 전달하도록 구성
  사용자 지정 인증 확장 프로그램을 사용하는 경우 보고서 관리자에서 사용자 지정 인증 쿠키를 전송하도록 구성해야 합니다. 그렇게 하지 않으면 보고서 관리자에서 HTTP 요청을 통해 보고서 서버 관련 쿠키만 전송합니다. 추가 쿠키를 전송하려면 RSReportServer.Config 파일을 수정해야 합니다.  
  
## <a name="modifying-the-rsreportserverconfig-file"></a>RSReportServer.Config 파일 수정  
 보고서 관리자를 추가 하 여 보고서 서버를 통해 추가 쿠키를 전송 하도록 설정할 수 있습니다.를 <`PassThroughCookies`> 요소는 RSReportServer.config 파일에 보고서 관리자 구성 설정입니다. 추가 쿠키 전송은 보고서 서버 인증 쿠키뿐만 아니라 타사 인증 시스템의 쿠키도 필요한 Single Sign-On 인증 솔루션에 유용합니다.  
  
 보고서 관리자 사용 시 HTTP 요청을 통해 추가 쿠키를 전송하려면 RSReportServer.config 파일에서 다음 요소를 설정합니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [보고서 서버 인증](authentication-with-the-report-server.md)   
 [RSReportServer 구성 파일](../report-server/rsreportserver-config-configuration-file.md)   
 [보안 확장 프로그램 개요](../extensions/security-extension/security-extensions-overview.md)   
 [보고서 서버 구성 및 관리&#40;SSRS 기본 모드&#41;](../report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
  
  
