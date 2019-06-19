---
title: '배포 검사 목록: 기존 SharePoint 팜에 Reporting Services 설치 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 436b4c3d-3f2f-464a-be7e-5c051d9ffb8f
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 66c366bfe8dbf79d2f392627ad018747357e7da4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095674"
---
# <a name="deployment-checklist-install-reporting-services-into-an-existing-sharepoint-farm"></a>배포 검사 목록: 기존 SharePoint 팜에 Reporting Services 설치
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 보고서 서버를 새로운 SharePoint 팜 또는 기존 SharePoint 팜에 설치할 수 있습니다. 이 항목에서는 기존 SharePoint 팜에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 을 설치하기 위한 가능한 시나리오와 최선의 구현 방법에 대해 설명합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 설치 프로그램을 실행하기 전에 다음 정보를 검토하십시오.  
  
|단계|링크|  
|----------|----------|  
|보고서 서버 배포에 사용되는 계정을 만들거나 식별합니다. 보고서 서버 서비스용 서비스 계정과 보고서 서버 데이터베이스에 연결하기 위한 자격 증명이 있어야 합니다.||  
|보고서 서버 데이터베이스를 호스팅할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 결정합니다. 로컬 또는 원격 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 사용할 수 있습니다. 보고서에 맞는 스토리지 용량을 가진 컴퓨터에 있는 인스턴스를 선택해야 합니다.||  
|구독에 보고서 서버 전자 메일을 사용하려면 조직에 전자 메일 서비스를 제공하는 SMTP 서버 또는 게이트웨이의 이름을 찾습니다(옵션).|[전자 메일 배달을 위한 보고서 서버 구성 &#40;SSRS 구성 관리자&#41;](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)|  
|참고: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]의 이전 CTP 릴리스에서 컴퓨터를 업그레이드하는 경우 구성 파일에 사용자 지정 변경 내용을 적용한 적이 있다면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]를 업그레이드한 후 구성 파일에 동일한 변경 내용을 적용해야 합니다. 관련이 있는 파일은 **web.config** 및 **client.config**입니다.||  
  
## <a name="installation-scenarios"></a>설치 시나리오  
 다음 표에서는 기존 SharePoint 팜에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 을 설치하기 위한 가능한 시나리오에 대해 설명합니다. 로컬 모드에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버와 통합하지 않고도 SharePoint 문서 라이브러리에서 로컬로 보고서를 렌더링할 수 있습니다. SharePoint 제품용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능은 필요하지만 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버는 아닙니다. 로컬 모드에 대한 자세한 내용은 [보고서 뷰어의 로컬 모드와 연결 모드 보고서를 보고서 뷰어에서 &#40;SharePoint 모드의 Reporting Services&#41; ](../../../2014/reporting-services/local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md) 하 고 [SharePoint 제품용 Reporting Services 추가 기능 검색 위치](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)합니다.  
  
|구성 시작|워크플로|구성 종료|주석|  
|----------------------------|--------------|--------------------------|--------------|  
|로컬 모드에서 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|설치|연결된 모드 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].||  
|연결된 모드 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 또는 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|내부 업그레이드|연결된 모드 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].||  
|연결된 모드 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 또는 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|마이그레이션|연결된 모드 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].||  
  
## <a name="installation-and-in-place-upgrade-checklist"></a>설치 및 내부 업그레이드 검사 목록  
 다음 표에서는 설치에 대해 검토하고 사용해야 하는 단계, 도구 및 정보에 대해 요약합니다.  
  
|단계|링크|  
|----------|----------|  
|**설치 및 초기 구성**||  
|모든 WFE(웹 프런트 엔드) 컴퓨터에 SharePoint 추가 기능을 설치합니다.|[팜에 추가 Reporting Services 웹 프런트 엔드 추가](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)|  
|SQL Server [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Reporting Services 및 데이터베이스 엔진을 설치합니다.|[SharePoint 2010용 Reporting Services SharePoint 모드 설치](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|하나 이상의 SSRS 서비스 애플리케이션을 만들고 서비스 애플리케이션 연결을 구성합니다.|' 서비스 응용 프로그램 ' 섹션을 참조 [Reporting Services SharePoint 모드 설치 SharePoint 2010 용](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|**추가 구성**||  
|SSRS 콘텐츠 형식을 문서 라이브러리에 추가합니다.|[보고서 서버 콘텐츠 형식을 라이브러리에 추가 &#40;Reporting Services sharepoint에서 통합 모드&#41;](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md)|  
|SQL Server 에이전트 프로비전|[SSRS 서비스 응용 프로그램에 대한 구독 및 경고 프로비전](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)|  
|서비스 애플리케이션에 대한 전자 메일 설정을 구성합니다.|[Reporting Services 서비스 애플리케이션에 대한 메일 구성&amp;#40;SharePoint 2010 및 SharePoint 2013&amp;#41;](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)|  
|c2WTS(Windows 토큰 서비스에 대한 클레임) 구성|[Windows 클레임 토큰 서비스 &#40;C2WTS&#41; 및 Reporting Services](../../../2014/sql-server/install/claims-to-windows-token-service-c2wts-and-reporting-services.md)|  
  
## <a name="migration-checklist"></a>마이그레이션 목록  
 다음은 기존 설치를 새 설치로 마이그레이션하기 위한 기본 단계 목록입니다.  
  
|단계|링크|  
|----------|----------|  
|새 서버를 설치 및 구성합니다. 여기에는 다음이 포함됩니다.<br /><br /> SharePoint 제품 준비 도구<br /><br /> SharePoint 2010 제품<br /><br /> SharePoint 2010 SP1<br /><br /> SharePoint 모드의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]<br /><br /> SharePoint 2010 제품을 위한 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능|[SharePoint 2010용 Reporting Services SharePoint 모드 설치](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|최소 하나의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션 생성||  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터베이스 백업||  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 암호화 키 백업||  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터베이스 및 암호화 키 복구||  
|모든 웹 애플리케이션을 새로운 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]서비스 애플리케이션에 매핑|새 설치 **가 이제 작동**|  
|이전 서버의 통합 URL을 제거합니다.|SharePoint 중앙 관리의 **일반 애플리케이션 설정** 페이지에서 **Reporting Services 통합**을 클릭합니다.|  
|원하는 경우 기존 설정에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]을 제거합니다.||  
  
## <a name="next-steps"></a>다음 단계  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services SharePoint 모드 설치 &#40;SharePoint 2010 및 SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)   
 [SharePoint 2010 팜에서 SQL Server BI 기능을 사용 하기 위한 지침](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)   
 [지원 되는 SharePoint와 Reporting Services 서버 및 추가 기능의 조합 &#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
  
