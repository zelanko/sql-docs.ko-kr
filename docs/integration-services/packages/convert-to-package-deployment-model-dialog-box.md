---
title: "패키지 배포 모델로 변환 대화 상자 | Microsoft Docs"
ms.custom: ""
ms.date: "08/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.bids.converttolegacydeployment.f1"
ms.assetid: 9e60a34a-10f7-48d1-966f-b3ff236ab4b7
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# 패키지 배포 모델로 변환 대화 상자
  **패키지 배포 모델로 변환** 명령을 사용하면 프로젝트 및 프로젝트의 각 패키지에서 해당 모델과의 호환성을 검사한 후 패키지를 패키지 배포 모델로 변환할 수 있습니다. 패키지에 매개 변수와 같이 프로젝트 배포 모델에 고유한 기능이 사용된 경우 패키지를 변환할 수 없습니다.  
  
## 작업 목록  
 패키지를 패키지 배포 모델로 변환하려면 두 단계가 필요합니다.  
  
1.  **프로젝트** 메뉴에서 **패키지 배포 모델로 변환** 명령을 선택하면 이 모델에 대한 프로젝트 및 각 패키지의 호환성이 검사됩니다. 결과는 **결과** 테이블에 표시됩니다.  
  
     프로젝트 또는 패키지가 호환성 테스트를 실패한 경우 **결과** 열에서 **실패** 를 클릭하여 자세한 내용을 확인합니다. **보고서 저장** 을 클릭하여 이 정보의 복사본을 텍스트 파일로 저장합니다.  
  
2.  프로젝트 및 모든 패키지가 호환성 테스트를 성공하면 **확인** 을 클릭하여 패키지를 변환합니다.  
  
> **참고:** 프로젝트를 프로젝트 배포 모델로 변환하려면 **Integration Services 프로젝트 변환 마법사**를 사용합니다. 자세한 내용은 [Integration Services Project Conversion Wizard](https://msdn.microsoft.com/library/hh213290.aspx)을 참조하세요.  
  
## 관련 항목:  
 [레거시 패키지 배포&#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md)   
 [Integration Services 프로젝트 변환 마법사](../../integration-services/packages/integration-services-project-conversion-wizard.md)  
  
  