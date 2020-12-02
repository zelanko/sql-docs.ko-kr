---
description: '5단원: 패키지 배포 모델에 대한 SSIS 패키지 구성 추가'
title: '5단원: 패키지 배포 모델에 대한 SSIS 패키지 구성 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 1c10dd54-67cb-4b63-9e4d-aa6ff0452ecb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c50bdc080ca6437cdb2291f901c429526976ab88
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88466615"
---
# <a name="lesson-5-add-ssis-package-configurations-for-the-package-deployment-model"></a>5단원: 패키지 배포 모델에 대한 SSIS 패키지 구성 추가

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



패키지 구성을 사용하면 개발 환경 외부에서 런타임 속성과 변수를 설정할 수 있습니다. 구성을 통해 쉽고 유연하게 배포할 수 있는 패키지를 개발할 수 있습니다. [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에서는 다음과 같은 구성 유형을 제공합니다.  
  
-   XML 구성 파일  
  
-   환경 변수  
  
-   레지스트리 항목  
  
-   부모 패키지 변수  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 테이블  
  
이 단원에서는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 예제 패키지([4단원: SSIS를 사용하여 오류 흐름 리디렉션 추가](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)에서 만듬)를 수정하여 패키지 배포 모델을 사용하고 패키지 구성을 활용합니다. 또한 이 자습서에 포함된 완료된 4단원 패키지를 복사할 수도 있습니다. 

패키지 구성 마법사를 사용하여 Foreach 루프 컨테이너의 **Directory** 속성을 업데이트하는 XML 구성을 만듭니다. **Directory** 속성에 매핑된 패키지 수준 변수를 사용하세요. 구성 파일을 만든 후에 변수 값을 개발 환경 외부에서 새 샘플 데이터 폴더 경로로 수정하세요. 패키지를 다시 실행하면 구성 파일이 변수 값을 채우고 해당 변수가 **Directory** 속성을 업데이트합니다. 그런 다음, 패키지는 하드 코딩된 원래 폴더가 아닌 새 데이터 폴더에서 파일을 반복합니다.  
  
> [!NOTE]
> 아직 준비가 되지 않았다면 [1단원 필수 구성 요소](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites)를 참조하세요.
  
## <a name="lesson-tasks"></a>단원 태스크  
이 단원에서는 다음 태스크를 다룹니다.  
  
-   [1단계: 4단원 패키지 복사](../integration-services/lesson-5-1-copying-the-lesson-4-package.md)  
  
-   [2단계: 패키지 구성 설정 및 구성](../integration-services/lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
-   [3단계: Directory 속성 구성 값 수정](../integration-services/lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
-   [4단계: 5단원 패키지 테스트](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>단원 시작  
  
-   [1단계: 4단원 패키지 복사](../integration-services/lesson-5-1-copying-the-lesson-4-package.md)  
  
  
  
