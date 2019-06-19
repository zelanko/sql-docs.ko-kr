---
title: '6단원: SSIS에서 프로젝트 배포 모델에 매개 변수 사용 | Microsoft Docs'
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 9216f18c-1762-4f2d-8c22-bd0ab7107555
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 54fb96d23fb02be01068ce5c2206913a0e6716f0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65721061"
---
# <a name="lesson-6-use-parameters-with-the-project-deployment-model-in-ssis"></a>6단원: SSIS에서 프로젝트 배포 모델에 매개 변수 사용

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



SQL Server 2012는 Integration Services 서버에 프로젝트를 배포할 수 있는 새로운 배포 모델을 제공하고 있습니다. Integration Services 서버에서는 패키지를 관리 및 실행하고 패키지에 대한 런타임 값을 구성할 수 있습니다.  
  
이 단원에서는 [5단원: 패키지 배포 모델에 대한 SSIS 패키지 구성 추가](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)에서 만든 패키지를 수정하여 프로젝트 배포 모델을 사용합니다. 구성 값을 예제 데이터 위치를 지정하는 매개 변수로 바꿉니다. 또한 자습서에 포함된 완료된 5단원 패키지를 복사할 수도 있습니다.  
  
Integration Services 프로젝트 구성 마법사를 사용하여 프로젝트를 프로젝트 배포 모델로 변환합니다. 이 모델은 디렉터리 속성을 설정하는 데 구성 값이 아닌 매개 변수를 사용합니다. 이 단원에서는 기존 SSIS 패키지를 새로운 프로젝트 배포 모델로 변환하기 위해 수행해야 하는 단계에 대해 일부 설명합니다.  
  
패키지를 다시 실행하는 경우 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버는 매개 변수를 사용하여 변수 값을 채웁니다. 변수는 다시 Directory 속성을 업데이트합니다. 패키지는 새 매개 변수에서 지정된 데이터 폴더의 파일을 반복합니다.  
  
> [!NOTE]
> 아직 준비가 되지 않았다면 [1단원 필수 구성 요소](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites)를 참조하세요.
    
## <a name="lesson-tasks"></a>단원 태스크  
이 단원에서는 다음 태스크를 다룹니다.  
  
1.  [1단계: 5단원 패키지 복사](../integration-services/lesson-6-1-copying-the-lesson-5-package.md)  
  
2.  [2단계: 프로젝트를 프로젝트 배포 모델로 변환](../integration-services/lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
3.  [3단계: 6단원 패키지 테스트](../integration-services/lesson-6-3-testing-the-lesson-6-package.md)  
  
4.  [4단계: 6단원 패키지 배포](../integration-services/lesson-6-4-deploying-the-lesson-6-package.md)  
  
## <a name="start-the-lesson"></a>단원 시작  
[1단계: 5단원 패키지 복사](../integration-services/lesson-6-1-copying-the-lesson-5-package.md)  
  
