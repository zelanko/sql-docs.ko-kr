---
title: Broker 이벤트 범주 | Microsoft 문서
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- SQL Server event classes, Broker event category
- Broker event category [SQL Server]
- event classes [SQL Server], Broker event category
ms.assetid: 470dc93c-0dda-4d89-829b-937738d59b31
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 65c28b905427c685c2d57a55ac0361aeef5f1a6b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67999730"
---
# <a name="broker-event-category"></a>Broker 이벤트 범주

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

**Broker** 이벤트 범주에는 일반적인 Service Broker 이벤트가 포함됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|설명|  
|-----------|-----------------|  
|[Broker:Activation 이벤트 클래스](../../relational-databases/event-classes/broker-activation-event-class.md)|큐 모니터가 활성화 저장 프로시저를 시작하는 경우에 생성되는 이벤트입니다.|  
|[Broker:Connection 이벤트 클래스](../../relational-databases/event-classes/broker-connection-event-class.md)|Service Broker에서 관리하는 전송 연결 상태를 보고하기 위해 생성되는 이벤트입니다.|  
|[Broker:Conversation 이벤트 클래스](../../relational-databases/event-classes/broker-conversation-event-class.md)|대화 진행률을 보고하기 위해 생성되는 이벤트입니다.|  
|[Broker:Conversation Group 이벤트 클래스](../../relational-databases/event-classes/broker-conversation-group-event-class.md)|데이터베이스에서 대화 그룹을 만들거나 삭제하는 경우에 생성되는 이벤트입니다.|  
|[Broker:Corrupted Message 이벤트 클래스](../../relational-databases/event-classes/broker-corrupted-message-event-class.md)|데이터베이스에서 손상된 메시지를 받았음을 보고하기 위해 생성되는 이벤트입니다.|  
|[Broker:Forwarded Message Dropped 이벤트 클래스](../../relational-databases/event-classes/broker-forwarded-message-dropped-event-class.md)|전달되어야 하는 Service Broker 메시지가 SQL Server에서 삭제된 경우 생성되는 이벤트입니다.|  
|[Broker:Forwarded Message Sent 이벤트 클래스](../../relational-databases/event-classes/broker-forwarded-message-sent-event-class.md)|SQL Server가 Service Broker 메시지를 전달할 때 생성되는 이벤트입니다.|  
|[Broker:Message Classify 이벤트 클래스](../../relational-databases/event-classes/broker-message-classify-event-class.md)|Service Broker가 메시지 라우팅을 지정하는 경우에 생성되는 이벤트입니다.|  
|[Broker:Message Drop 이벤트 클래스](../../relational-databases/event-classes/broker-message-drop-event-class.md)|Service Broker가 받은 메시지를 유지할 수 없는 경우에 생성되는 이벤트입니다. 이 메시지는 이 인스턴스의 서비스로 배달되어야 합니다.|  
|[Broker:Remote Message Ack 이벤트 클래스](../../relational-databases/event-classes/broker-remote-message-ack-event-class.md)|Service Broker가 메시지 승인을 보내거나 받는 경우에 생성되는 이벤트입니다.|  
  
 두 개의 보안 감사 이벤트도 Service Broker에 제공됩니다. 이러한 이벤트에 대한 자세한 내용은 [Audit Broker Login 이벤트 클래스](../../relational-databases/event-classes/audit-broker-login-event-class.md) 및 [Audit Broker Conversation 이벤트 클래스](../../relational-databases/event-classes/audit-broker-conversation-event-class.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Security Audit 이벤트 범주](../../analysis-services/trace-events/security-audit-event-category.md)  
  
  
