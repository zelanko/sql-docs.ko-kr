---
title: "배포 스크립트를 만드는 데 입력된 파일 이해 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- input files [Analysis Services]
- Analysis Services Deployment Wizard, scripts
- deploying [Analysis Services], input files
- Analysis Services Deployment Wizard, input files
- scripts [Analysis Services], deployment
- Analysis Services deployments, input files
- modifying input files
ms.assetid: 20e080cd-6a0e-4591-b022-ea4cd3638e36
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 84106e3dcb54700770d8441d78634767feb5b9da
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="deployment-script-files---input-used-to-create-deployment-script"></a>배포 스크립트 파일-입력은 배포 스크립트를 만드는 데 사용
  작성 하는 경우는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 프로젝트 파일을 생성 합니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]이러한 파일의 출력 폴더에 배치 된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트. 기본 결과는 \Bin 폴더에 출력됩니다. 다음 표에서는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 만드는 XML 파일을 나열합니다.  
  
|파일|Description|  
|---------------|-----------------|  
|\<*프로젝트 이름을*>.asdatabase|다차원 또는 1100/1103 테이블 형식 모델 프로젝트에 대 한 XMLA 파일 또는 테이블 형식 1200 모델을 더 높은 프로젝트에 대 한 JSON 파일입니다. 프로젝트의 모든 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체에 대한 선언적 정의가 포함됩니다.|  
|\<*프로젝트 이름을*>.deploymenttargets|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체가 생성되는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 및 데이터베이스의 이름이 포함됩니다.|  
|\<*프로젝트 이름을*>.configsettings|데이터 원본 연결 정보 및 개체 저장 위치와 같은 환경 관련 설정이 포함됩니다. 이 파일의 설정은의 설정을 재정의 \< *프로젝트 이름을*>.asdatabase 파일입니다.|  
|\<*프로젝트 이름을*>.deploymentoptions|배포가 트랜잭션인지 여부와 배포된 개체가 배포 후 처리되어야 하는지 여부와 같은 배포 옵션이 포함됩니다.|  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]는 해당 프로젝트 파일에 암호를 저장하지 않습니다.  
  
## <a name="modifying-the-input-files"></a>입력 파일 수정  
 전체를 편집 하지 않고 배포 옵션 및 배포 대상, 구성 설정을 변경할 수 있도록 입력된 파일에서 검색 된 값 이나 입력된 파일에서 값을 수정 \< *프로젝트 이름*>.asdatabase 파일 (또는 기존 스크립트를 생성 하는 경우 전체 스크립트 파일 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스). 개별 파일을 수정할 수 있으면 다른 용도의 다른 배포 스크립트를 쉽게 만들 수 있습니다.  
  
 다음 항목에서는 여러 입력 파일에서 값을 수정하는 방법을 설명합니다.  
  
-   [설치 대상 지정](../../analysis-services/multidimensional-models/deployment-script-files-specifying-the-installation-target.md)  
  
-   [파티션 및 역할 배포 옵션 지정](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md)  
  
-   [솔루션 배포를 위한 구성 설정 지정](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)  
  
-   [처리 옵션 지정](../../analysis-services/multidimensional-models/deployment-script-files-specifying-processing-options.md)  
  
## <a name="see-also"></a>참고 항목  
 [Analysis Services 배포 마법사 실행](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)   
 [Analysis Services 배포 스크립트 이해](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)  
  
  
