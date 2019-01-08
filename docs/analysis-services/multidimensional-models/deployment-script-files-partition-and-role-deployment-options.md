---
title: 파티션 및 역할 배포 옵션 지정 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8bd62cc5fef3ef13dede85c06b28b0501a83de2f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52513914"
---
# <a name="deployment-script-files---partition-and-role-deployment-options"></a>배포 스크립트 파일 - 파티션 및 역할 배포 옵션
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  합니다 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사에서 파티션 및 역할 배포 옵션을 읽습니다 합니다 \< *프로젝트 이름을*>.deploymentoptions 파일입니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 작성할 때 이 파일을 만듭니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 때 사용 하 여 파티션 및 역할 배포 옵션을 현재 프로젝트를 \< *프로젝트 이름*>.deploymentoptions 파일이 생성 됩니다. 이러한 구성 설정에 대한 자세한 내용은 [배포 스크립트를 만드는 데 사용하는 입력 파일 이해](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md)를 참조하십시오.  
  
## <a name="reviewing-the-partition-and-role-deployment-options"></a>파티션 및 역할 배포 옵션 검토  
 배포 옵션에 \< *프로젝트 이름*>.deploymentoptions 파일은 다음과 같습니다.  
  
 **파티션 배포 옵션**  
 합니다 \< *프로젝트 이름*>.deploymentoptions 파일은 대상 데이터베이스의 기존 파티션의 유지 하는 여부 하거나 덮어쓸지 (기본값) 지정 합니다. 기존 파티션을 유지하는 경우 새 파티션만 배포되고 기존의 모든 측정값 그룹에 있는 파티션 및 집계 디자인은 변경되지 않습니다.  
  
> [!NOTE]  
>  파티션이 존재하는 측정값 그룹이 삭제되면 파티션이 자동으로 삭제됩니다.  
  
 **역할 배포 옵션**  
 합니다 \< *프로젝트 이름*>.deploymentoptions 파일은 다음 역할 배포 옵션 중 하나를 지정 합니다.  
  
-   대상 데이터베이스의 기존 역할 및 역할 멤버는 유지되고 새로운 역할 및 역할 멤버만 배포됩니다.  
  
-   대상 데이터베이스의 모든 기존 역할 및 멤버가 배포되는 역할 및 멤버로 교체됩니다.  
  
-   대상 데이터베이스의 기존 역할 및 역할 멤버가 유지되고 새 역할이 배포되지 않습니다.  
  
-   **참고** 기존 역할과 멤버가 보존되는 경우 해당 역할과 관련된 권한은 없음으로 다시 설정됩니다. 보안 권한은 관련된 보안 역할이 아닌 보안을 설정하는 개체에 포함됩니다. Analysis Service 배포 마법사를 사용 하 여이 동작을 사용 하는 방법에 대 한 자세한 내용은 참조 'Retain Roles and 멤버' Microsoft 기술 자료에서 합니다.  
  
## <a name="modifying-the-partition-and-role-deployment-options"></a>파티션 및 역할 배포 옵션 수정  
 배포 해야 합니다 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에 저장 된 것과 다른 파티션 및 역할 옵션을 사용 하 여 프로젝트를 \< *프로젝트 이름*>.deploymentoptions 파일. 예를 들어 기존 파티션, 역할 및 역할 멤버에 표시 된 대로 모든 기존 파티션, 역할 및 멤버를 교체 하는 대신 유지 하려면 수는 \< *프로젝트 이름*>.deploymentoptions 파일입니다.  
  
 파티션 및 역할 배포를 수정 하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 때문에 프로젝트 내에서 파티션 및 역할 설정을 변경할 수 없습니다 합니다  *\<프로젝트 이름 >* **속성 페이지**  대화 상자 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 이러한 옵션이 표시 되지 않습니다. 역할 및 파티션에 대 한 배포 옵션을 변경 하려는 경우 내에서이 정보를 변경 해야 합니다 \< *프로젝트 이름*>.deploymentoptions 파일 자체입니다. 다음 절차에는 내에서 파티션 및 역할 배포 옵션을 변경 하는 방법을 설명 합니다 \< *프로젝트 이름*>.deploymentoptions 파일입니다.  
  
#### <a name="to-change-the-deployment-of-partitions-or-roles-after-the-input-files-have-been-generated"></a>입력 파일을 생성한 다음 파티션 또는 역할 배포를 변경하려면  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사를 대화식으로 실행하고 **파티션 및 역할 배포 옵션** 페이지에서 파티션 및 역할에 대한 새 배포 옵션을 지정합니다.  
  
     -또는-  
  
-   명령 프롬프트에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사를 실행하여 응답 파일 모드에서 마법사를 실행하도록 설정합니다. 응답 파일 모드에 대한 자세한 내용은 [Analysis Services 배포 마법사 실행](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)을 참조하세요.  
  
     -또는-  
  
-   엽니다는 \< *프로젝트 이름*>.deploymentoptions 임의의 텍스트 편집기에서 이동 하 고 수동으로 옵션을 변경 합니다. PartitionDeployment 옵션은 DeployPartitions, RetainPartitions 합니다. RoleDeployment에 대 한 옵션은 DeployRolesAndMembers, DeployRolesRetainMembers RetainRoles 합니다.
  
## <a name="see-also"></a>관련 항목:  
 [설치 대상 지정](../../analysis-services/multidimensional-models/deployment-script-files-specifying-the-installation-target.md)   
 [솔루션 배포를 위한 구성 설정 지정](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)   
 [처리 옵션 지정](../../analysis-services/multidimensional-models/deployment-script-files-specifying-processing-options.md)  
  
  
