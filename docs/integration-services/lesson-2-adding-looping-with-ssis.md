---
title: "2단원: SSIS를 사용하여 루핑 추가 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 01f2ed61-1e5a-4ec6-b6a6-2bd070c64077
caps.latest.revision: 32
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 32
---
# 2단원: SSIS를 사용하여 루핑 추가
[1단원: SSIS를 사용하여 프로젝트 및 기본 패키지 만들기](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md)에서는 단일 플랫 파일 원본에서 데이터를 추출하고 조회 변환을 사용하여 변환한 다음 **AdventureWorksDW2012** 샘플 데이터베이스의 **FactCurrency** 팩트 테이블로 로드한 패키지를 만들었습니다.  
  
그러나 ETL(추출, 변환 및 로드) 프로세스에서 플랫 파일을 하나만 사용하는 경우는 거의 없습니다. 일반적인 ETL 프로세스는 여러 플랫 파일 원본에서 데이터를 추출합니다. 여러 원본에서 데이터를 추출하려면 반복적인 제어 흐름이 필요합니다.  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 의 가장 기대되는 기능 중 하나는 패키지에 반복이나 루핑을 쉽게 추가할 수 있는 기능입니다.  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서는 Foreach Loop 컨테이너와 For Loop 컨테이너라는 패키지 루핑을 위한 두 가지 유형의 컨테이너를 제공합니다. Foreach 루프 컨테이너는 열거자를 사용하여 루핑을 수행하지만 For 루프 컨테이너는 대개 변수 식을 사용합니다. 이 단원에서는 Foreach 루프 컨테이너를 사용합니다.  
  
Foreach 루프 컨테이너를 사용하면 패키지에서 지정한 열거자의 각 멤버에 대해 제어 흐름을 반복할 수 있습니다. Foreach 루프 컨테이너를 사용하여 다음과 같은 항목을 열거할 수 있습니다.  
  
-   ADO 레코드 집합 행  
  
-   ADO.Net 스키마 정보  
  
-   파일 및 디렉터리 구조  
  
-   시스템, 패키지 및 사용자 변수  
  
-   변수에 포함된 열거 가능한 개체  
  
-   컬렉션의 항목  
  
-   XML 경로 언어(XPath)식의 노드  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] SMO(Management Objects)(!!)  
  
이 단원에서는 1단원에서 만든 단순 ETL 패키지를 Foreach 루프 컨테이너를 사용하도록 수정하고 자습서 패키지에서 폴더에 있는 모든 플랫 파일을 반복 처리할 수 있도록 사용자 정의 패키지 변수를 설정하는 방법에 대해 설명합니다. 이전 단원을 완료하지 않은 경우 자습서에 완성된 상태로 포함된 1단원 패키지를 복사할 수도 있습니다.  
  
이 단원에서는 데이터 흐름을 수정하지 않고 제어 흐름만 수정합니다.  
  
> [!IMPORTANT]  
> 이 자습서를 실행하려면 **AdventureWorksDW2012** 예제 데이터베이스가 필요합니다. **AdventureWorksDW2012**의 설치 및 배포 방법에 대한 자세한 내용은 [CodePlex의 Reporting Services 제품 샘플](http://go.microsoft.com/fwlink/p/?LinkID=526910)을 참조하십시오.  
  
## 단원 태스크  
이 단원에서는 다음 태스크를 다룹니다.  
  
-   [1단계: 1단원 패키지 복사](../integration-services/step-1-copying-the-lesson-1-package.md)  
  
-   [2단계: Foreach 루프 컨테이너 추가 및 구성](../integration-services/step-2-adding-and-configuring-the-foreach-loop-container.md)  
  
-   [3단계: 플랫 파일 연결 관리자 수정](../integration-services/step-3-modifying-the-flat-file-connection-manager.md)  
  
-   [4단계: 2단원 자습서 패키지 테스트](../integration-services/step-4-testing-the-lesson-2-tutorial-package.md)  
  
## 단원 시작  
[1단계: 1단원 패키지 복사](../integration-services/step-1-copying-the-lesson-1-package.md)  
  
## 참고 항목  
[For 루프 컨테이너](../integration-services/control-flow/for-loop-container.md)  
  
  
  
