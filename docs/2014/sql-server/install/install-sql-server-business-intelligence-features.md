---
title: SQL Server 2014 BI 기능 설치
ms.custom: ''
ms.prod: sql-server-2014
ms.reviewer: ''
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.date: 10/24/2018
ms.technology: install
ms.openlocfilehash: 93f362adfbc85500854943a479dac01988eb3a01
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952558"
---
# <a name="install-sql-server-2014-bi-features"></a>SQL Server 2014 BI 기능 설치

  Microsoft Business Intelligence 플랫폼에 속하는 SQL Server 기능에는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]및 분석 데이터를 만들거나 사용하는 데 사용되는 일부 클라이언트 애플리케이션이 포함됩니다. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 설명서 중 이 섹션에서는 이러한 기능을 설치하는 방법에 대해 설명합니다.  
  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 독립 실행형 서버로 설치하거나, 확장 구성으로 설치하거나, SharePoint 팜의 공유 서비스 애플리케이션으로 설치할 수 있습니다. 팜에 서비스를 설치하면 SharePoint에서만 사용 가능한 BI 기능을 사용할 수 있는데, 여기에는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 또는 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]의 테이블 형식 model 데이터베이스에서 실행되는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 의 임시 대화형 보고서 디자이너인 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 및 SharePoint용 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 이 포함됩니다.  
  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 또는 SharePoint용 PowerPivot의 설치 단계에 익숙한 경우 검사 목록으로 바로 이동하여 특정 시나리오를 사용하는 방법에 대한 지침을 확인할 수 있습니다. 자세한 내용은 [SharePoint를 사용 하 여 BI 기능을 설치 하기 위한 검사 목록](checklists-for-installing-bi-features-with-sharepoint.md)을 참조 하세요.  
  
## <a name="contents"></a>콘텐츠

이 섹션의 내용
  
|링크|Task|  
|----------|----------|  
|[SharePoint와 함께 SQL BI 기능을 설치하기 위한 검사 목록](checklists-for-installing-bi-features-with-sharepoint.md)|설치할 항목을 미리 알고 있고 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 또는 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]에 대한 설치 단계에 익숙한 경우 이 섹션의 검사 목록을 참조하여 설치 순서와 계정 및 권한 요구 사항 그리고 다중 서버 및 다중 기능 배포를 포함한 고급 토폴로지의 배포 단계를 확인할 수 있습니다.|  
|[SharePoint &#40;PowerPivot 및 Reporting Services를 사용 하 여 SQL Server BI 기능 설치&#41;](install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md)|이 섹션에서는 SharePoint 환경에 SQL Server 기능을 설치하는 방법에 대해 설명합니다. 여기에서는 SharePoint의 특정 버전 및 에디션에서 사용할 수 있는 SQL Server 기능을 설명하고 SharePoint용 PowerPivot 및 SharePoint 모드의 Reporting Services에 대한 설치 지침을 제공합니다.|  
|[다차원 및 데이터 마이닝 모드에서 Analysis Services 설치](install-analysis-services-in-multidimensional-and-data-mining-mode.md)<br /><br /> [테이블 형식 모드에서 Analysis Services 설치](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services)<br /><br /> [Data Quality Services 설치](../../data-quality-services/install-windows/install-data-quality-services.md)<br /><br /> [Integration Services 설치](../../integration-services/install-windows/install-integration-services.md)<br /><br /> [MDS(Master Data Services) 설치](../../master-data-services/install-windows/install-master-data-services.md)<br /><br /> [Reporting Services 기본 모드 보고서 서버 설치](../../reporting-services/install-windows/install-reporting-services-native-mode-report-server.md)|이 섹션에는 Analysis Services, Integration Services, Master Data Services 및 Reporting Services 설치 지침이 제공되며, 여기서 Analysis Services 및 Reporting Services는 SharePoint 없이 설치됩니다. 이를 *기본 모드*라고도 하며, Reporting Services 및 Analysis Services에 대 한 가장 일반적인 설치 시나리오입니다. 이 섹션에서는 서버의 작업 컨텍스트를 직접적으로 결정하는 설치 옵션에 대해 배웁니다. Reporting Services의 경우 이 서버는 사전 구성된 서버이거나 사용 전 여러 구성 단계가 필요할 수 있습니다. Analysis Services의 경우 선택한 설치 옵션에 따라 서버에 배포할 수 있는 프로젝트 유형이 결정됩니다.|  
|[SQL Server BI 기능 설치 확인 또는 문제 해결](../../../2014/sql-server/install/verify-or-troubleshoot-sql-server-bi-feature-installation-problems.md)|이 섹션에는 설치 확인을 위한 단계가 포함됩니다. 또한 웹에 대한 문제 해결 정보 링크를 제공합니다.|  
  
## <a name="related-content"></a>관련 콘텐츠  
  
|링크|Task|  
|----------|----------|  
|[SQL Server 2014로 업그레이드](../../database-engine/install-windows/upgrade-sql-server.md)<br /><br /> [Analysis Services 업그레이드](../../database-engine/install-windows/upgrade-analysis-services.md)<br /><br /> [SharePoint용 PowerPivot 업그레이드](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)<br /><br /> [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)|이 섹션의 지침에 따라 이전 버전에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 서버 및 콘텐츠를 업그레이드할 수 있습니다.|  
|[SQL Server 2014 제거](uninstall-sql-server.md)<br /><br /> [Uninstall PowerPivot for SharePoint](../../../2014/sql-server/install/uninstall-power-pivot-for-sharepoint.md)<br /><br /> [Reporting Services 제거](../../../2014/sql-server/install/uninstall-reporting-services.md)|이 섹션의 지침에 따라 BI 기능을 제거할 수 있습니다.|  
  
## <a name="see-also"></a>참고 항목

* [새로운 기능 &#40;Reporting Services&#41;](../../../2014/reporting-services/what-s-new-reporting-services.md)

* [Analysis Services 및 비즈니스 인텔리전스의 새로운 기능](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services)

* [SQL Server 2014 설치](../../database-engine/install-windows/install-sql-server.md)

* [SQL Server 2014로 업그레이드](../../database-engine/install-windows/upgrade-sql-server.md)
