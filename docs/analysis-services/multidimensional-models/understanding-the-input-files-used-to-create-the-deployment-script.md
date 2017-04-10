---
title: "배포 스크립트를 만드는 데 사용하는 입력 파일 이해 | Microsoft Docs"
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
  - "Analysis Services 배포 마법사, 스크립트"
  - "배포 [Analysis Services], 입력 파일"
  - "Analysis Services 배포 마법사, 입력 파일"
  - "스크립트 [Analysis Services], 배포"
  - "Analysis Services 배포, 입력 파일"
  - "입력 파일 수정"
ms.assetid: 20e080cd-6a0e-4591-b022-ea4cd3638e36
caps.latest.revision: 34
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 배포 스크립트를 만드는 데 사용하는 입력 파일 이해
   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 만들 때 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 는 프로젝트에 대한 XML 파일을 생성합니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 는 이러한 XML 파일을 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트의 Output 폴더에 저장합니다. 기본 결과는 \\Bin 폴더에 출력됩니다. 다음 표에서는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 만드는 XML 파일을 나열합니다.  
  
|XMLA 파일|Description|  
|---------------|-----------------|  
|\<*project name*\>.asdatabase|프로젝트의 모든 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체에 대한 선언적 정의가 포함됩니다.|  
|\<*project name*\>.deploymenttargets|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체가 생성되는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 및 데이터베이스의 이름이 포함됩니다.|  
|\<*project name*\>.configsettings|데이터 원본 연결 정보 및 개체 저장 위치와 같은 환경 관련 설정이 포함됩니다. 이 파일의 설정은 \<*project name*\>.asdatabase 파일의 설정을 무시합니다.|  
|\<*project name*\>.deploymentoptions|배포가 트랜잭션인지 여부와 배포된 개체가 배포 후 처리되어야 하는지 여부와 같은 배포 옵션이 포함됩니다.|  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 는 해당 프로젝트 파일에 암호를 저장하지 않습니다.  
  
## 입력 파일 수정  
 입력 파일의 값이나 입력 파일에서 검색한 값을 수정하면 전체 \<*project name*\>.asdatabase 파일 \(또는 기존 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스로\)부터 스크립트를 생성하는 경우 전체 XMLA 스크립트 파일을 편집하지 않고 배포 대상, 구성 설정 및 배포 옵션을 변경할 수 있습니다. 개별 파일을 수정할 수 있으면 다른 용도의 다른 배포 스크립트를 쉽게 만들 수 있습니다.  
  
 다음 항목에서는 여러 입력 파일에서 값을 수정하는 방법을 설명합니다.  
  
-   [설치 대상 지정](../../analysis-services/multidimensional-models/specifying-the-installation-target.md)  
  
-   [파티션 및 역할 배포 옵션 지정](../../analysis-services/multidimensional-models/specifying-partition-and-role-deployment-options.md)  
  
-   [솔루션 배포를 위한 구성 설정 지정](../../analysis-services/multidimensional-models/specifying-configuration-settings-for-solution-deployment.md)  
  
-   [처리 옵션 지정](../../analysis-services/multidimensional-models/specifying-processing-options.md)  
  
## 참고 항목  
 [Analysis Services 배포 마법사 실행](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)   
 [Analysis Services 배포 스크립트 이해](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)  
  
  