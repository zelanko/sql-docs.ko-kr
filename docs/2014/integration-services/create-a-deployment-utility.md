---
title: 배포 유틸리티 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- deploying packages [Integration Services], deployment utility
- deployment utility [Integration Services]
ms.assetid: 354322a4-ae8c-4d92-8e71-42d29dbd0614
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e5f7959496cfa2b473fbf5c500f424647df0a1c7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66060225"
---
# <a name="create-a-deployment-utility"></a>Create a Deployment Utility
  패키지를 배포하는 첫 번째 단계는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트의 배포 유틸리티를 만드는 것입니다. 배포 유틸리티는 다른 서버로 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트의 패키지를 배포하는 데 필요한 파일이 포함된 폴더입니다. 배포 유틸리티는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트가 저장된 컴퓨터에 만들어집니다.  
  
 먼저 배포 유틸리티를 만들도록 빌드 프로세스를 구성한 다음 프로젝트를 빌드하면 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트의 패키지 배포 유틸리티를 만들 수 있습니다. 프로젝트를 빌드할 때 프로젝트의 모든 패키지와 패키지 구성은 자동으로 포함됩니다. 추가 정보 파일 등의 추가 파일을 프로젝트와 함께 배포하려면 해당 파일을 **프로젝트의** 기타 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 폴더에 저장하십시오. 프로젝트가 빌드될 때 이러한 파일도 자동으로 포함됩니다.  
  
 각 프로젝트 배포를 다르게 구성할 수 있습니다. 프로젝트를 빌드하고 패키지 배포 유틸리티를 작성하기 전에 배포 유틸리티의 속성을 설정하여 프로젝트의 패키지를 배포하는 방법을 사용자 지정할 수 있습니다. 예를 들어 프로젝트를 배포할 때 패키지 구성을 업데이트할지 여부를 지정할 수 있습니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트의 속성에 액세스하려면 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
 다음 표에서는 배포 유틸리티 속성을 나열합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|AllowConfigurationChange|배포 도중 구성의 업데이트를 허용할지 여부를 지정하는 값입니다.|  
|CreateDeploymentUtility|프로젝트를 빌드할 때 패키지 배포 유틸리티를 만들지 여부를 지정하는 값입니다. 배포 유틸리티를 만들려면 이 속성을 `True`로 설정합니다.|  
|DeploymentOutputPath|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트와 관련된 배포 유틸리티의 위치입니다.|  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 빌드하면 매니페스트 파일인 \<project name>.SSISDeploymentManifest.xml이 패키지 종속 관계 및 패키지의 복사본과 함께 프로젝트의 bin\Deployment 폴더 또는 DeploymentOutputPath 속성에서 지정한 위치에 만들어지고 추가됩니다. 매니페스트 파일은 프로젝트의 패키지, 패키지 구성 및 모든 기타 파일을 나열합니다.  
  
 배포 폴더의 내용은 프로젝트를 작성할 때마다 새로 고쳐집니다. 즉, 배포 폴더에 저장되었지만 빌드 프로세스로 폴더에 다시 복사되지 않은 파일은 모두 삭제됩니다. 예를 들어 배포 폴더에 저장된 패키지 구성 파일은 삭제되지 않습니다.  
  
### <a name="to-create-a-package-deployment-utility"></a>패키지 배포 유틸리티를 만들려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 패키지 배포 유틸리티를 만들 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트가 들어 있는 솔루션을 엽니다.  
  
2.  프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **\<프로젝트 이름> 속성 페이지** 대화 상자에서 **배포 유틸리티**를 클릭합니다.  
  
4.  패키지를 구축할 때 패키지 구성을 업데이트 하려면 **AllowConfigurationChanges** 에 `True`입니다.  
  
5.  `CreateDeploymentUtility`를 `True`로 설정합니다.  
  
6.  필요에 따라 `DeploymentOutputPath` 속성을 수정하여 배포 유틸리티의 위치를 업데이트합니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **빌드**를 클릭합니다.  
  
9. **출력** 창에서 빌드 과정 및 빌드 오류를 확인합니다.  
  
## <a name="see-also"></a>관련 항목  
 [패키지 구성](../../2014/integration-services/package-configurations.md)   
 [패키지 구성 만들기](../../2014/integration-services/create-package-configurations.md)   
 [배포 유틸리티를 사용한 패키지 배포](../../2014/integration-services/deploy-packages-by-using-the-deployment-utility.md)   
 [배포 패키지 &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)  
  
  
