---
title: "패키지 재배포 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "패키지 재배포 [Integration Services]"
  - "패키지 배포 [Integration Services], 재배포"
ms.assetid: 86806efb-8cf4-4f9d-9824-1152cb4c495c
caps.latest.revision: 37
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 37
---
# 패키지 재배포
  프로젝트를 배포한 후 패키지 기능을 업데이트하거나 확장한 다음 업데이트된 패키지를 포함하는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 다시 배포해야 할 수 있습니다. 패키지 재배포 과정의 일부로 배포 유틸리티에 포함된 구성 속성을 검토하십시오. 예를 들어 패키지를 재배포한 후 구성을 변경할 수 없도록 하기를 원할 수 있습니다.  
  
## 재배치 프로세스  
 패키지 업데이트를 완료한 다음에는 프로젝트를 다시 빌드하고 대상 컴퓨터에 배포 폴더를 복사한 다음 패키지 설치 마법사를 다시 실행하십시오.  
  
 프로젝트 내의 소수 패키지만 업데이트한 경우 전체 프로젝트를 재배포하고 싶지 않을 수 있습니다. 소수의 패키지만 배포하려면 새 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 만들고 업데이트된 패키지를 추가한 다음 프로젝트를 빌드하고 배포하십시오. 다른 프로젝트에 패키지를 추가하는 경우 자동으로 패키지와 함께 패키지 구성이 복사됩니다.  
  
## 관련 작업  
 [배포 유틸리티를 사용한 패키지 배포](../../integration-services/packages/deploy-packages-by-using-the-deployment-utility.md)  
  
  