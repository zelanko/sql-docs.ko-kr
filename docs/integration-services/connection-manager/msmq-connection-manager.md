---
description: MSMQ 연결 관리자
title: MSMQ 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.msmqconnectionmanager.f1
helpviewer_keywords:
- connections [Integration Services], message queues
- connection managers [Integration Services], MSMQ
- MSMQ connection manager
- message queue connections [Integration Services]
ms.assetid: a86900e2-450e-479f-b207-e1b02361d395
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7eb223aaa1ab8ece253e90db998b258e843f225e
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724994"
---
# <a name="msmq-connection-manager"></a>MSMQ 연결 관리자

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  MSMQ 연결 관리자를 사용하면 패키지에서 MSMQ(메시지 큐)를 사용하는 메시지 큐에 연결할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 포함된 메시지 큐 태스크에서는 MSMQ 연결 관리자가 사용됩니다.  
  
 패키지에 MSMQ 연결 관리자를 추가하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 런타임에 MSMQ 연결로 확인되는 연결 관리자를 만들고, 연결 관리자 속성을 설정하며, 연결 관리자를 패키지의 **Connections** 컬렉션에 추가합니다. 연결 관리자의 **ConnectionManagerType** 속성이 **MSMQ**로 설정됩니다.  
  
 다음과 같은 방법으로 MSMQ 연결 관리자를 구성할 수 있습니다.  
  
-   연결 문자열을 제공합니다.  
  
-   연결할 메시지 큐의 경로를 제공합니다.  
  
 다음 표에서 보여 주는 것과 같이 경로 형식은 큐 형식에 따라 달라집니다.  
  
|큐 유형|샘플 경로|  
|----------------|-----------------|  
|공용|\<computer name>\\<queue name\>|  
|프라이빗|\<computer name>\Private$\\<queue name\>|  
  
 마침표(.)를 사용하여 로컬 컴퓨터를 나타낼 수 있습니다.  
  
## <a name="configuration-of-the-msmq-connection-manager"></a>MSMQ 연결 관리자 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용은 [MSMQ 연결 관리자 편집기]()를 참조하세요.  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)로 설정됩니다.  
  
## <a name="msmq-connection-manager-editor"></a>MSMQ 연결 관리자 편집기
  **MSMQ 연결 관리자** 대화 상자를 사용하여 MSMQ(메시지 큐)의 경로를 지정할 수 있습니다.  
  
 MSMQ 연결 관리자에 대한 자세한 내용은 [MSMQ Connection Manager](../../integration-services/connection-manager/msmq-connection-manager.md)를 참조하십시오.  
  
> [!NOTE]  
>  MSMQ 연결 관리자는 로컬 퍼블릭 큐, 로컬 프라이빗 큐 및 원격 퍼블릭 큐를 지원합니다. 원격 프라이빗 큐는 지원하지 않습니다. 스크립트 태스크를 사용하는 해결 방법은 [Sending to a Remote Private Message Queue with the Script Task](../../integration-services/extending-packages-scripting-task-examples/sending-to-a-remote-private-message-queue-with-the-script-task.md)를 참조하십시오.  
  
### <a name="options"></a>옵션  
 **이름**  
 워크플로의 MSMQ 연결 관리자에 고유한 이름을 지정합니다. 제공한 이름은 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에 표시됩니다.  
  
 **설명**  
 연결 관리자에 대한 설명을 입력합니다. 설명에 해당 연결 관리자의 용도를 정의하면 패키지를 이해하기 쉬우며 유지 관리가 간편합니다.  
  
 **Path**  
 메시지 큐의 전체 경로를 입력합니다. 경로 형식은 큐 유형에 따라 달라집니다.  
  
|큐 유형|샘플 경로|  
|----------------|-----------------|  
|공용|\<computer name>\\<queue name\>|  
|프라이빗|\<computer name>\Private$\\<queue name\>|  
  
 "."를 사용하여 로컬 컴퓨터를 나타낼 수 있습니다.  
  
 **Test**  
 MSMQ 연결 관리자를 구성했으면 **테스트**를 클릭하여 연결이 실행 가능한지 확인합니다.  
  
## <a name="see-also"></a>참고 항목  
 [메시지 큐 태스크](../../integration-services/control-flow/message-queue-task.md)   
 [Integration Services&#40;SSIS&#41; 연결](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
