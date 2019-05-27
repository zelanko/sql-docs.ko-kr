---
title: 패키지 배포 모델 대화 상자를 변환할 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.bids.converttolegacydeployment.f1
ms.assetid: 9e60a34a-10f7-48d1-966f-b3ff236ab4b7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dfe1f6e5b752284b6bb0feec96f4f3dfd67cc4f6
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66060344"
---
# <a name="convert-to-package-deployment-model-dialog-box"></a>패키지 배포 모델로 변환 대화 상자
  **패키지 배포 모델로 변환** 명령을 사용하면 프로젝트 및 프로젝트의 각 패키지에서 해당 모델과의 호환성을 검사한 후 패키지를 패키지 배포 모델로 변환할 수 있습니다. 패키지에 매개 변수와 같이 프로젝트 배포 모델에 고유한 기능이 사용된 경우 패키지를 변환할 수 없습니다.  
  
## <a name="task-list"></a>작업 목록  
 패키지를 패키지 배포 모델로 변환하려면 두 단계가 필요합니다.  
  
1.  **프로젝트** 메뉴에서 **패키지 배포 모델로 변환** 명령을 선택하면 이 모델에 대한 프로젝트 및 각 패키지의 호환성이 검사됩니다. 결과는 **결과** 테이블에 표시됩니다.  
  
     프로젝트 또는 패키지가 호환성 테스트를 실패한 경우 **결과** 열에서 **실패** 를 클릭하여 자세한 내용을 확인합니다. **보고서 저장** 을 클릭하여 이 정보의 복사본을 텍스트 파일로 저장합니다.  
  
2.  프로젝트 및 모든 패키지가 호환성 테스트를 성공하면 **확인** 을 클릭하여 패키지를 변환합니다.  
  
> [!NOTE]  
>  프로젝트를 프로젝트 배포 모델로 변환하려면 **Integration Services 프로젝트 변환 마법사**를 사용합니다. 자세한 내용은 [Integration Services Project Conversion Wizard](../../2014/integration-services/integration-services-project-conversion-wizard.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [프로젝트 및 패키지 배포](packages/deploy-integration-services-ssis-projects-and-packages.md)   
 [배포 패키지 &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)   
 [Integration Services 프로젝트 변환 마법사](../../2014/integration-services/integration-services-project-conversion-wizard.md)  
  
  
