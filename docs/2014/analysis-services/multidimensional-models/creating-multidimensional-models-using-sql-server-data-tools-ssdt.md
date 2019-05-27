---
title: 다차원 모델을 만들를 사용 하 여 SQL Server Data Tools (SSDT) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SSAS, environments
- Analysis Services, development
- SQL Server Analysis Services, environments
- projects [Analysis Services]
- solutions [Analysis Services]
ms.assetid: 132ed779-3ec8-4734-9698-802116d1b017
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 915ce0ebc6ff9ecd68647deb1653bfab0e1c956d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66076164"
---
# <a name="creating-multidimensional-models-using-sql-server-data-tools-ssdt"></a>SSDT(SQL Server Data Tools)를 사용하여 다차원 모델 만들기
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 솔루션 작성, 배포 및 관리를 위해 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 및 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]라는 두 가지 다른 환경을 제공합니다. 이러한 환경은 둘 다 프로젝트 시스템을 구현합니다. Visual Studio 프로젝트에 대한 자세한 내용은 MSDN Library의 [프로젝트의 컨테이너 특성(Projects as Containers)](https://go.microsoft.com/fwlink/?LinkId=63960) 을 참조하십시오.  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio 2010을 기반으로 비즈니스 인텔리전스 솔루션을 만들고 수정하는 데 사용되는 개발 환경입니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체(큐브, 차원 등)의 정의를 포함하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 만들 수 있습니다. 이러한 프로젝트는 ASSL( [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Scripting Language) 요소를 포함하는 XML 파일에 저장됩니다. 이러한 프로젝트는 다른 프로젝트도 포함할 수 있는 솔루션에 포함 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 등의 구성 요소 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]합니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서는 특정 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스와 무관한 솔루션의 일부로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 개발할 수 있습니다. 개발 중 테스트하기 위해 테스트 서버에 있는 인스턴스로 개체를 배포한 다음 동일한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 사용하여 하나 이상의 준비 서버나 프로덕션 서버에 있는 인스턴스로 개체를 배포할 수 있습니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 가 포함된 솔루션의 프로젝트와 항목을 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual SourceSafe와 같은 원본 코드 제어와 통합할 수 있습니다. 만들기에 대 한 자세한 내용은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 를 사용 하 여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 참조 하십시오 [Analysis Services 프로젝트 만들기 &#40;SSDT&#41;](create-an-analysis-services-project-ssdt.md). 또한 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 를 사용하여 기존 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 직접 연결하면 프로젝트를 사용하거나 개체 정의를 XML 파일에 저장하지 않고도 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체를 만들고 수정할 수도 있습니다. 자세한 내용은 [다차원 model 데이터베이스&#40;SSAS&#41;](multidimensional-model-databases-ssas.md)및 [온라인 모드로 Analysis Services 데이터베이스에 연결](connect-in-online-mode-to-an-analysis-services-database.md)라는 두 가지 다른 환경을 제공합니다.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 관리 환경으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]인스턴스 관리에 주로 사용됩니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체 백업 또는 처리 등의 관리 작업을 수행할 수 있으며 XMLA 스크립트를 사용하여 기존 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 직접 새 개체를 만들 수도 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서는 MDX(Multidimensional Expressions), DMX(Data Mining Extensions) 및 XMLA(XML for Analysis)로 작성된 스크립트를 개발하고 저장할 수 있는 Analysis Server Scripts 프로젝트를 제공합니다. 일반적으로 Analysis Server Scripts 프로젝트는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서 데이터베이스 및 큐브와 같은 개체를 다시 만들거나 관리 태스크를 수행하는 데 사용됩니다. 이러한 프로젝트는 솔루션의 일부로 저장되어 원본 코드 제어와 함께 통합될 수 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 Analysis Server Scripts 프로젝트를 만드는 방법에 대한 자세한 내용은 [SQL Server Management Studio의 Analysis Services 스크립트 프로젝트](../instances/analysis-services-scripts-project-in-sql-server-management-studio.md)를 참조하세요.  
  
## <a name="introducing-solutions-projects-and-items"></a>솔루션, 프로젝트 및 항목 소개  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 및 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 프로젝트를 제공하고 이러한 프로젝트가 다시 솔루션으로 구성됩니다. 한 솔루션에 여러 개의 프로젝트가 포함될 수 있으며 각 프로젝트는 일반적으로 여러 개의 항목을 포함합니다. 프로젝트를 만들면 자동으로 새 솔루션이 생성되며 필요한 경우 기존 솔루션에 다른 프로젝트를 추가할 수 있습니다. 프로젝트에 포함되는 개체는 프로젝트 유형에 따라 달라집니다. 각 프로젝트 컨테이너의 항목은 파일 시스템의 프로젝트 폴더에 파일로 저장됩니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 의 비즈니스 인텔리전스 프로젝트 유형에는 다음 프로젝트가 포함되어 있습니다.  
  
|프로젝트|Description|  
|-------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트|단일 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 대한 개체 정의를 포함합니다. 만드는 방법에 대 한 자세한 정보에 대 한는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 참조 하십시오 [Analysis Services 프로젝트 만들기 &#40;SSDT&#41;](create-an-analysis-services-project-ssdt.md)합니다.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 2008 데이터베이스 가져오기|기존 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에서 개체 정의를 가져와서 새 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 만드는 데 사용할 수 있는 마법사를 제공합니다.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 집합에 대한 개체 정의를 포함합니다. 자세한 내용은 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)를 참조하세요.|  
|보고서 프로젝트 마법사|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 사용하여 보고서 프로젝트를 만드는 과정을 안내하는 마법사를 제공합니다. 자세한 내용은 [Reporting Services&#40;SSRS&#41;](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)를 참조하세요.|  
|보고서 모델 프로젝트|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 모델에 대한 개체 정의를 포함합니다. 자세한 내용은 [Reporting Services&#40;SSRS&#41;](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)를 참조하세요.|  
|보고서 서버 프로젝트|하나 이상의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서에 대한 개체 정의를 포함합니다. 자세한 내용은 [Reporting Services&#40;SSRS&#41;](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)를 참조하세요.|  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에는 다음 표에 나와 있는 것처럼 다양한 쿼리나 스크립트에 중점을 둔 여러 프로젝트 유형이 포함되어 있습니다.  
  
|프로젝트|Description|  
|-------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 스크립트|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 대한 DMX, MDX 및 XMLA 스크립트와 이러한 스크립트를 실행할 수 있는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 연결을 포함합니다. 자세한 내용은 [SQL Server Management Studio의 Analysis Services 스크립트 프로젝트](../instances/analysis-services-scripts-project-in-sql-server-management-studio.md)를 참조하세요.|  
|SQL Server Compact 스크립트|SQL Server Compact용 SQL 스크립트와 이러한 스크립트를 실행할 수 있는 SQL Server Compact 인스턴스에 대한 연결을 포함합니다.|  
|SQL Server 스크립트|[!INCLUDE[tsql](../../includes/tsql-md.md)] 인스턴스에 대한 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 및 XQuery 스크립트와 이러한 스크립트를 실행할 수 있는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스에 대한 연결을 포함합니다. 자세한 내용은 [SQL Server Database Engine](../../database-engine/sql-server-database-engine-overview.md)을(를) 참조하세요.|  
  
 솔루션 및 프로젝트에 대한 자세한 내용은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] .NET 설명서 또는 MSDN Library의 "솔루션, 프로젝트 및 파일 관리"를 참조하십시오.  
  
## <a name="choosing-between-sql-server-management-studio-and-sql-server-data-tools"></a>SQL Server Management Studio 및 SQL Server Data Tools 중에서 선택  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 기존 개체를 관리하고 구성하기 위해 디자인되었으며, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 기능을 포함하는 비즈니스 인텔리전스 솔루션을 개발하기 위해 디자인되었습니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 와 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 차이점은 다음과 같습니다.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 의 인스턴스에 연결하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스 내의 개체를 구성 및 관리하기 위한 통합 환경을 제공합니다. 스크립트를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체 자체를 만들거나 수정할 수도 있지만 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서는 개체 디자인 및 정의를 위한 그래픽 인터페이스를 제공하지 않습니다.  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 는 비즈니스 인텔리전스 솔루션 개발을 위한 통합 개발 환경을 제공합니다. 프로젝트 및 솔루션에 포함된 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] , [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]및 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]개체의 XML 기반 정의를 사용하는 프로젝트 모드의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 사용할 수 있습니다. 프로젝트 모드로 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 를 사용하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서의 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 개체 변경 내용이 이러한 XML 기반 개체 정의에 적용되고 솔루션이 배포될 때까지 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 개체에 직접 적용되지 않습니다. 온라인 모드로 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 를 사용할 수도 있습니다. 이 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 직접 연결하여 기존 데이터베이스의 개체로 작업합니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 를 사용하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 활성 연결이 없어도 원본 제어 다중 사용자 환경에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 사용할 수 있으므로 비즈니스 인텔리전스 애플리케이션 개발이 향상됩니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 쿼리 및 테스트를 위해 기존 개체에 대한 직접 액세스를 제공하며 이전에 스크립팅된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 더 빨리 구현하는 데 사용할 수 있습니다. 그러나 프로젝트가 프로덕션 환경에 배포된 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 및 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]데이터베이스와 해당 개체를 사용할 때 주의해야 합니다. 이는 기존 데이터베이스의 개체에 대한 직접 변경 내용과 원래 배포 솔루션을 생성한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트의 변경 내용을 덮어쓰는 것을 방지하기 위한 것입니다. 자세한 내용은 [개발 단계 중의 Analysis Services 프로젝트 및 데이터베이스 작업](work-with-analysis-services-projects-and-databases-in-development.md)및 [프로덕션 환경에서 Analysis Services 프로젝트 및 데이터베이스 작업](work-with-analysis-services-projects-and-databases-in-production.md)을 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [Analysis Services 프로젝트 만들기&#40;SSDT&#41;](create-an-analysis-services-project-ssdt.md)  
  
-   [Analysis Services 프로젝트 속성 구성&#40;SSDT&#41;](configure-analysis-services-project-properties-ssdt.md)  
  
-   [Analysis Services 프로젝트 빌드&#40;SSDT&#41;](build-analysis-services-projects-ssdt.md)  
  
-   [Analysis Services 프로젝트 배포&#40;SSDT&#41;](deploy-analysis-services-projects-ssdt.md)  
  
-   [개발 단계 중의 Analysis Services 프로젝트 및 데이터베이스 작업](work-with-analysis-services-projects-and-databases-in-development.md)  
  
-   [프로덕션 환경에서 Analysis Services 프로젝트 및 데이터베이스 작업](work-with-analysis-services-projects-and-databases-in-production.md)  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 프로젝트 만들기&#40;SSDT&#41;](create-an-analysis-services-project-ssdt.md)   
 [SQL Server Management Studio의 Analysis Services 스크립트 프로젝트](../instances/analysis-services-scripts-project-in-sql-server-management-studio.md)   
 [다차원 model 데이터베이스&#40;SSAS&#41;](multidimensional-model-databases-ssas.md)  
  
  
