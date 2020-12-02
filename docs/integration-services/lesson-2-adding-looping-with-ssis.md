---
description: '2단원: SSIS를 사용하여 루핑 추가'
title: '2단원: SSIS를 사용하여 루핑 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 01f2ed61-1e5a-4ec6-b6a6-2bd070c64077
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0805b8709e2a0a689538f558672694c96ddff39b
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88390669"
---
# <a name="lesson-2-add-looping-with-ssis"></a>2단원: SSIS를 사용하여 루핑 추가

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



[1단원: SSIS를 사용하여 프로젝트 및 기본 패키지 만들기](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md)의 단일 플랫 파일 원본에서 데이터를 추출하는 패키지를 만들었습니다. 그런 다음, 조회 변환을 사용하여 데이터를 변환합니다. 마지막으로 패키지는 **AdventureWorksDW2012** 샘플 데이터베이스의 **FactCurrencyRate** 팩트 테이블 복사본에 데이터를 로드합니다.  
  
추출, 변환 및 로드(ETL) 프로세스는 일반적으로 여러 플랫 파일 원본에서 데이터를 추출합니다. 여러 원본에서 데이터를 추출하려면 반복적인 제어 흐름이 필요합니다. [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에서는 패키지에 반복 또는 루핑을 쉽게 추가할 수 있습니다.  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서는 Foreach Loop 컨테이너와 For Loop 컨테이너라는 패키지 루핑을 위한 두 가지 유형의 컨테이너를 제공합니다. Foreach 루프 컨테이너는 루핑을 위해 열거자를 사용하지만 For 루프 컨테이너는 일반적으로 변수 식을 사용합니다. 이 단원에서는 Foreach 루프 컨테이너를 사용합니다.  
  
Foreach 루프 컨테이너를 사용하면 패키지에서 지정한 열거자의 각 멤버에 대해 제어 흐름을 반복할 수 있습니다. Foreach 루프 컨테이너를 사용하여 다음과 같은 항목을 열거할 수 있습니다.  
  
-   ADO 레코드 집합 행  
  
-   ADO.Net 스키마 정보  
  
-   파일 및 디렉터리 구조  
  
-   시스템, 패키지 및 사용자 변수  
  
-   변수의 열거 가능한 개체  
  
-   컬렉션의 항목  
  
-   XML 경로 언어(XPath)식의 노드  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] SMO(Management Objects)(!!)  
  
이 단원에서는 1단원의 예제 ETL 패키지를 수정하여 Foreach 루프 컨테이너를 사용하고 패키지에 대한 사용자 정의 패키지 변수를 설정합니다. 그런 다음, 해당 변수를 사용하여 샘플 폴더의 일치하는 파일을 반복합니다.   
  
이 단원에서는 데이터 흐름을 수정하지 않고 제어 흐름만 수정합니다.  
  
> [!NOTE]  
> 아직 준비가 되지 않았다면 [1단원 필수 구성 요소](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites)를 참조하세요.

## <a name="lesson-tasks"></a>단원 태스크  
이 단원에서는 다음 태스크를 다룹니다.  
  
-   [1단계: 1단원 패키지 복사](../integration-services/lesson-2-1-copying-the-lesson-1-package.md)  
  
-   [2단계: Foreach 루프 컨테이너 추가 및 구성](../integration-services/lesson-2-2-adding-and-configuring-the-foreach-loop-container.md)  
  
-   [3단계: 플랫 파일 연결 관리자 수정](../integration-services/lesson-2-3-modifying-the-flat-file-connection-manager.md)  
  
-   [4단계: 2단원 자습서 패키지 테스트](../integration-services/lesson-2-4-testing-the-lesson-2-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>단원 시작  
[1단계: 1단원 패키지 복사](../integration-services/lesson-2-1-copying-the-lesson-1-package.md)  
  
## <a name="see-also"></a>참고 항목  
[For 루프 컨테이너](../integration-services/control-flow/for-loop-container.md)  
  
  
  
