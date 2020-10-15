---
description: SharePoint 모드에서 Reporting Services 2016 설치
title: SharePoint 모드에서 Reporting Services 2016 설치 | Microsoft Docs
ms.date: 12/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.topic: conceptual
helpviewer_keywords:
- default configuration [Reporting Services]
- installing Reporting Services, SharePoint integrated mode
- installation options [Reporting Services]
ms.assetid: ac6cba68-2665-4a39-8fa3-cb7d7e6723c0
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: e9c615e709d31b9bd1632d77490ac84ad9081aa0
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91892113"
---
# <a name="install-reporting-services-2016-in-sharepoint-mode"></a>SharePoint 모드에서 Reporting Services 2016 설치

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE [ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

SharePoint에서 SQL Server Reporting Services를 사용하면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint에 기반한 모든 배포에서 문서 라이브러리에서 보고서 만들기 및 보기, 전자 메일을 통해 보고서의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독 배달, [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], 데이터 경고 및 보고서 관리 기능을 사용할 수 있습니다. SharePoint 모드의 기능에 대한 자세한 내용은 [Reporting Services 보고서 서버](../../reporting-services/report-server-sharepoint/reporting-services-report-server.md)의 "서버 모드별 기능 지원 및 동작 차이" 섹션을 참조하세요.

> [!NOTE]
> SQL Server 2016 이후부터 SharePoint와의 Reporting Services 통합을 사용할 수 없습니다.

SharePoint 모드에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에 대해 설치할 두 가지 핵심 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소가 있습니다.  

|설치|설명|  
|------------------|-----------------|  
|**보고서 서버:** SharePoint 모드로 설치되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버|보고서 서버는 데이터 및 보고서 처리와 렌더링은 물론 등록 및 데이터 경고 처리를 수행합니다. SharePoint 모드 보고서 서버는 SharePoint 공유 서비스로 디자인되고 설치됩니다.<br /><br /> **방법:**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보고서 서버를 설치하려면 설치 미디어를 사용합니다.|  
|**추가 기능:** SharePoint 모드로 설치되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능 **rssharepoint.msi**입니다.|이 추가 기능은 SharePoint 웹 프런트 엔드 서버에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] UI(사용자 인터페이스) 페이지 및 기능을 설치합니다. UI 기능에는 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], SharePoint 중앙 관리의 관리 페이지, SharePoint 문서 라이브러리 내에 사용되는 기능 페이지 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 경고 페이지가 포함됩니다.<br /><br /> **방법:**  추가 기능은 웹 다운로드 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 미디어에서 설치될 수 있습니다. 자세한 내용은 [SharePoint 제품용 Reporting Services 추가 기능 검색 위치](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)를 참조하세요.|  
  
## <a name="in-this-section"></a>섹션 내용

 [지원되는 SharePoint와 Reporting Services 서버 및 추가 기능의 조합&#40;SQL Server 2016&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
 [SharePoint 제품용 Reporting Services 추가 기능 검색 위치](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
 [SharePoint 모드에서 첫 번째 보고서 서버 설치](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md)  
  
 [SharePoint용 Reporting Services 추가 기능 설치 또는 제거](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
 [팜에 추가 보고서 서버 추가&#40;SSRS 확장&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
 [팜에 추가 Reporting Services 웹 프런트 엔드 추가](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 [Reporting Services 서비스 애플리케이션에 대한 메일 구성&#40;SharePoint 2013 및 SharePoint 2016&#41;](./configure-e-mail-for-a-reporting-services-service-application.md)  
  
 [SSRS 서비스 애플리케이션에 대한 구독 및 경고 프로비전](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)  
  
 [c2WTS&#40;Windows 토큰 서비스에 대한 클레임&#41; 및 Reporting Services](../../reporting-services/install-windows/claims-to-windows-token-service-c2wts-and-reporting-services.md)  

## <a name="next-steps"></a>다음 단계

 [데이터 경고 아키텍처 및 워크플로](../../reporting-services/reporting-services-data-alerts.md#AlertingWF)   
 [경고 담당자용 데이터 경고 관리자](../../reporting-services/data-alert-manager-for-alerting-administrators.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)