---
title: "레거시 패키지 배포(SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Integration Services 패키지, 배포"
  - "패키지 배포 [Integration Services]"
  - "SQL Server Integration Services 패키지, 배포"
  - "패키지 배포 [Integration Services], 패키지 배포 정보"
  - "패키지 [Integration Services], 배포"
  - "SSIS 패키지, 배포"
ms.assetid: 0f5fc7be-e37e-4ecd-ba99-697c8ae3436f
caps.latest.revision: 46
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 46
---
# 레거시 패키지 배포(SSIS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 패키지를 배포 컴퓨터에서 프로덕션 서버나 다른 컴퓨터로 손쉽게 배포할 수 있는 도구와 마법사가 포함되어 있습니다.  
  
 패키지 배포 과정은 다음 네 단계로 구성됩니다.  
  
1.  첫 번째 단계는 선택 사항입니다. 이 단계에서는 런타임에 패키지 요소의 속성을 업데이트하는 패키지 구성을 만듭니다. 구성은 패키지를 배포할 때 자동으로 포함됩니다.  
  
2.  두 번째 단계는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 빌드하여 패키지 배포 유틸리티를 만드는 것입니다. 프로젝트의 배포 유틸리티에는 배포할 패키지가 포함됩니다.  
  
3.  세 번째 단계는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 빌드할 때 생성된 배포 폴더를 대상 컴퓨터로 복사하는 것입니다.  
  
4.  네 번째 단계는 대상 컴퓨터에서 패키지 설치 마법사를 실행하여 파일 시스템이나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 패키지를 설치하는 것입니다.  
  
## 관련 작업  
 배포 유틸리티를 만드는 방법에 대한 자세한 내용은 [배포 유틸리티 만들기](../../integration-services/packages/create-a-deployment-utility.md)를 참조하세요.  
  
 배포 유틸리티를 사용하여 패키지를 배포하는 방법에 대한 자세한 내용은 [배포 유틸리티를 사용한 패키지 배포](../../integration-services/packages/deploy-packages-by-using-the-deployment-utility.md)를 참조하세요.  
  
 패키지 구성을 만드는 방법에 대한 자세한 내용은 [패키지 구성 만들기](../../integration-services/packages/create-package-configurations.md)를 참조하세요.  
  
  