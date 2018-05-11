---
title: 배포 스크립트를 서비스의 분석을 이해 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6be56539605946468b1c2e2700e2c65841018a4d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="understanding-the-analysis-services-deployment-script"></a>Analysis Services 배포 스크립트 이해
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사에서 생성하는 XMLA 배포 스크립트는 다음 두 섹션으로 구성됩니다.  
  
-   배포 스크립트의 첫 번째 부분에는 대상 데이터베이스에서 적절한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체를 만들거나 변경하거나 삭제하는 데 필요한 명령이 포함되어 있습니다. 기본적으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에서 생성한 입력 파일은 증분 배포를 기반으로 합니다. 따라서 XMLA 배포 스크립트는 변경되거나 삭제된 개체에만 영향을 줍니다.  
  
-   배포 스크립트의 두 번째 부분에는 대상 서버(기본값 처리 옵션)에서 생성되거나 변경된 개체만 처리하거나 대상 데이터베이스를 전체 처리하는 데 필요한 명령만 포함됩니다. 배포 스크립트에 처리 명령이 포함되지 않도록 선택할 수도 있습니다.  
  
 단일 트랜잭션 또는 여러 트랜잭션에서 전체 배포 스크립트를 실행할 수 있습니다. 스크립트가 여러 트랜잭션에서 실행되는 경우 스크립트의 첫 번째 부분은 단일 트랜잭션으로 실행되고 각 개체는 자체 트랜잭션에서 처리됩니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사는 개체를 단일 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에만 배포하고 서버 수준 개체나 데이터는 배포하지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 배포 마법사 실행](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)   
 [배포 스크립트를 만드는 데 입력된 파일 이해](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md)  
  
  
