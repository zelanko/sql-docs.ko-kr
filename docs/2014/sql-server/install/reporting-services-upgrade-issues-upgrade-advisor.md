---
title: Reporting Services 업그레이드 문제 (업그레이드 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Report Manager [Reporting Services], upgrade issues
- Reporting Services, upgrades
- upgrading Reporting Services
- report servers [Reporting Services], upgrade issues
ms.assetid: d9663f25-98d7-4508-ae3c-55a7277211bd
caps.latest.revision: 42
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: a3adf211200ccc2596fe8766c11bffc653a2b3f2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37306933"
---
# <a name="reporting-services-upgrade-issues-upgrade-advisor"></a>Reporting Services 업그레이드 문제(업그레이드 관리자)
  다음 항목에 설명 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 로 업그레이드에 영향을 줄 수 있는 문제 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]합니다. 이러한 변화가 환경에 미치는 영향을 완화하기 위해 취할 수 있는 조치에 대해 설명합니다.  
  
 업그레이드 관리자는 보고서 서버 설치를 분석합니다. 보고서 디자이너가 컴퓨터에 설치된 유일한 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소인 경우와 같이 클라이언트 구성 요소만 설치된 경우에는 문제가 보고되지 않습니다.  
  
 설치를 구성한 방법에 따라 업그레이드 관리자가 보고하지 않는 추가적인 문제가 발생할 수도 있습니다. 이러한 문제는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 업그레이드를 방해하지 않지만 업그레이드가 완료된 후 보고서와 응용 프로그램이 실행되는 방법에는 영향을 줄 수 있습니다. 이러한 문제에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 "Reporting Services의 이전 버전과의 호환성"을 참조하십시오.  
  
 설치 프로그램을 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치를 업그레이드할 수 없는 경우에는 새 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스를 설치하고 기존 설치를 새 인스턴스로 마이그레이션할 수 있습니다. 자세한 내용은 "업그레이드 및 Migrate Reporting Services"를 참조 하세요 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서 [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)합니다.  
  
 다음 항목에서는 업그레이드 관리자가 보고하는 알려진 문제에 대해 설명하고 업그레이드를 성공적으로 수행하기 위해 기존 설치를 수정하는 방법에 대해 설명합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스를 분석하려면 보고서 서버에 업그레이드 관리자를 설치해야 합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]는 원격 분석을 지원하지 않습니다.  
>   
>  자세한 내용은 [업그레이드 관리자 설치](../../../2014/sql-server/install/installing-upgrade-advisor.md)합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [보고서 서버 웹 사이트에서 클라이언트 인증서 &#40;업그레이드 관리자&#41;](../../../2014/sql-server/install/client-certificates-on-the-report-server-web-site-upgrade-advisor.md)  
  
-   [사용자 지정 확장 프로그램이 보고서 서버에서 검색 됨 &#40;업그레이드 관리자&#41;](../../../2014/sql-server/install/custom-extensions-were-detected-on-the-report-server-upgrade-advisor.md)  
  
-   [사용자 지정 보고서 항목이 보고서 서버에서 검색 됨 &#40;업그레이드 관리자&#41;](../../../2014/sql-server/install/custom-report-items-were-detected-on-the-report-server-upgrade-advisor.md)  
  
-   [IIS 이전 버전과 호환성 구성 요소가 검색 되지 않았습니다 &#40;업그레이드 관리자&#41;](../../../2014/sql-server/install/iis-backward-compatibility-components-were-not-detected-upgrade-advisor.md)  
  
-   [IP 주소 제한이 검색 되었습니다. &#40;업그레이드 관리자&#41;](../../../2014/sql-server/install/ip-address-restriction-detected-upgrade-advisor.md)  
  
-   [보고서 서버 사이트에서 검색 하는 ISAPI 필터 &#40;업그레이드 관리자&#41;](../../../2014/sql-server/install/isapi-filters-detected-on-the-report-server-site-upgrade-advisor.md)  
  
-   [보고서 서버 컴퓨터에서 사용 되지 않는 확장 프로그램이 검색 된 &#40;업그레이드 관리자&#41;](../../../2014/sql-server/install/obsolete-extensions-were-detected-on-the-report-server-computer-upgrade-advisor.md)  
  
-   [보고서 서버 데이터베이스가 구성 되지 않았습니다 &#40;업그레이드 관리자&#41;](../../../2014/sql-server/install/report-server-database-is-not-configured-upgrade-advisor.md)  
  
-   [SQL Server 2005 보고서 서버 웹 서비스 그룹이 검색 되었습니다. &#40;업그레이드 관리자&#41;](../../../2014/sql-server/install/sql-server-2005-report-server-web-service-group-detected-upgrade-advisor.md)  
  
-   [가상 디렉터리가 지정 되지 &#40;업그레이드 관리자&#41;](../../../2014/sql-server/install/virtual-directories-are-unspecified-upgrade-advisor.md)  
  
-   [가상 디렉터리에 지원 되지 않는 인증 방법이 &#40;업그레이드 관리자&#41;](../../../2014/sql-server/install/virtual-directory-has-unsupported-authentication-method-upgrade-advisor.md)  
  
-   [SQL Server Standard 및 Enterprise의 CPU 및 메모리 제한을 변경 &#40;업그레이드 관리자&#41;](../../../2014/sql-server/install/cpu-memory-limits-changes-sql-server-standard-enterprise-upgrade-advisor.md)  
  
-   [SharePoint 팜에 대 한 필요한 도메인 계정 &#40;업그레이드 관리자&#41;](../../../2014/sql-server/install/domain-accounts-required-for-sharepoint-farm-upgrade-advisor.md)  
  
-   [보고서 서버로 직접 이동 &#40;업그레이드 관리자&#41;](../../../2014/sql-server/install/direct-browsing-to-report-server-upgrade-advisor.md)  
  
-   [Microsoft SharePoint 2007이 설치 되어 &#40;업그레이드 관리자&#41;](../../../2014/sql-server/install/microsoft-sharepoint-2007-is-installed-upgrade-advisor.md)  
  
-   [Microsoft SQL Server Reporting Services SharePoint 공유 서비스는 나란히 설치 &#40;업그레이드 관리자&#41;](../../../2014/sql-server/install/sql-server-reporting-services-sharepoint-shared-service-side-by-side-upgrade-advisor.md)  
  
-   [호환 되지 않는 데이터베이스 엔진 서버 데이터 정렬 &#40;업그레이드 관리자&#41;](../../../2014/sql-server/install/incompatible-database-engine-server-collation-upgrade-advisor.md)  
  
-   [기타 Reporting Services 업그레이드 문제](../../../2014/sql-server/install/other-reporting-services-upgrade-issues.md)  
  
  
