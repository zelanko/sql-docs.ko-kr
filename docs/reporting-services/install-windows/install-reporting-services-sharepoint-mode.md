---
title: SharePoint 모드에서 Reporting Services 2016 설치 | Microsoft Docs
ms.custom: ''
ms.date: 12/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
helpviewer_keywords:
- default configuration [Reporting Services]
- installing Reporting Services, SharePoint integrated mode
- installation options [Reporting Services]
ms.assetid: ac6cba68-2665-4a39-8fa3-cb7d7e6723c0
caps.latest.revision: 35
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 046cb064f7cb61bba17d7cff2c3cdd27e46e7b15
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38983245"
---
# <a name="install-reporting-services-2016-in-sharepoint-mode"></a>SharePoint 모드에서 Reporting Services 2016 설치

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE [ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

SharePoint에서 SQL Server Reporting Services를 사용하면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint에 기반한 모든 배포에서 문서 라이브러리에서 보고서 만들기 및 보기, 전자 메일을 통해 보고서의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독 배달, [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], 데이터 경고 및 보고서 관리 기능을 사용할 수 있습니다. SharePoint 모드의 기능에 대한 자세한 내용은 [Reporting Services 보고서 서버](../../reporting-services/report-server-sharepoint/reporting-services-report-server.md)의 “서버 모드별 기능 지원 및 동작 차이” 섹션을 참조하세요.

> [!NOTE]
> SQL Server 2016 이후부터 SharePoint와의 Reporting Services 통합을 사용할 수 없습니다.

SharePoint 모드에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에 대해 설치할 두 가지 핵심 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소가 있습니다.  

|설치|설명|  
|------------------|-----------------|  
|**보고서 서버:** SharePoint 모드로 설치되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버|보고서 서버는 데이터 및 보고서 처리와 렌더링은 물론 등록 및 데이터 경고 처리를 수행합니다. SharePoint 모드 보고서 서버는 SharePoint 공유 서비스로 디자인되고 설치됩니다.<br /><br /> **방법:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보고서 서버를 설치하려면 설치 미디어를 사용합니다.|  
|**추가 기능:** SharePoint 모드로 설치되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능 **rssharepoint.msi**입니다.|이 추가 기능은 SharePoint 웹 프런트 엔드 서버에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] UI(사용자 인터페이스) 페이지 및 기능을 설치합니다. UI 기능에는 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], SharePoint 중앙 관리의 관리 페이지, SharePoint 문서 라이브러리 내에 사용되는 기능 페이지 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 경고 페이지가 포함됩니다.<br /><br /> **방법:**  추가 기능은 웹 다운로드 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 미디어에서 설치될 수 있습니다. 자세한 내용은 [SharePoint 제품용 Reporting Services 추가 기능 검색 위치](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)를 참조하세요.|  
  
## <a name="in-this-section"></a>섹션 내용

 [지원되는 SharePoint와 Reporting Services 서버 및 추가 기능의 조합&#40;SQL Server 2016&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
 [SharePoint 제품용 Reporting Services 추가 기능 검색 위치](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
 [SharePoint 모드에서 첫 번째 보고서 서버 설치](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md)  
  
 [SharePoint용 Reporting Services 추가 기능 설치 또는 제거](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
 [팜에 추가 보고서 서버 추가&#40;SSRS 확장&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
 [팜에 추가 Reporting Services 웹 프런트 엔드 추가](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 [Reporting Services 서비스 응용 프로그램에 대한 메일 구성&#40;SharePoint 2013 및 SharePoint 2016&#41;](http://msdn.microsoft.com/38fc34a6-aae7-4dde-9ad2-f1eee0c42a9f)  
  
 [SSRS 서비스 응용 프로그램에 대한 구독 및 경고 프로비전](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)  
  
 [c2WTS&#40;Windows 토큰 서비스에 대한 클레임&#41; 및 Reporting Services](../../reporting-services/install-windows/claims-to-windows-token-service-c2wts-and-reporting-services.md)  

## <a name="next-steps"></a>다음 단계

 [데이터 경고 아키텍처 및 워크플로](../../reporting-services/reporting-services-data-alerts.md#AlertingWF)   
 [경고 담당자용 데이터 경고 관리자](../../reporting-services/data-alert-manager-for-alerting-administrators.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
