---
title: 메시지 큐 태스크 편집기 (보내기 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.msgqueuetask.send.f1
helpviewer_keywords:
- Message Queue Task Editor
ms.assetid: 565aa079-ac44-4407-8efc-cddab839de30
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 66323ccdb91076496f9796245c368697d9ebc8c3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66057597"
---
# <a name="message-queue-task-editor-send-page"></a>메시지 큐 태스크 편집기(보내기 페이지)
  **메시지 큐 태스크 편집기** 대화 상자의 **보내기** 페이지를 사용하여 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지에서 메시지를 보내도록 메시지 큐 태스크를 구성할 수 있습니다.  
  
 이 태스크에 대한 자세한 내용은 [Message Queue Task](control-flow/message-queue-task.md)를 참조하십시오.  
  
## <a name="options"></a>옵션  
 **UseEncryption**  
 메시지 암호화 여부를 나타냅니다. 기본값은 `False`입니다.  
  
 **EncryptionAlgorithm**  
 암호화 사용을 선택한 경우 사용할 암호화 알고리즘의 이름을 지정합니다. 메시지 큐 태스크에는 RC2 및 RC4 알고리즘을 사용할 수 있습니다. 기본값은 **RC2**입니다.  
  
> [!NOTE]  
>  RC4 알고리즘은 이전 버전과의 호환성을 위해서만 지원됩니다. 데이터베이스의 호환성 수준이 90 또는 100인 경우 새 자료는 RC4 또는 RC4_128로만 암호화할 수 있습니다. 이 옵션은 사용하지 않는 것이 좋습니다. 대신 AES 알고리즘 중 하나와 같은 새 알고리즘을 사용하십시오. 현재 릴리스의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 RC4 또는 RC4_128을 사용하여 암호화된 자료는 모든 호환성 수준에서 해독할 수 있습니다.  
  
> [!IMPORTANT]  
>  이러한 알고리즘은 MSMQ(메시지 큐) 기술에서 지원하는 암호화 알고리즘입니다. 이 두 암호화 알고리즘은 메시지 큐에서 현재 지원하지 않는 최신 알고리즘에 비해 암호화 방식이 취약한 것으로 간주됩니다. 따라서 메시지 큐 태스크를 사용하여 메시지를 전송할 때는 암호화 요구를 신중하게 고려해야 합니다.  
  
 **MessageType**  
 메시지 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**데이터 파일 메시지**|메시지가 파일에 저장됩니다. 이 값을 선택하면 동적 옵션 **DataFileMessage**가 표시됩니다.|  
|**변수 메시지**|메시지가 변수에 저장됩니다. 이 값을 선택하면 동적 옵션 **VariableMessage**가 표시됩니다.|  
|**문자열 메시지**|메시지가 메시지 큐 태스크에 저장됩니다. 이 값을 선택하면 동적 옵션 **StringMessage**가 표시됩니다.|  
  
## <a name="messagetype-dynamic-options"></a>MessageType 동적 옵션  
  
### <a name="messagetype--data-file-message"></a>MessageType = 데이터 파일 메시지  
 **DataFileMessage**  
 데이터 파일의 경로를 입력 하거나 줄임표 **(...)** 를 클릭 한 다음 파일을 찾습니다.  
  
### <a name="messagetype--variable-message"></a>MessageType = 변수 메시지  
 **VariableMessage**  
 변수 이름을 입력 하거나 줄임표 **(...)** 를 클릭 한 다음 변수를 선택 합니다. 변수는 쉼표로 구분됩니다.  
  
 **관련 항목:** 변수 선택  
  
### <a name="messagetype--string-message"></a>MessageType = 문자열 메시지  
 **StringMessage**  
 문자열 메시지를 입력 하거나 줄임표 **(...)** 를 클릭 한 다음 **문자열 메시지 입력** 대화 상자에 메시지를 입력 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [메시지 큐 태스크 편집기 &#40;일반 페이지&#41;](general-page-of-integration-services-designers-options.md)   
 [메시지 큐 태스크 편집기 &#40;수신 페이지&#41;](../../2014/integration-services/message-queue-task-editor-receive-page.md)   
 [식 페이지](expressions/expressions-page.md)  
  
  
