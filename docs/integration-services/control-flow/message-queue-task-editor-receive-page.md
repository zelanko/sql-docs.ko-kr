---
title: "메시지 큐 태스크 편집기 (받기 페이지) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.msgqueuetask.receive.f1
helpviewer_keywords:
- Message Queue Task Editor
ms.assetid: 7028756d-1dcc-480c-bbcd-e9654f0772a0
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1f51937fa402accf4e18fefdcec5763987241de4
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="message-queue-task-editor-receive-page"></a>메시지 큐 태스크 편집기(받기 페이지)
  **메시지 큐 태스크 편집기** 대화 상자의 **받기** 페이지를 사용하여 메시지 큐 태스크가 MSMQ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing) 메시지를 받도록 구성할 수 있습니다.  
  
 이 태스크에 대한 자세한 내용은 [Message Queue Task](../../integration-services/control-flow/message-queue-task.md)를 참조하십시오.  
  
## <a name="options"></a>옵션  
 **RemoveFromMessageQueue**  
 메시지를 받은 후 큐에서 제거할지 여부를 나타냅니다. 기본적으로 이 값은 **False**로 설정되어 있습니다.  
  
 **ErrorIfMessageTimeOut**  
 메시지 제한 시간이 초과할 경우 태스크 실패로 처리하고 오류 메시지를 표시할지 여부를 나타냅니다. 기본값은 **False**입니다.  
  
 **TimeoutAfter**  
 태스크 실패 시 오류 메시지를 표시하도록 선택하는 경우 제한 시간 오류 메시지가 표시될 때까지 기다리는 시간(초)을 지정합니다.  
  
 **MessageType**  
 메시지 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**데이터 파일 메시지**|메시지가 파일에 저장됩니다. 이 값을 선택하면 동적 옵션 **DataFileMessage**가 표시됩니다.|  
|**변수 메시지**|메시지가 변수에 저장됩니다. 이 값을 선택하면 동적 옵션 **VariableMessage**가 표시됩니다.|  
|**문자열 메시지**|메시지가 메시지 큐 태스크에 저장됩니다. 이 값을 선택하면 동적 옵션 **StringMessage**가 표시됩니다.|  
|**변수에 대한 문자열 메시지**|메시지<br /><br /> 이 값을 선택하면 동적 옵션 **StringMessage**가 표시됩니다.|  
  
## <a name="messagetype-dynamic-options"></a>MessageType 동적 옵션  
  
### <a name="messagetype--data-file-message"></a>MessageType = 데이터 파일 메시지  
 **SaveFileAs**  
 사용할 파일의 경로를 입력하거나 줄임표 단추 **(...)** 를 클릭한 다음 파일을 찾습니다.  
  
 **Overwrite**  
 데이터 파일 메시지의 내용을 저장할 경우 기존 파일의 데이터를 덮어쓸지 여부를 나타냅니다. 기본값은 **False**입니다.  
  
 **필터**  
 필터를 메시지에 적용할지 여부를 지정합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**필터 없음**|태스크에서 메시지를 필터링하지 않습니다. 이 값을 선택하면 동적 옵션 **IdentifierReadOnly**가 표시됩니다.|  
|**받을 패키지**|메시지는 지정한 패키지의 메시지만 받습니다. 이 값을 선택하면 동적 옵션 **Identifier**가 표시됩니다.|  
  
### <a name="filter-dynamic-options"></a>Filter 동적 옵션  
  
#### <a name="filter--no-filter"></a>Filter = 필터 없음  
 **IdentifierReadOnly**  
 이 옵션은 읽기 전용입니다. 이전에 Filter 속성을 설정할 때 이 옵션은 비어 있거나 패키지의 GUID를 포함할 수 있습니다.  
  
#### <a name="filter--from-package"></a>Filter = 받을 패키지  
 **Identifier**  
 필터를 적용하도록 선택한 경우 메시지를 받을 수 있는 패키지의 고유 식별자를 입력하거나 줄임표 단추 **(...)** 를 클릭한 다음 패키지를 지정합니다.  
  
 **관련 항목:** [패키지 선택](../../integration-services/control-flow/select-a-package.md)  
  
