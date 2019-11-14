---
title: sp_replqueuemonitor (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replqueuemonitor
- sp_replqueuemonitor_TSQL
helpviewer_keywords:
- sp_replqueuemonitor
ms.assetid: 6909a3f1-43a2-4df5-a6a5-9e6f347ac841
author: stevestein
ms.author: sstein
ms.openlocfilehash: d3c84d15087c3cb6bb63380bc6cf0c75e773b883
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2019
ms.locfileid: "74055213"
---
# <a name="sp_replqueuemonitor-transact-sql"></a>sp_replqueuemonitor(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  지정 된 게시에 대해 지연 업데이트 구독에 대 한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 큐 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 메시지 큐의 큐 메시지를 나열 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 큐를 사용하는 경우 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다. Message Queuing을 사용하는 경우 이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replqueuemonitor [ @publisher = ] 'publisher'  
    [ , [ @publisherdb = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @tranid = ] 'tranid' ]  
    [ , [ @queuetype = ] 'queuetype' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'`은 게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 NULL입니다. 해당 서버는 반드시 게시용으로 구성되어야 합니다. 모든 게시자에 대해 NULL입니다.  
  
`[ @publisherdb = ] 'publisher_db' ]`는 게시 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 NULL입니다. 모든 게시 데이터베이스에 대해 NULL입니다.  
  
`[ @publication = ] 'publication' ]`는 게시의 이름입니다. *게시*는 **sysname**이며 기본값은 NULL입니다. 모든 게시에 대해 NULL입니다.  
  
`[ @tranid = ] 'tranid' ]`은 트랜잭션 ID입니다. *id*는 **sysname**이며 기본값은 NULL입니다. 모든 트랜잭션에 대해 NULL입니다.  
  
`[ @queuetype = ] 'queuetype' ]`는 트랜잭션을 저장 하는 큐의 유형입니다. *queuetype* 은 **tinyint** 이며 기본값은 **0**이 고 다음 값 중 하나일 수 있습니다.  
  
|Value|설명|  
|-----------|-----------------|  
|**0**|모든 유형의 큐입니다.|  
|**1.**|메시지 큐|  
|**2**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 큐|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_replqueuemonitor** 는 지연 업데이트 구독이 있는 트랜잭션 복제 또는 스냅숏 복제에 사용 됩니다. SQL 명령을 포함하지 않거나 영향을 미치는 SQL 명령의 일부인 큐 메시지는 표시되지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_replqueuemonitor**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
