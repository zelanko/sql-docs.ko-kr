---
title: 배포 스크립트를 만드는 데 입력된 파일 이해 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- input files [Analysis Services]
- Analysis Services Deployment Wizard, scripts
- deploying [Analysis Services], input files
- Analysis Services Deployment Wizard, input files
- scripts [Analysis Services], deployment
- Analysis Services deployments, input files
- modifying input files
ms.assetid: 20e080cd-6a0e-4591-b022-ea4cd3638e36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a03735b1d412a7501ab59f88288c32ef7ec5514c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48165813"
---
# <a name="understanding-the-input-files-used-to-create-the-deployment-script"></a>배포 스크립트를 만드는 데 사용하는 입력 파일 이해
   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 만들 때 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 는 프로젝트에 대한 XML 파일을 생성합니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 이러한 XML 파일의 출력 폴더에 저장 된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트입니다. 기본 결과는 \Bin 폴더에 출력됩니다. 다음 표에서는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 만드는 XML 파일을 나열합니다.  
  
|XMLA 파일|Description|  
|---------------|-----------------|  
|\<*프로젝트 이름을*>.asdatabase|프로젝트의 모든 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체에 대한 선언적 정의가 포함됩니다.|  
|\<*프로젝트 이름을*>.deploymenttargets|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체가 생성되는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 및 데이터베이스의 이름이 포함됩니다.|  
|\<*프로젝트 이름을*>.configsettings|데이터 원본 연결 정보 및 개체 스토리지 위치와 같은 환경 관련 설정이 포함됩니다. 이 파일의 설정은의 설정을 재정의 합니다 \< *프로젝트 이름*>.asdatabase 파일입니다.|  
|\<*프로젝트 이름을*>.deploymentoptions|배포가 트랜잭션인지 여부와 배포된 개체가 배포 후 처리되어야 하는지 여부와 같은 배포 옵션이 포함됩니다.|  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]는 해당 프로젝트 파일에 암호를 저장하지 않습니다.  
  
## <a name="modifying-the-input-files"></a>입력 파일 수정  
 배포 대상, 구성 설정을 변경할 수는 입력된 파일에서 검색 된 값 이나 입력된 파일에서 값을 수정 하 고 전체를 편집 하지 않고 배포 옵션 \< *프로젝트 이름을*>.asdatabase 파일 (또는 기존 스크립트를 생성 하는 경우 전체 XMLA 스크립트 파일 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스). 개별 파일을 수정할 수 있으면 다른 용도의 다른 배포 스크립트를 쉽게 만들 수 있습니다.  
  
 다음 항목에서는 여러 입력 파일에서 값을 수정하는 방법을 설명합니다.  
  
-   [설치 대상 지정](deployment-script-files-specifying-the-installation-target.md)  
  
-   [파티션 및 역할 배포 옵션 지정](deployment-script-files-partition-and-role-deployment-options.md)  
  
-   [솔루션 배포를 위한 구성 설정 지정](deployment-script-files-solution-deployment-config-settings.md)  
  
-   [처리 옵션 지정](deployment-script-files-specifying-processing-options.md)  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 배포 마법사 실행](running-the-analysis-services-deployment-wizard.md)   
 [Analysis Services 배포 스크립트 이해](understanding-the-analysis-services-deployment-script.md)  
  
  