### <a name="messagetype--variable-message"></a>MessageType = 변수 메시지  
 **필터**  
 필터를 메시지에 적용할지 여부를 지정합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**필터 없음**|태스크에서 메시지를 필터링하지 않습니다. 이 값을 선택하면 동적 옵션 **IdentifierReadOnly**가 표시됩니다.|  
|**받을 패키지**|메시지는 지정한 패키지의 메시지만 받습니다. 이 값을 선택하면 동적 옵션 **Identifier**가 표시됩니다.|  
  
 **변수**  
 변수 이름을 입력 하거나 클릭 \< **새 변수...** > 새 변수를 구성 합니다.  
  
 **관련 항목:** [변수 추가](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
### <a name="filter-dynamic-options"></a>Filter 동적 옵션  
  
#### <a name="filter--no-filter"></a>Filter = 필터 없음  
 **IdentifierReadOnly**  
 이 옵션은 비어 있습니다.  
  
#### <a name="filter--from-package"></a>Filter = 받을 패키지  
 **Identifier**  
 필터를 적용하도록 선택한 경우 메시지를 받을 수 있는 패키지의 고유 식별자를 입력하거나 줄임표 단추 **(...)** 를 클릭한 다음 패키지를 지정합니다.  
  
 **관련 항목:** [패키지 선택](../../integration-services/control-flow/select-a-package.md)  
  
### <a name="messagetype--string-message"></a>MessageType = 문자열 메시지  
 **Compare**  
 필터를 메시지에 적용할지 여부를 지정합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**InclusionThresholdSetting**|메시지를 비교하지 않습니다.|  
|**정확히 일치**|메시지가 **CompareString** 옵션의 문자열과 정확히 일치해야 합니다.|  
|**대/소문자 무시**|메시지가 **CompareString** 옵션의 문자열과 일치해야 하지만 비교 시 대/소문자를 무시합니다.|  
|**포함**|메시지가 **CompareString** 옵션의 문자열을 포함해야 합니다.|  
  
 **CompareString**  
 **Compare** 옵션을 **없음**으로 설정한 경우가 아니면 메시지를 비교할 문자열을 제공합니다.  
  
### <a name="messagetype--string-message-to-variable"></a>MessageType = 변수에 대한 문자열 메시지  
 **Compare**  
 필터를 메시지에 적용할지 여부를 지정합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**InclusionThresholdSetting**|메시지를 비교하지 않습니다.|  
|**정확히 일치**|메시지가 **CompareString** 옵션의 문자열과 정확히 일치해야 합니다.|  
|**대/소문자 무시**|메시지가 **CompareString** 옵션의 문자열과 일치해야 하지만 비교 시 대/소문자를 무시합니다.|  
|**포함**|메시지가 **CompareString** 옵션의 문자열을 포함해야 합니다.|  
  
 **CompareString**  
 **Compare** 옵션을 **없음**으로 설정한 경우가 아니면 메시지를 비교할 문자열을 제공합니다.  
  
 **변수**  
 받은 메시지를 보유 하거나 클릭 하 여 변수 이름을 입력 \< **새 변수...** > 새 변수를 구성 합니다.  
  
 **관련 항목:** [변수 추가](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="see-also"></a>관련 항목:  
 [Integration Services 오류 및 메시지 참조](../../integration-services/integration-services-error-and-message-reference.md)   
 [메시지 큐 태스크 편집기 &#40; 일반 페이지 &#41;](../../integration-services/control-flow/message-queue-task-editor-general-page.md)   
 [메시지 큐 태스크 편집기 &#40; 전송 페이지 &#41;](../../integration-services/control-flow/message-queue-task-editor-send-page.md)   
 [식 페이지](../../integration-services/expressions/expressions-page.md)   
 [메시지 큐 태스크](../../integration-services/control-flow/message-queue-task.md)  
  
  
