---
title: "1 단원: 배포 번들 작성 준비 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: b6fe283c-9856-4ba1-a497-e3912424fd18
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0850bf9b55f3960736d45b1730f25f6c96c667a9
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="lesson-1-preparing-to-create-the-deployment-bundle"></a>1단원: 배포 번들 작성 준비
이 단원에서는 자습서를 지원하는 작업 폴더 및 환경 변수를 만들고 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 만든 다음 여러 패키지와 지원 파일을 프로젝트에 추가하고 패키지에서 구성을 구현합니다.  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]는 패키지를 프로젝트 단위로 배포합니다. 따라서 배포 번들을 만드는 첫 번째 단계에서는 모든 패키지와 패키지 종속 파일을 하나의 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트에 수집해야 합니다. 배포된 패키지에 다른 정보를 포함하면 도움이 되는 경우가 많습니다. 예를 들어 이 패키지 그룹에 대한 기본 설명서를 제공하는 추가 정보 파일을 프로젝트에 추가합니다.  
  
패키지와 파일을 추가한 후에 아직 구성이 사용되지 않는 패키지에 구성을 추가합니다. 이러한 구성은 패키지 및 패키지 개체의 속성을 런타임에 업데이트합니다. 이후의 단원에서는 배포된 환경에서 패키지를 지원하기 위해 패키지 배포 도중에 이러한 구성의 값을 수정합니다.  
  
구성을 추가한 후에 ETL 패키지 작성을 위한 [!INCLUDE[ssIS](../includes/ssis-md.md)] 그래픽 도구인 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 디자이너에서 패키지를 열고 배포에서 해결해야 하는 문제를 더 잘 이해할 수 있도록 패키지 및 패키지 요소의 속성과 패키지 구성을 검사해야 합니다. 예를 들어 패키지 중 하나가 텍스트 파일에서 데이터를 추출하므로 배포된 패키지를 성공적으로 실행하려면 데이터 파일의 위치를 업데이트해야 합니다.  
  
**이 단원에 소요되는 예상 시간:** 1시간  
  
## <a name="lesson-tasks"></a>단원 태스크  
이 단원에서는 다음 태스크를 다룹니다.  
  
-   [1 단계: 만들기 작업 폴더 및 환경 변수](../integration-services/lesson-1-1-creating-working-folders-and-environment-variables.md)  
  
-   [2 단계: 배포 프로젝트 만들기](../integration-services/lesson-1-2-creating-the-deployment-project.md)  
  
-   [3 단계: 패키지 및 기타 파일 추가](../integration-services/lesson-1-3-adding-packages-and-other-files.md)  
  
-   [4 단계: 패키지 구성 추가](../integration-services/lesson-1-4-adding-package-configurations.md)  
  
-   [5 단계: 업데이트 된 패키지 테스트](../integration-services/lesson-1-5-testing-the-updated-packages.md)  
  
## <a name="start-the-lesson"></a>단원 시작  
[1단계: 작업 폴더 및 환경 변수 만들기](../integration-services/lesson-1-1-creating-working-folders-and-environment-variables.md)  
  
  
  

