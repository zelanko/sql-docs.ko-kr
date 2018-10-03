---
title: 메일 보내기 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sendmailtask.f1
- sql13.dts.designer.sendmailtask.general.f1
- sql13.dts.designer.sendmailtask.mail.f1
helpviewer_keywords:
- mail [Integration Services]
- Send Mail task
- e-mail [Integration Services]
- messages [Integration Services]
- sending messages
ms.assetid: fe0b7cbc-fe8e-4fe2-95b4-2953efff5869
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 805036ee530834ea2581613578fa0417087def82
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47682505"
---
# <a name="send-mail-task"></a>메일 보내기 태스크
  메일 보내기 태스크는 전자 메일 메시지를 보냅니다. 메일 보내기 태스크를 사용하면 패키지 워크플로의 태스크 성공 여부에 관계없이 패키지가 메시지를 보낼 수 있거나 런타임 시 패키지에서 발생한 이벤트에 응답하여 메시지를 보낼 수 있습니다. 예를 들어 이 태스크는 데이터베이스 백업 태스크의 성공 또는 실패에 대해 데이터베이스 관리자에게 알릴 수 있습니다.  
  
 다음과 같은 방법으로 메일 보내기 태스크를 구성할 수 있습니다.  
  
-   전자 메일 메시지의 메시지 텍스트를 제공합니다.  
  
-   전자 메일 메시지의 제목 줄을 제공합니다.  
  
-   메시지의 우선 순위 수준을 설정합니다. 이 태스크는 보통, 낮음 및 높음의 3가지 우선 순위 수준을 지원합니다.  
  
-   받는 사람, 참조 및 숨은 참조 줄의 받는 사람을 지정합니다. 태스크에서 받는 사람을 여러 명 지정하면 세미콜론으로 구분됩니다.  
  
    > [!NOTE]  
    >  인터넷 표준에 따라 받는 사람, 참조 및 숨은 참조 줄은 각각 256자로 제한됩니다.  
  
-   첨부 파일을 포함합니다. 태스크에서 첨부 파일을 여러 개 지정하면 파이프(|) 문자로 구분됩니다.  
  
    > [!NOTE]  
    >  패키지를 실행할 때 첨부 파일이 없으면 오류가 발생합니다.  
  
-   사용할 SMTP 연결 관리자를 지정합니다.  
  
    > [!IMPORTANT]  
    >  SMTP 연결 관리자는 익명 인증과 Windows 인증만 지원하며 기본 인증은 지원하지 않습니다.  
  
 메시지 텍스트는 사용자가 제공한 문자열, 텍스트가 포함된 파일에 대한 연결 또는 텍스트가 포함된 변수 이름일 수 있습니다. 이 태스크는 파일 연결 관리자를 사용하여 파일에 연결합니다. 자세한 내용은 [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)을 참조하세요.  
  
 이 태스크는 SMTP 연결 관리자를 사용하여 메일 서버에 연결합니다. 자세한 내용은 [SMTP Connection Manager](../../integration-services/connection-manager/smtp-connection-manager.md)을 참조하세요.  
  
## <a name="custom-logging-messages-available-on-the-send-mail-task"></a>메일 보내기 태스크에 사용할 수 있는 사용자 지정 로깅 메시지  
 다음 표에서는 메일 보내기 태스크에 대한 사용자 지정 로그 항목을 나열합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)을 참조하세요.  
  
|로그 항목|설명|  
|---------------|-----------------|  
|**SendMailTaskBegin**|태스크에서 전자 메일 메시지 보내기를 시작했음을 나타냅니다.|  
|**SendMailTaskEnd**|태스크에서 전자 메일 메시지 보내기를 완료했음을 나타냅니다.|  
|**SendMailTaskInfo**|태스크에 대한 설명 정보를 제공합니다.|  
  
## <a name="configuring-the-send-mail-task"></a>메일 보내기 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [식 페이지](../../integration-services/expressions/expressions-page.md)  
  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.SendMailTask.SendMailTask>  
  
## <a name="related-tasks"></a>관련 작업  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 [태스크 또는 컨테이너의 속성 설정](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)을 클릭합니다.  
  
## <a name="related-content"></a>관련 내용  
  
-   shareourideas.com의 기술 문서 - [C#의 배달 알림으로 메일을 보내는 방법](http://go.microsoft.com/fwlink/?LinkId=237625)  
  
## <a name="send-mail-task-editor-general-page"></a>메일 보내기 태스크 편집기(일반 페이지)
  **메일 보내기 태스크 편집기** 대화 상자의 **일반 페이지** 를 사용하여 메일 보내기 태스크의 이름을 지정하고 설명할 수 있습니다.  
  
### <a name="options"></a>Options  
 **이름**  
 메일 보내기 태스크에 사용할 고유 이름을 제공합니다. 이 이름은 태스크 아이콘에서 레이블로 사용됩니다.  
  
 **참고** 태스크 이름은 패키지 내에서 고유해야 합니다.  
  
 **설명**  
 메일 보내기 태스크에 대한 설명을 입력합니다.  
  
## <a name="send-mail-task-editor-mail-page"></a>메일 보내기 태스크 편집기(메일 페이지)
  **메일 보내기 태스크 편집기** 대화 상자의 **메일** 페이지를 사용하여 받는 사람, 메시지 유형 및 메시지 우선 순위를 지정할 수 있습니다. 또한 메시지에 파일을 첨부할 수 있습니다. 메시지 텍스트는 사용자가 제공한 문자열, 텍스트가 포함된 파일에 대한 파일 연결 또는 텍스트가 포함된 변수 이름일 수 있습니다.  
  
### <a name="options"></a>Options  
 **SMTPConnection**  
 목록에서 SMTP 연결 관리자를 선택하거나 **\<새 연결...>** 을 클릭하여 새 연결 관리자를 만듭니다.  
  
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
  
|값|설명|  
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
  
### <a name="messagesourcetype-dynamic-options"></a>MessageSourceType 동적 옵션  
  
#### <a name="messagesourcetype--direct-input"></a>MessageSourceType = 직접 입력  
 **MessageSource**  
 메시지 텍스트를 입력하거나 찾아보기 단추(...)를 클릭한 다음 **메시지 원본** 대화 상자에 메시지를 입력합니다.  
  
#### <a name="messagesourcetype--file-connection"></a>MessageSourceType = 파일 연결  
 **MessageSource**  
 목록에서 파일 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="messagesourcetype--variable"></a>MessageSourceType = 변수  
 **MessageSource**  
 목록에서 변수를 선택하거나 \<**새 변수...**>를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목:** [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), [변수 추가](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 태스크](../../integration-services/control-flow/integration-services-tasks.md)   
 [제어 흐름](../../integration-services/control-flow/control-flow.md)  
  
  
