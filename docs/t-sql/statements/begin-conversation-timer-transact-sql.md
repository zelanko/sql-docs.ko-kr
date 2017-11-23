---
title: BEGIN CONVERSATION TIMER (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CONVERSATION
- BEGIN_CONVERSATION_TSQL
- TIMER_TSQL
- TIMER
- CONVERSATION TIMER
- CONVERSATION_TIMER_TSQL
- BEGIN CONVERSATION TIMER
- BEGIN_CONVERSATION_TIMER_TSQL
- CONVERSATION_TSQL
- BEGIN CONVERSATION
dev_langs: TSQL
helpviewer_keywords:
- BEGIN CONVERSATION TIMER statement
- DialogTimer message
- dialogs [Service Broker], beginning
- timeouts [Service Broker]
- timer messages [Service Broker]
- conversations [Service Broker], timers
- starting timers [Service Broker]
- http://schemas.microsoft.com/SQL/ServiceBroker/DialogTimer message
ms.assetid: 98e49b3f-a38f-4180-8171-fa9cb30db4cb
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d3772f81727b60f5c7932671fa10f5ca6454047c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="begin-conversation-timer-transact-sql"></a>BEGIN CONVERSATION TIMER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  타이머를 시작합니다. 제한 시간이 만료 되 면 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 유형의 메시지를 넣습니다 `http://schemas.microsoft.com/SQL/ServiceBroker/DialogTimer` 대화에 대 한 로컬 큐에 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
BEGIN CONVERSATION TIMER ( conversation_handle )  
   TIMEOUT = timeout   
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 BEGIN CONVERSATION TIMER **(***conversation_handle***)**  
 대화에 시간을 지정합니다. *conversation_handle* 형식 이어야 합니다 **uniqueidentifier**합니다.  
  
 TIMEOUT  
 큐에 메시지를 넣을 때까지 대기하는 시간(초)을 지정합니다.  
  
## <a name="remarks"></a>주의  
 대화 타이머는 특정 시간이 지난 후 응용 프로그램이 대화에서 메시지를 받는 방법을 제공합니다. 타이머가 만료되기 전에 대화에서 BEGIN CONVERSATION TIMER를 호출하면 제한 시간이 새 값으로 설정됩니다. 대화 수명과 달리 대화의 각 측면에는 별도의 대화 타이머가 있습니다. **DialogTimer** 대화의 원격측에 영향을 주지 않고 로컬 큐에 메시지가 도착 합니다. 따라서 응용 프로그램은 다양한 용도로 타이머 메시지를 사용할 수 있습니다.  
  
 예를 들어 대화 타이머를 사용하여 응용 프로그램이 지연된 응답을 너무 오랫동안 대기하지 않도록 할 수 있습니다. 응용 프로그램이 30초 후에 대화를 완료하도록 하려면 해당 대화의 대화 타이머를 60초(30초에 30초의 유예 기간을 더한 값)로 설정할 수 있습니다. 대화가 60초 후에도 계속 열려 있으면 응용 프로그램은 해당 대화에 대한 제한 시간 메시지를 큐에 받습니다.  
  
 또는 응용 프로그램은 대화 타이머를 사용하여 특정 시간에 활성화를 요청할 수 있습니다. 예를 들어 몇 분마다 활성 연결 수를 보고하는 서비스 또는 매일 저녁 열려 있는 주문 수를 보고하는 서비스를 만들 수 있습니다. 원하는 시간;에 만료 되도록 대화 타이머를 설정 하는 서비스 타이머가 만료 되 면 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 보냅니다는 **DialogTimer** 메시지입니다. **DialogTimer** 메시지를 통해 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 시작 되는 활성화 저장 프로시저는 큐에 대 한 합니다. 저장 프로시저는 원격 서비스로 메시지를 보내고 대화 타이머를 다시 시작합니다.  
  
 BEGIN CONVERSATION TIMER는 사용자 정의 함수에 유효하지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 서비스는 대화의 멤버에 대 한 SEND 권한이 있는 사용자에 게 대화 타이머를 기본값 설정에 대 한 권한을 **sysadmin** 고정 서버 역할의 멤버는 **db_owner** 고정된 데이터베이스 역할입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `@dialog_handle`로 식별되는 대화에 2분이라는 제한 시간을 설정합니다.  
  
```  
-- @dialog_handle is of type uniqueidentifier and  
-- contains a valid conversation handle.  
  
BEGIN CONVERSATION TIMER (@dialog_handle)  
TIMEOUT = 120 ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [BEGIN DIALOG conversation&#40; Transact SQL &#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [END CONVERSATION &#40; Transact SQL &#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [수신 &#40; Transact SQL &#41;](../../t-sql/statements/receive-transact-sql.md)  
  
  
