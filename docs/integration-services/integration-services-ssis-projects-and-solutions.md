---
title: "Integration Services(SSIS) 프로젝트 및 솔루션 | Microsoft Docs"
ms.custom: ""
ms.date: "08/24/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.importprojectwizard.f1"
helpviewer_keywords: 
  - "프로젝트 [Integration Services], 만들기"
  - "폴더 [Integration Services], 프로젝트"
  - "파일 [Integration Services], 프로젝트"
  - "폴더 [Integration Services]"
  - "프로젝트 [Integration Services], 프로젝트 정보"
ms.assetid: 28ea8120-0a79-4029-93f0-07d521b32bee
caps.latest.revision: 63
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 62
---
# Integration Services(SSIS) 프로젝트 및 솔루션
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 패키지 개발을 위해 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 를 제공합니다.  
  
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스 또는 [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지 저장소에 패키지를 배포하는 경우 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스를 사용하여 패키지를 관리합니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스는 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서만 사용할 수 있습니다. 서비스에 대한 자세한 내용은 [Integration Services 서비스&#40;SSIS 서비스&#41;](../integration-services/service/integration-services-service-ssis-service.md)를 참조하세요. 패키지 배포에 대한 자세한 내용은 [레거시 패키지 배포&#40;SSIS&#41;](../integration-services/packages/legacy-package-deployment-ssis.md)를 참조하세요.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버에 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 배포하는 경우 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 Transact-SQL 뷰 및 저장 프로시저를 사용하여 프로젝트를 관리합니다. 프로젝트 배포에 대한 자세한 내용은 [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx)를 참조하십시오. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]서버에 대한 자세한 내용은 [Integration Services&#40;SSIS&#41; 서버](https://msdn.microsoft.com/library/ms137731.aspx)를 참조하세요.  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 및 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에 대한 개요는 [Integration Services&#40;SSIS&#41; 및 관리 도구](https://msdn.microsoft.com/library/ms140028.aspx)%20및%20Studio%20Environments.md)을 참조하세요.  
  
## Integration Services 프로젝트는 패키지를 포함합니다.  
 프로젝트는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 개발하는 컨테이너입니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트는 패키지와 관련된 파일을 저장하고 그룹화합니다. 예를 들어 특정 ETL(추출, 변환 및 로드) 솔루션을 만드는 데 필요한 파일이 프로젝트에 포함됩니다.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 만들려면 먼저 이러한 종류의 프로젝트에 포함되는 기본 내용에 대해 잘 알고 있어야 합니다. 프로젝트에 포함되는 내용을 이해한 후에는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 만들고 사용할 수 있습니다.  
  
## Integration Services 프로젝트의 폴더  
 다음 다이어그램은 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 의 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]프로젝트에 있는 폴더를 보여 줍니다.  
  
 ![Integration Services 프로젝트의 폴더](../integration-services/media/solutionexplorer.gif "Integration Services 프로젝트의 폴더")  
  
 다음 표에서는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트에 표시되는 폴더에 대해 설명합니다.  
  
|Folder|Description|  
|------------|-----------------|  
|[!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지|패키지가 포함됩니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 패키지](../integration-services/integration-services-ssis-packages.md)를 참조하세요.|  
|기타|패키지 파일 이외의 파일을 포함합니다.|  
  
## Integration Services 프로젝트의 파일  
 신규 또는 기존 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 솔루션에 추가하면 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 에서 확장명이 .dtproj, .dtproj.user 및 .database인 프로젝트 파일이 생성됩니다.  
  
-   *.dtproj 파일에는 패키지와 같은 프로젝트 구성 및 항목에 대한 정보가 포함됩니다.  
  
-   *.dtproj.user 파일에는 프로젝트를 사용하기 위한 기본 설정에 대한 정보가 포함됩니다.  
  
-   *.database 파일에는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 여는 데 필요한 정보가 포함됩니다.  
  
## Integration Services 프로젝트의 버전 대상 지정  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 SQL Server 2016, SQL Server 2014 또는 SQL Server 2012를 대상으로하는 패키지를 만들고, 유지 관리하고 실행할 수 있습니다.  
  
 솔루션 탐색기에서 Integration Services 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택하여 프로젝트에 대한 속성 페이지를 엽니다. **구성 속성** 의 **일반**탭에서 **TargetServerVersion** 속성을 선택하고 SQL Server 2016, SQL Server 2014 또는 SQL Server 2012를 선택합니다.  
  
 ![TargetServerVersion property in project properties dialog box](../integration-services/media/targetserverversion2.png "TargetServerVersion property in project properties dialog box")  
  
## 솔루션은 프로젝트를 포함합니다.  
 솔루션은 종단 간 비즈니스 솔루션을 개발할 때 사용되는 프로젝트를 그룹화 및 관리하는 컨테이너입니다. 솔루션을 사용하면 여러 프로젝트를 하나의 단위로 취급하고 비즈니스 솔루션에 관련된 하나 이상의 관련 프로젝트를 하나로 묶을 수 있습니다.  
  
 솔루션에는 여러 형식의 프로젝트가 포함될 수 있습니다. [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너를 사용하여 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 만들려면 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 제공하는 솔루션의 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]프로젝트를 사용합니다.  
  
 새 솔루션을 만들 때 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 는 솔루션 탐색기에 솔루션 폴더를 추가하고 확장명이 .sln 및 .suo인 파일을 만듭니다.  
  
-   *.sln 파일에는 솔루션 구성에 대한 정보가 포함되고 솔루션의 프로젝트가 나열됩니다.  
  
-   *.suo 파일에는 솔루션을 사용하기 위한 기본 설정에 대한 정보가 포함됩니다.  
  
 새 프로젝트를 만들면 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 에서 솔루션이 자동으로 생성되지만 빈 솔루션을 만든 다음 프로젝트를 나중에 추가할 수도 있습니다.  
  
> **참고**: 기본적으로 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 새 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 만들 때는 **프로젝트 탐색기** 창에 솔루션이 표시되지 않습니다. 이 기본 동작을 변경하려면 **도구** 메뉴에서 **옵션**을 클릭합니다. **옵션** 대화 상자에서 **프로젝트 및 솔루션**을 확장한 다음 **일반**을 선택합니다. **일반** 페이지에서 **솔루션 항상 표시**를 선택합니다.  
  
## 관련 작업  
 [솔루션에서 Integration Services 프로젝트 추가 또는 제거](../Topic/Add%20or%20Remove%20an%20Integration%20Services%20Project%20in%20a%20Solution.md)  
  
 [새 Integration Services 프로젝트 만들기](../Topic/Create%20a%20New%20Integration%20Services%20Project.md)  
  
 [Integration Services 프로젝트에 항목 추가](../Topic/Add%20an%20Item%20to%20an%20Integration%20Services%20Project.md)  
  
 [프로젝트 항목 복사](../Topic/Copy%20Project%20Items.md)  
  
## 관련 내용  
 [Integration Services 프로젝트 배포](../Topic/Development%20of%20an%20Integration%20Services%20Project.md)  
  
  