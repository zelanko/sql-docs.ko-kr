---
title: '5단원: 패키지 배포 모델을 위한 패키지 구성 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1c10dd54-67cb-4b63-9e4d-aa6ff0452ecb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 25922725e202bc7b38e2c6141a097df1af119ed2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767425"
---
# <a name="lesson-5-adding-package-configurations-for-the-package-deployment-model"></a>5단원: 패키지 배포 모델을 위한 패키지 구성 추가
  패키지 구성을 사용하면 개발 환경 외부에서 런타임 속성과 변수를 설정할 수 있습니다. 구성을 통해 쉽고 유연하게 배포할 수 있는 패키지를 개발할 수 있습니다. [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서는 다음과 같은 구성 유형을 제공합니다.  
  
-   XML 구성 파일  
  
-   환경 변수  
  
-   레지스트리 항목  
  
-   부모 패키지 변수  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 테이블  
  
 이 단원에서는 간단한 수정 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 만든 패키지 [4 단원: 오류 흐름 리디렉션 추가](lesson-4-add-error-flow-redirection-with-ssis.md) 패키지 배포 모델을 사용 하 여 패키지 구성을 활용 합니다. 또한 자습서에 포함된 완료된 4단원 패키지를 복사할 수도 있습니다. 패키지 구성 마법사를 통해 Directory 속성에 매핑된 패키지 수준 변수를 사용하여 Foreach 루프 컨테이너의 `Directory` 속성을 업데이트하는 XML 구성을 만듭니다. 구성 파일을 생성했으면 개발 환경 외부에서 변수 값을 수정하고 수정된 속성을 새 예제 데이터 폴더로 지정합니다. 패키지를 다시 실행 하 고 구성 파일은 변수의 값을 채웁니다 변수 업데이트 하는 경우는 `Directory` 속성입니다. 결과적으로 패키지는 패키지에 하드 코드된 원래 폴더의 파일이 아니라 새 데이터 폴더의 파일을 반복 처리합니다.  
  
> [!IMPORTANT]  
>  이 자습서를 실행하려면 **AdventureWorksDW2012** 예제 데이터베이스가 필요합니다. **AdventureWorksDW2012**의 설치 및 배포 방법에 대한 자세한 내용은 [CodePlex의 Reporting Services 제품 샘플](https://go.microsoft.com/fwlink/?LinkID=526910)을 참조하십시오.  
  
## <a name="lesson-tasks"></a>단원 태스크  
 이 단원에서는 다음 태스크를 다룹니다.  
  
-   [1단계: 4 단원 패키지 복사](lesson-5-1-copying-the-lesson-4-package.md)  
  
-   [2단계: 패키지 구성 설정 및 구성](lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
-   [3단계: Directory 속성 구성 값 수정](lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
-   [4단계: 5 단원 자습서 패키지 테스트](lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>단원 시작  
  
-   [1단계: 4 단원 패키지 복사](lesson-5-1-copying-the-lesson-4-package.md)  
  
  
