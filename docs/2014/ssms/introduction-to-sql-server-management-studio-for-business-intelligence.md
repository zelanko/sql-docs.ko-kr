---
title: Business Intelligence 용 SQL Server Management Studio 소개 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio for Integration Services
- SQL Server Management Studio for Reporting Services
- SQL Server Management Studio for Analysis Services
ms.assetid: ffaa77b7-03d0-4d7a-aa42-c5091a4f2ceb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 435bd85fd024ff8e302cdb91f63c8cbfa02ebb9e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48152698"
---
# <a name="introduction-to-sql-server-management-studio-for-business-intelligence"></a>비즈니스 인텔리전스용 SQL Server Management Studio 소개
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 및 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]를 액세스, 구성 및 관리하려면 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 사용합니다. 3가지 비즈니스 인텔리전스 기술 모두 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에 의존하지만 각 기술과 관련된 관리 태스크는 약간씩 다릅니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]및 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 솔루션은 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]가 아닌 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 사용하여 만들고 수정합니다. [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)][!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[vsprvs](../includes/vsprvs-md.md)]기반의 개발 환경입니다.  
  
## <a name="managing-analysis-services-solutions-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 Analysis Services 솔루션 관리  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 개체를 관리할 수 있습니다. 예를 들어 백업을 수행하고 개체를 처리할 수 있습니다.  
  
 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] MDX(Multidimensional Expressions), DMX(Data Mining Extensions) 및 XMLA(XML for Analysis)로 작성된 스크립트를 개발 및 저장할 수 있는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 스크립트 프로젝트를 제공합니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 스크립트 프로젝트를 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에서 관리 태스크를 수행하거나 데이터베이스 및 큐브와 같은 개체를 다시 만들 수 있습니다. 예를 들어 기존 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 직접 새 개체를 만드는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 스크립트 프로젝트에서 XMLA 스크립트를 개발할 수 있습니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 스크립트 프로젝트는 솔루션의 일부로 저장되어 원본 코드 제어와 함께 통합될 수 있습니다.  
  
 사용 하는 방법에 대 한 자세한 내용은 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 참조 하세요 [SQL Server Management Studio의 Analysis Services 스크립트 프로젝트](../analysis-services/instances/analysis-services-scripts-project-in-sql-server-management-studio.md)합니다.  
  
## <a name="managing-integration-services-solutions-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 Integration Services 솔루션 관리  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스를 사용하여 패키지를 관리하고 실행 중인 패키지를 모니터링할 수 있습니다. 또한 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 를 사용하여 패키지를 폴더로 구성하고 패키지를 실행하고 패키지를 가져오거나 내보내고 DTS(데이터 변환 서비스) 패키지를 마이그레이션하고 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 업그레이드할 수 있습니다.  
  
## <a name="managing-reporting-services-projects-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 Reporting Services 프로젝트 관리  
 SQL Server Management Studio를 사용하여 Reporting Services 기능을 활성화하고 서버 및 데이터베이스를 관리하고 역할 및 작업을 관리할 수 있습니다.  
  
 공유 일정 폴더를 사용하여 공유 일정을 관리하고 보고서 서버 데이터베이스(ReportServer, ReportServerTempdb)를 관리할 수 있습니다. 또한 보고서 서버 데이터베이스를 새로운 또는 다른 SQL Server 데이터베이스 엔진([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)])으로 이동할 때 Master 시스템 데이터베이스에서 RSExecRole을 만듭니다. 이러한 태스크에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [SQL Server Management Studio의 Reporting Services&#40;SSRS&#41;](../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md)  
  
-   [보고서 서버 데이터베이스 관리 &#40;SSRS 기본 모드&#41;](../reporting-services/report-server/report-server-database-ssrs-native-mode.md)  
  
-   [RSExecRole 만들기](../reporting-services/security/create-the-rsexecrole.md)  
  
 다양한 기능을 설정 및 구성하고 서버 기본값을 설정하고 역할 및 작업을 관리함으로써 서버를 관리할 수도 있습니다. 이러한 태스크에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [보고서 서버 속성 설정 &#40;Management Studio&#41;](../reporting-services/tools/set-report-server-properties-management-studio.md)  
  
-   [만들기, 삭제 또는 역할을 수정 &#40;Management Studio&#41;](../reporting-services/security/role-definitions-create-delete-or-modify.md)  
  
-   [Reporting Services에 대한 클라이언트 쪽 인쇄 기능 사용 및 사용 안 함 설정](../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)  
  
## <a name="see-also"></a>관련 항목  
 [다차원 모델을 만들 SQL Server Data Tools를 사용 하 여 &#40;SSDT&#41;](../analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)   
 [SQL Server Data Tools의 reporting Services &#40;SSDT&#41;](../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md)  
  
  
