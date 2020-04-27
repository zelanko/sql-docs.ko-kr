---
title: 보고서 서버(Reporting Services 기본 모드) 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report server configuration
- report servers [Reporting Services], configuring
ms.assetid: ef84ce9d-9156-48e9-8073-7e0535476932
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 10e4a4befd8300863d8637a87e8c9bd03622d0af
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66104071"
---
# <a name="configure-a-report-server-reporting-services-native-mode"></a>보고서 서버(Reporting Services 기본 모드) 구성
  설치 중에 선택한 옵션에 따라 보고서 서버를 사용하기 전에 추가 구성이 필요할 수 있습니다. 보고서 서버 구성은 최소한 다음과 같은 요소로 구성됩니다.  
  
-   보고서 서버 서비스 계정(설치 중 구성됨)  
  
-   보고서 서버에 대한 액세스를 제공하는 웹 서비스 URL  
  
-   애플리케이션 데이터, 보고서 및 기타 항목을 저장하는 보고서 서버 데이터베이스  
  
 기본 모드 기본 구성 또는 SharePoint 통합 모드 기본 구성 설치 옵션 중 하나를 선택한 경우 설치 프로그램은 최소 설정을 구성합니다. 파일만 모드로 보고서 서버를 설치한 경우(설치 마법사의 **구성 없이 설치** 옵션) 서비스 계정만 구성됩니다. 설치가 완료된 후 웹 서비스 URL과 보고서 서버 데이터베이스를 구성해야 합니다.  
  
 보고서 관리자는 기본 모드 보고서 서버의 선택적 기능이지만 사용자에게 보고서 서버에 대한 액세스 권한을 부여하고 보고서 서버 콘텐츠를 관리할 수 있도록 보고서 관리자를 구성하는 것이 좋습니다. 보고서 서버를 SharePoint 통합 모드로 배포하는 경우 SharePoint 서버의 웹 프런트 엔드를 사용하여 액세스 권한을 부여할 수 있습니다.  
  
 필요한 경우 보고서 서버 전자 메일 및 무인 실행 계정과 같은 추가 기능을 구성할 수 있습니다. 자세한 내용은 [Reporting Services 기본 모드 보고서 서버 관리](manage-a-reporting-services-native-mode-report-server.md)를 참조하세요.  
  
 보고서 서버를 구성하려면 Reporting Services 구성 도구를 사용합니다.  
  
### <a name="to-minimally-configure-a-report-server-installation"></a>보고서 서버 설치를 최소한으로 구성하려면  
  
1.  Reporting Services 구성 관리자를 시작한 후 보고서 서버 인스턴스에 연결합니다. 자세한 내용은 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)를 참조하세요.  
  
2.  **웹 서비스 URL** 을 클릭하여 보고서 서버에 대한 URL을 구성하는 페이지를 엽니다. URL을 정의하는 방법은 [URL 구성&#40;SSRS 구성 관리자&#41;](../install-windows/configure-a-url-ssrs-configuration-manager.md)을 참조하세요.  
  
3.  **데이터베이스** 를 클릭하여 보고서 서버 데이터베이스를 만듭니다. 자세한 내용은 [기본 모드 보고서 서버 데이터베이스 만들기&#40;SSRS 구성 관리자&#41;](../install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)를 참조하세요.  
  
4.  **웹 서비스 URL** 페이지로 돌아가 URL을 클릭하여 작동하는지 확인합니다.  
  
5.  "다음 단계"의 지침에 따라 배포를 완료합니다.  
  
## <a name="next-steps"></a>다음 단계  
 배포를 완료하려면 보고서 관리자 또는 SharePoint 통합을 구성해야 합니다. 자세한 내용은 [보고서 관리자 구성&#40;기본 모드&#41;](configure-web-portal.md)을 참조하세요.  
  
 Windows 방화벽을 켜면 보고서 서버에서 사용하도록 구성된 포트는 대부분 닫혀 있습니다. 원격 클라이언트 컴퓨터에서 보고서 관리자를 열 때 빈 페이지가 표시되면 포트가 닫혀 있기 때문일 수 있습니다. 방화벽을 구성하는 방법은 [Configure a Firewall for Report Server Access](configure-a-firewall-for-report-server-access.md)을 참조하십시오.  
  
 Windows Vista 또는 Windows Server 2008을 사용 중인 경우 보고서 관리자를 로컬로 열려면 추가 단계를 수행해야 합니다. 자세한 내용은 [로컬 관리에 대해 기본 모드 보고서 서버 구성&#40;SSRS&#41;](configure-a-native-mode-report-server-for-local-administration-ssrs.md)를 참조하세요.  
  
 폴더를 만들고 항목을 업로드하고 보고서를 실행하여 설치가 제대로 되었는지 확인합니다. [Reporting Services 설치 확인](../install-windows/verify-a-reporting-services-installation.md) 의 지침에 따라 설치를 확인합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services 기본 모드 보고서 서버 관리](manage-a-reporting-services-native-mode-report-server.md)   
 [보고서 서버 액세스를 위한 방화벽 구성](configure-a-firewall-for-report-server-access.md)   
 [로컬 관리에 대해 기본 모드 보고서 서버 구성&#40;SSRS&#41;](configure-a-native-mode-report-server-for-local-administration-ssrs.md)   
 [원격 관리를 위한 보고서 서버 구성](configure-a-report-server-for-remote-administration.md)   
 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
