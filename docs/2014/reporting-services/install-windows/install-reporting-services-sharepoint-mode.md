---
title: SharePoint 모드 설치 Reporting Services (SharePoint 2010 및 SharePoint 2013) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- default configuration [Reporting Services]
- installing Reporting Services, SharePoint integrated mode
- installation options [Reporting Services]
ms.assetid: ac6cba68-2665-4a39-8fa3-cb7d7e6723c0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ef049b4ded6408e651d5ec2c3db99c10bf7c27b6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108773"
---
# <a name="reporting-services-sharepoint-mode-installation-sharepoint-2010-and-sharepoint-2013"></a>Reporting Services SharePoint 모드 설치(SharePoint 2010 및 SharePoint 2013)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 sharepoint 모드는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint 제품을 기반으로 보고서 생성 및 배달을 제공 하는 서버 구성 요소의 모음입니다.  
  
 SharePoint 모드에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 실행하면 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 및 데이터 경고 기능을 사용할 수 있습니다. SharePoint 모드의 기능에 대 한 자세한 내용은 [Reporting Services Report Server](../reporting-services-report-server.md) 의 "서버 모드의 기능 지원 및 동작 차이점" 섹션을 참조 하십시오.  
  
 SharePoint 모드의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에는 기본적으로 두 가지 설치가 필요합니다.  
  
|설치|Description|  
|------------------|-----------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 제품용 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 추가 기능|이 추가 기능은 SharePoint 웹 프런트 엔드 서버에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] UI(사용자 인터페이스) 페이지 및 기능을 설치합니다. UI 기능에는 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], SharePoint 중앙 관리의 관리 페이지, SharePoint 문서 라이브러리 내에 사용되는 기능 페이지 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 경고 페이지가 포함됩니다.|  
|SharePoint 모드로 설치 된 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|보고서 서버는 데이터 및 보고서 처리와 렌더링은 물론 등록 및 데이터 경고 처리를 수행합니다. SharePoint 모드 보고서 서버는 SharePoint 공유 서비스로 설계되고 설치됩니다.|  
  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 설치하려면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 미디어를 사용합니다.  
  
 고급 배포 시나리오에 대 한 지침은 [배포 검사 목록: Reporting Services, 파워 뷰 및 SharePoint용 PowerPivot](../../sql-server/install/deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md) 및 [배포 검사 목록: 기존 SharePoint 팜에 Reporting Services 설치](../../sql-server/install/deployment-checklist-install-reporting-services-existing-sharepoint-farm.md)를 참조 하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [지원 되는 SharePoint 및 Reporting Services 서버 조합 및 추가 기능 &#40;SQL Server 2014&#41;](supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
 [Install Reporting Services SharePoint Mode for SharePoint 2013](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md)  
  
 [SharePoint 2010에 대 한 Reporting Services SharePoint 모드 설치](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)  
  
 [Sharepoint 2010 및 SharePoint 2013 &#40;Reporting Services 추가 기능을 설치 하거나 제거&#41;](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
 [SharePoint 제품용 Reporting Services 추가 기능을 찾을 수 있는 위치](where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
 [팜에 추가 보고서 서버 추가 &#40;SSRS 확장&#41;](add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
 [팜에 추가 Reporting Services 웹 프런트 엔드 추가](add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 [Reporting Services 서비스 응용 프로그램에 대 한 전자 메일 구성 &#40;SharePoint 2010 및 SharePoint 2013&#41;](configure-e-mail-for-a-reporting-services-service-application.md)  
  
 [SSRS 서비스 애플리케이션에 대한 구독 및 경고 프로비전](provision-subscriptions-and-alerts-for-ssrs-service-applications.md)  
  
 [Windows 토큰 서비스에 대 한 클레임 &#40;C2WTS&#41; 및 Reporting Services](../../sql-server/install/claims-to-windows-token-service-c2wts-and-reporting-services.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 경고 아키텍처 및 워크플로](../reporting-services-data-alerts.md#AlertingWF)   
 [경고 담당자를 위한 데이터 경고 관리자입니다.](../data-alert-manager-for-alerting-administrators.md)  
  
  
