---
title: 데이터 흐름 구성 요소에서 식 사용 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], data flow
- expressions [Integration Services], data flow components
ms.assetid: 9181b998-d24a-41fb-bb3c-14eee34f910d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0c996889b6127bb8ea16bab077bfd9d757921b11
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85420350"
---
# <a name="use-an-expression-in-a-data-flow-component"></a>데이터 흐름 구성 요소에서 식 사용
  이 절차에서는 조건부 분할 변환 또는 파생 열 변환에 식을 추가하는 방법을 설명합니다. 조건부 분할 변환에서는 데이터 행을 변환 출력으로 바꾸는 조건을 정의하는 데 식을 사용하며 파생 열 변환에서는 열에 할당된 값을 정의하는 데 식을 사용합니다.  
  
 변환에서 식을 구현하려면 패키지에 적어도 하나 이상의 데이터 흐름 태스크와 원본이 이미 들어 있어야 합니다. 패키지에 항목을 추가하는 방법은 다음 항목을 참조하십시오.  
  
-   [제어 흐름에서 태스크 또는 컨테이너 추가 또는 삭제](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
    
  
-   [데이터 흐름에서 구성 요소 추가 또는 삭제](data-flow/add-or-delete-a-component-in-a-data-flow.md)  
  
-   [데이터 흐름의 구성 요소 연결](data-flow/connect-components-in-a-data-flow.md)  
  
### <a name="to-create-an-expression"></a>식을 만들려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 **제어 흐름** 탭을 클릭하고 식을 구현할 데이터 흐름이 포함된 데이터 흐름 태스크를 클릭합니다.  
  
4.  **데이터 흐름** 탭을 클릭하고 **도구 상자** 에서 조건부 분할 변환 또는 파생 열 변환을 디자인 화면으로 끌어 옵니다.  
  
5.  원본 또는 변환의 녹색 연결선을 조건부 분할 변환 또는 파생 열 변환으로 끌어 옵니다.  
  
6.  변환을 두 번 클릭하여 대화 상자를 엽니다.  
  
7.  왼쪽 창에서 **변수** 를 확장하여 시스템 및 사용자 정의 변수를 표시하고 **열** 을 확장하여 변환 입력 열을 표시합니다.  
  
8.  오른쪽 창에서 **수치 연산 함수**, **문자열 함수**, **날짜/시간 함수**, **NULL 함수**, **형식 캐스트**및 **연산자** 를 확장하여 식 문법이 제공하는 함수, 캐스트 및 연산자에 액세스합니다.  
  
9. 변환에 따라 다음 중 하나를 수행하여 식을 작성합니다.  
  
    -   **조건부 분할 변환 편집기** 대화 상자에서 변수, 열, 함수, 연산자 및 캐스트를 **조건** 열로 끌어 옵니다. 또는 **조건** 열에 직접 식을 입력할 수 있습니다.  
  
    -   **파생 열 변환 편집기** 대화 상자에서 변수, 열, 함수, 연산자 및 캐스트를 **식** 열로 끌어 옵니다. 또는 **식** 열에 직접 식을 입력할 수 있습니다.  
  
        > [!NOTE]  
        >  **조건** 열이나 **식** 열에서 포커스가 제거될 때 식 구문이 유효하지 않은 경우 식 텍스트가 강조 표시될 수 있습니다.  
  
10. **확인**을 클릭하여 대화 상자를 닫습니다.  
  
    > [!NOTE]  
    >  식이 유효하지 않으면 식의 구문 오류를 설명하는 경고가 나타납니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services &#40;SSIS&#41; 식](expressions/integration-services-ssis-expressions.md)   
 [조건부 분할 변환](data-flow/transformations/conditional-split-transformation.md)   
 [파생 열 변환](data-flow/transformations/derived-column-transformation.md)   
 [데이터 흐름 태스크](control-flow/data-flow-task.md)   
 [데이터 흐름](data-flow/data-flow.md)  
  
  
