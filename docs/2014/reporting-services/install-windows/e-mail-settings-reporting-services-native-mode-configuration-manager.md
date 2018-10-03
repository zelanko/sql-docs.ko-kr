---
title: 전자 메일 설정-구성 관리자 (SSRS 기본 모드) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.rsconfigtool.emailsettings.f1
helpviewer_keywords:
- SQL11.rsconfigtool.emailsettings.F1
ms.assetid: cdad1529-bfa6-41fb-9863-d9ff1b802577
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d9abd39577d521d8d14d0ecc20ebc75a0f91404d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48050425"
---
# <a name="e-mail-settings---configuration-manager-ssrs-native-mode"></a>전자 메일 설정 - 구성 관리자(SSRS 기본 모드)
  이 페이지에서는 보고서 서버에서 보고서 서버 전자 메일 배달을 가능하게 하는 SMTP(Simple Mail Transport Protocol) 설정을 지정할 수 있습니다. 보고서 서버 전자 메일 배달 확장 프로그램을 사용하여 전자 메일 구독을 통해 보고서 또는 보고서 처리 알림을 배포할 수 있습니다. 보고서 서버 전자 메일 배달 확장 프로그램을 사용하려면 SMTP 서버 및 보낸 사람 주소: 필드에 사용할 전자 메일 주소가 필요합니다.  
  
 메일 서버 호스트 및 렌더링 확장 프로그램 가용성을 제한하는 설정을 포함한 추가 구성 설정을 사용하여 전자 메일 구독을 추가로 사용자 지정할 수 있습니다. 이러한 설정을 지정할 수 없습니다는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager입니다. 추가 설정을 구성하려면 RSReportServer.config 파일을 직접 편집해야 합니다. 자세한 내용은 참조 하세요. [전자 메일 배달을 위한 보고서 서버를 구성 &#40;&AMP;#40;SSRS 구성 관리자&#41; ](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md) 하 고 [Reporting Services Configuration Files](../report-server/reporting-services-configuration-files.md) 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 책 온라인.  
  
 이 페이지를 열려면 Reporting Services 구성 관리자를 시작한 다음 탐색 창에서 **전자 메일 설정** 을 클릭합니다. 자세한 내용은 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)을 참조하세요.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드입니다.  
  
## <a name="options"></a>변수  
 **보낸 사람 주소**  
 생성된 전자 메일의 보낸 사람: 필드에 사용할 전자 메일 주소를 지정합니다. SMTP 서버에서 메일을 보낼 수 있는 권한이 있는 사용자 계정을 지정해야 합니다.  
  
 **현재 SMTP 배달 방법**  
 보고서 서버 전자 메일이 SMTP 서버를 통해 라우팅되도록 지정합니다. Reporting Services 구성 관리자에서는 이 배달 방법만 지정할 수 있습니다.  
  
 다른 배달 방법으로는 로컬 SMTP 서비스 픽업 디렉터리를 사용하는 방법이 있으며 이는 네트워크 SMTP 서비스를 사용할 수 없는 경우에 사용할 수 있습니다. 로컬 SMTP 서비스 픽업 디렉터리를 지정하려면 RSReportServer.config 파일을 편집해야 합니다. 구성 파일을 편집하여 로컬 SMTP 서비스 픽업 디렉터리를 사용할 경우 Reporting Services 구성 관리자에서는 **현재 배달 방법** 옵션을 *사용자 지정* 으로 설정하여 구성 파일에 배달 방법이 지정되어 있음을 나타냅니다.  
  
 구성 파일에서 배달 방법을 통해 설정 된 `SendUsing` 구성 설정입니다. 지정 하는 방법에 대 한 자세한 내용은 합니다 `SendUsing` 설정을 참조 하세요 [전자 메일 배달을 위한 보고서 서버 구성 &#40;&AMP;#40;SSRS 구성 관리자&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md).  
  
 **SMTP 서버**  
 사용할 SMTP 서버 또는 게이트웨이를 지정합니다. 네트워크에서 로컬 서버나 SMTP 서버를 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [전자 메일 배달을 위한 보고서 서버 구성 &#40;SSRS 구성 관리자&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)   
 [Reporting Services 구성 관리자 F1 도움말 항목 &#40;SSRS 기본 모드&#41;](../../sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)  
  
  
