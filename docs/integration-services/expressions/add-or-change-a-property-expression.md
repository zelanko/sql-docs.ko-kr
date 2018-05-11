---
title: 속성 식 추가 또는 변경 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: expressions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- expressions [Integration Services], creating
- expressions [Integration Services], property expressions
ms.assetid: cb5da499-065f-4fa6-9f6d-5bc5f385241e
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 423942773422452cc6b46b808fbe53a61270db2f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="add-or-change-a-property-expression"></a>속성 식 추가 또는 변경
  패키지, 태스크, Foreach 루프 컨테이너, For 루프 컨테이너, 시퀀스 컨테이너, 이벤트 처리기, 패키지 및 프로젝트 수준의 연결 관리자 및 로그 공급자에 속성 식을 만들 수 있습니다.  
  
 속성 식을 만들거나 변경하려면 **속성 식 편집기** 또는 **식 작성기**를 사용하면 됩니다. **속성 식 편집기** 는 태스크와 컨테이너에 사용할 수 있는 사용자 지정 편집기나 **속성** 창에서 액세스할 수 있고, **식 작성기** 는 **속성 식 편집기**내에서 액세스할 수 있습니다. **속성 식 편집기** 와 **식 작성기**모두에서 식을 작성할 수 있지만 **식 작성기** 에서는 복잡한 식을 간단하게 작성할 수 있게 해주는 그래픽 도구 집합을 제공합니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 제공하는 구문, 연산자 및 함수에 대한 자세한 내용은 [연산자&#40;SSIS 식&#41;](../../integration-services/expressions/operators-ssis-expression.md) 및 [함수&#40;SSIS 식&#41;](../../integration-services/expressions/functions-ssis-expression.md)를 참조하세요. 각 연산자 또는 함수에 대한 항목에는 식에 해당 연산자나 함수를 사용하는 예가 포함되어 있습니다. 더 복잡한 식의 예는 [패키지에서 속성 식 사용](../../integration-services/expressions/use-property-expressions-in-packages.md)을 참조하세요.  
  
### <a name="to-create-or-change-a-property-expression"></a>속성 식을 만들거나 변경하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지가 들어 있는 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 열고 다음 중 하나를 수행합니다.  
  
    -   항목이 태스크 또는 컨테이너인 경우 항목을 두 번 클릭한 다음 편집기에서 **식** 을 클릭합니다.  
  
    -   항목을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **식** 입력란을 클릭한 다음 줄임표(...)를 클릭합니다.  
  
4.  **속성 식 편집기**에서 **속성** 목록의 속성을 선택하고 다음 중 하나를 수행하십시오.  
  
    -   **식** 열에서 속성 식을 직접 입력하거나 변경한 다음 **확인**을 클릭합니다.  
  
         —또는—  
  
    -   속성의 식 행에서 줄임표(…)를 클릭하여 **식 작성기**를 엽니다.  
  
5.  (옵션) **식 작성기**에서 다음 태스크 중 하나를 수행합니다.  
  
    -   사용자 정의 변수에 액세스하려면 **변수**를 확장합니다.  
  
    -   [!INCLUDE[ssIS](../../includes/ssis-md.md)] 식 언어가 제공하는 함수, 캐스트 및 연산자에 액세스하려면 **수치 연산 함수**, **문자열 함수**, **날짜/시간 함수**, **NULL 함수**, **형식 캐스팅**및 **연산자**를 확장합니다.  
  
    -   **식 작성기**에서 식을 작성하거나 변경하려면 변수, 열, 함수, 연산자 및 캐스트를 **식** 입력란으로 끌어 놓거나 이 입력란에 식을 직접 입력합니다.  
  
    -   식의 계산 결과를 보려면 **식 작성기** 에서 **식 계산**을 클릭합니다.  
  
         식이 유효하지 않으면 식의 구문 오류를 설명하는 경고가 나타납니다.  
  
        > [!NOTE]  
        >  식 계산은 계산 결과를 속성에 할당하지 않습니다.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services&#40;SSIS&#41; 식](../../integration-services/expressions/integration-services-ssis-expressions.md)   
 [패키지에서 속성 식 사용](../../integration-services/expressions/use-property-expressions-in-packages.md)   
 [Integration Services&#40;SSIS&#41; 패키지](../../integration-services/integration-services-ssis-packages.md)   
 [Integration Services 컨테이너](../../integration-services/control-flow/integration-services-containers.md)   
 [Integration Services 태스크](../../integration-services/control-flow/integration-services-tasks.md)   
 [Integration Services&#40;SSIS&#41; 이벤트 처리기](../../integration-services/integration-services-ssis-event-handlers.md)   
 [Integration Services&#40;SSIS&#41; 연결](../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [Integration Services&#40;SSIS&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)  
  
  
