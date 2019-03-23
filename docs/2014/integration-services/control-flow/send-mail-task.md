---
title: 메일 보내기 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sendmailtask.f1
helpviewer_keywords:
- mail [Integration Services]
- Send Mail task
- e-mail [Integration Services]
- messages [Integration Services]
- sending messages
ms.assetid: fe0b7cbc-fe8e-4fe2-95b4-2953efff5869
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3308899190aa63ebb9be93c4c9af15d5e0f94600
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58380131"
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
  
 메시지 텍스트는 사용자가 제공한 문자열, 텍스트가 포함된 파일에 대한 연결 또는 텍스트가 포함된 변수 이름일 수 있습니다. 이 태스크는 파일 연결 관리자를 사용하여 파일에 연결합니다. 자세한 내용은 [Flat File Connection Manager](../connection-manager/file-connection-manager.md)을 참조하세요.  
  
 이 태스크는 SMTP 연결 관리자를 사용하여 메일 서버에 연결합니다. 자세한 내용은 [SMTP Connection Manager](../connection-manager/smtp-connection-manager.md)을 참조하세요.  
  
## <a name="custom-logging-messages-available-on-the-send-mail-task"></a>메일 보내기 태스크에 사용할 수 있는 사용자 지정 로깅 메시지  
 다음 표에서는 메일 보내기 태스크에 대한 사용자 지정 로그 항목을 나열합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../performance/integration-services-ssis-logging.md) 및 [로깅할 메시지 사용자 지정](../custom-messages-for-logging.md)을 참조하세요.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`SendMailTaskBegin`|태스크에서 전자 메일 메시지 보내기를 시작했음을 나타냅니다.|  
|`SendMailTaskEnd`|태스크에서 전자 메일 메시지 보내기를 완료했음을 나타냅니다.|  
|`SendMailTaskInfo`|태스크에 대한 설명 정보를 제공합니다.|  
  
## <a name="configuring-the-send-mail-task"></a>메일 보내기 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [메일 보내기 태스크 편집기&#40;일반 페이지&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [메일 보내기 태스크 편집기&#40;메일 페이지&#41;](../send-mail-task-editor-mail-page.md)  
  
-   [식 페이지](../expressions/expressions-page.md)  
  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.SendMailTask.SendMailTask>  
  
## <a name="related-tasks"></a>관련 작업  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 [태스크 또는 컨테이너의 속성 설정](../set-the-properties-of-a-task-or-container.md)을 클릭합니다.  
  
## <a name="related-content"></a>관련 내용  
  
-   shareourideas.com의 기술 문서 - [C#의 배달 알림으로 메일을 보내는 방법](https://go.microsoft.com/fwlink/?LinkId=237625)  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 태스크](integration-services-tasks.md)   
 [제어 흐름](control-flow.md)  
  
  
