---
title: 프로세스 실행 태스크 편집기 (프로세스 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executeprocesstask.process.f1
helpviewer_keywords:
- Execute Process Task Editor
ms.assetid: 0fc22406-e79b-47a4-a7e4-108d4ce6202f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fa799404777f8f0ef0a8a07a81c8c7961c636004
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66059025"
---
# <a name="execute-process-task-editor-process-page"></a>프로세스 실행 태스크 편집기(프로세스 페이지)
  **프로세스 실행 태스크 편집기** 대화 상자의 **프로세스** 페이지를 사용하여 프로세스 실행 옵션을 구성할 수 있습니다. 이러한 옵션에는 실행할 실행 파일, 해당 위치, 명령 프롬프트 인수, 입력 제공 및 출력 캡처 변수가 포함됩니다.  
  
 이 태스크에 대한 자세한 내용은 [Execute Process Task](control-flow/execute-process-task.md)를 참조하세요.  
  
## <a name="options"></a>옵션  
 **RequireFullFileName**  
 지정한 위치에 실행 파일이 없는 경우 태스크 실패 여부를 나타냅니다.  
  
 **실행 파일**  
 실행할 실행 파일 이름을 입력합니다.  
  
 **인수**  
 명령 프롬프트 인수를 제공합니다.  
  
 **WorkingDirectory**  
 실행 파일이 포함 된 폴더의 경로를 입력 하거나 찾아보기 단추 **(...)** 를 클릭 하 여 폴더를 찾습니다.  
  
 **StandardInputVariable**  
 프로세스에 입력을 제공할 변수를 선택 하거나 \< **새 변수** ...>를 클릭 하 여 새 변수를 만듭니다.  
  
 **관련 항목:**  [변수 추가](../../2014/integration-services/add-variable.md)  
  
 **StandardOutputVariable**  
 프로세스 출력을 캡처할 변수를 선택 하거나 \< **새 변수** ...>를 클릭 하 여 새 변수를 만듭니다.  
  
 **StandardErrorVariable**  
 프로세서의 오류 출력을 캡처할 변수를 선택 하거나 \< **새 변수** ...>를 클릭 하 여 새 변수를 만듭니다.  
  
 **FailTaskIfReturnCodeIsNotSuccessValue**  
 프로세스 종료 코드가 **SuccessValue**에 지정한 값과 다른 경우 태스크 실패 여부를 나타냅니다.  
  
 **SuccessValue**  
 성공을 표시하기 위해 실행 파일에서 반환하는 값을 지정합니다. 기본적으로 이 값은 **0**으로 설정됩니다.  
  
 **초과가**  
 프로세스가 실행될 수 있는 시간(초)을 지정합니다. 값 **0** 은 제한 시간 값이 사용되지 않으며 프로세스가 완료되거나 오류가 발생할 때까지 실행됨을 나타냅니다.  
  
 **TerminateProcessAfterTimeOut**  
 **TimeOut** 옵션에 지정한 제한 시간 후의 프로세스 강제 종료 여부를 나타냅니다. 이 옵션은 **TimeOut** 이 **0**이 아닌 경우에만 사용할 수 있습니다.  
  
 **WindowStyle**  
 프로세스를 실행할 창 스타일을 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [식 페이지](expressions/expressions-page.md)  
  
  
