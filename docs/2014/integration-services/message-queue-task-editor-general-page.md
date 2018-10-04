---
title: 메시지 큐 태스크 편집기 (일반 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.msgqueuetask.general.f1
helpviewer_keywords:
- Message Queue Task Editor
ms.assetid: 09368b18-37a5-4321-a173-7cfe5d42d2a2
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ea436e349a19d10eeb86a62b74f154b56b60ef7a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48204013"
---
# <a name="message-queue-task-editor-general-page"></a>메시지 큐 태스크 편집기(일반 페이지)
  **메시지 큐 태스크 편집기** 대화 상자의 **일반 페이지** 를 사용하여 메시지 큐 태스크의 이름을 지정하고 설명하며 메시지 형식을 지정하고 태스크에서 메시지를 보내거나 받을지를 나타낼 수 있습니다.  
  
 이 태스크에 대한 자세한 내용은 [Message Queue Task](control-flow/message-queue-task.md)를 참조하십시오.  
  
## <a name="options"></a>변수  
 **이름**  
 메시지 큐 태스크에 사용할 고유 이름을 제공합니다. 이 이름은 태스크 아이콘에서 레이블로 사용됩니다.  
  
> [!NOTE]  
>  태스크 이름은 패키지 내에서 고유해야 합니다.  
  
 **설명**  
 메시지 큐 태스크에 대한 설명을 입력합니다.  
  
 **Use2000Format**  
 2000 형식의 MSMQ(메시지 큐)를 사용할지 여부를 나타냅니다. 기본값은 `False`입니다.  
  
 **MSMQConnection**  
 기존 MSMQ 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목**: [MSMQ 연결 관리자](connection-manager/msmq-connection-manager.md), [MSMQ 연결 관리자 편집기](../../2014/integration-services/msmq-connection-manager-editor.md)  
  
 **메시지**  
 메시지 큐 태스크에서 메시지를 보내거나 받을지를 지정합니다. **메시지 보내기**를 선택하면 대화 상자의 왼쪽 창에 보내기 페이지가 표시되고 **메시지 받기**를 선택하면 받기 페이지가 표시됩니다. 기본적으로 이 값은 **메시지 보내기**로 설정됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [메시지 큐 태스크 편집기 &#40;페이지를 수신 합니다.&#41;](../../2014/integration-services/message-queue-task-editor-receive-page.md)   
 [메시지 큐 태스크 편집기 &#40;보내기 페이지&#41;](../../2014/integration-services/message-queue-task-editor-send-page.md)   
 [식 페이지](expressions/expressions-page.md)  
  
  
