---
title: "Power BI Mobile access에 대 한 보고서 서버를 사용 하도록 설정 | Microsoft Docs"
ms.date: 12/17/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c1a71522-394b-46a7-b9ec-f964bdd81d82
caps.latest.revision: 7
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f9c4b3e4ce530f822f28e7a3db52e802c90d492a
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="enable-a-report-server-for-power-bi-mobile-access"></a>Power BI Mobile에 액세스할 수 있도록 보고서 서버 활성화
Power BI Mobile 앱을 사용하여 모바일 보고서를 사용할 수 있습니다. Power BI Mobile 앱을 Reporting Services에 연결하기 위해서는 몇 가지 구성 사항이 있습니다.  
  
-   [모바일 보고서에서는 Reporting Services 기본 모드가 필요합니다.](#nativemode)  
-   [Reporting Services에 대한 기본 인증 구성 사용](#basicauth) (CTP 3.2용)  
-   [클라이언트 장치를 위한 올바른 인증서 신뢰와 함께 HTTPS를 사용하는 것이 좋습니다.](#https)  
-   [방화벽 설정 검토](#firewall)  
  
<a name="nativemode"/>  
## <a name="reporting-services-native-mode-required"></a>Reporting Services 기본 모드 필수  
모바일 보고서는 기본 모드의 기능입니다. SharePoint 통합 모드에서는 사용할 수 없습니다. Power BI Mobile 앱은 기본 모드 인스턴스에서만 작동합니다.  
  
<a name="basicauth"/>  
## <a name="enable-basic-authentication"></a>기본 인증 사용  
iOS Power BI Mobile 앱에서는 기본 인증이 있어야 모바일 보고서를 연결 및 사용할 수 있습니다. Reporting Services는 기본적으로 활성화되는 기본 인증으로 구성되지 않습니다. 기본 인증 구성 방법에 대한 내용은 [보고서 서버에서 기본 인증 구성](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)을 참조하십시오.  
  
또한, Windows 인증을 활성화하여 게시자 앱이 모바일 보고서를 게시할 수 있도록 허용해야 합니다.  
  
<a name="https"/>  
## <a name="enable-https"></a>HTTPS 사용  
기본 인증을 사용하는 경우 Reporting Services에서 HTTPS를 사용하는 것이 좋습니다. HTTPS를 활성화한 경우 사용된 인증서가 iOS Power BI Mobile 앱을 실행하는 클라이언트 장치에서 신뢰할 수 있는지 확인하십시오. 이것은 인증 체인이 유효해야 하고 클라이언트 장치에서 사용할 수 있어야 함을 의미합니다.  
  
개발 또는 평가 목적으로 자체 서명 인증서를 사용해야 하는 경우 보고서 서버에서 인증서를 내보낸 후 모바일 장치에 설치할 수 있습니다. 해당 장치에 설치하는 방법은 장치 문서를 참조하십시오.  
  
SSL 사용에 대한 자세한 내용은 [기본 모드 보고서 서버에서 SSL 연결 구성](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)을 참조하십시오.  
  
<a name="firewall"/>  
## <a name="review-firewall-settings"></a>방화벽 설정 검토  
방화벽 설정을 검토하여 모든 장치를 Reporting Services에 성공적으로 연결할 수 있는지 확인하는 것이 좋습니다.   
  
Windows 방화벽 구성 방법에 대한 자세한 내용은 [보고서 서버에 액세스할 수 있도록 방화벽 구성](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
  
[보고서 서버에서 기본 인증 구성](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)  
[기본 모드 보고서 서버에서 SSL 연결 구성](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)  
[보고서 서버에 액세스할 수 있도록 방화벽 구성](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)  
  
  
  
  
  
  


