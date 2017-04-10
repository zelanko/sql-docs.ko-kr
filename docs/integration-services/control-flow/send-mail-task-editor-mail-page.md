---
title: "메일 보내기 태스크 편집기(메일 페이지) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.sendmailtask.mail.f1"
helpviewer_keywords: 
  - "메일 보내기 태스크 편집기"
ms.assetid: adb385d5-ef24-4d18-b9ea-b39e00a7075e
caps.latest.revision: 30
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 30
---
# 메일 보내기 태스크 편집기(메일 페이지)
  **메일 보내기 태스크 편집기** 대화 상자의 **메일** 페이지를 사용하여 받는 사람, 메시지 유형 및 메시지 우선 순위를 지정할 수 있습니다. 또한 메시지에 파일을 첨부할 수 있습니다. 메시지 텍스트는 사용자가 제공한 문자열, 텍스트가 포함된 파일에 대한 파일 연결 또는 텍스트가 포함된 변수 이름일 수 있습니다.  
  
 이 태스크에 대한 자세한 내용은 [Send Mail Task](../../integration-services/control-flow/send-mail-task.md)를 참조하십시오.  
  
## 옵션  
 **SMTPConnection**  
 목록에서 SMTP 연결 관리자를 선택하거나 **\<새 연결...>**을 클릭하여 새 연결 관리자를 만듭니다.  
  
> [!IMPORTANT]  
>  SMTP 연결 관리자는 익명 인증과 Windows 인증만 지원하며 기본 인증은 지원하지 않습니다.  
  
 **관련 항목:** [SMTP 연결 관리자](../../integration-services/connection-manager/smtp-connection-manager.md)  
  
 **보낸 사람**  
 보낸 사람의 전자 메일 주소를 지정합니다.  
  
 **수행할 작업**  
 받는 사람의 전자 메일 주소를 세미콜론으로 구분하여 입력합니다.  
  
 **Cc**  
 메시지의 복사본을 받을 사람의 전자 메일 주소를 세미콜론으로 구분하여 지정합니다.  
  
 **Bcc**  
 메시지의 숨은 참조 복사본을 받을 사람의 전자 메일 주소를 세미콜론으로 구분하여 지정합니다.  
  
 **Subject**  
 전자 메일 메시지의 제목을 입력합니다.  
  
 **MessageSourceType**  
 메시지의 원본 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**직접 입력**|원본을 메시지 텍스트로 설정합니다. 이 값을 선택하면 동적 옵션 **MessageSource**가 표시됩니다.|  
|**파일 연결**|원본을 메시지 텍스트가 포함된 파일로 설정합니다. 이 값을 선택하면 동적 옵션 **MessageSource**가 표시됩니다.|  
|**변수**|원본을 메시지 텍스트가 포함된 변수로 설정합니다. 이 값을 선택하면 동적 옵션 **MessageSource**가 표시됩니다.|  
  
 **Priority**  
 메시지의 우선 순위를 설정합니다.  
  
 **Attachments**  
 전자 메일 메시지에 첨부하는 파일의 이름을 파이프(|)로 구분하여 입력합니다.  
  
> [!NOTE]  
>  인터넷 표준에 따라 받는 사람, 참조 및 숨은 참조 줄은 각각 256자로 제한됩니다.  
  
## MessageSourceType 동적 옵션  
  
### MessageSourceType = 직접 입력  
 **MessageSource**  
 메시지 텍스트를 입력하거나 찾아보기 단추(...)를 클릭한 다음 **메시지 원본** 대화 상자에 메시지를 입력합니다.  
  
### MessageSourceType = 파일 연결  
 **MessageSource**  
 목록에서 파일 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### MessageSourceType = 변수  
 **MessageSource**  
 목록에서 변수를 선택하거나 \<**새 변수...**>를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목:** [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), [변수 추가](../Topic/Add%20Variable.md)  
  
## 관련 항목:  
 [Integration Services 오류 및 메시지 참조](../../integration-services/integration-services-error-and-message-reference.md)   
 [메일 보내기 태스크 편집기&#40;일반 페이지&#41;](../../integration-services/control-flow/send-mail-task-editor-general-page.md)   
 [식 페이지](../../integration-services/expressions/expressions-page.md)  
  
  