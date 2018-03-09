---
title: "BI용 SQL Server Management Studio 소개 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Management Studio for Integration Services
- SQL Server Management Studio for Reporting Services
- SQL Server Management Studio for Analysis Services
ms.assetid: ffaa77b7-03d0-4d7a-aa42-c5091a4f2ceb
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4fc26ef0feb4ff86087bd0ddc571299621207464
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="introduction-to-sql-server-management-studio-for-business-intelligence"></a>비즈니스 인텔리전스용 SQL Server Management Studio 소개
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)], [!INCLUDE[ssISnoversion](../includes/ssisnoversion_md.md)] 및 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion_md.md)]를 액세스, 구성 및 관리하려면 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)]를 사용합니다. 3가지 비즈니스 인텔리전스 기술 모두 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)]에 의존하지만 각 기술과 관련된 관리 태스크는 약간씩 다릅니다.  
  
> [!NOTE]  
> [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion_md.md)]및 [!INCLUDE[ssISnoversion](../includes/ssisnoversion_md.md)] 솔루션은 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull_md.md)]가 아닌 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)]를 사용하여 만들고 수정합니다. [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull_md.md)][!INCLUDE[msCoName](../includes/msconame_md.md)][!INCLUDE[vsprvs](../includes/vsprvs_md.md)]기반의 개발 환경입니다.  
  
## <a name="managing-analysis-services-solutions-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 Analysis Services 솔루션 관리  
[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 개체를 관리할 수 있습니다. 예를 들어 백업을 수행하고 개체를 처리할 수 있습니다.  
  
[!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] MDX(Multidimensional Expressions), DMX(Data Mining Extensions) 및 XMLA(XML for Analysis)로 작성된 스크립트를 개발 및 저장할 수 있는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 스크립트 프로젝트를 제공합니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 스크립트 프로젝트를 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 인스턴스에서 관리 태스크를 수행하거나 데이터베이스 및 큐브와 같은 개체를 다시 만들 수 있습니다. 예를 들어 기존 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 인스턴스에 직접 새 개체를 만드는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 스크립트 프로젝트에서 XMLA 스크립트를 개발할 수 있습니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 스크립트 프로젝트는 솔루션의 일부로 저장되어 원본 코드 제어와 함께 통합될 수 있습니다.  
  
[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)]를 사용하는 방법에 대한 자세한 내용은 [SQL Server Management Studio를 사용한 개발 및 구현](http://msdn.microsoft.com/en-us/c4f5a06b-e2e4-4660-a3a8-6fd356742c02)을 참조하세요.  
  
## <a name="managing-integration-services-solutions-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 Integration Services 솔루션 관리  
[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion_md.md)] 서비스를 사용하여 패키지를 관리하고 실행 중인 패키지를 모니터링할 수 있습니다. 또한 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 를 사용하여 패키지를 폴더로 구성하고 패키지를 실행하고 패키지를 가져오거나 내보내고 DTS(데이터 변환 서비스) 패키지를 마이그레이션하고 [!INCLUDE[ssISnoversion](../includes/ssisnoversion_md.md)] 패키지를 업그레이드할 수 있습니다.  
  
## <a name="managing-reporting-services-projects-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 Reporting Services 프로젝트 관리  
SQL Server Management Studio를 사용하여 Reporting Services 기능을 활성화하고 서버 및 데이터베이스를 관리하고 역할 및 작업을 관리할 수 있습니다.  
  
공유 일정 폴더를 사용하여 공유 일정을 관리하고 보고서 서버 데이터베이스(ReportServer, ReportServerTempdb)를 관리할 수 있습니다. 또한 보고서 서버 데이터베이스를 새로운 또는 다른 SQL Server 데이터베이스 엔진([!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] [!INCLUDE[ssDE](../includes/ssde_md.md)])으로 이동할 때 Master 시스템 데이터베이스에서 RSExecRole을 만듭니다. 이러한 태스크에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [Management Studio 방법 도움말 항목](http://msdn.microsoft.com/en-us/60685458-9108-47bf-820a-5e7db454d408)  
  
-   [보고서 서버 데이터베이스 관리](http://msdn.microsoft.com/en-us/97b2e1b5-3869-4766-97b9-9bf206b52262)  
  
-   [방법: RSExecRole 만들기](http://msdn.microsoft.com/en-us/7ac17341-df7e-4401-870e-652caa2859c0)  
  
다양한 기능을 설정 및 구성하고 서버 기본값을 설정하고 역할 및 작업을 관리함으로써 서버를 관리할 수도 있습니다. 이러한 태스크에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [방법: 보고서 서버 속성 설정(Management Studio)](http://msdn.microsoft.com/en-us/1ed0f84b-b12a-4e49-b65c-a11a99f9093f)  
  
-   [방법: 역할 만들기, 삭제 또는 수정(Management Studio)](http://msdn.microsoft.com/en-us/3d1d56e6-a283-44a7-8417-36cb4d2c74d1)  
  
-   [Reporting Services에 대한 클라이언트 쪽 인쇄 기능 설정 및 해제](http://msdn.microsoft.com/en-us/0e709c96-7517-4547-8ef6-5632f8118524)  
  
## <a name="see-also"></a>참고 항목  
[SQL Server Data Tools를 사용한 개발 및 구현](http://msdn.microsoft.com/en-us/132ed779-3ec8-4734-9698-802116d1b017)  
[SQL Server Data Tools의 Reporting Services](http://msdn.microsoft.com/en-us/0903c7b2-ac59-45f1-b7d0-922ecd9d76f8)  
  
