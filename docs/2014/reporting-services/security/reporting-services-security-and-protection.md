---
title: Reporting Services 보안 및 보호 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- security [Reporting Services]
- Reporting Services, security
ms.assetid: 270075c5-bf12-4467-a775-abbda3d954a5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ca88c252e37362f2a5b64bb8d41ebac27f0e24dd
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59943139"
---
# <a name="reporting-services-security-and-protection"></a>Reporting Services 보안 및 보호
  이 섹션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 보안 기능에 대해 설명합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 지원되는 권한 부여 모델 및 인증 공급자에 대해서도 설명합니다.  
  
## <a name="extended-protection-for-authentication"></a>인증에 대한 확장된 보호  
 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]부터는 인증에 대한 확장된 보호가 지원됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능은 채널 바인딩 및 서비스 바인딩을 사용해 인증 보호를 향상시킬 수 있도록 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능은 확장된 보호를 지원하는 운영 체제에서 사용해야 합니다. 자세한 내용은 [Extended Protection for Authentication with Reporting Services](extended-protection-for-authentication-with-reporting-services.md)을(를) 참조하세요.  
  
## <a name="authentication-and-authorization"></a>인증 및 권한 부여  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 보고서 서버에 대해 사용자 및 클라이언트 애플리케이션에 부여할 다양한 인증 유형을 제공합니다. 보고서 서버에 맞는 인증 유형을 사용하면 조직에서 요구되는 적합한 수준의 보안을 확보할 수 있습니다. 자세한 내용은 [Authentication with the Report Server](authentication-with-the-report-server.md)을(를) 참조하세요.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 또한 역할 및 권한을 이용하여 보고서 서버 카탈로그 내용에 대한 사용자 액세스 권한을 제어합니다. 즉, 누가 어떤 내용에 액세스할 수 있는지, 액세스하는 방법 등을 제어합니다. 자세한 내용은 [역할 및 사용 권한&#40;Reporting Services&#41;](roles-and-permissions-reporting-services.md)을 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|링크|  
|-----------------------|-----------|  
|SSL(Secure Socket Layer)를 구성하여 클라이언트와 보고서 서버의 연결에 보안을 설정합니다.|[기본 모드 보고서 서버에서 SSL 연결 구성](configure-ssl-connections-on-a-native-mode-report-server.md)|  
  
  
