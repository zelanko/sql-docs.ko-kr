---
title: 파티션 및 역할 배포 옵션 지정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- input files [Analysis Services]
- partitions [Analysis Services], deployment options
- Analysis Services deployments, roles
- Analysis Services deployments, partitions
- Analysis Services Deployment Wizard, roles
- Analysis Services Deployment Wizard, partitions
- deploying [Analysis Services], roles
- roles [Analysis Services], deployment options
- deploying [Analysis Services], partitions
- modifying role deployments
- modifying partition deployments
ms.assetid: e9b9ca57-a5cc-4fc0-87b5-305257038d56
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b9b36013f13360a2afcf9546cd1e286b35ae4acd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66075347"
---
# <a name="specifying-partition-and-role-deployment-options"></a>파티션 및 역할 배포 옵션 지정
  배포 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 마법사는 \< *프로젝트 이름*> deploymentoptions 파일에서 파티션 및 역할 배포 옵션을 읽습니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]프로젝트를 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 빌드할 때이 파일을 만듭니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]\< *프로젝트 이름*> deploymentoptions 파일이 생성 될 때 현재 프로젝트의 파티션 및 역할 배포 옵션을 사용 합니다. 이러한 구성 설정에 대한 자세한 내용은 [Understanding the Input Files Used to Create the Deployment Script](deployment-script-files-input-used-to-create-deployment-script.md)를 참조하십시오.  
  
## <a name="reviewing-the-partition-and-role-deployment-options"></a>파티션 및 역할 배포 옵션 검토  
 \< *프로젝트 이름*> deploymentoptions 파일의 배포 옵션은 다음과 같습니다.  
  
 **파티션 배포 옵션**  
 \< *프로젝트 이름*> deploymentoptions 파일은 대상 데이터베이스의 기존 파티션을 유지 하거나 덮어쓸지 (기본값) 여부를 지정 합니다. 기존 파티션을 유지하는 경우 새 파티션만 배포되고 기존의 모든 측정값 그룹에 있는 파티션 및 집계 디자인은 변경되지 않습니다.  
  
> [!NOTE]  
>  파티션이 존재하는 측정값 그룹이 삭제되면 파티션이 자동으로 삭제됩니다.  
  
 **역할 배포 옵션**  
 \< *프로젝트 이름*> deploymentoptions 파일은 다음 역할 배포 옵션 중 하나를 지정 합니다.  
  
-   대상 데이터베이스의 기존 역할 및 역할 멤버는 유지되고 새로운 역할 및 역할 멤버만 배포됩니다.  
  
-   대상 데이터베이스의 모든 기존 역할 및 멤버가 배포되는 역할 및 멤버로 교체됩니다.  
  
-   대상 데이터베이스의 기존 역할 및 역할 멤버가 유지되고 새 역할이 배포되지 않습니다.  
  
-   **참고** 기존 역할과 멤버가 보존되는 경우 해당 역할과 관련된 권한은 없음으로 다시 설정됩니다. 보안 권한은 관련된 보안 역할이 아닌 보안을 설정하는 개체에 포함됩니다. Analysis Service 배포 마법사를 사용 하 여이 동작을 수행 하는 방법에 대 한 자세한 내용은 Microsoft 기술 자료에서 ' 역할 및 멤버 유지 '를 참조 하십시오.  
  
## <a name="modifying-the-partition-and-role-deployment-options"></a>파티션 및 역할 배포 옵션 수정  
 \< *프로젝트 이름*> deploymentoptions 파일 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에 저장 된 것과 다른 파티션 및 역할 옵션을 사용 하 여 프로젝트를 배포 해야 할 수 있습니다. 예를 들어 \< *프로젝트 이름*> deploymentoptions 파일에 표시 된 대로 기존 파티션, 역할 및 멤버를 모두 대체 하는 대신 기존 파티션, 역할 및 역할 멤버를 유지 하려고 할 수 있습니다.  
  
 프로젝트에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 파티션 및 역할의 배포를 수정 하려면의 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] * \<프로젝트 이름>* **속성 페이지** 대화 상자에 이러한 옵션이 표시 되지 않기 때문에 프로젝트 내에서 파티션 및 역할 설정을 변경할 수 없습니다. 역할 및 파티션에 대 한 배포 옵션을 변경 하려면 \< *프로젝트 이름*>. deploymentoptions 파일 자체에서이 정보를 변경 해야 합니다. 다음 절차에서는 \< *프로젝트 이름*> deploymentoptions 파일 내에서 파티션 및 역할 배포 옵션을 변경 하는 방법에 대해 설명 합니다.  
  
#### <a name="to-change-the-deployment-of-partitions-or-roles-after-the-input-files-have-been-generated"></a>입력 파일을 생성한 다음 파티션 또는 역할 배포를 변경하려면  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사를 대화식으로 실행하고 **파티션 및 역할 배포 옵션** 페이지에서 파티션 및 역할에 대한 새 배포 옵션을 지정합니다.  
  
     또는  
  
-   명령 프롬프트에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사를 실행하여 응답 파일 모드에서 마법사를 실행하도록 설정합니다. 응답 파일 모드에 대 한 자세한 내용은 [Analysis Services 배포 마법사 실행](running-the-analysis-services-deployment-wizard.md)을 참조 하세요.  
  
     또는  
  
-   \<텍스트 편집기에서 *프로젝트 이름*> deploymentoptions를 열고 옵션을 수동으로 변경 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [설치 대상 지정](deployment-script-files-specifying-the-installation-target.md)   
 [솔루션 배포를 위한 구성 설정 지정](deployment-script-files-solution-deployment-config-settings.md)   
 [처리 옵션 지정](deployment-script-files-specifying-processing-options.md)  
  
  
