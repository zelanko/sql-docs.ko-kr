---
title: "Reporting Services SharePoint 모드 설치 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
helpviewer_keywords: 
  - "기본 구성 [Reporting Services]"
  - "Reporting Services 설치, SharePoint 통합 모드 "
  - "설치 옵션 [Reporting Services]"
ms.assetid: ac6cba68-2665-4a39-8fa3-cb7d7e6723c0
caps.latest.revision: 35
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 35
---
# Reporting Services SharePoint 모드 설치
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 사용하면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint에 기반한 모든 배포에서 문서 라이브러리에서 보고서 만들기 및 보기,  [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]전자 메일을 통해 보고서의 구독 배달, [!INCLUDE[msCoName](../../includes/msconame-md.md)] , 데이터 경고 및 보고서 관리 기능을 사용할 수 있습니다. SharePoint 모드의 기능에 대한 자세한 내용은 [Reporting Services 보고서 서버](../../reporting-services/report-server-sharepoint/reporting-services-보고서-서버.md)의 "서버 모드별 기능 지원 및 동작 차이" 섹션을 참조하세요.  
  
 SharePoint 모드에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에 대해 설치할 두 가지 핵심 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소가 있습니다.  
  
|설치|설명|  
|------------------|-----------------|  
|**보고서 서버:** SharePoint 모드로 설치되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버|보고서 서버는 데이터 및 보고서 처리와 렌더링은 물론 등록 및 데이터 경고 처리를 수행합니다. SharePoint 모드 보고서 서버는 SharePoint 공유 서비스로 디자인되고 설치됩니다.<br /><br /> **방법:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보고서 서버를 설치하려면 설치 미디어를 사용합니다.|  
|**추가 기능:** SharePoint 제품용 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능**rssharepoint.msi**입니다.|이 추가 기능은 SharePoint 웹 프런트 엔드 서버에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] UI(사용자 인터페이스) 페이지 및 기능을 설치합니다. UI 기능에는 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], SharePoint 중앙 관리의 관리 페이지, SharePoint 문서 라이브러리 내에 사용되는 기능 페이지 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 경고 페이지가 포함됩니다.<br /><br /> **방법:** 추가 기능은 웹 다운로드 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 미디어에서 설치될 수 있습니다. 자세한 내용은 [SharePoint 제품용 Reporting Services 추가 기능 검색 위치](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)를 참조하세요.|  
  
## 섹션 내용  
 [지원되는 SharePoint와 Reporting Services 서버 및 추가 기능의 조합&#40;SQL Server 2016&#41;](../../reporting-services/install-windows/supported combinations of sharepoint and reporting services server.md)  
  
 [SharePoint 제품용 Reporting Services 추가 기능 검색 위치](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
 [SharePoint 모드에서 첫 번째 보고서 서버 설치](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md)  
  
 [SharePoint용 Reporting Services 추가 기능 설치 또는 제거](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
 [팜에 추가 보고서 서버 추가&#40;SSRS 확장&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
 [팜에 추가 Reporting Services 웹 프런트 엔드 추가](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 [Reporting Services 서비스 응용 프로그램에 대한 메일 구성&#40;SharePoint 2013 및 SharePoint 2016&#41;](http://msdn.microsoft.com/ko-kr/38fc34a6-aae7-4dde-9ad2-f1eee0c42a9f)  
  
 [SSRS 서비스 응용 프로그램에 대한 구독 및 경고 프로비전](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)  
  
 [c2WTS&#40;Windows 토큰 서비스에 대한 클레임&#41; 및 Reporting Services](../../reporting-services/install-windows/claims-to-windows-token-service-c2wts-and-reporting-services.md)  
  
## 참고 항목  
 [데이터 경고 아키텍처 및 워크플로](../../reporting-services/reporting-services-data-alerts.md#AlertingWF)   
 [경고 담당자를 위한 데이터 경고 관리자입니다.](../../reporting-services/data-alert-manager-for-alerting-administrators.md)  
  
  