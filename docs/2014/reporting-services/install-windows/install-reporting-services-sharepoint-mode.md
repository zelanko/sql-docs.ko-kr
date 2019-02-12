---
title: Reporting Services SharePoint 모드 설치 (SharePoint 2010 및 SharePoint 2013) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- default configuration [Reporting Services]
- installing Reporting Services, SharePoint integrated mode
- installation options [Reporting Services]
ms.assetid: ac6cba68-2665-4a39-8fa3-cb7d7e6723c0
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: c46be33ef74736a7dda0e080c1a4928c090f656d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56043194"
---
# <a name="reporting-services-sharepoint-mode-installation-sharepoint-2010-and-sharepoint-2013"></a>Reporting Services SharePoint 모드 설치(SharePoint 2010 및 SharePoint 2013)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드의 보고서 생성 및 전달을 기반을 제공 하는 서버 구성 요소 모음인 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고 [!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint 제품입니다.  
  
 SharePoint 모드에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 실행하면 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 및 데이터 경고 기능을 사용할 수 있습니다. SharePoint 모드의 기능에 대 한 자세한 내용은 "지원 및 동작 차이 서버 모드별 기능" 섹션을 참조 [Reporting Services 보고서 서버](../reporting-services-report-server.md)  
  
 SharePoint 모드의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에는 기본적으로 두 가지 설치가 필요합니다.  
  
|설치|Description|  
|------------------|-----------------|  
|합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 제품에 추가 합니다.|이 추가 기능은 SharePoint 웹 프런트 엔드 서버에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] UI(사용자 인터페이스) 페이지 및 기능을 설치합니다. UI 기능에는 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], SharePoint 중앙 관리의 관리 페이지, SharePoint 문서 라이브러리 내에 사용되는 기능 페이지 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 경고 페이지가 포함됩니다.|  
|합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버가 SharePoint 모드 설치|보고서 서버는 데이터 및 보고서 처리와 렌더링은 물론 등록 및 데이터 경고 처리를 수행합니다. SharePoint 모드 보고서 서버는 SharePoint 공유 서비스로 설계되고 설치됩니다.|  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 설치하려면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 미디어를 사용합니다.  
  
 고급 배포 시나리오에 대 한 자세한 내용은 참조 하세요. [배포 검사 목록: SharePoint 용 reporting Services, Power View 및 PowerPivot](../../sql-server/install/deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md) 고 [배포 검사 목록: 기존 SharePoint 팜에 Reporting Services 설치](../../sql-server/install/deployment-checklist-install-reporting-services-existing-sharepoint-farm.md)합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [지원 되는 SharePoint와 Reporting Services 서버 및 추가 기능의 조합 &#40;SQL Server 2014&#41;](supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
 [SharePoint 2013 용 Reporting Services SharePoint 모드 설치](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md)  
  
 [SharePoint 2010용 Reporting Services SharePoint 모드 설치](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)  
  
 [설치 또는 제거는 Reporting Services 추가-SharePoint 용 &#40;SharePoint 2010 및 SharePoint 2013&#41;](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
 [SharePoint 제품용 Reporting Services 추가 기능 검색 위치](where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
 [팜에 추가 보고서 서버 추가&#40;SSRS 확장&#41;](add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
 [팜에 추가 Reporting Services 웹 프런트 엔드 추가](add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 [Reporting Services 서비스 애플리케이션에 대한 메일 구성&amp;#40;SharePoint 2010 및 SharePoint 2013&amp;#41;](configure-e-mail-for-a-reporting-services-service-application.md)  
  
 [SSRS 서비스 응용 프로그램에 대한 구독 및 경고 프로비전](provision-subscriptions-and-alerts-for-ssrs-service-applications.md)  
  
 [Windows 클레임 토큰 서비스 &#40;C2WTS&#41; 및 Reporting Services](../../sql-server/install/claims-to-windows-token-service-c2wts-and-reporting-services.md)  
  
## <a name="see-also"></a>관련 항목  
 [데이터 경고 아키텍처 및 워크플로](../reporting-services-data-alerts.md#AlertingWF)   
 [경고 담당자를 위한 데이터 경고 관리자입니다.](../data-alert-manager-for-alerting-administrators.md)  
  
  
