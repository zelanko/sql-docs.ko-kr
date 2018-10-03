---
title: 배포 마법사를 사용 하 여 모델 솔루션 배포 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services Deployment Wizard
- deploying [Analysis Services], Analysis Services Deployment Wizard
- Analysis Services deployments, Analysis Services Deployment Wizard
- Analysis Services Deployment Wizard, about Analysis Services Deployment Wizard
ms.assetid: ff711e8e-971c-43ba-b479-effc034af4a4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a0136631904a9f4bf8a0cdb7c22e7c9241ba3aff
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48087653"
---
# <a name="deploy-model-solutions-using-the-deployment-wizard"></a>배포 마법사를 사용하여 모델 솔루션 배포
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에서 생성된 XML 출력 파일을 입력 파일로 사용합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 배포를 사용자 지정할 수 있도록 이러한 입력 파일을 쉽게 수정할 수 있습니다. 그런 다음 생성된 배포 스크립트를 즉시 실행하거나 나중에 배포할 때 사용할 수 있도록 저장할 수 있습니다.  
  
 여기에 설명된 대로 마법사를 사용하여 배포할 수 있습니다. 또한 배포를 자동화하거나 동기화 기능을 사용할 수 있습니다. 배포된 데이터베이스가 큰 경우 대상 시스템에서 파티션 사용을 고려하세요. 또한 AMO(Analysis Management Objects)를 사용하여 파티션 만들기 및 채우기를 자동화할 수 있습니다.  
  
> [!IMPORTANT]  
>  XML 출력 파일과 배포 스크립트가 데이터 원본 또는 가장 용도의 연결 문자열에 지정되는 경우 사용자 ID와 암호가 포함되지 않습니다. 이 시나리오에서는 처리 용도로 이러한 사용자 ID와 암호가 필요하므로 이러한 정보를 직접 추가하세요. 배포에 처리가 포함되지 않은 경우 배포 후 필요에 따라 이 연결 및 가장 정보를 추가할 수 있습니다. 배포에 처리가 포함될 경우 마법사 내에 이 정보를 추가하거나 이 정보가 저장된 후 배포 스크립트에 추가할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 다음 항목에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사, 입력 파일 및 배포 스크립트를 사용하는 방법에 대해 설명합니다.  
  
|항목|Description|  
|-----------|-----------------|  
|[Analysis Services 배포 마법사 실행](running-the-analysis-services-deployment-wizard.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사를 실행할 수 있는 여러 방법에 대해 설명합니다.|  
|[배포 스크립트를 만드는 데 사용하는 입력 파일 이해](deployment-script-files-input-used-to-create-deployment-script.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사가 입력 값으로 사용하는 파일 및 이러한 각 파일에 포함되는 내용에 대해 설명하고 각 입력 파일에서 값을 수정하는 방법을 설명하는 항목 링크를 제공합니다.|  
|[Analysis Services 배포 스크립트 이해](understanding-the-analysis-services-deployment-script.md)|배포 스크립트에 포함된 내용 및 스크립트 실행 방법에 대해 설명합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [XMLA를 사용 하 여 모델 솔루션 배포](deploy-model-solutions-using-xmla.md)   
 [Analysis Services 데이터베이스 동기화](synchronize-analysis-services-databases.md)   
 [배포 스크립트를 만드는 데 입력된 파일 이해](deployment-script-files-input-used-to-create-deployment-script.md)   
 [배포 유틸리티를 사용하여 모델 솔루션 배포](deploy-model-solutions-with-the-deployment-utility.md)  
  
  
