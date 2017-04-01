---
title: "파티션 및 역할 배포 옵션 지정 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "입력 파일 [Analysis Services]"
  - "파티션 [Analysis Services], 배포 옵션"
  - "Analysis Services 배포, 역할"
  - "Analysis Services 배포, 파티션"
  - "Analysis Services 배포 마법사, 역할"
  - "Analysis Services 배포 마법사, 파티션"
  - "배포 [Analysis Services], 역할"
  - "역할 [Analysis Services], 배포 옵션"
  - "배포 [Analysis Services], 파티션"
  - "역할 배포 수정"
  - "파티션 배포 수정"
ms.assetid: e9b9ca57-a5cc-4fc0-87b5-305257038d56
caps.latest.revision: 37
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 파티션 및 역할 배포 옵션 지정
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사는 \<*프로젝트 이름*>.deploymentoptions 파일에서 파티션 및 역할 배포 옵션을 읽습니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 작성할 때 이 파일을 만듭니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 는 \<*프로젝트 이름*>.deploymentoptions 파일이 생성될 때 현재 프로젝트의 파티션 및 역할 배포 옵션을 사용합니다. 이러한 구성 설정에 대한 자세한 내용은 [Understanding the Input Files Used to Create the Deployment Script](../../analysis-services/multidimensional-models/understanding-the-input-files-used-to-create-the-deployment-script.md)를 참조하십시오.  
  
## 파티션 및 역할 배포 옵션 검토  
 \<*프로젝트 이름*>.deploymentoptions 파일의 배포 옵션에는 다음이 포함됩니다.  
  
 **파티션 배포 옵션**  
 \<*프로젝트 이름*>.deploymentoptions 파일은 대상 데이터베이스의 기존 파티션을 유지하거나 덮어쓸지(기본값) 여부를 지정합니다. 기존 파티션을 유지하는 경우 새 파티션만 배포되고 기존의 모든 측정값 그룹에 있는 파티션 및 집계 디자인은 변경되지 않습니다.  
  
> [!NOTE]  
>  파티션이 존재하는 측정값 그룹이 삭제되면 파티션이 자동으로 삭제됩니다.  
  
 **역할 배포 옵션**  
 \<*프로젝트 이름*>.deploymentoptions 파일은 다음 역할 배포 옵션 중 하나를 지정합니다.  
  
-   대상 데이터베이스의 기존 역할 및 역할 멤버는 유지되고 새로운 역할 및 역할 멤버만 배포됩니다.  
  
-   대상 데이터베이스의 모든 기존 역할 및 멤버가 배포되는 역할 및 멤버로 교체됩니다.  
  
-   대상 데이터베이스의 기존 역할 및 역할 멤버가 유지되고 새 역할이 배포되지 않습니다.  
  
-   **참고** 기존 역할과 멤버가 보존되는 경우 해당 역할과 관련된 권한은 없음으로 다시 설정됩니다. 보안 권한은 관련된 보안 역할이 아닌 보안을 설정하는 개체에 포함됩니다. Analysis Service 배포 마법사를 사용하여 이 동작과 작업하는 방법은 Microsoft 기술 자료 문서인 '역할 및 멤버 유지(Retain Roles and Members)'를 참조하십시오.  
  
## 파티션 및 역할 배포 옵션 수정  
 \<*프로젝트 이름*>.deploymentoptions 파일에 저장된 것과 다른 파티션 및 역할 옵션을 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 배포해야 할 수 있습니다. 예를 들어 \<*프로젝트 이름*>.deploymentoptions 파일에 표시된 대로 모든 기존 파티션, 역할 및 멤버를 교체하는 대신 기존 파티션, 역할 및 멤버를 유지할 수 있습니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에서 파티션 및 역할 배포를 수정하려는 경우 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 *\<프로젝트 이름>* **속성 페이지** 대화 상자에 이러한 옵션이 표시되지 않기 때문에 프로젝트 내에서 파티션 및 역할 설정을 변경할 수 없습니다. 역할 및 파티션에 대한 배포 옵션을 변경하려면 \<*프로젝트 이름*>.deploymentoptions 파일 자체에서 이 정보를 변경해야 합니다. 다음 절차에서는 \<*프로젝트 이름*>.deploymentoptions 파일 내에서 파티션 및 역할 배포 옵션을 변경하는 방법에 대해 설명합니다.  
  
#### 입력 파일을 생성한 다음 파티션 또는 역할 배포를 변경하려면  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사를 대화식으로 실행하고 **파티션 및 역할 배포 옵션** 페이지에서 파티션 및 역할에 대한 새 배포 옵션을 지정합니다.  
  
     —또는—  
  
-   명령 프롬프트에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사를 실행하여 응답 파일 모드에서 마법사를 실행하도록 설정합니다. 응답 파일 모드에 대한 자세한 내용은 [Analysis Services 배포 마법사 실행](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)을 참조하세요.  
  
     —또는—  
  
-   임의의 텍스트 편집기에서 \<*프로젝트 이름*>.deploymentoptions를 열고 옵션을 직접 변경합니다.  
  
## 관련 항목:  
 [설치 대상 지정](../../analysis-services/multidimensional-models/specifying-the-installation-target.md)   
 [솔루션 배포를 위한 구성 설정 지정](../../analysis-services/multidimensional-models/specifying-configuration-settings-for-solution-deployment.md)   
 [처리 옵션 지정](../../analysis-services/multidimensional-models/specifying-processing-options.md)  
  
  