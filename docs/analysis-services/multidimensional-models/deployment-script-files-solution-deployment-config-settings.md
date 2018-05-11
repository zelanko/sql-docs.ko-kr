---
title: 솔루션 배포에 대 한 구성 설정 지정 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b75af0331a6f2afbea0159bc3e2e3425e8667a81
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="deployment-script-files---solution-deployment-config-settings"></a>배포 스크립트 파일-솔루션 배포 구성 설정
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사는 파티션 및 역할 배포 옵션을 읽습니다 로부터 배포 스크립트에서 사용 하 여 \< *프로젝트 이름을*>.configsettings 파일입니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]빌드할 때이 파일을 만듭니다는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 현재 프로젝트의 구성 설정을 사용 하 여 만듭니다는 \< *프로젝트 이름을*>.configsettings 파일입니다.  
  
## <a name="reviewing-the-configuration-settings-for-deployment"></a>배포를 위한 구성 설정 검토  
 다음은에 저장 된 구성 설정의 \< *프로젝트 이름을*>.configsettings 파일:  
  
-   **데이터 원본 연결 문자열** 이 문자열은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 지정된 값에 따른 각 데이터 원본에 대한 연결 문자열입니다. 사용자 ID와 암호는 문자열의 나머지 부분이 이 파일에 저장되기 전에 항상 연결 문자열에서 제거됩니다. 그러나 배포 마법사가 Analysis Services 인스턴스에 직접 배포하는 경우 마법사 내에서 적절한 사용자 ID와 암호 정보를 추가하여 배포 데이터베이스가 성공적으로 처리되도록 할 수 있습니다. 이 연결 정보는 배포 마법사에 의해 저장되는 경우 배포 스크립트 자체에 저장되지 않습니다.  
  
-   **가장 계정** 이 설정은 각 데이터 원본에서 문을 실행하기 위해 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 가 사용하는 사용자 이름을 지정합니다. 가장 계정이 지정되지 않은 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 해당 로그온 계정을 사용하여 문을 실행합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 로그인 계정에 데이터 원본에 대한 사용 권한이 직접 부여된 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 모든 데이터베이스에 대한 모든 데이터베이스 관리자가 이 로그온 계정을 통해 데이터 원본에 액세스할 수 있습니다. 사용자 계정과 암호를 지정하는 경우 이 정보는 이 파일에 가장 정보가 저장되기 전에 항상 제거됩니다. 그러나 배포 마법사가 Analysis Services 인스턴스에 직접 배포하는 경우 마법사 내에서 적절한 사용자 ID와 암호 정보를 추가하여 배포 데이터베이스가 성공적으로 처리되도록 할 수 있습니다. 이 가장 정보는 배포 마법사에 의해 저장되는 경우 배포 스크립트 자체에 저장되지 않습니다.  
  
-   **키 오류 로그 파일** 이 설정은 데이터베이스에 있는 각 큐브, 측정값 그룹, 파티션 및 차원에 대한 키 오류 로그 파일의 파일 이름과 경로를 지정합니다.  
  
-   **저장소 위치** 이 설정은 데이터베이스에 있는 각 큐브, 측정값 그룹 및 파티션에 대한 저장소 위치를 지정합니다. 개체에 값이 제공되지 않은 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사는 개체에 대한 기본 위치를 사용합니다. 예를 들어 파티션은 측정값 그룹의 위치를 사용하고, 측정값 그룹은 큐브의 위치를 사용하고, 큐브는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 있는 개체의 기본 위치를 사용합니다. 저장소 위치는 로컬이거나 UNC(Universal Naming Convention) 경로일 수 있습니다.  
  
-   **보고서 서버** 이 설정은 보고서 서버 및 데이터베이스에 있는 각 큐브에 정의된 각 보고서 동작의 폴더 위치를 지정합니다.  
  
## <a name="modifying-the-configuration-settings-for-deployment"></a>배포를 위한 구성 설정 수정  
 경우에 따라 배포 해야 할 수 있습니다는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에 저장 된 것과 다른 구성 설정을 사용 하 여 프로젝트의 \< *프로젝트 이름을*>.configsettings 파일입니다. 예를 들어 하나 이상의 데이터 원본에 대한 연결 문자열을 변경하거나 특정 파티션 또는 측정값 그룹에 대한 저장소 위치를 지정해야 할 수 있습니다.  
  
 파티션 및 역할의 배포를 수정 하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 내에서이 정보를 변경 해야는 \< *프로젝트 이름을*> 아래 절차에 설명 된 대로.configsettings 파일입니다. 때문에 프로젝트 내에서 파티션 및 역할 설정을 변경할 수 없습니다는  *\<프로젝트 이름 >* **속성 페이지** 대화 상자에서 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 이러한 옵션이 표시 되지 않습니다.  
  
> [!NOTE]  
>  구성 설정은 모든 개체나 새로 만든 개체에만 적용될 수 있습니다. 이전에 배포된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 추가 개체를 배포할 때 기존 개체를 덮어쓰지 않으려는 경우에만 새로 만든 개체에 구성 설정을 적용하십시오. 구성 설정이 모든 개체에 적용 또는 새로 만든 사람 에게만이 옵션을 설정 하는지 여부를 지정 하는 \< *프로젝트 이름을*>.deploymentoptions 파일입니다. 자세한 내용은 [파티션 및 역할 배포 옵션 지정](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md)을 참조하세요.  
  
#### <a name="to-change-configuration-settings-after-the-input-files-have-been-generated"></a>입력 파일을 생성한 다음 구성 설정을 변경하려면  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사를 대화식으로 실행하고 **구성 설정** 페이지에서 배포할 개체의 구성 설정을 지정합니다.  
  
     —또는—  
  
-   명령 프롬프트에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사를 실행하여 응답 파일 모드에서 마법사를 실행하도록 설정합니다. 응답 파일 모드에 대한 자세한 내용은 [Running the Analysis Services Deployment Wizard](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)을 참조하십시오.  
  
     —또는—  
  
-   수정 된 \< *프로젝트 이름*> 텍스트 편집기를 사용 하 여.configsettings 파일입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [설치 대상 지정](../../analysis-services/multidimensional-models/deployment-script-files-specifying-the-installation-target.md)   
 [파티션 및 역할 배포 옵션 지정](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md)   
 [처리 옵션 지정](../../analysis-services/multidimensional-models/deployment-script-files-specifying-processing-options.md)  
  
  
