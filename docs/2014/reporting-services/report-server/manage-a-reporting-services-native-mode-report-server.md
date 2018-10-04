---
title: Reporting Services 기본 모드 보고서 서버 관리 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Configuration tool
- configuration options [Reporting Services]
- report servers [Reporting Services], configuring
ms.assetid: 6ca03a09-d6a8-4c93-ba12-1c99dcbfb618
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 2c6190ec6494e5a723aa449c5d4053c12979076c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48206113"
---
# <a name="manage-a-reporting-services-native-mode-report-server"></a>Reporting Services 기본 모드 보고서 서버 관리
  이 섹션에서는 Reporting Services 구성 관리자를 사용하여 기본 모드 보고서 서버 인스턴스를 구성하는 절차를 제공합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 이 섹션의 항목은 필요한 지침을 쉽게 찾을 수 있도록 범주로 구성되어 있습니다. 첫 번째 섹션에는 기본 모드 보고서 서버의 기본 구성 태스크에 대한 항목, 두 번째 섹션에는 고급 구성 항목이 포함되어 있고 세 번째 섹션에는 SharePoint 통합 모드에서 실행되도록 보고서 서버를 구성하는 방법에 대한 항목이 있습니다.  
  
### <a name="basic-configuration"></a>기본 구성  
 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
 Reporting Services 구성 도구를 시작하는 단계에 대해 설명합니다.  
  
 [서비스 계정 구성 &#40;SSRS 구성 관리자&#41;](../../sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)  
 보고서 서버 서비스에 대한 계정 및 암호 정보를 지정하는 방법에 대해 설명합니다.  
  
 [서비스 주체 이름 등록 &#40;SPN&#41; 보고서 서버에 대 한](register-a-service-principal-name-spn-for-a-report-server.md)  
 Kerberos 인증을 사용하는 네트워크에서 도메인 사용자 계정으로 실행되는 보고서 서버의 SPN을 수동으로 등록하는 방법에 대해 설명합니다.  
  
 [URL 구성 &#40;SSRS 구성 관리자&#41;](../install-windows/configure-a-url-ssrs-configuration-manager.md)  
 보고서 서버 웹 서비스 및 보고서 관리자에 액세스하는 데 사용되는 하나 이상의 URL을 설정하는 방법에 대해 설명합니다.  
  
 [기본 모드 보고서 서버 데이터베이스 만들기 &#40;SSRS 구성 관리자&#41;](../install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)  
 보고서 서버 데이터베이스를 만드는 단계에 대해 설명합니다. 이 단계는 Reporting Services 설치를 배포하는 데 필요합니다.  
  
### <a name="advanced-or-optional-configuration"></a>고급 또는 선택 사항 구성  
 [기본 모드 보고서 서버 스케일 아웃 배포 구성 &#40;SSRS 구성 관리자&#41;](../install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)  
 여러 보고서 서버에서 보고서 서버 데이터베이스를 공유하도록 구성하는 단계에 대해 설명합니다.  
  
 [전자 메일 배달을 위한 보고서 서버 구성 &#40;SSRS 구성 관리자&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)  
 전자 메일 배포를 위한 보고서 서버를 구성하는 단계에 대해 설명합니다.  
  
 [보고서 서버 액세스를 위한 방화벽 구성](configure-a-firewall-for-report-server-access.md)  
 보고서 서버의 인바운드 요청과 아웃바운드 응답에 사용되는 포트를 여는 방법에 대해 설명합니다.  
  
 [로컬 관리를 위한 기본 모드 보고서 서버 구성 &#40;SSRS&#41;](configure-a-native-mode-report-server-for-local-administration-ssrs.md)  
 http://localhost를 사용하여 보고서 서버 또는 보고서 관리자에 연결할 때 필요한 추가 단계에 대해 설명합니다.  
  
 [원격 관리를 위한 보고서 서버 구성](configure-a-report-server-for-remote-administration.md)  
 다른 컴퓨터에서 연결하여 구성할 수 있도록 원격 보고서 서버 인스턴스를 구성하는 방법에 대해 설명합니다.  
  
 [Reporting Services 기능 설정 또는 해제](turn-reporting-services-features-on-or-off.md)  
 Reporting Services 설치에서 사용하지 않는 기능을 제거하는 방법에 대해 설명합니다.  
  
 [원격 오류 사용 &#40;Reporting Services&#41;](enable-remote-errors-reporting-services.md)  
 원격 서버에서 발생하는 오류 조건에 대한 추가 정보를 반환하도록 보고서 서버에 대한 서버 속성을 설정하는 방법에 대해 설명합니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 서버 구성 및 관리&#40;SSRS 기본 모드&#41;](configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [보고서 서버의 구성 및 관리&#40;Reporting Services SharePoint 모드&#41;](../configure-administer-report-server-reporting-services-sharepoint-mode.md)  
  
  
