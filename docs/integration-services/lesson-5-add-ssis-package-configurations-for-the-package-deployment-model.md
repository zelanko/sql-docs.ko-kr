---
title: '5단원: 패키지 배포 모델을 위한 SSIS 패키지 구성 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 1c10dd54-67cb-4b63-9e4d-aa6ff0452ecb
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7248f267678ec1800f881362fb368e363e52b4bd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-5-add-ssis-package-configurations-for-the-package-deployment-model"></a>5단원: 패키지 배포 모델을 위한 SSIS 패키지 구성 추가
패키지 구성을 사용하면 개발 환경 외부에서 런타임 속성과 변수를 설정할 수 있습니다. 구성을 통해 쉽고 유연하게 배포할 수 있는 패키지를 개발할 수 있습니다. [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서는 다음과 같은 구성 유형을 제공합니다.  
  
-   XML 구성 파일  
  
-   환경 변수  
  
-   레지스트리 항목  
  
-   부모 패키지 변수  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] table  
  
이 단원에서는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 4단원: SSIS를 사용하여 오류 흐름 리디렉션 추가 [에서 만든 간단한](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md) 패키지를 수정하여 패키지 배포 모델을 사용하고 패키지 구성을 활용합니다. 또한 자습서에 포함된 완료된 4단원 패키지를 복사할 수도 있습니다. 패키지 구성 마법사를 통해 Directory 속성에 매핑된 패키지 수준 변수를 사용하여 Foreach 루프 컨테이너의 **Directory** 속성을 업데이트하는 XML 구성을 만듭니다. 구성 파일을 생성했으면 개발 환경 외부에서 변수 값을 수정하고 수정된 속성을 새 예제 데이터 폴더로 지정합니다. 패키지를 다시 실행하면 구성 파일이 변수 값을 채우고 해당 변수가 **Directory**속성을 업데이트합니다. 결과적으로 패키지는 패키지에 하드 코드된 원래 폴더의 파일이 아니라 새 데이터 폴더의 파일을 반복 처리합니다.  
  
> [!IMPORTANT]  
> 이 자습서를 실행하려면 **AdventureWorksDW2012** 예제 데이터베이스가 필요합니다. **AdventureWorksDW2012**의 설치 및 배포 방법에 대한 자세한 내용은 [CodePlex의 Reporting Services 제품 샘플](http://go.microsoft.com/fwlink/p/?LinkID=526910)을 참조하십시오.  
  
## <a name="lesson-tasks"></a>단원 태스크  
이 단원에서는 다음 태스크를 다룹니다.  
  
-   [1단계: 4단원 패키지 복사](../integration-services/lesson-5-1-copying-the-lesson-4-package.md)  
  
-   [2단계: 패키지 구성 설정 및 구성](../integration-services/lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
-   [3단계: Directory 속성 구성 값 수정](../integration-services/lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
-   [4단계: 5단원 자습서 패키지 테스트](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>단원 시작  
  
-   [1단계: 4단원 패키지 복사](../integration-services/lesson-5-1-copying-the-lesson-4-package.md)  
  
  
  
