---
title: 배포 스크립트를 서비스 분석을 이해 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services Deployment Wizard, scripts
- deploying [Analysis Services], scripts
- Analysis Services deployments, scripts
- scripts [Analysis Services], deployment
ms.assetid: a63ebee9-9848-48f1-82ad-64ecf2e47019
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 84bc0e699a0fb47b78b1b0d075a0ef87c8a4dcc3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48099296"
---
# <a name="understanding-the-analysis-services-deployment-script"></a>Analysis Services 배포 스크립트 이해
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사에서 생성하는 XMLA 배포 스크립트는 다음 두 섹션으로 구성됩니다.  
  
-   배포 스크립트의 첫 번째 부분에는 대상 데이터베이스에서 적절한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체를 만들거나 변경하거나 삭제하는 데 필요한 명령이 포함되어 있습니다. 기본적으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에서 생성한 입력 파일은 증분 배포를 기반으로 합니다. 따라서 XMLA 배포 스크립트는 변경되거나 삭제된 개체에만 영향을 줍니다.  
  
-   배포 스크립트의 두 번째 부분에는 대상 서버(기본값 처리 옵션)에서 생성되거나 변경된 개체만 처리하거나 대상 데이터베이스를 전체 처리하는 데 필요한 명령만 포함됩니다. 배포 스크립트에 처리 명령이 포함되지 않도록 선택할 수도 있습니다.  
  
 단일 트랜잭션 또는 여러 트랜잭션에서 전체 배포 스크립트를 실행할 수 있습니다. 스크립트가 여러 트랜잭션에서 실행되는 경우 스크립트의 첫 번째 부분은 단일 트랜잭션으로 실행되고 각 개체는 자체 트랜잭션에서 처리됩니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사는 개체를 단일 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에만 배포하고 서버 수준 개체나 데이터는 배포하지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 배포 마법사 실행](running-the-analysis-services-deployment-wizard.md)   
 [배포 스크립트를 만드는 데 사용하는 입력 파일 이해](deployment-script-files-input-used-to-create-deployment-script.md)  
  
  
