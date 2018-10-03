---
title: '3단계: 플랫 파일 연결 관리자 수정 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 459e3995-2116-4f15-aaa2-32f26113869c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2e5f2aecb84754ee470a9cbafabdf06e38d38ae1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48102043"
---
# <a name="step-3-modifying-the-flat-file-connection-manager"></a>3단계: 플랫 파일 연결 관리자 수정
  이 태스크에서는 1단원에서 만들어 구성한 플랫 파일 연결 관리자를 수정합니다. 처음 만든 플랫 파일 연결 관리자는 파일 하나를 정적으로 로드하도록 구성되어 있습니다. 플랫 파일 연결 관리자를 사용하여 반복적으로 파일을 로드하려면 런타임에 로드할 파일의 경로를 포함하는 사용자 정의 변수 `User:varFileName`을 허용하도록 연결 관리자의 ConnectionString 속성을 수정해야 합니다.  
  
 사용자 정의 변수 `User::varFileName`의 값을 사용하도록 연결 관리자를 수정하여 해당 관리자의 ConnectionString 속성을 채우면 연결 관리자가 여러 플랫 파일에 연결할 수 있습니다. 런타임에 Foreach 루프 컨테이너가 반복될 때마다 `User::varFileName` 변수가 동적으로 업데이트됩니다. 따라서 변수를 업데이트하면 연결 관리자가 다른 플랫 파일에 연결하고 데이터 흐름 태스크가 다른 데이터 집합을 처리합니다.  
  
### <a name="to-configure-the-flat-file-connection-manager-to-use-a-variable-for-the-connection-string"></a>연결 문자열에 변수를 사용하도록 플랫 파일 연결 관리자를 구성하려면  
  
1.  **연결 관리자** 창에서 **Sample Flat File Source Data**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
2.  속성 창에서 **Expressions**의 빈 셀을 클릭한 다음 줄임표 단추 **(…)** 를 클릭합니다.  
  
3.  에 **속성 식 편집기** 대화 상자의 합니다 **속성** 열, 입력 또는 선택 `ConnectionString`합니다.  
  
4.  **식** 열에서 줄임표 단추 **(…)** 를 클릭하여 **식 작성기** 대화 상자를 엽니다.  
  
5.  **식 작성기** 대화 상자에서 **변수** 노드를 확장합니다.  
  
6.  **User::varFileName**변수를 **식** 상자로 끌어 놓습니다.  
  
7.  **확인** 을 클릭하여 **식 작성기** 대화 상자를 닫습니다.  
  
8.  다시 **확인** 을 클릭하여 **PropertiesExpressionEditor** 대화 상자를 닫습니다.  
  
## <a name="next-lesson-task"></a>다음 단원 태스크  
 [4단계: 2단원 자습서 패키지 테스트](../integration-services/lesson-2-4-testing-the-lesson-2-tutorial-package.md)  
  
  
