---
title: '3단원: SSIS 패키지 설치 | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 87bc4d82-39d8-424f-886f-98cf1e4bb07a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5f325c9322d9194ff9dfb99dcf5bcae902a59faa
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295974"
---
# <a name="lesson-3-install-ssis-packages"></a>3단원: SSIS 패키지 설치

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[2단원: SSIS에서 배포 번들 만들기](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)에서는 배포 유틸리티를 빌드하고 다른 컴퓨터에 패키지를 설치해야 하는 항목이 포함된 배포 번들을 만들었습니다. 또한 배포 번들에서 파일 목록을 확인하고 배포 유틸리티를 작성할 때 만들었던 매니페스트 파일의 내용을 검사했습니다.  
  
이 단원에서는 배포 번들을 대상 컴퓨터에 복사한 다음 패키지 설치 마법사를 실행하여 패키지, 패키지 종속 파일 및 보조 파일을 해당 컴퓨터에 설치합니다. 패키지는 **msdb**[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스에 설치되고 다른 항목은 파일 시스템에 설치됩니다. 패키지 설치를 완료한 후에 패키지 실행 유틸리티를 통해 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 에서 패키지를 실행하여 배포를 테스트합니다.  
  
**이 단원에 소요되는 예상 시간:** : 30분  
  
## <a name="lesson-tasks"></a>단원 태스크  
이 단원에서는 다음 태스크를 다룹니다.  
  
-   [1단계: 배포 번들 복사](../integration-services/lesson-3-1-copying-the-deployment-bundle.md)  
  
-   [2단계: 패키지 설치 마법사 실행](../integration-services/lesson-3-2-running-the-package-installation-wizard.md)  
  
-   [3단계: 배포된 패키지 테스트](../integration-services/lesson-3-3-testing-the-deployed-packages.md)  
  
## <a name="start-the-lesson"></a>단원 시작  
[1단계: 배포 번들 복사](../integration-services/lesson-3-1-copying-the-deployment-bundle.md)  
  
  
  
