---
title: '3단계: 3단원 자습서 패키지 테스트 | Microsoft Docs'
ms.custom: ''
ms.date: 01/04/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 1096a476-93cf-4474-86f5-27d6357eb380
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c7e644744a53318ed1359bc0cdb47c3c896ed5ff
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58274849"
---
# <a name="lesson-3-3-test-the-lesson-3-tutorial-package"></a>3-3단원: 3단원 자습서 패키지 테스트

이 태스크에서는 **Lesson 3.dtsx** 패키지를 실행합니다. 패키가 실행될 때 **로그 이벤트** 창에는 로그 공급자가 로그 파일에 기록하는 SSIS인 로그 항목이 나열됩니다. 패키지 실행이 완료되면 로그 파일의 내용을 볼 수 있습니다.  
  
## <a name="check-the-package-layout"></a>패키지 레이아웃 확인  
패키지를 테스트하기 전에, 다음 다이어그램에 표시된 개체와 유사한 3단원 패키지의 제어 흐름과 데이터 흐름을 확인합니다. 제어 흐름은 2단원과 동일해야 하고 데이터 흐름은 1단원 및 2단원과 동일해야 합니다.  
  
**제어 흐름**  
  
![패키지의 제어 흐름](../integration-services/media/task4lesson2control.gif "패키지의 제어 흐름")  
  
**데이터 흐름**  
  
![패키지의 데이터 흐름](../integration-services/media/task9lesson1data.gif "패키지의 데이터 흐름")  
  
## <a name="run-the-lesson-3-tutorial-package"></a>3단원 자습서 패키지 실행  
  
1.  SSIS 메뉴에서 **로그 이벤트**를 선택합니다.  
  
2.  **디버그** 메뉴에서 **디버깅 시작**을 선택합니다.  
  
3.  패키지의 실행이 완료된 후에 **디버그** 메뉴에서 **디버깅 중지**를 선택합니다.  
  
## <a name="examine-the-generated-log-file"></a>생성된 로그 파일 검사  
  
-   메모장이나 다른 텍스트 편집기를 사용하여 TutorialLog.log 파일을 엽니다.  
  
-   **PipelineExecutionPlan** 및 **PipelineExecutionTrees** 이벤트에 대해 생성된 정보에 대한 전체 설명은 이 자습서의 범위를 벗어납니다.  로그 파일에서 첫 번째 줄에 **SSIS 로그 구성** 대화 상자의 **세부 정보** 탭에 지정된 정보 필드가 나열되어 있는 것을 볼 수 있습니다. 또한 Foreach 루프가 반복될 때마다 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]가 선택한 두 이벤트 **PipelineExecutionPlan**과 **PipelineExecutionTrees**를 기록한 것을 볼 수 있습니다.  
  
## <a name="next-lesson"></a>다음 단원  
[4단원: SSIS를 사용하여 오류 흐름 리디렉션 추가](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
  
  
  
