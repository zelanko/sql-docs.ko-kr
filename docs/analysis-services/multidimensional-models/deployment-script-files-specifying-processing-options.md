---
title: "처리 옵션을 지정 하 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Analysis Services deployments, processing options
- input files [Analysis Services]
- deploying [Analysis Services], processing options
- modifying processing options
- Analysis Services Deployment Wizard, processing options
ms.assetid: e9e50817-908e-4210-bc3d-8e2957568241
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 37535b41f5ae5e7c68a47d18a4b91253c7f54d81
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
---
# <a name="deployment-script-files---specifying-processing-options"></a>배포 스크립트 파일-처리 옵션 지정
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사에서 처리 옵션을 읽습니다는 \< *프로젝트 이름을*>.deploymentoptions 파일입니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]빌드할 때이 파일을 만듭니다는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에 지정 된 처리 옵션을 사용 하 여는 **배포** 페이지  *\<프로젝트 이름 >* **속성 페이지** 대화 상자를 만들는 \< *프로젝트 이름을*>.deploymentoptions 파일입니다.  
  
## <a name="reviewing-the-processing-options-for-deployment"></a>배포를 위한 처리 옵션 검토  
 에 저장 된 구성 설정은 \< *프로젝트 이름을*>.deploymentoptions 파일은 다음과 같습니다.  
  
-   **처리 방법** 이 설정은 배포 후 배포된 개체가 처리되는지 여부와 수행할 처리 유형을 제어합니다. 3가지 처리 옵션은 다음과 같습니다.  
  
    -   기본 처리(기본값)  
  
    -   전체 처리  
  
    -   InclusionThresholdSetting  
  
-   **쓰기 저장(writeback) 테이블 옵션** 쓰기 저장(writeback)이 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 설정된 경우 이 설정은 쓰기 저장(writeback)의 처리 방법을 정의합니다. 3가지 쓰기 저장(writeback) 테이블 옵션은 다음과 같습니다.  
  
    -   기본적으로 쓰기 저장(writeback) 테이블이 있는 경우 이 테이블이 사용됩니다. 쓰기 저장(Writeback) 테이블이 없는 경우 새 쓰기 저장 테이블이 생성됩니다.  
  
    -   쓰기 저장(writeback) 테이블이 이미 있으면 배포가 실패합니다. 쓰기 저장(Writeback) 테이블이 없는 경우 새 쓰기 저장 테이블이 생성됩니다.  
  
    -   쓰기 저장(writeback) 테이블이 이미 존재하는지 여부에 관계없이 새로운 쓰기 저장(writeback) 테이블이 생성됩니다. 이 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사는 기존 테이블을 삭제하고 이를 새로운 쓰기 저장(writeback) 테이블로 교체합니다.  
  
-   **트랜잭션 배포** 이 설정은 메타데이터 배포가 변경되고 처리 명령이 단일 트랜잭션 또는 개별 트랜잭션에 발생하는지 여부를 제어합니다.  
  
    -   이 옵션이 **True** (기본값)인 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 모든 메타데이터 변경 내용과 단일 트랜잭션 내의 모든 처리 명령을 배포합니다.  
  
    -   이 옵션이 **False**인 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 단일 트랜잭션의 메타데이터 변경 내용을 배포하고 해당 트랜잭션의 각 처리 명령을 배포합니다.  
  
## <a name="modifying-the-processing-options-for-deployment"></a>배포를 위한 처리 옵션 수정  
 그러나 배포 해야 할 수는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에 저장 된 것과 다른 처리 옵션을 사용 하 여 프로젝트의 \< *프로젝트 이름*>.deploymentoptions 파일입니다. 예를 들어 모든 개체를 완전히 처리하거나 기본 처리 옵션을 사용하여 처리할 수 있으며, 또는 처리가 발생하지 않도록 할 수도 있습니다. 큐브 또는 차원이 쓰기 설정된 경우 새 쓰기 저장(writeback) 테이블이나 기존 테이블을 사용하도록 지정할 수 있습니다.  
  
 배포 중에 사용된 처리 옵션을 수정하려는 경우 프로젝트를 편집하고 다시 작성하거나 다음 절차에 설명된 대로 다음 방법 중 하나를 사용하여 입력 파일에서 처리 옵션을 변경할 수 있습니다.  
  
#### <a name="to-change-processing-options-after-the-input-files-have-been-generated"></a>입력 파일을 생성한 다음 처리 옵션을 변경하려면  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사를 대화형으로 실행합니다. **처리 옵션** 페이지에서 배포할 프로젝트의 처리 옵션을 지정합니다.  
  
     —또는—  
  
-   명령 프롬프트에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사를 실행하여 응답 파일 모드에서 마법사를 실행하도록 설정합니다. 응답 파일 모드에 대한 자세한 내용은 [Running the Analysis Services Deployment Wizard](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)을 참조하십시오.  
  
     —또는—  
  
-   수정 된 \< *프로젝트 이름*> 텍스트 편집기를 사용 하 여.deploymentoptions 파일입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [설치 대상 지정](../../analysis-services/multidimensional-models/deployment-script-files-specifying-the-installation-target.md)   
 [파티션 및 역할 배포 옵션 지정](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md)   
 [솔루션 배포에 대 한 구성 설정 지정](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)  
  
  
