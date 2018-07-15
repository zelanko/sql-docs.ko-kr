---
title: MSMQ 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], message queues
- connection managers [Integration Services], MSMQ
- MSMQ connection manager
- message queue connections [Integration Services]
ms.assetid: a86900e2-450e-479f-b207-e1b02361d395
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f9be09df9ab705d45dfdeee7caebfeb556a7a669
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37306123"
---
# <a name="msmq-connection-manager"></a>MSMQ 연결 관리자
  MSMQ 연결 관리자를 사용하면 패키지에서 MSMQ(메시지 큐)를 사용하는 메시지 큐에 연결할 수 있습니다.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에 포함된 메시지 큐 태스크에서는 MSMQ 연결 관리자가 사용됩니다.  
  
 패키지에 MSMQ 연결 관리자를 추가 하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 연결 런타임에 MSMQ 연결으로 확인 되는 연결 관리자 속성을 설정 하 고 연결 관리자를 추가 하는 관리자를 만들고는 `Connections` 컬렉션에는 패키지입니다. 합니다 `ConnectionManagerType` 연결 관리자의 속성이 `MSMQ`합니다.  
  
 다음과 같은 방법으로 MSMQ 연결 관리자를 구성할 수 있습니다.  
  
-   연결 문자열을 제공합니다.  
  
-   연결할 메시지 큐의 경로를 제공합니다.  
  
 다음 표에서 보여 주는 것과 같이 경로 형식은 큐 형식에 따라 달라집니다.  
  
|큐 유형|샘플 경로|  
|----------------|-----------------|  
|공개|\<컴퓨터 이름>\\<큐 이름\>|  
|Private|\<컴퓨터 이름>\Private$\\<큐 이름\>|  
  
 마침표(.)를 사용하여 로컬 컴퓨터를 나타낼 수 있습니다.  
  
## <a name="configuration-of-the-msmq-connection-manager"></a>MSMQ 연결 관리자 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용은 [MSMQ 연결 관리자 편집기](../msmq-connection-manager-editor.md)를 참조하세요.  
  
 연결 관리자를 프로그래밍 방식으로 구성 하는 방법에 대 한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 하 고 [프로그래밍 방식으로 연결 추가](../building-packages-programmatically/adding-connections-programmatically.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [메시지 큐 태스크](../control-flow/message-queue-task.md)   
 [Integration Services &#40;SSIS&#41; 연결](integration-services-ssis-connections.md)  
  
  
